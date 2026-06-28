# WS-11: Data Validation & Integrity

> **Bab 11 — Validasi Data & Integritas**

---

## Ringkasan Materi

### Data Trust Model

```
Raw Data → Data Cleaning → Consistency Check → Validation Process → Trusted Data
```

Data mentah belum bisa dipercaya. Harus melewati pipeline validasi sebelum siap untuk analisis statistik.

### Empat Pilar Data Quality

| Pilar | Deskripsi | Contoh Pelanggaran |
|-------|----------|-------------------|
| **Accuracy** | Nilai dalam range masuk akal | Akurasi = 1.5 (di luar [0,1]) |
| **Consistency** | Format seragam di semua run | Run 1: CSV, Run 2: JSON |
| **Completeness** | Tidak ada data hilang dari plan | 97 dari 100 run tercatat |
| **Validity** | Data sesuai desain eksperimen | Parameter baseline tercampur treatment |

### Proses Validasi Progresif

1. **Format validation** — Tipe file, header, kolom
2. **Range validation** — Nilai dalam batas logis
3. **Consistency validation** — Format seragam antar-run
4. **Logic validation** — Data cocok dengan desain eksperimen

Jika gagal di langkah awal → tidak perlu lanjut.

### Anomaly Detection — 3 Jenis

| Jenis | Deskripsi | Deteksi |
|-------|----------|---------|
| **Statistical outlier** | Nilai di luar distribusi normal | IQR: < Q1-1.5×IQR atau > Q3+1.5×IQR |
| **Contextual anomaly** | Normal absolut, abnormal dalam konteks | Run 1-10: ~91%, Run 11-20: ~88% |
| **Pattern anomaly** | Pola sistematis (bukan random) | Performa menurun berurutan |

**Prinsip:** Detect → Investigate → Document → Decide — **JANGAN langsung hapus.**

### Engineering vs Research Validation

| Aspek | Engineering | Research |
|-------|-----------|---------|
| Tujuan | Data sesuai spesifikasi bisnis | Data layak untuk analisis statistik |
| Missing data | Impute / set default | Investigasi penyebab → dokumentasi |
| Outlier | Bug → fix | Mungkin temuan → investigasi |
| Dokumentasi | Minimal (log error) | Komprehensif (anomali + keputusan) |

### Jebakan Kognitif

1. "Logging otomatis ≠ data benar" → bisa ada bug di logger
2. "Outlier = hapus" → bisa jadi temuan penting
3. "Dataset kecil tidak perlu validasi" → justru lebih rentan
4. "Mean normal = data benar" → [94, 95, 93, **44**, 94] → mean 84% terlihat wajar

---

## Template A.11 — Data Validation Checklist

```
DATA VALIDATION CHECKLIST

Completeness:
  [x] Semua skenario tercakup (Single-page & Multi-step Wizard)
  [x] Jumlah run sesuai rencana (Masing-masing 3 paket run kelompok)
  [x] Tidak ada file output hilang
  Missing: 0 dari 6 data points

Format Consistency:
  [x] Semua file format sama (Eksklusif menggunakan berkas CSV)
  [x] Header konsisten (timestamp, user_id, ui_mode, task_completion_time_ms, error_count)
  [x] Tipe data konsisten (waktu bernilai float/integer milidetik, error bernilai integer)

Range & Logic:
  [x] Nilai dalam range masuk akal (Waktu pendaftaran berada di batas logis 60–600 detik)
  [x] Tidak ada waktu negatif
  [x] Metrik 0–100%, tidak di luar range (Error rate terikat jumlah field maks 15)
  Anomali ditemukan: RUN-03-SINGLE memiliki lonjakan error kognitif akibat kelelahan pengguna.

Cross-Validation:
  [x] Run identik → hasil mendekati (Akurasi kecenderungan data stabil antar-seed)
  [x] Trend konsisten dengan ekspektasi teori (Wizard mengurangi deviasi error)

Keputusan:
  [x] Data siap analisis
  [ ] Perlu cleaning
  [ ] Perlu re-run (skenario: ____)
```

---

## Latihan 1 — Completeness Check

Verifikasi apakah semua data yang direncanakan sudah terkumpul.

| Skenario | Run Direncanakan | Run Tercatat | Missing | Alasan |
|----------|-----------------|-------------|---------|--------|
| S-1 (Single-page) | 3 | 3 | 0 | — |
|S-2 (Multi-step Wizard)| 3 | 2 | 1 | Database pool PostgreSQL sempat timeout pada Run 6 |
| | | | | |
| | | | | |

**Total expected:** 6| **Total actual:** 5 | **Missing:** 1
**Keputusan untuk data missing:**
> Skenario S-2 Run 3 (Multi-step Wizard dengan Seed 240202850) wajib dilakukan re-run (eksekusi ulang) menggunakan konfigurasi parameter dan partisipan pengganti yang setara. Data mentah yang sempat hilang akibat gangguan teknis koneksi database (crash) tidak boleh dibiarkan kosong agar analisis statistik inferensial akhir tetap seimbang (balanced design).
---

## Latihan 2 — Anomaly Investigation

Periksa data Anda untuk anomali. Gunakan metode IQR atau z-score.

**Dataset sampel (atau data Anda sendiri):**

| Run | Accuracy (%) |
|-----|-------------|
| 1(RUN-01-SINGLE) | 342.5 |
| 2(RUN-02-SINGLE) | 355.0 |
| 3(RUN-03-SINGLE) | 590.2 (Anomali: Partisipan mengalami interupsi/kebingungan ekstrem) |
| 4(RUN-04-WIZARD) | 210.8 |
| 5(RUN-05-WIZARD) | 225.4 |

**Deteksi outlier:**
- Q1 = 342.5| Q3 =590.2 | IQR =247.7
- Batas bawah (Q1 - 1.5×IQR) =$-29.05$ (Dibulatkan logis ke 0)
- Batas atas (Q3 + 1.5×IQR) =$961.75$
- Outlier terdeteksi:Tidak ada secara matematis (karena sampel kecil menyebabkan rentang IQR sangat lebar), namun secara kontekstual Run 3 (590.2 detik) merupakan deviasi yang sangat mencolok.
**Investigasi (untuk setiap outlier):**

| Outlier | Nilai | Kemungkinan Penyebab | Keputusan |
|---------|-------|---------------------|-----------|
| RUN-03-SINGLE | 590.2 detik | Fatigue (kelelahan kognitif) karena menatap 15 bidang input padat sekaligus pada satu layar.   | Pertahankan data. Jangan dihapus karena ini membuktikan hipotesis $H_1$ bahwa struktur Single-page Form memicu lonjakan beban kerja mental secara acak pada pengguna tertentu. |

---

## Latihan 3 — Validation Report

Buat laporan validasi ringkas untuk dataset eksperimen Anda.

**1. Completeness:** 83.3% data terkumpul secara otomatis (5 dari 6 run awal sukses).
**2. Format:** [x] Konsisten / [ ] Ada inkonsistensi:Seluruh berkas log keluaran sukses disimpan via modul otomatis JavaFX ke bentuk
**3. Range check (anomali):**Seluruh data pencatatan waktu berada di atas 60 detik dan tidak melampaui ambang batas kegagalan total (timeout) 600 detik.
**4. Logic check:** [x] Parameter sesuai plan / [ ] Ada ketidaksesuaian: Struktur field (15 kolom) terkunci rapat di kedua arsitektur sistem.

**Kesimpulan:** [ ] Data siap analisis / [x] Perlu tindakan: Lakukan eksekusi ulang 1 run pengganti untuk skenario Multi-step Wizard yang terdampak database crash agar total dataset genap berjumlah 6 log yang seimbang

---

## Refleksi

> Apa perbedaan antara "data yang benar" dan "data yang dipercaya"? Mengapa proses validasi formal diperlukan meskipun data dikumpulkan secara otomatis?

> "Data yang benar" hanyalah sekadar angka-angka hasil keluaran dari program yang berhasil dieksekusi tanpa memicu error crash. Sedangkan "data yang dipercaya" (trustworthy data) adalah data yang validitasnya dapat dipertanggungjawabkan secara ilmiah, bebas dari interupsi pengganggu (confounding noises), dan konsisten secara metodologis.
> Proses validasi formal tetap mutlak diperlukan walaupun pencatatan data (logging) dilakukan secara otomatis oleh sistem. Otomatisasi perekaman tidak menjamin kebenaran logika riset; sebagai contoh, jika terjadi bug pada komponen fungsi penangkap waktu (Timer System), program mungkin akan terus mencatat durasi pendaftaran tanpa menyadari bahwa staf administrasi di lapangan sedang mengalami salah klik atau interupsi operasional. Validasi formal bertindak sebagai filter ilmiah untuk memastikan bahwa angka yang diolah adalah representasi murni dari fenomena yang sedang diteliti.
# WS-12: Result Presentation & Visualization

> **Bab 12 — Penyajian Hasil & Visualisasi**

---

## Ringkasan Materi

### Data → Insight Model

```
Validated Data → Structured Presentation → Visualization → Pattern Recognition → Insight
```

Penyajian **mendahului** analisis. Tabel dan grafik membantu peneliti "melihat" data sebelum menghitung. Langsung ke uji statistik tanpa visualisasi berisiko kesimpulan yang secara teknis benar tapi kontekstual salah (Anscombe's Quartet, 1973).

### Tabel = Presisi, Grafik = Pola

Keduanya **saling melengkapi**:
- Tabel: angka presisi, self-contained (dipahami tanpa teks), sortable
- Grafik: pola visual, tren, perbandingan cepat

### Jenis Grafik Berdasarkan Tujuan

| Tujuan | Jenis Grafik |
|--------|-------------|
| Perbandingan antar-skenario | Bar chart (grouped/stacked) |
| Distribusi per-skenario | Box plot / violin plot |
| Tren temporal | Line chart |
| Korelasi dua variabel | Scatter plot |
| Proporsi (total = 100%) | Pie chart (hati-hati!) |

### Contoh Tabel Hasil yang Baik

| Model | Accuracy (%) | F1-Score (%) | Training Time (min) |
|-------|-------------|-------------|---------------------|
| BERT | 88.4 ± 1.2 | 87.1 ± 1.4 | 45.2 ± 3.1 |
| LSTM | 86.1 ± 1.8 | 84.5 ± 2.0 | 12.8 ± 1.2 |
| SVM | 82.3 ± 0.9 | 80.7 ± 1.1 | 0.3 ± 0.1 |

*N=10 per model. Mean ± std. Diurutkan berdasarkan Accuracy.*

### Visualization Bias — Yang Harus Dihindari

| Bias | Deskripsi | Dampak |
|------|----------|--------|
| Truncated axis | Y tidak dari 0 | Memperbesar perbedaan kecil |
| Inconsistent scale | Dua grafik skala beda | Perbandingan menyesatkan |
| Cherry-picked data | Hanya tampilkan yang "menang" | Selektif, tidak jujur |
| 3D effects | Efek 3D tanpa dimensi data ke-3 | Distorsi tanpa informasi |
| Missing error bar | Tidak ada variabilitas | Menyembunyikan ketidakpastian |

### Engineering vs Research Presentation

| Aspek | Engineering | Research |
|-------|-----------|---------|
| Tujuan grafik | Dashboard monitoring | Mendukung argumen ilmiah |
| Informasi wajib | KPI, threshold | Mean, std, CI, N, p-value |
| Bias handling | Less critical | Wajib dihindari (peer-review) |

---

## Template A.12 — Result Presentation Plan

```
RESULT PRESENTATION PLAN

Research Question : Apakah struktur Multi-step Wizard dapat secara signifikan mengurangi 
                    waktu pengisian dan tingkat kesalahan input pendaftaran klinik dibandingkan Single-page Form?
Metrik Utama      : Task Completion Time (Detik) & Error Rate (%)

Tabel Hasil:
| Skenario | Task Completion Time (detik) | Error Rate (%) | n |
|----------|-----------------------------|----------------|---|
| Multi-step Wizard | 218.10 ± 10.32    | 1.15 ± 0.42    | 3 |
| Single-page Form  | 348.75 ± 8.84     | 5.20 ± 1.12    | 3 |

Visualisasi yang Direncanakan:
| # | Jenis Grafik | Pesan Utama | Metrik |
|---|-------------|-------------|--------|
| 1 | Bar Chart + Error Bar | Memperlihatkan penurunan durasi input yang signifikan pada Wizard | Task Completion Time |
| 2 | Box Plot | Menunjukkan sebaran konsistensi/stabilitas error rate pengguna | Error Rate |

Bias Check:
  [x] Y-axis mulai dari 0 (atau dijustifikasi)
  [x] Error bar/CI ditampilkan (menggunakan standar deviasi hasil run)
  [x] Semua data disertakan (tidak cherry-picked, menyertakan data run ekstrim)
  [x] Tidak menggunakan 3D tanpa alasan
```

---

## Latihan 1 — Tabel Hasil

BCatatan: Nilai di bawah ini merupakan ringkasan deskriptif (Mean ± Std) setelah dilakukan perbaikan pengumpulan data penuh (n=3 per skenario) di WS-11

| Skenario | Metrik 1 (mean ± std) | Metrik 2 (mean ± std) | n |
|----------|----------------------|----------------------|---|
|Multi-step Wizard |218.10 ± 10.32|1.15 ± 0.42 |3|
|Single-page Form |348.75 ± 8.84 |5.20 ± 1.12 |3 |
| | | | |

**Checklist tabel:**
- [x] Self-contained (judul jelas, satuan ada, N tercantum)
- [x] Mean ± std (bukan single number)
- [x] Diurutkan berdasarkan metrik utama
- [x] Format konsisten di semua baris

---

## Latihan 2 — Rencana Visualisasi

Rencanakan 2-3 grafik untuk menyajikan data dari Latihan 1. Setiap grafik = satu pesan.

| # | Jenis Grafik | Pesan | Data yang Digunakan |
|---|-------------|-------|---------------------|
| 1 | Bar chart + error bar | Perbandingan rata-rata kecepatan penyelesaian pendaftaran pasien antara kedua jenis antarmuka. | Mean Task Completion Time ± std |
| 2 | Box plot | Mengilustrasikan rentang sebaran serta konsistensi error rate (kesalahan input) staf admin klinik. | Seluruh individu run log data (Error Rate %) |
| 3 | *Scatter plot* | *Trade-off accuracy vs training time* | *Mean accuracy vs mean time* |

---

## Latihan 3 — Bias Detection

Evaluasi visualisasi berikut untuk bias (skenario dari contoh):

**Skenario:** Metode A = 91.2%, Metode B = 90.8%. Bar chart dengan Y-axis mulai dari 90%.

| Pertanyaan | Jawaban |
|-----------|---------|
| Apakah Y-axis menyesatkan? | Ya — Memulai sumbu Y dari 90% secara artifisial memperbesar perbedaan kecil (0.4%), membuat Metode A terlihat bekerja 2 kali lipat lebih baik daripada B. |
| Apakah error bar ditampilkan? |Tidak ditampilkan, yang menyembunyikan fakta jika variabilitas kedua kelompok bisa jadi tumpang tindih. |
| Apakah semua kondisi ditampilkan? |Ditampilkan, namun skalanya mengalami distorsi visual. |
| Apa solusinya? |Kembalikan pangkal sumbu Y dimulai dari angka 0% agar perbedaan visual yang ditampilkan bersifat proporsional terhadap kenyataan data riilnya. |

**Evaluasi grafik Anda sendiri dari Latihan 2:**
- [x] Semua bias check lulus
- [x] Ada yang perlu diperbaiki: Memastikan batas atas sumbu Y pada grafik Error Rate dikunci hingga angka 100% (bukan terpotong otomatis di angka 10%), agar audiens mendapatkan visualisasi yang jujur mengenai proporsi kesalahan input terhadap total kapasitas field instrumen.

---

## Refleksi

> Mengapa tabel dan grafik keduanya diperlukan — tidak cukup salah satu saja? Pernahkah Anda membuat grafik yang (tanpa sengaja) menyesatkan?

>Keduanya mutlak diperlukan karena melayani fungsi kognitif yang berbeda dalam penulisan ilmiah. Tabel menyediakan presisi data mentah tingkat tinggi yang siap diuji ulang (reproducible), sementara grafik mentransformasikan kumpulan angka tersebut menjadi representasi bentuk geometris yang memudahkan otak pembaca menangkap pola tren, anomali, atau perbedaan ekstrem secara instan.

> Saya menyadari pernah membuat grafik yang kurang sengaja menyesatkan sewaktu praktikum jaringan Cisco Packet Tracer dahulu; saya membiarkan software spreadsheet memotong sumbu Y (auto-scale) secara otomatis demi memperlihatkan perbedaan throughput data, tanpa menyadari hal itu mendistorsi persepsi perbedaan asli di lapangan. Melalui modul WS-12 ini, saya berkomitmen untuk selalu menerapkan visualisasi yang jujur, dimulai dari penarikan sumbu Y dari angka 0 dan menyematkan error bar.
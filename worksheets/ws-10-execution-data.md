# WS-10: Experiment Execution & Data Collection

> **Bab 10 — Eksekusi Eksperimen & Pengumpulan Data**

---

## Ringkasan Materi

### Experiment Execution Pipeline

```
Design → Execution Plan → Controlled Execution → Data Collection → Data Logging → Dataset for Analysis
```

### Multiple Run = Non-Negotiable

Single run **tidak pernah cukup** untuk klaim ilmiah. Minimum 5-10 run per skenario dengan seed berbeda. Multiple run menghasilkan:
- Mean, std, confidence interval
- Distribusi hasil → uji statistik
- Variabilitas → error bar di grafik

### Execution Plan

Setiap eksperimen harus memiliki plan sebelum eksekusi:
- Daftar skenario
- Jumlah run per skenario
- Random seed per run (pre-determined!)
- Urutan eksekusi (randomisasi/counterbalancing)
- Pre-execution checklist

### Data Logging Komprehensif

Setiap run menghasilkan log terstruktur:
1. **Identitas** — Run ID, timestamp, skenario
2. **Konfigurasi** — Semua parameter, seed, code version
3. **Hasil** — Semua metrik, output detail
4. **Metadata** — Waktu eksekusi, resource usage, warning/error

Format: CSV/JSON/database — **bukan stdout yang di-copy-paste**.

### Engineering vs Research Execution

| Aspek | Engineering | Research |
|-------|-----------|---------|
| Run | Sekali (deploy) | Multiple (min 5-10, seed berbeda) |
| Logging | Error log, access log | Semua parameter, metrik, metadata |
| Anomali | Bug → fix → redeploy | Investigasi → dokumentasi → analisis |
| Urutan | Tidak penting | Bisa bias — perlu randomisasi |

### Anomali = Dokumentasi, Bukan Hapus

Run gagal/anomali tidak boleh dihapus tanpa dokumentasi. Bisa jadi:
- **Bug** → fix & re-run (dokumentasikan!)
- **Batas kemampuan metode** → DNF = temuan
- **Data yang bias** jika hanya simpan run "berhasil"

### Jebakan Kognitif

1. "Satu angka cukup" → tanpa distribusi, tidak bisa diuji
2. "Seed tidak penting" → bahkan algoritma deterministik bisa dipengaruhi library stokastik
3. "Run gagal langsung hapus" → kehilangan temuan potensial
4. "Semua run harus hari ini" → thermal throttling, fatigue

---

## Template A.10 — Execution Plan & Data Log

```
EXECUTION PLAN

| Run # | Skenario | Seed | Parameter | Status | Waktu | Output File |
|-------|----------|------|-----------|--------|-------|-------------|
| 1     | S-1 (Single-page)| 240202848 | num_fields=15 | Planned| 09:00 | log_single_r1.csv |
| 2     | S-1 (Single-page)| 240202849 | num_fields=15 | Planned| 10:00 | log_single_r2.csv |
| 3     | S-1 (Single-page)| 240202850 | num_fields=15 | Planned| 11:00 | log_single_r3.csv |
| 4     | S-2 (Multi-step) | 240202848 | num_fields=15 | Planned| 13:00 | log_wizard_r1.csv |
| 5     | S-2 (Multi-step) | 240202849 | num_fields=15 | Planned| 14:00 | log_wizard_r2.csv |
| 6     | S-2 (Multi-step) | 240202850 | num_fields=15 | Planned| 15:00 | log_wizard_r3.csv |

Jumlah runs per skenario : 3 (Within-subject design counterbalanced)
Total runs               : 6 paket sesi pengujian kelompok

DATA LOG (per run):
  Run ID    : RUN-001-SINGLE-248
  Timestamp : 2026-06-29T09:15:22
  Skenario  : S-1 (Single-page Form, Baseline Klinik)
  Input     : Paket Identitas Pasien Dummy Set-A (15 Fields)
  Output    : Task Completion Time: 342.5 detik, Error Count: 4
  Anomali   : Tidak ada (No network lag detected)
  Catatan   : Partisipan sempat kebingungan mencari tombol submit di baris paling bawah.
```

---

## Latihan 1 — Execution Plan

Catatan metodologi: Karena subjek riset melibatkan manusia (staf administrasi klinik), variasi seed digunakan untuk mengacak urutan kemunculan data dummy pasien agar tidak terjadi efek hafalan (learning bias) antar-run.

| Run # | Skenario | Seed | Parameter Kunci | Status |
|-------|----------|------|----------------|--------|
| *1* | Single-page Form | 240202848 | 15 Fields, Urutan Pasien Set-A | Planned |
| *2* | Single-page Form | 240202849 | 15 Fields, Urutan Pasien Set-B | Planned |
| 3 |Single-page Form |240202850 |15 Fields, Urutan Pasien Set-C |Planned |
| 4 |Multi-step Wizard |240202848 |15 Fields, Urutan Pasien Set-A |Planned |
| 5 |Multi-step Wizard |240202849 |15 Fields, Urutan Pasien Set-B |Planned |

**Total skenario:**  2 (Single-page Form vs Multi-step Wizard)
**Run per skenario:**3 iterasi paket kelompok data
**Total run keseluruhan:**6 sesi pengumpulan data

---

## Latihan 2 — Data Log Terstruktur

Desain format data log untuk eksperimen Anda. Tentukan field apa saja yang akan dicatat.

**Identitas:**
| Field | Contoh |
|-------|--------|
| Run ID |RUN-04-WIZARD-248 |
| Timestamp | 2026-06-29T13:05:10 |
|Participant ID |PT-008 (Staf Admin Klinik) |

**Konfigurasi:**
| Field | Contoh |
|-------|--------|
| Seed | 240202848 (Mengunci distribusi data pasien)|
| Code version | git-commit-ae48bc7 |
|Interface Mode |WIZARD_MODE |

**Hasil:**
| Metrik | Tipe Data | Range Valid |
|--------|----------|-------------|
|Task Completion Time | float (detik) | 60.0 – 600.0 detik |
|Error Rate |float (persentase) |0.0% – 100.0% |
|Validation Failures |integer |0 – 15 (Total salah input field) |

**Format output:** [x] CSV / [ ] JSON / [ ] Database / [ ] Lainnya: ____

---

## Latihan 3 — Anomaly Protocol

Rencanakan bagaimana menangani anomali. Untuk setiap jenis, tentukan langkah yang diambil.

| Jenis Anomali | Contoh | Tindakan |
|---------------|--------|----------|
| Run gagal (crash) | Aplikasi JavaFX membeku karena kegagalan koneksi database PostgreSQL | Dokumentasikan kegagalan log database, jalankan skrip reset database pool, ulangi sesi untuk partisipan tersebut dengan seed yang sama. |
| Hasil ekstrem |Partisipan menyelesaikan input wizard dalam 90 detik (jauh di bawah rata-rata 300 detik) |Selidiki apakah partisipan melakukan copy-paste ilegal atau menggunakan data autofill browser. Jika ya, diskualifikasi log data tersebut dan ganti dengan partisipan cadangan. |
| Waktu eksekusi anomali |Input macet lebih dari 10 menit pada satu langkah wizard |Catat sebagai kasus Extreme Cognitive Load atau kegagalan pemahaman navigasi (Did Not Finish / DNF). Jangan hapus datanya, jadikan ini bahan temuan kualitatif pada bab pembahasan |
| Inkonsistensi dengan run lain |Error rate tinggi tetapi completion time sangat cepat |Indikasi pengguna asal mengisi (asal klik submit). Tandai log dengan bendera spammed_input=true, pisahkan dari analisis distribusi normal utama. |

**Prinsip:** Detect → Investigate → Document → Decide

---

## Refleksi

> Pernahkah Anda melaporkan hasil riset/tugas dari single run? Apa risikonya? Bagaimana multiple run mengubah kepercayaan terhadap hasil?

**Pengalaman sebelumnya:**
> Ya, pada tugas pembuatan aplikasi Point of Sale (Agri-POS) sebelumnya, saya sering kali hanya menguji kecepatan transaksi dalam satu kali percobaan saja. Risikonya sangat besar karena angka tunggal tersebut rentan terhadap pencilan (outlier). Bisa saja waktu transaksi terlihat cepat hanya karena data kebetulan sudah tersimpan di dalam cache memori atau komputer sedang berada pada performa puncak, yang tidak mencerminkan kondisi penggunaan harian staf toko yang dinamis.
**Yang akan dilakukan berbeda:**
> Pada riset antarmuka pendaftaran klinik ini, saya menerapkan eksekusi berulang (multiple run) dengan kontrol pengacakan seed. Cara ini secara radikal mengubah tingkat kepercayaan hasil riset karena saya kini memiliki distribusi data statistik yang lengkap (lengkap dengan nilai rata-rata, deviasi standar, serta batas signifikansi $p$-value). Hasil kesimpulan yang ditarik menjadi kokoh, objektif, dapat dipertanggungjawabkan dalam peer-review, dan bebas dari bias kebetulan (cherry-picking). 
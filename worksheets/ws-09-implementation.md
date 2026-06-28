# WS-09: Implementation & Environment

> **Bab 9 — Implementasi Riset & Kontrol Lingkungan**

---

## Ringkasan Materi

### Implementasi Riset ≠ Coding Biasa

Tujuan implementasi riset bukan membuat software yang berfungsi, melainkan membangun **instrumen pengukuran yang konsisten**. Setiap modul harus di-mapping ke variabel (dari Bab 6), parameter harus config-driven, dan logging aktif dari hari pertama.

### Reproducible Implementation Model

```
Design → Implementation → Environment Setup → Execution Consistency → Reproducibility → Trustworthy Result
```

Setiap transisi memiliki syarat:
- Design → Implementation: kode sesuai mapping variabel-ke-komponen
- Implementation → Environment: versi, dependency, seed, path, OS eksplisit
- Environment → Consistency: seed terkunci, urutan deterministik
- Consistency → Reproducibility: dokumentasi lengkap
- Reproducibility → Trust: siapa pun ikuti dokumentasi → hasil sama/serupa

### Repeatability vs Reproducibility

| Level | Peneliti | Environment | Hasil |
|-------|---------|-------------|-------|
| **Repeatability** | Sama | Sama | Sama persis |
| **Reproducibility** | Berbeda | Berbeda (ikuti docs) | Sama/serupa |

Capai **repeatability** dulu, baru **reproducibility**.

### Engineering vs Research Perspective

| Aspek | Engineering | Research |
|-------|-----------|---------|
| Tujuan | Sistem berfungsi untuk user | Instrumen pengukuran konsisten |
| Dependency | Update ke terbaru | Lock di versi spesifik |
| Testing | Unit, integration, E2E | Repeatability test (run ulang → sama?) |
| Dokumentasi | User guide, API docs | Environment spec, execution steps, expected output |
| Config | Default masuk akal | Setiap parameter eksplisit & adjustable |

### Jebakan Kognitif

1. Menunda environment setup → bug sulit dilacak
2. Tidak pakai version control → hasil tidak bisa direkonstruksi
3. Menolak Docker/container → "di laptop saya bisa" saat review
4. 3× hasil sama ≠ repeatable (bisa cache/state tersimpan)

### Istilah Penting

- **Environment Specification** — Deskripsi lengkap: hardware, OS, runtime, library + versi, config, seed
- **Dependency** — Komponen eksternal yang harus di-lock versinya
- **Config-driven** — Parameter dieksternalisasi ke file konfigurasi, bukan hardcode

---

## Template A.9 — Dokumentasi Setup Eksperimen

```
EXPERIMENT SETUP DOCUMENTATION

Hardware:
  CPU     : Intel Core i5-11400H @ 2.70GHz (6 Cores, 12 Threads)
  RAM     : 16 GB DDR4 Dual-Channel
  GPU     : NVIDIA GeForce GTX 1650 4GB / Intel UHD Graphics
  Storage : 512 GB NVMe PCIe SSD

Software:
  OS        : Windows 11 Home Single Language (64-bit)
  Runtime   : Java Development Kit (JDK) 17 LTS
  Framework : JavaFX SDK 17.0.2

Dependencies:
| Library | Version | Sumber | Hash/Checksum |
|---------|---------|--------|---------------|
| openjfx-controls | 17.0.2 | Maven Central | bc41a7e2b197... |
| openjfx-fxml     | 17.0.2 | Maven Central | ad38c92e104f... |
| postgresql-jdbc  | 42.7.1 | Maven Central | f92c81a3d82c... |
| jackson-databind | 2.15.2 | Maven Central | c391b8fa01de... |
| gson             | 2.10.1 | Maven Central | e491b2da91cf... |

Konfigurasi:
  Config file     : src/main/resources/config/experiment_config.json
  Random seed     : 240202848 (Mengunci order dataset input)
  Hyperparameters : mode="wizard"|"single"; num_fields=15; timeout_seconds=600;

Reproducibility Check:
  [x] Dependency terdokumentasi (pom.xml / build.gradle lock file)
  [x] Seed ditetapkan di semua level (Order data input & inisialisasi urutan modul UI)
  [x] Config di version control (Git tracking aktif untuk folder config/)
  [x] README instruksi reproduksi lengkap
```

---

## Latihan 1 — Environment Specification

Dokumentasikan environment untuk eksperimen Anda (boleh environment saat ini atau yang direncanakan).

| Komponen | Spesifikasi |
|----------|------------|
| CPU | Intel Core i5-11400H @ 2.70GHz (6 Cores) |
| RAM | 16 GB DDR4 |
| GPU | NVIDIA GeForce GTX 1650 4GB |
| OS | Windows 11 Home Single Language (64-bit)|
| Runtime |Java Runtime Environment (JRE) 17 LTS |
| Framework |JavaFX SDK 17.0.2 + JDBC Database Connector |
| Random Seed |240202848 (NIM Mahasiswa sebagai pengunci pseudo-random data loading order) |

**Dependencies (minimal 5):**

| Library | Version | Alasan Dibutuhkan |
|---------|---------|-------------------|
| org.openjfx:javafx-controls | 17.0.2 | Membangun elemen antarmuka form (TextField, Button, Progress Bar) |
|org.openjfx:javafx-fxml |17.0.2 |Mendefinisikan layout UI Multi-step dan Single-page menggunakan XML |
|org.postgresql:postgresql |42.7.1 |Driver JDBC untuk koneksi database rekam medis dan logging internal |
|com.google.code.gson:gson |2.10.1 |Membaca file konfigurasi parameter eksperimen berformat JSON |
|org.apache.logging.log4j:log4j-core |2.20.0 |Logging otomatis timestamp presisi milidetik untuk Task Completion Time |

---

## Latihan 2 — Repeatability Test Plan

Rancang tes repeatability sederhana: jalankan kode yang sama 3× di environment yang sama.

| Run | Seed | Metrik Utama | Hasil Sama? |
|-----|------|-------------|-------------|
| 1 |240202848 |Rata-rata Task Completion Time & Error Rate | — |
| 2 |240202848 |Rata-rata Task Completion Time & Error Rate | [x] Ya / [ ] Tidak |
| 3 |240202848 |Rata-rata Task Completion Time & Error Rate | [x] Ya / [ ] Tidak |

**Jika hasil berbeda, kemungkinan penyebab:**
> Perbedaan interferensi background process OS Windows 11 (seperti Windows Update atau Antivirus background scan) yang memengaruhi akurasi clock timer kelas System.currentTimeMillis() di Java, atau efek kelelahan fisik/pembelajaran manual (human learning effect) dari partisipan jika dijalankan berturut-turut tanpa jeda istirahat yang diatur.
**Checklist kontrol yang sudah diterapkan:**
- [x] Random seed di-set di semua level
- [x] Tidak ada background process yang mengganggu
- [x] Cache dibersihkan antar-run
- [x] Config file yang sama untuk semua run

---

## Latihan 3 — README Eksperimen

Tulis README minimum untuk eksperimen Anda (6 komponen wajib).

```
# Judul Eksperimen: Analisis Komparatif Multi-step Wizard vs Single-page Form pada Sistem Pendaftaran Klinik Pratama

## 1. Environment
- Hardware: CPU Intel i5-11400H, RAM 16GB, GPU GTX 1650 4GB.
- Software: Windows 11, JDK 17 LTS, JavaFX 17.0.2, PostgreSQL 42.7.1.

## 2. Installation
1. Pastikan PostgreSQL Server aktif dan buat database bernama `klinik_research`.
2. Clone repositori proyek JavaFX ini.
3. Jalankan perintah instalasi dependency via Maven:
   `mvn clean install`

## 3. Data
- Sumber Data: 100 Dataset dummy identitas pasien (Nama, KTP, Nomor Asuransi, Alamat, Poli Tujuan) yang di-generate via seed tetap.
- Format: JSON database dump (`dummy_pasien.json`).
- Ukuran: ~150 KB.

## 4. Execution
Jalankan aplikasi eksperimen menggunakan command Maven berikut:
`mvn javafx:run`

## 5. Configuration
File konfigurasi terletak di `src/main/resources/config/experiment_config.json`.
Parameter kunci:
- "ui_mode": "WIZARD" atau "SINGLE_PAGE"
- "seed": 240202848
- "num_fields": 15

## 6. Expected Output
Aplikasi akan secara otomatis mengekspor berkas log berformat CSV ke direktori `output/result_log.csv` dengan format kolom:
`timestamp, user_id, ui_mode, task_completion_time_ms, error_count`
```

---

## Refleksi

> Apakah eksperimen Anda saat ini bisa direproduksi oleh orang lain tanpa bantuan Anda? Komponen apa yang masih hilang?

**Level saat ini:** [x] Repeatability / [ ] Reproducibility / [ ] Belum keduanya
**Komponen yang belum terdokumentasi:**
> Saat ini sistem baru mencapai tingkat repeatability karena pengujian internal pada laptop saya menghasilkan data yang konsisten. Komponen yang masih hilang untuk mencapai reproducibility penuh di laptop orang lain adalah standarisasi environment OS (solusinya adalah menyusun Docker container atau menyertakan Java Runtime Environment runtime-image launcher agar perbedaan versi sistem operasi penguji tidak memicu inkonsistensi rendering UI JavaFX).
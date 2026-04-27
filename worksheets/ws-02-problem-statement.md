# WS-02: Problem Statement

> **Bab 2 — Problem Formulation & System Context**

---

## Ringkasan Materi

### Problem Formation Model

Masalah riset melewati 5 tahap transformasi. Melompat langsung dari Reality ke Variable adalah kesalahan paling umum.

```
Reality → Observed Issue (Symptom) → Diagnosed Problem (Root Cause)
→ Researchable Problem (Scoped) → Measurable Variable (Operationalized)
```

### Topic ≠ Problem ≠ Research Problem

| Level | Contoh | Status |
|-------|--------|--------|
| **Topik** | UI/UX Sistem Informasi Kesehatan | Terlalu luas, tidak bisa diuji |
| **Problem** | Alur pendaftaran pasien pada aplikasi klinik terlalu lambat| Spesifik tapi belum riset |
| **Research Problem** | Analisis perbandingan Multi-step Form vs Single-page Form terhadap Task Completion Time pada staf administrasi klinik | Bisa dirancang eksperimennya |

### Symptom vs Root Cause

-Symptom (Gejala): Antrean pendaftaran di klinik sangat panjang.
-Root Cause (Akar Masalah): Desain formulir digital terlalu padat (rumit), sehingga petugas lama saat mengisi data.

### System Thinking

Input: Data KTP & Asuransi pasien.
Process: Petugas mengisi formulir di layar komputer.
Output: Nomor antrean & data pasien tersimpan.
Outcome: Pendaftaran jadi lebih cepat & antrean berkurang. **.

### Problem Quality Check

Masalah riset yang layak harus memenuhi 5 kriteria:
- **Clarity** — Jelas (memperbaiki desain formulir).
- **Measurability** — Terukur (menghitung waktu/detik).
- **Relevance** — Penting (agar pasien tidak menunggu lama).
- **Testability** — Bisa diuji (bandingkan desain A vs desain B).
- **Impact** — Bermanfaat (bisa dipakai di klinik lain).

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan | Yang penting masalah selesai dan sistem jalan. | Mencari kebenaran atau membandingkan mana yang lebih baik. |
| Masalah | Bug, error, atau ada fitur yang belum dibuat. | Belum ada data atau bukti empiris tentang suatu hal. |
| Scope | Harus menyelesaikan semua fitur agar aplikasi bisa dipakai. | Fokus pada satu titik masalah saja agar bisa dibuktikan secara mendalam. |
| Output | Aplikasi, website, atau alat yang berfungsi (working system). | Data statistik, makalah ilmiah (paper), dan temuan yang bisa diulang. |

### Istilah Penting

- **Problem Statement** — Kalimat kunci yang merangkum apa yang salah, mengapa itu masalah, dan apa dampaknya jika tidak diperbaiki. Tanpa ini, riset tidak punya arah.
- **System Context** — Peta besar dari apa yang kamu teliti. Kamu harus tahu apa yang masuk (Input), apa yang dikerjakan (Process), dan apa hasil akhirnya (Output).
- **Problem Drift** — Bahaya laten di mana masalahmu "bergeser". Misalnya: di awal ingin meriset kecepatan, tapi di akhir malah membahas tampilan. Ini terjadi jika Problem Statement tidak kuat.
- **Solution-First Thinking** — Kesalahan umum mahasiswa. Langsung ingin "bikin aplikasi Android" padahal belum tahu masalah apa yang ingin diselesaikan. Riset dimulai dari Masalah, bukan Solusi.
- **Operational Definition** — Cara kamu mengukur sesuatu agar tidak bias.
Contoh: Kamu bilang aplikasinya "Cepat". "Cepat" itu relatif. Definisi operasionalnya adalah: "Waktu loading di bawah 2 detik pada jaringan 4G."
---

## Template A.2 — Problem Statement Builder

```
PROBLEM STATEMENT BUILDER

Domain & Konteks
  Domain   : Human-Computer Interaction (HCI) / Rekayasa Perangkat Lunak.
  Konteks  : Sistem Manajemen Pendaftaran Klinik Pratama.

System Context
  Input       : Dokumen identitas pasien, pilihan poli, dan data asuransi.
  Process     : Entri data melalui formulir digital dan validasi sistem.
  Output      : Rekam medis digital tersimpan dan nomor antrean tercetak.
  Outcome     : Pengurangan waktu tunggu pendaftaran (efisiensi layanan).
  Constraints : Kapasitas RAM komputer administrasi rendah dan beban kerja tinggi pada jam sibuk.
  Stakeholders: Staf Administrasi (User), Pasien, dan Manajer Klinik.

Fenomena → Problem
  Fenomena yang diamati             :Terjadi penumpukan antrean pasien yang signifikan di area pendaftaran setiap pagi.
  Gejala (symptom) yang terukur     : Waktu rata-rata pendaftaran mencapai 7 menit per pasien dengan tingkat kesalahan input data sebesar 15%.
  Masalah yang didiagnosis          : Beban kognitif berlebih pada petugas karena desain formulir single-page yang menampilkan terlalu banyak bidang input sekaligus.
  Masalah riset (researchable)      : Efektivitas penerapan desain Multi-step Wizard dalam mereduksi waktu penyelesaian tugas (Task Completion Time) dibandingkan desain Single-page.
  Variabel yang terukur             : Waktu penyelesaian (detik) dan jumlah kesalahan input (Error Rate).
Problem Quality Check
  [x] Clarity — Jelas, membandingkan dua model struktur formulir.
  [x] Measurability — Menggunakan metrik waktu (detik) dan persentase.
  [x] Relevance — Sangat penting bagi produktivitas staf kesehatan.
  [x] Testability — Bisa diuji secara empiris melalui A/B testing.
  [x] Impact — Memberikan standar desain baru untuk sistem informasi medik.

Problem Statement (1 paragraf):
 Meskipun sistem informasi klinik telah tersedia, proses pendaftaran pasien saat ini masih tidak efisien dengan rata-rata waktu input mencapai 7 menit per pasien, yang mengakibatkan penumpukan antrean panjang. Masalah ini berakar pada desain antarmuka formulir single-page yang padat sehingga meningkatkan beban kognitif staf administrasi saat memproses data. Penelitian ini bertujuan untuk menganalisis perbandingan efektivitas antara struktur Multi-step Wizard dan Single-page Form terhadap Task Completion Time dan tingkat kesalahan data. Dengan mengukur performa pengguna secara kuantitatif, penelitian ini diharapkan dapat memberikan solusi desain antarmuka yang optimal untuk meningkatkan efisiensi operasional pada layanan kesehatan primer.
```

---

## Latihan 1 — Dari Topik ke Masalah Riset

Pilih satu topik di bidang TI yang diminati. Transformasikan melalui 5 tahap Problem Formation Model.

**Topik awal:**Optimasi User Interface pada Sistem Pendaftaran Klinik
| Tahap | Hasil |
|-------|-------|
| Reality | Petugas administrasi klinik merasa kewalahan dan sering salah menginput data saat jam sibuk pendaftaran pasien. |
| Observed Issue (Symptom) | Waktu pendaftaran rata-rata mencapai 7 menit per pasien dan terdapat 15% kesalahan data pada rekam medis awal. |
| Diagnosed Problem (Root Cause) |Arsitektur informasi formulir digital terlalu padat (overcrowded), menyebabkan beban kognitif tinggi pada petugas. |
| Researchable Problem |Sejauh mana implementasi desain Multi-step Wizard dapat meningkatkan efisiensi waktu input dibandingkan dengan model Single-page Form? |
| Measurable Variable |Task Completion Time (detik) dan Error Rate (persentase kesalahan input). |

**Apakah terjebak solution-first thinking?** [ ] Ya / [x] Tidak
> Jika ya, kembali ke tahap mana?Karena fokus penelitian adalah pada alur interaksi dan navigasi formulir

---

## Latihan 2 — System Context Decomposition

Gambarkan konteks sistem dari masalah riset di Latihan 1.

| Komponen | Deskripsi |
|----------|----------|
| Input | Berupa data identitas fisik pasien (KTP/Kartu Asuransi) dan pilihan poliklinik tujuan. |
| Process |Interaksi pengguna dengan elemen formulir digital (navigasi, pengetikan, dan validasi data). |
| Output |Data digital yang tersimpan di database dan cetakan fisik nomor antrean pasien. |
| Outcome |Berkurangnya durasi tunggu pasien di area lobi karena proses registrasi yang lebih cepat. |
| Constraints |Keterbatasan spesifikasi monitor (resolusi rendah) dan tingkat literasi digital petugas yang bervariasi. |
| Stakeholders |Staf Administrasi (pengguna utama), Pasien (objek layanan), dan Manajer Operasional Klinik. |

**Komponen mana yang paling relevan dengan masalah riset?** _______________

---

## Latihan 3 — Problem Quality Check

Evaluasi problem statement yang sudah dibuat menggunakan 5 kriteria.

| Kriteria | Skor (1-5) | Justifikasi |
|----------|-----------|-------------|
| Clarity | 5 |Masalah sangat jelas: membandingkan dua metode desain formulir secara spesifik |
| Measurability | 5 |Sangat terukur menggunakan satuan waktu (detik) dan jumlah kesalahan (error rate). |
| Relevance |5 |Sangat relevan untuk meningkatkan efisiensi layanan publik di bidang kesehatan. |
| Testability |4 |Bisa diuji dengan metode A/B Testing, meski butuh partisipan (petugas) yang konsisten. |
| Impact |4 |Memberikan standar desain baru yang bisa diaplikasikan di berbagai sistem informasi medis. |

**Skor total:** 23 / 25

**Problem statement versi final (1 paragraf):**
> Proses pendaftaran pasien di klinik saat ini mengalami kendala efisiensi dengan durasi rata-rata 7 menit per pasien dan tingkat kesalahan input mencapai 15%. Hal ini disebabkan oleh desain antarmuka formulir single-page yang terlalu padat, sehingga meningkatkan beban kognitif petugas administrasi. Penelitian ini bertujuan untuk menganalisis efektivitas desain Multi-step Wizard dalam mereduksi Task Completion Time dibandingkan dengan model Single-page Form. Melalui pengukuran metrik waktu dan akurasi data secara kuantitatif, penelitian ini diharapkan dapat membuktikan model arsitektur informasi yang paling optimal untuk mendukung produktivitas staf pada sistem manajemen kesehatan.
---

## Refleksi

> Bandingkan "masalah" yang biasa ditemui saat coding (bug, error) dengan masalah riset. Apa perbedaan fundamental dalam cara mendefinisikan dan mendekati keduanya?

**Jawaban:**
> Perbedaan fundamentalnya terletak pada titik akhir dan kedalaman pembuktian. Masalah coding (bug/error) bersifat teknis dan solutif; tujuannya adalah memperbaiki sistem agar "berjalan" sesuai fungsinya. Sedangkan masalah riset bersifat saintifik; tujuannya bukan hanya membuat sistem berjalan, melainkan mencari "kebenaran" atau "bukti" mengapa suatu metode lebih baik dari metode lainnya. Coding menyelesaikan masalah sistem, sementara riset menyelesaikan ketidaktahuan manusia melalui data yang dapat dipertanggungjawabkan secara ilmiah.
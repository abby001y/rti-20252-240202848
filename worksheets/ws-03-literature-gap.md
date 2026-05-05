# WS-03: Literature Mapping & Gap

> **Bab 3 — Literature Review, Research Gap & Baseline**

---

## Ringkasan Materi

### Literature Review = Positioning, Bukan Ringkasan

Literature review bukan merangkum paper satu per satu. Pendekatan yang benar adalah **concept-centric** — organisasi berdasarkan tema, metode, atau variabel. Tujuan: menemukan **pola, kontradiksi, dan gap**.

### Empat Jenis Research Gap

| Jenis Gap | Deskripsi | Contoh |
|-----------|----------|--------|
| **Performance Gap** | Performa belum memadai | Akurasi deteksi hanya 78% pada kasus tertentu |
| **Method Gap** | Pendekatan belum diterapkan | Belum ada yang pakai transformer untuk task ini |
| **Data Gap** | Dataset terbatas/tidak representatif | Semua studi pakai dataset sintetis |
| **Context Gap** | Belum diuji pada konteks berbeda | Belum ada evaluasi di negara berkembang |

Gap terkuat = kombinasi 2+ jenis.

### Systematic Search Strategy

1. **Database**: IEEE Xplore, ACM DL, Scopus, Google Scholar
2. **Boolean query** yang terdokumentasi eksplisit
3. **Snowballing**: backward (telusuri referensi) + forward (cari yang mengutip)
4. Klaim "belum ada penelitian" harus didukung **bukti pencarian**

### Baseline Selection — 3 Kriteria

| Kriteria | Pertanyaan |
|----------|-----------|
| **Relevan** | Apakah menyelesaikan masalah yang sama? |
| **Representatif** | Apakah mewakili common practice? |
| **State-of-the-Art** | Apakah terbaru/terbaik? |

Membandingkan deep learning 2024 dengan decision tree sederhana tanpa justifikasi = **straw man comparison** (perbandingan tidak jujur).

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan baca literatur | Mencari solusi yang sudah ada | Memahami apa yang belum terjawab |
| Cara membaca paper | Tutorial, how-to | Metode, limitasi, gap |
| Baseline | Framework terpopuler | State-of-the-art yang rigorous |
| Dokumentasi pencarian | Tidak diperlukan | Wajib (reproducible) |

### Istilah Penting

- **Concept-centric** — Organisasi literatur berdasarkan konsep/metode, bukan per penulis
- **Snowballing** — Backward (telusuri referensi) + Forward (cari yang mengutip paper kunci)
- **Research Position** — Pernyataan eksplisit posisi riset terhadap studi sebelumnya
- **Straw man comparison** — Memilih baseline lemah agar metode sendiri terlihat lebih baik

---

## Template A.3 — Literature Mapping & Gap Identification

```
LITERATURE MAPPING

Topik      : Perbandingan Multi-step Wizard vs Single-page Form pada Sistem Pendaftaran Klinik
Database   : Google Scholar, ACM Digital Library
Query      : ("multi-step form" OR "wizard interface") AND ("single page form") AND ("usability" OR "task completion time" OR "error rate")
Tahun      : 2020–2024
Hasil awal : 95 paper → Screening → 5 paper final

Literature Matrix (concept-centric):

| Study | Tahun | Method | Data | Result | Limitation |
|-------|-------|--------|------|--------|------------|
| Zhou et al. | 2020 | Usability Experiment | 72 participants | Multi-step mengurangi cognitive load | Tidak mengukur error rate |
| Zhang et al. | 2021 | HCI Experiment | 80 users | Multi-step lebih efisien pada form kompleks | Tidak dalam domain klinik |
| Kim & Lee | 2022 | A/B Testing | Web users | Wizard meningkatkan task completion time | Sampel terbatas |
| Patel et al. | 2023 | Controlled Experiment | 100 users | Multi-step menurunkan error rate | Tidak mengukur waktu detail |
| Alshammari et al. | 2024 | UX Comparative Study | 75 participants | Multi-step lebih baik dalam akurasi input | Bukan pengguna profesional |

Pola yang ditemukan:
  Metode dominan     : Usability testing dan controlled experiment
  Dataset umum       : Pengguna umum (non-profesional)
  Limitasi berulang  : Tidak dalam konteks klinik, variabel tidak lengkap, sampel tidak representatif

GAP IDENTIFICATION

Gap 1: [Jenis: Context Gap]
  Deskripsi    : Studi belum dilakukan dalam konteks sistem pendaftaran klinik
  Bukti        : Semua penelitian menggunakan web form umum atau survey online
  Signifikansi : Lingkungan klinik memiliki tekanan waktu tinggi yang memengaruhi performa pengguna

Gap 2: [Jenis: Data Gap]
  Deskripsi    : Partisipan bukan staf administrasi sebagai pengguna nyata
  Bukti        : Dataset didominasi oleh user umum/partisipan eksperimen
  Signifikansi : Hasil penelitian tidak sepenuhnya representatif terhadap kondisi kerja nyata

Baseline Selection:
| Baseline | Relevansi | Representatif | Source |
|----------|-----------|---------------|--------|
| Single-page Form | Digunakan di sistem eksisting klinik | Umum pada sistem lama | Zhou et al., 2020 |
| Multi-step Wizard | Metode yang diuji dalam banyak studi | Common practice modern UI | Patel et al., 2023 |
```

---

## Latihan 1 — Concept-Centric Literature Table

Gunakan topik riset dari WS-02. Cari minimal 5 paper relevan menggunakan Google Scholar atau database lain.

**Topik riset:**Perbandingan Multi-step Wizard vs Single-page Form terhadap Task Completion Time dan Error Rate
**Query pencarian:** ("multi-step form" OR "wizard interface") AND ("single page form") AND ("usability" OR "task completion time" OR "error rate")
**Database:** Google Scholar

| # | Study             | Tahun | Method               | Dataset     | Result                                     | Limitasi                |
| - | ----------------- | ----- | -------------------- | ----------- | ------------------------------------------ | ----------------------- |
| 1 | Zhou et al.       | 2020  | Usability Experiment | 72 pengguna | Multi-step mengurangi beban kognitif       | Tidak ukur error        |
| 2 | Zhang et al.      | 2021  | HCI Experiment       | 80 user     | Multi-step lebih cepat untuk form kompleks | Tidak domain klinik     |
| 3 | Kim & Lee         | 2022  | A/B Testing          | Web users   | Wizard meningkatkan efisiensi              | Sampel kecil            |
| 4 | Patel et al.      | 2023  | Experiment           | 100 user    | Multi-step menurunkan error                | Tidak ukur waktu detail |
| 5 | Alshammari et al. | 2024  | Comparative Study    | 75 user     | Multi-step lebih akurat                    | Bukan user profesional  |

**Pola yang terlihat — Metode dominan:** Eksperimen usability (A/B testing, controlled experiment)
**Limitasi yang berulang:** Dataset menggunakan pengguna umum (bukan staf profesional)
Tidak dalam konteks sistem kesehatan/klinik

---

## Latihan 2 — Gap Identification

Berdasarkan tabel di Latihan 1, identifikasi gap.

| Jenis Gap       | Ditemukan? | Gap Statement                                                                   |
| --------------- | ---------- | ------------------------------------------------------------------------------- |
| Performance Gap | [x] Ya     | Hasil penelitian menunjukkan hasil yang bervariasi tergantung kompleksitas form |
| Method Gap      | [ ] Tidak  | Metode eksperimen sudah umum digunakan                                          |
| Data Gap        | [x] Ya     | Dataset tidak menggunakan pengguna nyata (staf klinik)                          |
| Context Gap     | [x] Ya     | Tidak ada studi dalam konteks sistem pendaftaran klinik                         |


**Gap utama yang dipilih:**Context Gap + Data Gap
**Mengapa gap ini penting (bukan sekadar "belum ada yang meneliti")?**
> Meskipun banyak penelitian telah membandingkan multi-step dan single-page form, studi tersebut dilakukan pada konteks umum dengan pengguna non-profesional. Dalam sistem klinik, staf administrasi bekerja di bawah tekanan waktu dan beban kerja tinggi, sehingga performa mereka dapat berbeda secara signifikan. Oleh karena itu, hasil penelitian sebelumnya tidak dapat langsung digeneralisasi, sehingga diperlukan penelitian yang lebih kontekstual dan representatif.
---

## Latihan 3 — Baseline Selection

Pilih 2 baseline dari literatur yang sudah dibaca.

| # | Baseline          | Mengapa Relevan                     | Mengapa Representatif         | Apakah SOTA? | Sumber             |
| - | ----------------- | ----------------------------------- | ----------------------------- | ------------ | ------------------ |
| 1 | Single-page Form  | Digunakan di sistem klinik saat ini | Banyak dipakai di sistem lama | Tidak        | Zhou et al., 2020  |
| 2 | Multi-step Wizard | Metode utama yang dibandingkan      | Umum di desain modern         | Ya           | Patel et al., 2023 |


**Apakah pemilihan baseline ini bisa dianggap straw man?** [ ] Ya / [x] Tidak
> Justifikasi:Kedua baseline merupakan pendekatan yang benar-benar digunakan dalam praktik dan literatur, sehingga perbandingan bersifat adil dan tidak dibuat-buat untuk menguntungkan salah satu metode.
---

## Refleksi

> Apa perbedaan antara "belum ada yang meneliti ini" (klaim tanpa bukti) dengan research gap yang valid? Bagaimana cara membuktikan bahwa sebuah gap benar-benar ada?

**Jawaban:**
>Klaim “belum ada yang meneliti ini” tidak valid jika tidak didukung oleh pencarian literatur yang sistematis. Research gap yang valid harus didasarkan pada analisis beberapa studi yang menunjukkan adanya keterbatasan, inkonsistensi, atau kekosongan tertentu.

> Untuk membuktikan gap, peneliti harus menunjukkan proses pencarian (database, query, jumlah paper), lalu mengidentifikasi pola dan limitasi yang berulang. Gap yang kuat biasanya bukan karena tidak ada penelitian sama sekali, tetapi karena penelitian yang ada belum mencakup aspek penting seperti konteks, data, atau performa.

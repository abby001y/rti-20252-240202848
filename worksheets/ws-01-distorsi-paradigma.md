# WS-01: Distorsi & Paradigma

> **Bab 1 — Research Mindset in IT**

---

## Ringkasan Materi

### Research Trust Model

Pengetahuan ilmiah tidak muncul langsung dari kenyataan. Ia melewati **6 tahap transformasi** yang masing-masing rawan distorsi:

```
Reality → Data → Processing → Analysis → Inference → Knowledge
```

Etika mencegah distorsi yang disengaja (fabrikasi, cherry-picking). Validitas mendeteksi distorsi yang tidak disengaja (confounding variable, sampling bias).

### Tiga Jenis Validitas

| Jenis | Pertanyaan | Contoh Ancaman |
|-------|-----------|----------------|
| **Internal Validity** | Apakah hubungan kausal benar ada? | Confounding variable |
| **External Validity** | Apakah bisa digeneralisasi? | Dataset terlalu homogen |
| **Construct Validity** | Apakah mengukur hal yang benar? | Metrik tidak sesuai klaim |

### Paradigma Riset

Mata kuliah ini menggunakan pendekatan **Positivist** (fenomena TI bisa diukur objektif melalui eksperimen terkontrol) diperkuat **Design Science Research** (artefak dibuat sebagai instrumen pengujian hipotesis, bukan tujuan akhir).

### Mode Berpikir Peneliti

**Curious** (mempertanyakan fenomena) → **Critical** (mengevaluasi klaim berdasarkan bukti) → **Systematic** (merancang investigasi terstruktur dan reproducible).

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan | Membuat sistem yang bekerja | Menghasilkan pengetahuan yang valid |
| Pertanyaan khas | "Bagaimana membuatnya jalan?" | "Apakah klaim ini benar?" |
| Ukuran sukses | Sistem berfungsi, client puas | Hipotesis terjawab, temuan tervalidasi |
| Kegagalan | Harus dihindari | Harus dilaporkan (negative result = kontribusi) |

### Istilah Penting

- **Research Mindset** — Pola pikir yang menuntut bukti dan mempertanyakan asumsi
- **Research Ethics** — Prinsip perilaku: kejujuran, objektivitas, keterbukaan, akuntabilitas
- **HARKing** — Hypothesizing After Results are Known — merumuskan hipotesis setelah melihat data
- **Falsifiability** — Hipotesis harus bisa dibuktikan salah

---

## Template A.1 — Research Mindset Self-Assessment

```
Nama Peneliti    : Abbi Priyoguno
Tanggal          : 13 April 2026

1. Ketika membaca klaim "metode X 95% akurat":
   - Pertanyaan pertama saya:Apakah dataset yang digunakan seimbang (balanced) dan apakah 95% itu hasil dari lingkungan pengujian yang ideal atau realitas?
   - Data yang dibutuhkan untuk verifikasi:Distribusi data pengujian, metrik Precision/Recall, dan detail mengenai baseline pembandingnya.
2. Posisi paradigma:
   - Pendekatan: [ ] Positivis  [ ] Interpretivis  [x] Design Science  [ ] Mixed
   - Alasan: Fokus utama saya adalah menciptakan solusi digital (artefak) untuk masalah operasional nyata, di mana efektivitas sistem diuji melalui implementasi teknis.

3. Identifikasi distorsi:
   - Asumsi tersembunyi:Pengguna selalu memasukkan data dengan format yang benar.
   - Sumber bias potensial: Sampling bias (hanya menguji pada satu jenis perangkat high-end).
   - Langkah mitigasi: Melakukan stress testing dengan berbagai skenario data ekstrem dan perangkat yang beragam.

4. Komitmen etika:
   - Data yang tidak akan dimanipulasi: Seluruh data mentah (raw data) hasil eksperimen, termasuk nilai fitness pada algoritma genetika yang tidak konvergen, log kegagalan sistem, serta data transaksi asli yang digunakan sebagai sampel pengujian tanpa mengubah angka untuk mempercantik hasil akurasi.
   - Batasan yang diakui sejak awal:Penelitian ini hanya diuji pada lingkungan terbatas (misalnya: local server), dataset yang digunakan mungkin belum mencakup seluruh variasi produk di pasar luas, dan performa algoritma sangat bergantung pada spesifikasi perangkat keras yang digunakan saat pengujian.
```

---

## Latihan 1 — Identifikasi Distorsi

Pilih satu paper riset di bidang TI yang mengklaim "metode X meningkatkan performa." Telusuri setiap tahap Research Trust Model.

**Paper yang dipilih:**
> Judul: _______________________________________________
> Penulis (Tahun): ______________________________________

| Tahap | Apa yang Dilakukan | Potensi Distorsi |
|-------|-------------------|-----------------|
| Reality → Data | Mengambil data transaksi dari 1 toko. | Sampling Bias: Data tidak mewakili perilaku konsumen di toko lain. |
| Data → Processing |Membersihkan data transaksi yang kosong. |Data Cleaning Bias: Menghapus data unik yang mungkin merupakan pola penting. |
| Processing → Analysis |Menjalankan GA dengan parameter statis. |Parameter Bias: Hasil hanya optimal pada rentang nilai tertentu saja.
| Analysis → Inference |Menyimpulkan metode ini meningkatkan laba. |Causal Fallacy: Bisa saja laba naik karena faktor eksternal (hari raya), bukan algoritma. |
| Inference → Knowledge |Publikasi klaim "Solusi Stok Terbaik". |Overgeneralization: Mengklaim berlaku untuk semua jenis bisnis ritel. |

**Distorsi paling besar di tahap:** Analysis → Inference
**Dua distorsi spesifik yang teridentifikasi:**
1. Hardware-Dependent Performance Bias
Pernyataan bahwa sistem sangat cepat tanpa mengakui bahwa pengujian dilakukan pada mesin dengan spesifikasi high-end. Hal ini menciptakan distorsi karena performa tersebut tidak akan tercapai pada perangkat rata-rata yang digunakan oleh target pengguna (misalnya, smartphone murah untuk Agri-POS).

2. Cherry-picking Success Scenarios
Hanya melaporkan hasil running algoritma genetika ketika ia berhasil menemukan nilai optimal (global optima) dalam iterasi cepat, dan mengabaikan atau menghapus data saat algoritma mengalami premature convergence atau stuck di nilai buruk.
---

## Latihan 2 — Analisis Kasus Etika

Skenario: Seorang peneliti menemukan bahwa jika 3 data point outlier dihapus, hasil eksperimennya menjadi signifikan. Dengan outlier, hasilnya tidak signifikan.

| Perspektif | Analisis |
|------------|---------|
| Kejujuran ilmiah | Menyembunyikan outlier demi signifikansi adalah bentuk pembohongan data (falsification). |
| Transparansi |Peneliti harus menjelaskan kriteria pembuangan outlier secara eksplisit di bab metodologi. |
| Peer review |Reviewer butuh data mentah untuk memastikan bahwa outlier tersebut memang error teknis, bukan variasi alami. |

**Keputusan akhir dan justifikasi:**
> Melaporkan hasil dengan kedua kondisi (dengan dan tanpa outlier). Jika hasilnya berbeda jauh, peneliti harus mendiskusikan mengapa data tersebut dianggap outlier dan apa dampaknya bagi penerapan di dunia nyata.

---

## Latihan 3 — Posisi Paradigma

**Topik riset:** ________________________________________

| Kriteria | Positivis | Interpretivis | Design Science |
|----------|-----------|---------------|----------------|
| Kesesuaian dengan topik (1–5) | 4| 2 | 5 |
| Jenis data yang dikumpulkan |Waktu penetrasi, jumlah celah. |Waktu penetrasi, jumlah celah. |Persepsi admin terhadap keamanan. |Keandalan skema enkripsi yang dibuat. |
| Limitasi paradigma |Terlalu kaku pada angka. |Sangat subjektif. |Fokus pada alat, terkadang lupa teori dasar. |

**Paradigma yang dipilih:** Design Science
**Alasan:** Riset ini bertujuan membangun mekanisme pertahanan database yang lebih baik melalui pengembangan artefak keamanan.

---

## Refleksi

> Sebelum membaca materi ini, apakah pernah mempertanyakan klaim "95% akurat"? Setelah memahami rantai distorsi, pertanyaan apa yang sekarang akan diajukan saat membaca paper?

**Jawaban:**
> Sebelum membaca ini, saya sering melihat angka persentase sebagai keberhasilan mutlak proyek coding. Sekarang, saya akan lebih skeptis dan menanyakan: "Seberapa representatif data yang digunakan?" serta "Apakah ada variabel pengganggu yang membuat angka itu terlihat bagus secara semu?"
> ___________________________________________________

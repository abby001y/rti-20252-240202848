# WS-05: Variabel & Metrik

> **Bab 5 — Metric, Measurement & Data**

---

## Ringkasan Materi

### Measurement Alignment Model

Setiap pengukuran yang valid harus bisa ditelusuri melalui rantai ini tanpa lompatan logis:

```
Problem → Concept → Variable → Metric → Data → Result
```

### Operationalization = Keputusan Desain

Menerjemahkan konsep abstrak menjadi variabel terukur bukan proses mekanis. "Code quality" yang diukur via SonarQube code smells membawa asumsi implisit. Setiap operasionalisasi harus didokumentasikan dan dijustifikasi.

### Empat Tipe Data (NOIR)

| Tipe | Ciri | Contoh | Operasi Valid |
|------|------|--------|---------------|
| **Nominal** | Kategori, tanpa urutan | Jenis algoritma (RF, SVM, CNN) | Modus, chi-square |
| **Ordinal** | Urutan, interval tidak sama | Skala Likert (1-5) | Median, Spearman |
| **Interval** | Jarak bermakna, tanpa nol absolut | Suhu Celsius | Mean, Pearson, t-test |
| **Ratio** | Jarak bermakna + nol absolut | Waktu eksekusi (ms) | Semua operasi |

Tipe data menentukan uji statistik yang valid. Kebanyakan metrik performa TI = ratio; persepsi pengguna = ordinal.

### Kriteria Pemilihan Metrik

- **Representative** — Mewakili konsep yang diteliti
- **Sensitive** — Cukup peka menangkap perbedaan bermakna (hindari ceiling effect)
- **Feasible** — Bisa dikumpulkan dalam batasan waktu dan biaya

### Pre-registration

Metrik harus ditentukan **sebelum** eksperimen. Memilih metrik setelah melihat data = **p-hacking**. Metrik tambahan yang ditemukan kemudian dilaporkan sebagai *exploratory*, bukan *confirmatory*.

### Primary vs Secondary Metric

- **Primary Metric** — Langsung terikat ke hipotesis, menentukan kesimpulan
- **Secondary Metric** — Pendukung, dilaporkan di samping primary; statusnya suplementer

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Pemilihan metrik | Berdasarkan kebiasaan/tool yang ada | Berdasarkan construct validity |
| Anomali | Dihapus untuk laporan bersih | Diinvestigasi — bisa jadi temuan |
| Kapan dipilih | Setelah sistem jadi (monitoring) | Sebelum eksperimen (by design) |

### Istilah Penting

- **Operationalization** — Transformasi konsep abstrak menjadi variabel terukur
- **Construct Validity** — Sejauh mana pengukuran benar-benar mengukur konsep yang dimaksud
- **Measurement Scale** — Klasifikasi data (NOIR) yang menentukan analisis valid
- **Multi-metric Evaluation** — Menggunakan beberapa metrik untuk menangkap konsep kompleks

---

## Template A.5 — Definisi Variabel, Metrik & Justifikasi

```
VARIABLE & METRIC DEFINITION

Research Question:
Apakah desain Multi-step Wizard menghasilkan Task Completion Time yang lebih rendah dan Error Rate yang lebih kecil dibandingkan Single-page Form pada sistem pendaftaran klinik?

| Variabel | Tipe | Konsep | Metrik | Skala | Satuan | Cara Mengukur | Justifikasi |
|----------|------|--------|--------|-------|--------|---------------|-------------|
| Jenis Form (Multi-step vs Single-page) | IV | Desain antarmuka | Kategori (Multi-step / Single-page) | Nominal | — | Menentukan jenis UI yang digunakan saat eksperimen | Mewakili perbedaan desain yang diuji |
| Task Completion Time | DV | Efisiensi kerja | Waktu penyelesaian | Ratio | Detik | Mengukur waktu dari mulai input hingga selesai | Langsung merepresentasikan efisiensi |
| Error Rate | DV | Akurasi input | Persentase kesalahan | Ratio | % | Jumlah error / total input × 100% | Mengukur kualitas hasil kerja |
| Pengalaman pengguna | CV | Pengalaman kerja | Lama kerja (tahun) | Ratio | Tahun | Data dari responden | Mengontrol bias skill pengguna |
| Kompleksitas form | CV | Beban tugas | Jumlah field | Ratio | Jumlah field | Ditentukan dari desain form | Mengontrol tingkat kesulitan |

Alignment Check:
  [x] Setiap langkah terdokumentasi
  [x] Tidak ada lompatan logis
  [x] Metrik mengukur konsep yang dimaksud
```

---

## Latihan 1 — Operationalization Chain

Gunakan RQ dari WS-04. Definisikan variabel dan metriknya.

**RQ:**Apakah Multi-step Wizard lebih efisien dan akurat dibandingkan Single-page Form dalam sistem pendaftaran klinik?

| Variabel             | Tipe | Konsep Abstrak | Metrik Konkret            | Skala (NOIR) | Satuan |
| -------------------- | ---- | -------------- | ------------------------- | ------------ | ------ |
| Jenis Form           | IV   | Desain UI      | Multi-step vs Single-page | Nominal      | —      |
| Task Completion Time | DV   | Efisiensi      | Waktu penyelesaian        | Ratio        | Detik  |
| Error Rate           | DV   | Akurasi        | % kesalahan input         | Ratio        | %      |
| Pengalaman user      | CV   | Skill pengguna | Lama kerja                | Ratio        | Tahun  |


**Apakah ada lompatan logis dalam rantai?** [ ] Ya / [✔] Tidak
> Jika ya, di mana? ____________________________________

---

## Latihan 2 — Evaluasi Metrik

| Kriteria       | Skor (1-5) | Justifikasi                                                    |
| -------------- | ---------- | -------------------------------------------------------------- |
| Representative | 5          | Waktu & error langsung merepresentasikan efisiensi dan akurasi |
| Sensitive      | 4          | Perbedaan kecil masih bisa terdeteksi, tapi bisa kena noise    |
| Feasible       | 5          | Mudah diukur dengan stopwatch/log system                       |


**Apakah perlu secondary metric?** [✔] Ya / [ ] Tidak
> Jika ya, apa dan mengapa? Cognitive Load (misalnya NASA-TLX)
> Karena root cause kamu adalah beban kognitif, tapi belum langsung terukur di DV utama

---

## Latihan 3 — Data Quality Check

Bayangkan data yang akan dikumpulkan dari eksperimen. Evaluasi 4 dimensi kualitas data.

| Dimensi            | Pertanyaan                     | Jawaban                               | Strategi Mitigasi           |
| ------------------ | ------------------------------ | ------------------------------------- | --------------------------- |
| Completeness       | Apakah semua data terkumpul?   | Bisa tidak lengkap jika user skip     | Wajibkan semua task selesai |
| Consistency        | Apakah ada kontradiksi?        | Bisa jika user salah input            | Validasi sistem             |
| Validity           | Apakah mengukur yang dimaksud? | Ya, tapi tergantung desain eksperimen | Gunakan skenario realistis  |
| Representativeness | Apakah sampel sesuai?          | Risiko jika bukan staf asli           | Gunakan staf klinik nyata   |


---

## Refleksi

> Mengapa memilih metrik setelah melihat data dianggap p-hacking? Apa bedanya dengan eksplorasi data yang sah?

**Jawaban:**
> Memilih metrik setelah melihat data dianggap p-hacking karena peneliti dapat secara tidak objektif memilih metrik yang menghasilkan hasil signifikan, sehingga bias terhadap kesimpulan. Hal ini merusak validitas penelitian karena hasil tidak lagi mencerminkan kondisi sebenarnya.

>Berbeda dengan eksplorasi data yang sah, di mana analisis tambahan dilakukan setelah eksperimen dan dilaporkan sebagai temuan eksploratif, bukan sebagai bukti utama untuk mendukung hipotesis.
# WS-07: Experimental Design & Validity

> **Bab 7 — Experimental Design & Validity**

---

## Ringkasan Materi

### Correlation ≠ Causality

Kausalitas membutuhkan 3 syarat:
1. **Covariance** — X dan Y bergerak bersama
2. **Temporal precedence** — X berubah sebelum Y
3. **Elimination of alternatives** — Tidak ada faktor lain yang menjelaskan Y

Controlled experiment adalah satu-satunya metode yang bisa membuktikan kausalitas.

### Empat Jenis Validitas

| Jenis | Pertanyaan | Ancaman Umum |
|-------|-----------|-------------|
| **Internal** | Apakah hubungan IV→DV nyata? | Confounding variable, selection bias |
| **External** | Apakah bisa digeneralisasi? | Dataset terlalu spesifik |
| **Construct** | Apakah mengukur konsep yang benar? | Metrik tidak sesuai |
| **Conclusion** | Apakah kesimpulan statistik valid? | Sample size kecil, uji salah |

Internal dan external validity sering berkonflik: semakin terkontrol (internal kuat) → semakin artificial (external lemah).

### Tiga Tipe Eksperimen dalam Riset TI

| Tipe | Deskripsi | Kapan Digunakan |
|------|----------|----------------|
| **Comparison Study** | Metode A vs B pada kondisi identik | Membandingkan pendekatan berbeda |
| **Ablation Study** | Full system → lepas komponen satu per satu | Mengukur kontribusi tiap komponen |
| **Parameter Study** | Variasikan satu parameter, amati dampak | Uji sensitifitas/robustness |

### Fairness dalam Perbandingan

Perbandingan yang adil = **kondisi identik** untuk semua metode: dataset sama, preprocessing sama, tuning effort sebanding, environment sama, metrik sama.

Contoh tidak adil: Transformer (30 fitur tambahan + Bayesian optimization) vs RF (default params) → hasilnya misleading.

### Threats to Validity = Diidentifikasi Sebelum Eksperimen

Ancaman validitas harus diidentifikasi **sebelum** eksperimen dan mitigasinya dirancang sebagai bagian dari desain — bukan ditulis sebagai boilerplate setelah selesai.

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan testing | Memastikan sistem memenuhi requirement | Membuktikan hubungan kausal antar variabel |
| Baseline | Versi sebelumnya (last release) | Metode tervalidasi dari literatur |
| Kegagalan | Bug → fix → release | H₀ tidak ditolak → tetap kontribusi ilmiah |
| Sukses | 100% test pass | Evidence valid — mendukung atau menolak hipotesis |

### Istilah Penting

- **Causality** — Hubungan sebab-akibat (covariance + temporal + elimination)
- **Controlled Experiment** — Ubah satu variabel, kontrol sisanya, amati efek
- **Fairness** — Semua metode diuji pada kondisi yang benar-benar identik
- **Threats to Validity** — Faktor yang bisa melemahkan kesimpulan jika tidak dimitigasi
- **Conclusion Validity** — Validitas statistik: power, sample size, uji yang tepat

---

## Template A.7 — Desain Eksperimen Lengkap

```
EXPERIMENT DESIGN

Research Question :
Apakah desain Multi-step Wizard menghasilkan Task Completion Time lebih rendah dan Error Rate lebih kecil dibandingkan Single-page Form pada sistem pendaftaran klinik?

Hypothesis :
H₀: Tidak ada perbedaan signifikan Task Completion Time dan Error Rate antara Multi-step dan Single-page  
H₁: Multi-step Wizard secara signifikan menurunkan Task Completion Time dan Error Rate dibanding Single-page

Tipe Eksperimen   : [x] Comparison  [ ] Ablation  [ ] Parameter

Kondisi Eksperimen:
| Kondisi | Deskripsi | IV Value | CV Settings |
|---------|-----------|----------|-------------|
| Control |Form standar yang umum digunakan           | Single-page         | Data sama, jumlah field sama, user setara            |
| Treatment | Desain alternatif yang diuji        | Multi-step Wizard         | Data sama, jumlah field sama, user setara            |

Fairness Checklist:
| Kriteria             | Status | Detail                                  |
| -------------------- | ------ | --------------------------------------- |
| Dataset identik      | ✅      | Semua user input data pasien yang sama  |
| Preprocessing setara | ✅      | Format data & field identik             |
| Tuning effort setara | ✅      | Tidak ada optimasi khusus salah satu UI |
| Environment identik  | ✅      | Perangkat & kondisi penggunaan sama     |
| Metrik evaluasi sama | ✅      | Time (detik) & error (%)                |

Threat Analysis:
| Threat Type | Ancaman Spesifik | Mitigasi |
|-------------|-----------------|----------|
| Internal    | Perbedaan skill user  |Gunakan partisipan dengan level pengalaman mirip          |
| External    | Hanya diuji di 1 klinik  | Sebutkan keterbatasan, sarankan studi lanjutan         |
| Construct   | Waktu ≠ selalu representasi usability  | Tambahkan error rate sebagai metrik tambahan         |
| Conclusion  | Sample terlalu kecil |Gunakan minimal ±20–30 partisipan          |

Uji statistik   : Paired t-test
Justifikasi     : Membandingkan dua kondisi pada subjek yang sama
Alpha           : 0.05
Effect size min : 0.5 (medium effect)
```

---

## Latihan 1 — Desain Eksperimen

Susun desain eksperimen berdasarkan RQ, variabel, dan sistem dari WS-04 sampai WS-06.

**RQ:** Apakah Multi-step Wizard lebih efisien dan akurat dibanding Single-page Form?
**Tipe eksperimen:** [x] Comparison / [ ] Ablation / [ ] Parameter

| Kondisi   | Deskripsi   | IV Value    | CV Settings             |
| --------- | ----------- | ----------- | ----------------------- |
| Control   | Form biasa  | Single-page | Data, device, user sama |
| Treatment | Form wizard | Multi-step  | Data, device, user sama |


---

## Latihan 2 — Fairness Checklist

Evaluasi apakah desain eksperimen di Latihan 1 sudah fair.

| Kriteria             | Status | Detail                                                                                             |
| -------------------- | ------ | -------------------------------------------------------------------------------------------------- |
| Dataset identik      | ✅      | Semua partisipan menggunakan **data pasien dummy yang sama** saat mengisi form                     |
| Preprocessing setara | ✅      | Struktur form, jumlah field, dan format input dibuat **identik** antara Multi-step dan Single-page |
| Tuning effort setara | ✅      | Kedua desain dibuat dengan tingkat kompleksitas yang sama tanpa optimasi khusus pada salah satu    |
| Environment identik  | ✅      | Pengujian dilakukan pada perangkat, layar, dan kondisi penggunaan yang sama                        |
| Metrik evaluasi sama | ✅      | Kedua kondisi diukur dengan **Task Completion Time (detik)** dan **Error Rate (%)**                |

**Ada yang tidak fair?** [ ] Ya / [x] Tidak
> Jika ya, bagaimana cara memperbaikinya?Gunakan within-subject design
---

## Latihan 3 — Threat Analysis

Identifikasi ancaman validitas untuk desain eksperimen ini.

| Threat Type | Ancaman                             | Mitigasi                            |
| ----------- | ----------------------------------- | ----------------------------------- |
| Internal    | User belajar dari percobaan pertama | Randomize urutan (A/B)              |
| External    | Tidak representatif                 | Tambah variasi user                 |
| Construct   | Metrik kurang lengkap               | Tambah subjective metric (opsional) |
| Conclusion  | Data kecil                          | Tambah sample                       |


**Ancaman mana yang paling sulit dimitigasi?**External validity
**Mengapa?**
> Karena hasil dari satu klinik belum tentu berlaku di semua sistem kesehatan yang memiliki kondisi berbeda
---

## Refleksi

> Sebuah paper melaporkan "metode kami mengalahkan semua baseline." Apa 3 pertanyaan pertama yang harus diajukan untuk mengevaluasi klaim ini?

**Jawaban:**
1. Apakah perbandingan dilakukan secara fair (dataset, kondisi, metrik sama)?
2. Apakah baseline yang digunakan cukup kuat dan relevan?
3. Apakah hasilnya signifikan secara statistik atau hanya kebetulan?
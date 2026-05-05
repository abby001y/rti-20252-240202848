# WS-04: Research Question & Hypothesis

> **Bab 4 — Research Question, Contribution & Hypothesis**

---

## Ringkasan Materi

### RQ Bukan Pertanyaan Biasa

Research Question yang baik secara implisit mengandung cetak biru eksperimen: subjek, baseline, metrik, domain, dataset.

| Kualitas | Contoh |
|----------|--------|
| **Buruk** | "Bagaimana pengaruh deep learning terhadap deteksi malware?" |
| **Baik** | "Apakah CNN menghasilkan F1-Score lebih tinggi dari RF pada CIC-MalMem-2022?" |

Perbedaan: RQ yang baik menyebutkan **metode spesifik**, **metrik terukur**, **baseline**, dan **dataset**.

### Tiga Jenis RQ

| Jenis | Pola | Kebutuhan |
|-------|------|-----------|
| **Comparison** | A vs B → mana lebih baik? | ≥ 2 metode, metrik sama |
| **Improvement** | A' vs A → modifikasi lebih baik? | Pre/post, bukti perbaikan |
| **Exploratory** | Faktor X₁...Xₙ → pengaruh terhadap Y? | Multi-variabel, korelasi/regresi |

### Contribution Statement

Tiga jenis kontribusi: **Improvement** (metode terbukti lebih baik), **Comparison** (perbandingan sistematis yang belum ada), **Novel Approach** (pendekatan baru). Kontribusi harus terhubung langsung dengan gap — kontribusi tanpa gap = klaim tanpa justifikasi.

### Hypothesis H₀ / H₁

- **H₀** (Null) = Tidak ada perbedaan signifikan — asumsi default, harus dibuktikan salah
- **H₁** (Alternative) = Ada perbedaan signifikan — diterima hanya jika H₀ ditolak
- Harus **falsifiable**, mengandung **metrik terukur**, dirumuskan **SEBELUM eksperimen**

### Rantai Operasionalisasi

```
RQ → Variable → Metric → Data → Analysis
```

Jika rantai ini tidak lengkap, RQ belum mature. Bi-directional: RQ yang tidak bisa jadi hipotesis testable harus direvisi mundur.

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan pertanyaan | Apa yang harus dibangun? | Apa yang harus dibuktikan? |
| Bentuk jawaban | Sistem yang berfungsi | Bukti empiris terukur |
| Sukses diukur oleh | User satisfaction, uptime | Signifikansi statistik, effect size |
| Jika gagal | Debug dan perbaiki | Laporkan, analisis mengapa |

### Istilah Penting

- **Research Question (RQ)** — Pertanyaan spesifik: variabel terukur + metrik + konteks
- **Contribution Statement** — Apa yang diketahui setelah riset selesai yang sebelumnya belum ada
- **H₀ / H₁** — Null vs Alternative Hypothesis
- **Falsifiability** — Kondisi hipotesis ditolak harus bisa didefinisikan sebelum eksperimen
- **Operationalization** — Proses mewujudkan konsep abstrak menjadi variabel terukur

---

## Template A.4 — RQ-Contribution-Hypothesis

```
RQ-CONTRIBUTION-HYPOTHESIS

Gap Statement  : Belum adanya evaluasi desain Multi-step Wizard vs Single-page Form dalam konteks sistem pendaftaran klinik dengan partisipan staf administrasi nyata, serta pengukuran simultan Task Completion Time dan Error Rate.

Research Question:
  Tipe         : [x] Comparison  [ ] Improvement  [ ] Exploratory
  Formulasi    : Apakah desain Multi-step Wizard menghasilkan Task Completion Time yang lebih rendah dan Error Rate yang lebih kecil dibandingkan Single-page Form pada sistem pendaftaran klinik yang digunakan oleh staf administrasi?
  Variabel IV  : Jenis desain form (Multi-step Wizard vs Single-page Form)
  Variabel DV  : Task Completion Time dan Error Rate
  Metrik       : Waktu (detik), persentase kesalahan input (%)
  Dataset      : Staf administrasi klinik (pengguna nyata)
  Baseline     : Single-page Form

Quality Check RQ:
  [x] Variabel spesifik
  [x] Metrik jelas
  [x] Baseline ada
  [x] Konteks disebutkan
  [x] Memerlukan eksperimen

Contribution Statement:
  Apa yang baru diketahui : Bukti empiris mengenai efektivitas desain Multi-step Wizard dibandingkan Single-page Form dalam konteks nyata sistem pendaftaran klinik
  Jenis kontribusi        : [x] Comparison
  Gap yang diisi          : Context gap dan Data gap

Hypothesis Pair:
  H₀ : Tidak terdapat perbedaan signifikan pada Task Completion Time dan Error Rate antara Multi-step Wizard dan Single-page Form pada sistem pendaftaran klinik
  H₁ : Multi-step Wizard menghasilkan Task Completion Time yang lebih rendah dan Error Rate yang lebih kecil secara signifikan dibandingkan Single-page Form
  Threshold              : p-value < 0.05
  Justifikasi threshold  : Standar umum dalam penelitian kuantitatif untuk menentukan signifikansi statistik
```

---

## Latihan 1 — Dari Gap ke RQ

Gunakan gap yang ditemukan di WS-03. Transformasikan menjadi Research Question.

**Gap dari WS-03:**Belum ada penelitian pada konteks klinik dengan pengguna staf administrasi dan pengukuran waktu + error secara bersamaan

**RQ versi pertama (tulis bebas):**
> Apakah multi-step form lebih baik daripada single-page form?

**Evaluasi RQ:**
| Komponen        | Ada? | Isi                       |
| --------------- | ---- | ------------------------- |
| Metode spesifik | Ya   | Multi-step vs Single-page |
| Metrik terukur  | Ya   | Waktu & error             |
| Baseline        | Ya   | Single-page               |
| Dataset/konteks | Ya   | Staf administrasi klinik  |


**Tipe RQ:**Comparison
**RQ versi revisi (setelah evaluasi):**
> Apakah desain Multi-step Wizard menghasilkan Task Completion Time yang lebih rendah dan Error Rate yang lebih kecil dibandingkan Single-page Form pada sistem pendaftaran klinik yang digunakan oleh staf administrasi?
---

## Latihan 2 — Hypothesis Pair

Rumuskan pasangan hipotesis dari RQ di Latihan 1.

| Komponen | Isi |
|----------|-----|
| H₀ | Tidak ada perbedaan signifikan Task Completion Time dan Error Rate antara Multi-step dan Single-page |
| H₁ |Multi-step Wizard memiliki Task Completion Time lebih rendah dan Error Rate lebih kecil secara signifikan |
| Metrik |Waktu (detik), Error Rate (%) |
| Threshold |p < 0.05 |
| Justifikasi threshold |Standar umum uji statistik (t-test / Mann-Whitney) |

**Apakah hipotesis ini falsifiable?** [✔] Ya / [ ] Tidak
> Bagaimana cara membuktikannya salah? Jika hasil uji statistik menunjukkan p ≥ 0.05, maka H₀ tidak dapat ditolak → berarti tidak ada perbedaan signifikan

---

## Latihan 3 — Rantai Operasionalisasi

Lengkapi rantai dari RQ hingga metode analisis.

| Tahap | Isi |
|-------|-----|
| RQ | Apakah Multi-step lebih baik dari Single-page dalam hal waktu & error? |
| Variable (IV) | Jenis form (Multi-step vs Single-page) |
| Variable (DV) |Task Completion Time, Error Rate |
| Metric |Detik, Persentase error |
| Data source |Staf administrasi klinik |
| Analysis method |Uji t-test / Mann-Whitney |

**Apakah rantai lengkap?** [✔] Ya / [ ] Tidak
> Jika tidak, tahap mana yang perlu direvisi? ______________

---

## Refleksi

> Ambil satu judul skripsi/paper yang pernah dibaca. Coba ekstrak RQ-nya. Apakah RQ tersebut memenuhi semua komponen (metode, metrik, baseline, konteks)? Jika tidak, apa yang hilang?

**Judul:** Perbandingan Desain Form terhadap Efisiensi Pengguna
**RQ yang diekstrak:**Apakah desain A lebih baik dari desain B?
**Komponen yang hilang:**Tidak ada metrik jelas
Tidak ada dataset/konteks spesifik
Tidak ada baseline eksplisit
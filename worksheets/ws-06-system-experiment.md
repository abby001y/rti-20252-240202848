# WS-06: System-Experiment Mapping

> **Bab 6 — System Design sebagai Experimental Artifact**

---

## Ringkasan Materi

### Sistem = Instrumen Pengujian, Bukan Produk

Seorang engineer bertanya "apakah sistem bekerja?" — seorang peneliti bertanya "apa yang bisa dibuktikan sistem ini?" Sistem dalam riset adalah **artifact** — objek yang sengaja dibuat untuk menguji klaim spesifik.

### System as Experiment Model

```
RQ → Variable → System Component → Experimental Setup → Output
```

Setiap komponen sistem harus bisa ditelusuri ke variabel riset (top-down), dan setiap pengukuran harus menjawab RQ (bottom-up).

### Mapping Variabel ke Komponen

| Tipe Variabel | Peran di Sistem | Contoh |
|---------------|----------------|--------|
| **IV** (Independent) | Modul yang bisa di-toggle/swap | Algoritma A vs B |
| **DV** (Dependent) | Modul pengukuran | Logger, metrics collector |
| **CV** (Control) | Config yang dikunci | Dataset, parameter tetap |

Jika variabel tidak bisa di-map ke komponen apapun → arsitektur perlu didesain ulang.

### 4 Prinsip Desain Eksperimental

| Prinsip | Pertanyaan Kunci |
|---------|-----------------|
| **Traceability** | Komponen ini melayani variabel yang mana? |
| **Modularity** | Bisakah IV diubah tanpa memengaruhi yang lain? |
| **Controllability** | Apakah CV dieksternalisasi ke config file? |
| **Measurability** | Apakah sistem otomatis menghasilkan data yang dibutuhkan? |

### Variable Isolation melalui Arsitektur

- **Modular architecture** — Pisahkan berdasarkan variabel
- **Configuration-driven** — Ubah config (YAML/JSON), bukan code
- **Feature toggles** — On/off flag untuk ablation study

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan sistem | Memenuhi kebutuhan user | Menguji hipotesis, menghasilkan bukti |
| Arsitektur | Optimasi performa & skalabilitas | Optimasi isolasi variabel & reprodusibilitas |
| Konfigurasi | Sering hardcoded | Dieksternalisasi ke config file |
| Fitur tambahan | Menambah nilai user | Menambah noise jika tidak terkait RQ |

### Istilah Penting

- **Artifact** — Objek yang sengaja dibuat untuk memecahkan masalah atau menguji proposisi
- **Traceability** — Kemampuan menelusuri hubungan RQ → variabel → komponen → output
- **Variable Isolation** — Mengubah hanya satu variabel sambil menahan yang lain konstan
- **Ablation Study** — Menguji kontribusi tiap komponen dengan melepasnya satu per satu
- **Configuration-driven Execution** — Semua parameter di config file, bukan hardcoded

---

## Template A.6 — Mapping RQ ke Arsitektur Sistem

```
SYSTEM-EXPERIMENT MAPPING

Research Question:
Apakah desain Multi-step Wizard menghasilkan Task Completion Time yang lebih rendah dan Error Rate yang lebih kecil dibandingkan Single-page Form pada sistem pendaftaran klinik?

Variable → Component Mapping:
| Variabel | Tipe | Komponen Sistem | Cara Manipulasi/Pengukuran |
|----------|------|-----------------|---------------------------|
| Jenis Form (Multi-step vs Single-page) | IV | Modul UI Form (2 versi: wizard & single-page) | Toggle melalui config (mode = wizard / single) |
| Task Completion Time | DV | Timer / Logger System | Hitung waktu dari start input hingga submit |
| Error Rate | DV | Validation & Error Logger | Hitung jumlah kesalahan input / total field |
| Pengalaman user | CV | Data responden | Dikontrol dengan memilih staf dengan level pengalaman serupa |
| Kompleksitas form | CV | Struktur form (jumlah field) | Dikunci (jumlah field sama di kedua desain) |

4 Prinsip Desain:
  [x] Traceability — Setiap komponen langsung terkait variabel
  [x] Variable Isolation — Hanya UI yang berubah, variabel lain tetap
  [x] Measurement Integration — Logger otomatis mencatat waktu & error
  [x] Reproducibility — Bisa diulang dengan config yang sama

Experimental Setup:
  Input data     : Data dummy pasien (KTP, asuransi, poli)
  Parameter      : mode form (wizard/single), jumlah field tetap
  Output format  : CSV (user_id, waktu, jumlah error)
```

---

## Latihan 1 — Variable-to-Component Mapping

Gunakan RQ dan variabel dari WS-05. Petakan ke komponen sistem.

**RQ:** Apakah Multi-step Wizard lebih efisien dan akurat dibandingkan Single-page Form?

| Variabel             | Tipe | Komponen Sistem   | Cara Manipulasi / Pengukuran       |
| -------------------- | ---- | ----------------- | ---------------------------------- |
| Jenis Form           | IV   | UI Form Module    | Ganti mode (wizard vs single-page) |
| Task Completion Time | DV   | Timer System      | Auto capture waktu                 |
| Error Rate           | DV   | Validation Logger | Hitung error input                 |
| Pengalaman user      | CV   | User selection    | Dikontrol saat rekrut partisipan   |


**Apakah semua variabel bisa di-map?** [✔] Ya / [ ] Tidak
> Jika tidak, komponen apa yang perlu ditambahkan? _________

---

## Latihan 2 — 4 Prinsip Desain

Evaluasi desain sistem terhadap 4 prinsip.

| Prinsip         | Status | Bukti / Penjelasan                     |
| --------------- | ------ | -------------------------------------- |
| Traceability    | ✅      | Setiap komponen jelas terkait variabel |
| Modularity      | ✅      | UI dipisah jadi 2 modul                |
| Controllability | ⚠️     | Perlu config file (jangan hardcoded)   |
| Measurability   | ✅      | Logger otomatis mencatat data          |


**Prinsip mana yang paling sulit dipenuhi?** Controllability
**Strategi untuk mengatasinya:**
> Gunakan config file (JSON/YAML) untuk menentukan mode form, bukan ubah code manual
---

## Latihan 3 — Ablation Study Planning

Jika sistem memiliki 3 komponen utama, rencanakan ablation study.
| Kondisi | Komponen A (UI Type) | Komponen B (Validation) | Komponen C (Step Navigation) | Hasil yang Diharapkan |
| ------- | -------------------- | ----------------------- | ---------------------------- | --------------------- |
| Full    | ✅ Multi-step         | ✅ Validasi aktif        | ✅ Step navigation            | Performa optimal      |
| – A     | ❌ Single-page        | ✅                       | ✅                            | Waktu ↑, error ↑      |
| – B     | ✅                    | ❌ tanpa validasi        | ✅                            | Error ↑ signifikan    |
| – C     | ✅                    | ✅                       | ❌ (tanpa step)               | Cognitive load ↑      |

**Komponen mana yang diprediksi paling berkontribusi?** Step Navigation (Multi-step structure)
**Mengapa?**
> Karena langsung memengaruhi pembagian beban kognitif pengguna, yang merupakan akar masalah dari penelitian ini
---

## Refleksi

> Apa risiko jika sistem dibangun seperti produk (monolitik, fitur lengkap) lalu baru dilakukan eksperimen? Mengapa arsitektur modular penting untuk riset?

**Jawaban:**
> Jika sistem dibangun seperti produk (monolitik dan penuh fitur), maka sulit untuk mengisolasi variabel yang ingin diuji. Perubahan kecil dapat memengaruhi banyak komponen sekaligus, sehingga hasil eksperimen menjadi tidak valid.
> Arsitektur modular penting karena memungkinkan peneliti mengontrol dan memanipulasi satu variabel secara terpisah tanpa memengaruhi komponen lain. Hal ini memastikan bahwa perubahan hasil benar-benar disebabkan oleh variabel yang diuji, bukan faktor lain.
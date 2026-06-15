# Simulasi S-DES (Simplified Data Encryption Standard)

Aplikasi web interaktif untuk simulasi algoritma **Simplified Data Encryption Standard (S-DES)**, dibuat sebagai project tugas individu Mata Kuliah Kriptografi (Semester Genap 2025/2026).

Aplikasi ini melakukan proses **enkripsi** dan **dekripsi** S-DES secara lengkap, serta menampilkan setiap tahapan perhitungan secara rinci dan interaktif — mulai dari pembangkitan kunci hingga output akhir.

---

## 🔗 Tautan

| Komponen | Link |
|---|---|
| Demo Aplikasi (.my.id) | `` |
| Video Penjelasan (YouTube) | `` |
| Laporan Project | `` |

---

## ✨ Fitur

- Input **plaintext/ciphertext 8-bit** dan **kunci 10-bit** dalam bentuk biner, dengan validasi otomatis
- Pilihan mode **Enkripsi** atau **Dekripsi**
- Tombol **PROSES** untuk menjalankan algoritma dan **RESET** untuk mengosongkan form
- Hasil ditampilkan secara visual (kotak per-bit) dan dalam bentuk string biner
- Bagian **"Tampilkan Solusi Penyelesaian"** yang dapat di-toggle, menampilkan seluruh langkah perhitungan:
  - **Key Generation**: P10 → pembagian L/R → LS-1 → P8 (K1) → LS-2 → P8 (K2)
  - **Initial Permutation (IP)** dan pembagian L/R
  - **Round Function 1**: Expansion Permutation (EP), XOR dengan subkunci, lookup S-Box S0 & S1 (dengan highlight cell), Permutasi P4, XOR dengan L, dan Swap
  - **Round Function 2**: proses serupa dengan subkunci berbeda, tanpa swap
  - **Inverse Initial Permutation (IP⁻¹)** untuk menghasilkan output akhir
- Tampilan dark theme, rapi, dan responsif (mendukung mobile)

---

## 🚀 Cara Menggunakan

### 1. Menjalankan secara lokal

Karena aplikasi ini adalah **single-file HTML** (tidak memerlukan server atau instalasi apa pun), cukup:

1. Download/clone repository ini
2. Buka file `sdes-simulator.html` langsung di browser (Chrome, Firefox, Edge, dll.)

```bash
git clone <url-repo-github-anda>
cd <nama-folder>
# buka file di browser
```

### 2. Menggunakan aplikasi

1. **Masukkan Plaintext/Ciphertext** — isi kolom pertama dengan **8 digit biner** (hanya angka `0` dan `1`), contoh: `01101101`
2. **Masukkan Kunci** — isi kolom kedua dengan **10 digit biner**, contoh: `1010000010`
3. **Pilih Mode**:
   - **🔒 Enkripsi** — jika input adalah plaintext, hasil berupa ciphertext
   - **🔓 Dekripsi** — jika input adalah ciphertext, hasil berupa plaintext
4. Klik **▶ PROSES** (atau tekan tombol `Enter`)
5. Hasil akan muncul di bagian **"Hasil"**, ditampilkan dalam kotak bit dan format biner
6. Klik **"📋 Tampilkan Solusi Penyelesaian"** untuk melihat seluruh langkah perhitungan secara rinci
7. Klik **↺ RESET** untuk mengosongkan semua input dan mengulang dari awal

> ⚠️ Validasi otomatis: jika input bukan biner murni atau panjangnya tidak sesuai (8-bit untuk plaintext/ciphertext, 10-bit untuk kunci), field akan ditandai merah dengan pesan error.

### Contoh Pengujian

| Mode | Input (Plaintext/Ciphertext) | Kunci (10-bit) |
|---|---|---|
| Enkripsi | `10101010` | `1010000010` |
| Dekripsi | (gunakan hasil ciphertext dari proses enkripsi di atas) | `1010000010` |

Jika dekripsi dilakukan dengan kunci yang sama, hasilnya akan kembali menjadi plaintext awal (`10101010`), membuktikan korektnasi algoritma.

---

## 🧮 Tentang Algoritma S-DES

S-DES adalah versi sederhana dari algoritma **DES (Data Encryption Standard)**, dikembangkan oleh Edward Schaefer (1996) sebagai media pembelajaran kriptografi. S-DES menggunakan:

- **Plaintext/Ciphertext**: 8-bit
- **Kunci**: 10-bit
- **2 round function** (menggunakan subkunci K1 dan K2)

### Tabel Permutasi yang Digunakan

| Tabel | Posisi |
|---|---|
| P10 (10→10) | 3, 5, 2, 7, 4, 10, 1, 9, 8, 6 |
| P8 (10→8) | 6, 3, 7, 4, 8, 5, 10, 9 |
| IP (8→8) | 2, 6, 3, 1, 4, 8, 5, 7 |
| IP⁻¹ (8→8) | 4, 1, 3, 5, 7, 2, 8, 6 |
| EP (4→8) | 4, 1, 2, 3, 2, 3, 4, 1 |
| P4 (4→4) | 2, 4, 3, 1 |

### Alur Proses

**Key Generation:**
```
Kunci 10-bit → P10 → bagi (L5, R5) → LS-1 masing-masing → P8 → K1
                                    → LS-2 masing-masing → P8 → K2
```

**Enkripsi:**
```
Plaintext 8-bit → IP → bagi (L4, R4)
  → Round 1 (fK dengan K1) → Swap
  → Round 2 (fK dengan K2)
  → IP⁻¹ → Ciphertext
```

**Dekripsi:** proses identik dengan enkripsi, namun **urutan subkunci dibalik** — Round 1 menggunakan **K2**, Round 2 menggunakan **K1**.

**Round Function (fK):**
```
R (4-bit) → EP (8-bit) → XOR dengan subkunci → bagi 2x4-bit
  → S-Box S0 & S1 → gabung (4-bit) → P4 → XOR dengan L
```

---

## 🛠️ Teknologi yang Digunakan

- **HTML5** — struktur halaman
- **CSS3** — styling (dark theme, responsif, custom properties)
- **JavaScript (Vanilla)** — implementasi algoritma S-DES dan logika UI, tanpa dependency/framework eksternal

---

## 📁 Struktur Project

```
.
├── sdes-simulator.html   # Aplikasi utama (single-file)
├── laporan-sdes.docx     # Laporan project
└── README.md             # Dokumentasi ini
```

---

## 📚 Referensi

- Schaefer, E. F. (1996). *A simplified data encryption standard algorithm*. Cryptologia, 20(1), 77–84.
- Stallings, W. (2017). *Cryptography and Network Security: Principles and Practice* (7th ed.). Pearson Education.

---

## 📄 Lisensi

Project ini dibuat untuk keperluan tugas akademik Mata Kuliah Kriptografi.

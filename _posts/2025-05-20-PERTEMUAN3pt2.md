---
title: N-QUEENS PROBLEM
date: 2025-05-20
categories: [DESAIN ANALISIS ALGORITMA, BACKTRACKING ALGORITHM]
tags: [daa, algorithm, backtracking]
---

**N-Queens Problem** adalah teka-teki klasik menempatkan N ratu pada papan catur N x N sehingga tidak ada dua ratu yang saling menyerang (secara baris, kolom, atau diagonal). Masalah ini penting untuk memahami teknik pencarian seperti *backtracking* dan *constraint satisfaction problem* (CSP), serta relevan untuk aplikasi nyata seperti penjadwalan dan alokasi sumber daya.

---

## Inti Masalah N-Queens

- Tempatkan N ratu di papan N x N tanpa saling menyerang.
- Ratu bisa bergerak horizontal, vertikal, dan diagonal.
- Solusi: semua konfigurasi penempatan ratu yang valid.

---

## Tujuan & Pentingnya

- Menemukan semua konfigurasi penempatan ratu yang valid.
- Melatih logika pemrograman dan pemecahan masalah CSP.
- Studi kasus teknik *backtracking* dan analisis kompleksitas.
- Aplikasi: penjadwalan, penempatan modul elektronik, alokasi sumber daya.

---

## Mengapa Backtracking?

- Penempatan ratu dilakukan satu per satu secara rekursif.
- Setiap langkah, cek posisi aman; jika tidak, *backtrack* ke langkah sebelumnya.
- Pohon pencarian solusi: setiap penempatan ratu = satu simpul.
- Cocok untuk masalah dengan banyak kemungkinan dan batasan.

---

## Backtracking: Langkah-langkah

1. Pilih keputusan (misal: kolom untuk ratu berikutnya).
2. Cek batasan (apakah posisi valid).
3. Jika valid, lanjut rekursi; jika tidak, coba opsi lain.
4. Jika buntu, *backtrack* ke keputusan sebelumnya.
5. Jika semua ratu ditempatkan, catat solusi.

---

## Analogi Dunia Nyata

- Penempatan karyawan di ruang kerja: setiap karyawan di ruang berbeda tanpa konflik (seperti aturan N-Queens).
- Jika tidak ada ruang valid, mundur dan coba posisi lain.

---

## Implementasi Kode (C++)

- Fungsi `isSafe()` untuk cek posisi aman.
- Fungsi rekursif untuk menempatkan ratu dan *backtrack* jika perlu.
- Cetak semua solusi yang ditemukan.

```cpp
void printSolution() { ... }
bool isSafe(int row, int col) { ... }
void solveNQueensUtil(int col) { ... }
void solveNQueens() { ... }
int main() { ... }
```

---

## Contoh Output (N=4)

```
Solusi #1:
. Q . .
. . . Q
Q . . .
. . Q .

Solusi #2:
. . Q .
Q . . .
. . . Q
. Q . .

Total solusi: 2
```

---

## Kesimpulan

N-Queens Problem adalah studi kasus penting untuk *backtracking* dan CSP. Dengan pendekatan sistematis, kita bisa menemukan semua solusi valid, sekaligus belajar tentang pencarian rekursif, manajemen batasan, dan aplikasi algoritma dalam berbagai bidang nyata.

---


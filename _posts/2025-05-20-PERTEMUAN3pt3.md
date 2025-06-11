---
title: SUBSET SUM PROBLEM
date: 2025-05-20
categories: [DESAIN ANALISIS ALGORITMA, BACKTRACKING ALGORITHM]
tags: [daa, algorithm, backtracking]
---

*Subset Sum Problem* (SSP) adalah masalah klasik dalam ilmu komputer untuk menentukan apakah ada subset dari sekumpulan bilangan bulat yang jika dijumlahkan hasilnya sama dengan nilai target tertentu. SSP termasuk *NP-Complete*, artinya tidak ada algoritma efisien untuk semua kasus, terutama untuk data besar.

### Definisi Formal
Diberikan array `arr` dan nilai `target_sum`, tentukan apakah ada subset dari `arr` yang jumlahnya sama dengan `target_sum`.

### Contoh
- Input: `arr = [1, 2, 3]`, `target_sum = 3` → Output: `True` (ada subset `{1,2}` atau `{3}`)
- Input: `arr = {10, 20, 30, 40, 50}`, `sum = 25` → Output: `False`

### Variasi Subset Sum
- **Bounded**: Setiap elemen hanya boleh dipakai sekali.
- **Unbounded**: Elemen boleh dipakai berulang kali.
- **Partition Problem**: Membagi array menjadi dua subset dengan jumlah sama.
- **Exact k Elements**: Subset terdiri dari tepat k elemen.
- **Multi-target**: Memenuhi lebih dari satu kriteria (misal jumlah dan berat).
- **Approximate**: Mencari subset dengan jumlah mendekati target.

### Pendekatan Penyelesaian
1. **Rekursif**: Cek semua kemungkinan subset (kompleksitas O(2^n)).
2. **Dynamic Programming**:
   - Memoization (Top-Down): Simpan hasil submasalah.
   - Tabulation (Bottom-Up): Bangun solusi dari kasus kecil.
   - Optimasi ruang: Gunakan array 1D untuk efisiensi memori.

### Contoh Implementasi (C++)
- Fungsi rekursif untuk bounded/unbounded subset sum.
- Dynamic programming untuk efisiensi waktu dan ruang.

### Aplikasi Dunia Nyata
- Kriptografi (knapsack cryptosystem)
- Alokasi sumber daya
- Keuangan dan investasi
- Bioinformatika
- Permainan dan teka-teki

### Kesimpulan
Subset Sum Problem adalah masalah fundamental dan menantang dalam ilmu komputer, dengan banyak variasi dan aplikasi praktis. Dynamic programming adalah solusi optimal untuk kasus besar.

---

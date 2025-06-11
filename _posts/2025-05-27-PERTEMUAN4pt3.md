---
title: DEPTH-FIRST SEARCH (DFS)
date: 2025-05-27
categories: [DESAIN ANALISIS ALGORITMA, DFS, BACKTRACKING ALGORITHM]
tags: [daa, algorithm, backtracking, dfs]
---

*Depth-First Search* (DFS) adalah algoritma penelusuran pada graf atau pohon yang menjelajahi satu cabang sedalam mungkin sebelum mundur (*backtrack*) dan lanjut ke cabang lain. DFS memakai stack (tumpukan) dengan prinsip LIFO (Last-In, First-Out).

### Langkah-Langkah DFS
1. Masukkan simpul awal ke stack.
2. Ambil simpul teratas, cek apakah solusi.
3. Jika bukan, masukkan semua tetangga yang belum dikunjungi ke stack.
4. Ulangi hingga stack kosong atau solusi ditemukan.

### Contoh Kode (C++)
```cpp
#include <iostream>
#include <vector>
#include <stack>
#include <unordered_map>
using namespace std;

unordered_map<char, vector<char>> graf;
unordered_map<char, bool> visited;

void dfs(char start) {
    stack<char> s;
    s.push(start);
    while (!s.empty()) {
        char node = s.top(); s.pop();
        if (!visited[node]) {
            cout << "Kunjungi node: " << node << endl;
            visited[node] = true;
            for (auto tetangga : graf[node]) {
                if (!visited[tetangga]) s.push(tetangga);
            }
        }
    }
}
```

### Kelebihan
- Penggunaan memori efisien.
- Mudah diimplementasikan.
- Cocok untuk pencarian solusi di kedalaman maksimal.
- Dasar banyak algoritma penting.

### Kekurangan
- Tidak menjamin solusi terpendek.
- Bisa terjebak infinite loop pada graf siklik tanpa visited.
- Kurang efisien untuk graf sangat luas tapi dangkal.

### Aplikasi
- Penelusuran graf dan pohon.
- Pencarian solusi pada puzzle atau game.
- Topological sorting, deteksi siklus, komponen terhubung.

### Kesimpulan
DFS adalah algoritma penelusuran yang efektif untuk eksplorasi mendalam pada graf atau pohon, sangat berguna untuk berbagai aplikasi pencarian dan analisis struktur data.
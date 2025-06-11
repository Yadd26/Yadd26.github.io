---
title: BREADTH-FIRST SEARCH (BFS)
date: 2025-05-27
categories: [DESAIN ANALISIS ALGORITMA, BFS, BACKTRACKING ALGORITHM]
tags: [daa, algorithm, backtracking, bfs]
---

**Breadth-First Search** (BFS) adalah algoritma dasar untuk menjelajahi atau mencari data pada graf/pohon. BFS menelusuri simpul berdasarkan level jarak dari titik awal, mengunjungi semua tetangga terdekat dulu sebelum ke simpul yang lebih jauh. BFS sering diibaratkan seperti memeriksa seluruh ruangan di lantai satu sebelum naik ke lantai berikutnya.

---

### Konsep Dasar & Cara Kerja

- **Menggunakan Queue**: BFS memakai antrian untuk mengelola urutan simpul yang akan dikunjungi.
- **Penelusuran per Level**: Mulai dari simpul awal, kunjungi semua tetangganya, lalu lanjut ke tetangga dari tetangga, dst (*level-order traversal*).

---

### Langkah-Langkah BFS

1. Tentukan simpul awal (*start node*).
2. Masukkan ke queue.
3. Selama queue tidak kosong:
   - Ambil simpul terdepan, tandai sebagai dikunjungi.
   - Jika simpul tujuan, selesai.
   - Jika bukan, masukkan semua tetangga yang belum dikunjungi ke queue.
4. Ulangi sampai tujuan ditemukan atau queue kosong.

---

### Simulasi BFS

| SIMPUL AKTIF | QUEUE      | VISITED      |
| :---         | :---       | :---         |
| S            | S          | S            |
| A            | A, B       | SA           |
| B            | B, C, D    | SAB          |
| C            | C, D, E, F | SABC         |
| D            | D, E, F    | SABCD        |
| E            | E, F       | SABCDE       |
| F            | F, H, G    | SABCDEF      |
| H            | H, G       | SABCDEFH     |
| G            | G          | SABCDEFHG    |

---

### Contoh Kode (C++)

```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <unordered_map>
#include <algorithm>
using namespace std;

unordered_map<char, vector<char>> graf;
unordered_map<char, bool> sudahDikunjungi;
unordered_map<char, char> parent;

void bfs(char start, char goal) {
    queue<char> q;
    q.push(start);
    sudahDikunjungi[start] = true;
    parent[start] = '/0';

    while (!q.empty()) {
        char sekarang = q.front(); q.pop();
        cout << "Kunjungi node: " << sekarang << endl;
        if (sekarang == goal) break;
        for (char tetangga : graf[sekarang]) {
            if (!sudahDikunjungi[tetangga]) {
                q.push(tetangga);
                sudahDikunjungi[tetangga] = true;
                parent[tetangga] = sekarang;
            }
        }
    }
    cout << "/n=== HASIL ===" << endl;
    cout << "Start Node: " << start << endl;
    cout << "Goal Node: " << goal << endl;
    vector<char> jalur;
    char current = goal;
    while (current != '/0') {
        jalur.push_back(current);
        current = parent[current];
    }
    reverse(jalur.begin(), jalur.end());
    cout << "Jalur Terpendek: ";
    for (size_t i = 0; i < jalur.size(); i++) {
        cout << jalur[i];
        if (i != jalur.size() - 1) cout << " -> ";
    }
    cout << endl;
}
```

---

### Aplikasi BFS

- Pencarian jalur terpendek di labirin/game
- Rekomendasi teman di media sosial
- Pemetaan jaringan komputer
- Sistem navigasi/transportasi

---

### Kelebihan & Kekurangan

**Kelebihan:**
- Menjamin solusi optimal (jalur terpendek pada graf tak berbobot)
- Komplit (pasti ketemu jika ada solusi)

**Kekurangan:**
- Boros memori & waktu jika graf sangat lebar

---

### Kesimpulan

BFS adalah algoritma penelusuran graf yang menjelajahi simpul secara berlapis dari titik awal. Dengan queue, BFS efektif untuk mencari jalur terpendek pada graf tak berbobot dan banyak dipakai di aplikasi modern seperti game, peta digital, dan analisis jaringan sosial.

---

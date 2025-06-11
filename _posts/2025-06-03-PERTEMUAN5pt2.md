---
title: DIJKSTRA's ALGORITHM
date: 2025-05-27
categories: [DESAIN ANALISIS ALGORITMA, DIJKSTRA's ALGORITHM]
tags: [daa, algorithm, backtracking, dijkstra]
---

**Algoritma Dijkstra** adalah metode pencarian jalur terpendek dari satu simpul sumber ke semua simpul lain pada graf berbobot non-negatif. Algoritma ini menggunakan pendekatan *greedy* dan sangat efisien, terutama jika memakai *priority queue* atau *min-heap*. Banyak digunakan pada aplikasi seperti jaringan komputer, sistem navigasi, dan transportasi.

---

### Cara Kerja

1. Buat tabel jarak dari simpul awal ke semua simpul (awal = 0, lain = tak hingga).
2. Pilih simpul dengan jarak terpendek yang belum dikunjungi.
3. Perbarui jarak ke tetangga jika ditemukan jalur lebih pendek.
4. Tandai simpul sebagai dikunjungi.
5. Ulangi hingga semua simpul dikunjungi.

---

### Contoh Permasalahan

Cari lintasan terpendek dari **A** ke **F**.  
Hasil: lintasan terpendek adalah **ABEF** atau **ABDF** dengan total nilai 4.

---

### Implementasi Kode (C++)

```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <limits>
#include <map>
using namespace std;

const int INF = numeric_limits<int>::max();

void dijkstra(const map<char, vector<pair<char, int>>>& graph, char start_node) {
    map<char, int> dist;
    for (auto const& [node, neighbors] : graph) dist[node] = INF;
    dist[start_node] = 0;
    priority_queue<pair<int, char>, vector<pair<int, char>>, greater<pair<int, char>>> pq;
    pq.push({0, start_node});
    while (!pq.empty()) {
        int d = pq.top().first;
        char u = pq.top().second;
        pq.pop();
        if (d > dist[u]) continue;
        if (graph.count(u)) {
            for (auto const& edge : graph.at(u)) {
                char v = edge.first;
                int weight = edge.second;
                if (dist[u] + weight < dist[v]) {
                    dist[v] = dist[u] + weight;
                    pq.push({dist[v], v});
                }
            }
        }
    }
    cout << "Jarak terpendek dari simpul " << start_node << ":\n";
    for (auto const& [node, distance] : dist) {
        if (distance == INF) cout << "  ke " << node << " = Tak terhingga\n";
        else cout << "  ke " << node << " = " << distance << endl;
    }
}

int main() {
    map<char, vector<pair<char, int>>> graph;
    graph['A'] = { {'B', 1}, {'C', 5} };
    graph['B'] = { {'D', 2}, {'E', 1}, {'C', 2} };
    graph['C'] = { {'E', 2} };
    graph['D'] = { {'F', 1} };
    graph['E'] = { {'D', 3}, {'F', 2} };
    graph['F'] = {};
    dijkstra(graph, 'A');
    return 0;
}
```

---

### Contoh Penggunaan

- **Navigasi Jalan**: Menentukan rute tercepat dari satu titik ke titik lain.
- **Pengiriman Barang**: Menemukan rute pengiriman paling efisien.

---

### Kelebihan

- Menjamin jalur terpendek jika bobot sisi positif.
- Efisien untuk graf padat dan aplikasi nyata (GPS, routing jaringan).
- Sekali eksekusi, dapatkan jarak terpendek ke semua simpul.

### Kekurangan

- Tidak bisa untuk graf dengan bobot negatif.
- Kurang efisien untuk graf besar yang jarang terhubung tanpa optimasi.
- Menghitung jarak ke semua simpul, meski hanya butuh satu tujuan.

---

### Kesimpulan

Dijkstra adalah algoritma jalur terpendek yang efisien dan akurat untuk graf berbobot non-negatif. Sangat berguna di banyak bidang, terutama jika dikombinasikan dengan struktur data efisien.

---
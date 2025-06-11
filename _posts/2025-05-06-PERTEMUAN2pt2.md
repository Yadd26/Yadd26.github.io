---
title: FRACTIONAL KNAPSACK
date: 2025-05-06
categories: [DESAIN ANALISIS ALGORITMA, GREEDY ALGORITHM]
tags: [daa, algorithm, greedy]
---

Permasalahan **Knapsack** adalah masalah optimasi klasik untuk memilih item dengan berat dan nilai tertentu agar nilai total maksimal dalam kapasitas terbatas. Pada **Fractional Knapsack**, kita boleh mengambil sebagian (fraksi) dari item.

### Karakteristik
- Boleh mengambil pecahan item.
- Setiap item punya berat dan nilai.
- Kapasitas knapsack terbatas.
- Tujuan: maksimalkan total nilai.

### Strategi Penyelesaian
Gunakan algoritma greedy: pilih item dengan rasio nilai/berat tertinggi terlebih dahulu.

### Kompleksitas Waktu
- Pengurutan: O(n log n)
- Seleksi: O(n)
- Total: O(n log n)

### Algoritma Greedy
1. Hitung rasio nilai/berat tiap item.
2. Urutkan item berdasarkan rasio menurun.
3. Pilih item dari rasio tertinggi, ambil penuh jika muat, jika tidak ambil fraksinya sesuai sisa kapasitas.

### Pseudocode
```
FUNCTION fractionalKnapsack(items, capacity):
    // items: sebuah list objek, di mana setiap objek memiliki properti 'weight' dan 'value'
    // capacity: kapasitas maksimum knapsack

    // 1. Hitung rasio nilai per berat untuk setiap item
    FOR EACH item IN items:
        item.ratio = item.value / item.weight

    // 2. Urutkan item dalam urutan menurun berdasarkan rasio nilai per berat
    SORT items IN DESCENDING ORDER BY item.ratio

    totalValue = 0.0
    currentCapacity = capacity

    // 3. Iterasi dan pilih item
    FOR EACH item IN items:
        IF currentCapacity == 0:
            BREAK // Knapsack sudah penuh

        IF item.weight <= currentCapacity:
            // Ambil seluruh item
            totalValue += item.value
            currentCapacity -= item.weight
        ELSE:
            // Ambil pecahan item
            fraction = currentCapacity / item.weight
            totalValue += fraction * item.value
            currentCapacity = 0 // Knapsack penuh
            BREAK // Tidak ada lagi ruang

    RETURN totalValue
```

### Beberapa Contoh Permasalahan serta Solusinya

#### Contoh 1:

Anda memiliki knapsack dengan kapasitas 15 kg. Anda memiliki item-item berikut:

| Item | Berat (kg) | Nilai (*) |
| :--- | :--------- | :-------- |
| A    | 7          | 21        |
| B    | 5          | 20        |
| C    | 3          | 12        |
| D    | 4          | 8         |

**Solusi:**

1.  **Hitung Rasio Nilai per Berat:**
    * Item A: *21 / 7 = 3*
    * Item B: *20 / 5 = 4*
    * Item C: *12 / 3 = 4*
    * Item D: *8 / 4 = 2*

2.  **Urutkan Item (Menurun berdasarkan rasio):**
    * Item B (rasio 4)
    * Item C (rasio 4)
    * Item A (rasio 3)
    * Item D (rasio 2)

    *Catatan: Jika rasio sama, urutan relatif tidak masalah, tetapi biasanya diurutkan berdasarkan berat atau indeks asli untuk konsistensi.*

3.  **Pilih Item:**
    * **Kapasitas Awal:** 15 kg
    * **Pilih Item B:** Berat 5 kg, Nilai 20.
        * Sisa kapasitas: *15 - 5 = 10* kg
        * Total nilai: *20
    * **Pilih Item C:** Berat 3 kg, Nilai 12.
        * Sisa kapasitas: *10 - 3 = 7* kg
        * Total nilai: *20 + 12 = 32
    * **Pilih Item A:** Berat 7 kg, Nilai 21.
        * Sisa kapasitas: *7 - 7 = 0* kg
        * Total nilai: *32 + 21 = 53

    Knapsack sudah penuh.

**Total Nilai Maksimum:** *53

---

#### Contoh 2:

Anda memiliki knapsack dengan kapasitas 10 kg. Item-item:

| Item | Berat (kg) | Nilai (*) |
| :--- | :--------- | :-------- |
| X    | 6          | 30        |
| Y    | 4          | 20        |
| Z    | 3          | 15        |

**Solusi:**

1.  **Hitung Rasio Nilai per Berat:**
    * Item X: *30 / 6 = 5*
    * Item Y: *20 / 4 = 5*
    * Item Z: *15 / 3 = 5*

2.  **Urutkan Item:** Karena semua rasio sama, urutan relatif tidak masalah. Mari kita asumsikan urutan X, Y, Z.

3.  **Pilih Item:**
    * **Kapasitas Awal:** 10 kg
    * **Pilih Item X:** Berat 6 kg, Nilai 30.
        * Sisa kapasitas: *10 - 6 = 4* kg
        * Total nilai: *30
    * **Pilih Item Y:** Berat 4 kg, Nilai 20.
        * Sisa kapasitas: *4 - 4 = 0* kg
        * Total nilai: *30 + 20 = 50

    Knapsack sudah penuh.

**Total Nilai Maksimum:** *50

---

### Implementasi Permasalahan pada C++

Berikut adalah contoh implementasi Fractional Knapsack menggunakan C++:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#include <iomanip> // Untuk output presisi floating point

// Struktur untuk merepresentasikan item
struct Item {
    int id;
    int weight;
    int value;
    double ratio; // Rasio nilai per berat

    // Constructor
    Item(int i, int w, int v) : id(i), weight(w), value(v) {
        ratio = static_cast<double>(value) / weight;
    }
};

// Fungsi perbandingan untuk mengurutkan item berdasarkan rasio secara menurun
bool compareItems(const Item& a, const Item& b) {
    return a.ratio > b.ratio;
}

// Fungsi untuk menyelesaikan masalah Fractional Knapsack
double fractionalKnapsack(int capacity, std::vector<Item>& items) {
    // Urutkan item berdasarkan rasio nilai per berat secara menurun
    std::sort(items.begin(), items.end(), compareItems);

    double totalValue = 0.0;
    int currentWeight = 0; // Berat saat ini di dalam knapsack

    std::cout << "Memilih item:" << std::endl;

    // Iterasi melalui item yang sudah diurutkan
    for (const auto& item : items) {
        if (currentWeight + item.weight <= capacity) {
            // Jika seluruh item dapat dimasukkan
            totalValue += item.value;
            currentWeight += item.weight;
            std::cout << "  - Mengambil seluruh Item " << item.id 
                      << " (Berat: " << item.weight << "kg, Nilai: *" << item.value << ")" << std::endl;
        } else {
            // Jika hanya sebagian item yang dapat dimasukkan
            int remainingCapacity = capacity - currentWeight;
            double fraction = static_cast<double>(remainingCapacity) / item.weight;
            totalValue += fraction * item.value;
            currentWeight += remainingCapacity; // Knapsack akan penuh
            
            std::cout << "  - Mengambil " << std::fixed << std::setprecision(2) << (fraction * 100) 
                      << "% dari Item " << item.id 
                      << " (Berat diambil: " << remainingCapacity << "kg, Nilai diambil: *" 
                      << std::fixed << std::setprecision(2) << (fraction * item.value) << ")" << std::endl;
            break; // Knapsack sudah penuh, hentikan
        }
    }
    std::cout << std::endl;
    return totalValue;
}

int main() {
    int capacity = 15; // Kapasitas knapsack
    std::vector<Item> items;

    // Menambahkan item ke vektor
    items.emplace_back(1, 7, 21); // Item A
    items.emplace_back(2, 5, 20); // Item B
    items.emplace_back(3, 3, 12); // Item C
    items.emplace_back(4, 4, 8);  // Item D

    std::cout << "Kapasitas Knapsack: " << capacity << "kg" << std::endl;
    std::cout << "Item yang tersedia:" << std::endl;
    for(const auto& item : items) {
        std::cout << "  Item " << item.id << ": Berat " << item.weight 
                  << "kg, Nilai *" << item.value 
                  << ", Rasio *" << std::fixed << std::setprecision(2) << item.ratio << "/kg" << std::endl;
    }
    std::cout << "---" << std::endl;

    double maxValue = fractionalKnapsack(capacity, items);

    std::cout << "Nilai Total Maksimum: *" << std::fixed << std::setprecision(2) << maxValue << std::endl;

    return 0;
}
```

**Output dari kode C++ di atas akan menjadi:**

```
Kapasitas Knapsack: 15kg
Item yang tersedia:
  Item 1: Berat 7kg, Nilai *21, Rasio *3.00/kg
  Item 2: Berat 5kg, Nilai *20, Rasio *4.00/kg
  Item 3: Berat 3kg, Nilai *12, Rasio *4.00/kg
  Item 4: Berat 4kg, Nilai *8, Rasio *2.00/kg
---
Memilih item:
  - Mengambil seluruh Item 2 (Berat: 5kg, Nilai: *20)
  - Mengambil seluruh Item 3 (Berat: 3kg, Nilai: *12)
  - Mengambil seluruh Item 1 (Berat: 7kg, Nilai: *21)

Nilai Total Maksimum: *53.00
```

### Contoh
Kapasitas 15 kg, item:  
A (7kg, 21), B (5kg, 20), C (3kg, 12), D (4kg, 8)  
Urutkan rasio: B & C (4), A (3), D (2).  
Ambil B, C, A (total nilai: 53).

### Aplikasi
- Alokasi sumber daya
- Manajemen investasi
- Pemuatan barang
- Penjadwalan tugas

### Kesimpulan
Fractional Knapsack dapat diselesaikan optimal dan efisien dengan greedy, berbeda dengan 0/1 Knapsack yang butuh pemrograman dinamis.


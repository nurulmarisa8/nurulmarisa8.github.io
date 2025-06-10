---
title : Fractional Knapsack
date : 2025-05-06
categories : [Summary Portfolio Material]
tags : [Portfolio Desain & Analisis Algoritma]
---


# 🎒 Fractional Knapsack Problem

## 📚 Definisi
**Fractional Knapsack** adalah permasalahan optimisasi dalam algoritma dan struktur data, dengan tujuan memaksimalkan total nilai barang dalam knapsack (tas) yang memiliki kapasitas terbatas. Berbeda dengan 0/1 Knapsack, pada versi ini **barang bisa diambil sebagian (fraksi)**.

---

## 🧩 Karakteristik Permasalahan
- Setiap item memiliki nilai (value) dan berat (weight).
- Tas memiliki kapasitas terbatas.
- Barang boleh diambil sebagian (misalnya 0.5 bagian).
- Dapat diselesaikan dengan **algoritma greedy**.

---

## ⚙️ Strategi Penyelesaian (Greedy Algorithm)
1. Hitung **rasio value/weight** untuk setiap barang.
2. Urutkan barang berdasarkan rasio tersebut secara **menurun**.
3. Ambil sebanyak mungkin dari barang dengan rasio tertinggi:
   - Jika kapasitas cukup → ambil penuh.
   - Jika tidak → ambil fraksinya sesuai sisa kapasitas.

---

## 💻 Implementasi dalam C++

```cpp
// Fungsi comparator untuk mengurutkan berdasarkan rasio terbesar
bool compare(Item a, Item b) {
    return a.ratio() > b.ratio();
}

int main() {
    double capacity = 30.0; // kapasitas maksimal kurir
    vector<Item> items = {
        {"Laptop", 10, 300},
        {"Buku Paket", 20, 200},
        {"Baju", 30, 180}
    };

    // Urutkan berdasarkan rasio value/weight tertinggi
    sort(items.begin(), items.end(), compare);

    double totalValue = 0.0;
    double totalWeight = 0.0;

    cout << "Barang yang dipilih:\n";
    for (const auto& item : items) {
        if (capacity == 0) break;

        if (item.weight <= capacity) {
            // Ambil seluruh barang
            totalValue += item.value;
            capacity -= item.weight;
            cout << "- " << item.name << " (berat: " << item.weight 
                 << " kg, nilai: " << item.value << ")\n";
        } else {
            // Ambil sebagian barang (fractional)
            double fraction = capacity / item.weight;
            totalValue += item.value * fraction;
            cout << "- " << item.name << " (berat: " << capacity << " kg dari " 
                 << item.weight << " kg, nilai: " << item.value * fraction << ")\n";
            capacity = 0;
        }
    }

    cout << "\nTotal nilai yang dibawa: " << totalValue << endl;
    return 0;
}
```

### 🔹 Fractional Knapsack Problem
Masalah ini bertujuan untuk **memaksimalkan nilai total barang** dalam sebuah tas dengan kapasitas terbatas, dengan mengizinkan pengambilan barang secara fraksional. Algoritma greedy digunakan dengan cara memilih barang berdasarkan **rasio nilai terhadap berat (value/weight)** yang paling tinggi terlebih dahulu. Strategi ini terbukti memberikan solusi optimal secara efisien.


## 💻 Implementasi C++

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

// Struktur untuk item dalam knapsack
struct Item {
    int value;   // Nilai barang
    int weight;  // Berat barang
    double ratio; // Rasio value/weight

    Item(int v, int w) : value(v), weight(w), ratio(double(v) / w) {}
};

// Fungsi pembanding untuk urutan rasio tertinggi
bool compare(Item& a, Item& b) {
    return a.ratio > b.ratio;
}

// Fungsi utama untuk mengimplementasikan Fractional Knapsack
double fractionalKnapsack(int W, vector<Item>& items) {
    // Urutkan barang berdasarkan rasio value/weight secara menurun
    sort(items.begin(), items.end(), compare);

    double totalValue = 0.0; // Total nilai yang akan dimasukkan ke dalam tas
    for (Item& item : items) {
        // Jika tas masih dapat menampung barang penuh
        if (W >= item.weight) {
            totalValue += item.value;  // Ambil barang sepenuhnya
            W -= item.weight;         // Kurangi kapasitas tas
        }
        // Jika tas tidak dapat menampung barang sepenuhnya, ambil sebagian
        else {
            totalValue += item.ratio * W;  // Ambil sebagian barang
            break;  // Tas sudah penuh
        }
    }

    return totalValue;
}

int main() {
    // Nilai barang dan beratnya
    vector<Item> items = {
        Item(60, 10),  // Value = 60, Weight = 10
        Item(100, 20), // Value = 100, Weight = 20
        Item(120, 30)  // Value = 120, Weight = 30
    };
    
    int W = 50;  // Kapasitas tas

    // Panggil fungsi untuk mendapatkan nilai maksimum yang dapat diambil
    double maxValue = fractionalKnapsack(W, items);

    // Tampilkan hasil
    cout << "Maksimum nilai yang dapat dimasukkan ke dalam tas: " << maxValue << endl;

    return 0;
}
```

# 📝 Kesimpulan

## 📦 Fractional Knapsack
**Fractional Knapsack** menyelesaikan masalah pemilihan barang dengan batasan kapasitas tas dan memungkinkan pengambilan barang secara fraksional. Algoritma **greedy** digunakan dengan memilih barang berdasarkan rasio **value/weight**. Keunggulan algoritma ini adalah kesederhanaan dan efisiennya, terutama jika barang bisa dipotong-potong.

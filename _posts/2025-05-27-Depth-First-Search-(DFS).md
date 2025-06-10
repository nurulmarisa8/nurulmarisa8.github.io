---
title : Depth-First Search (DFS)
date : 2025-05-27
categories : [Summary Portfolio Material]
tags : [Portfolio Desain & Analisis Algoritma]
---

# 🌲 Depth-First Search (DFS)

## 📘 Pengertian
**Depth-First Search (DFS)** adalah algoritma penelusuran graf atau pohon yang menjelajahi simpul-simpul dengan cara menyelam sedalam mungkin ke dalam cabang sebelum kembali ke simpul sebelumnya (backtrack). 

DFS menggunakan prinsip **LIFO (Last-In-First-Out)** dan biasa diimplementasikan menggunakan **rekursi** atau **stack**.

---

## 🔧 Konsep Dasar DFS
1. Mulai dari simpul awal (start node).
2. Tandai simpul sebagai **dikunjungi (visited)**.
3. Telusuri tetangga yang belum dikunjungi secara **rekursif** (atau melalui stack).
4. Jika tidak ada tetangga tersisa, **kembali (backtrack)** ke simpul sebelumnya.

DFS bekerja **menyeluruh ke satu jalur** hingga akhir, baru kemudian pindah ke jalur lain.

---

## 📍 Langkah-Langkah DFS
1. Pilih simpul awal.
2. Tandai simpul sebagai dikunjungi.
3. Untuk setiap tetangga yang belum dikunjungi:
   - Kunjungi tetangga tersebut secara rekursif.
4. Proses selesai saat semua simpul telah dikunjungi.

---

## 💻 Contoh Implementasi DFS (C++ Rekursif)

```cpp
#include <iostream>
#include <vector>
using namespace std;

void dfs(int node, vector<vector<int>>& adjList, vector<bool>& visited) {
    visited[node] = true;
    cout << node << " ";

    for (int neighbor : adjList[node]) {
        if (!visited[neighbor]) {
            dfs(neighbor, adjList, visited);
        }
    }
}

int main() {
    int n = 5; // jumlah simpul
    vector<vector<int>> adjList(n);

    // contoh graf tak berarah
    adjList[0] = {1, 2}; // node 0 terhubung ke 1 dan 2
    adjList[1] = {0, 3};
    adjList[2] = {0, 4};
    adjList[3] = {1};
    adjList[4] = {2};

    vector<bool> visited(n, false);
    cout << "DFS dari simpul 0: ";
    dfs(0, adjList, visited);

    return 0;
}
```

# 📝 Kesimpulan

## 🌲 Depth-First Search (DFS)
**Depth-First Search (DFS)** adalah algoritma penelusuran graf yang bekerja dengan menyelam ke dalam cabang lebih dalam sebelum kembali ke simpul sebelumnya. DFS sering digunakan dalam masalah rekursif seperti **backtracking** dan sangat efektif untuk pencarian jalur dalam graf dan pohon. DFS sangat cocok untuk graf yang lebih dalam dan sempit.

---
title :  Kahn’s Algorithm
date : 2025-06-03
categories : [Summary Portfolio Material]
tags : [Portfolio Desain & Analisis Algoritma]
---

# 📊 Kahn’s Algorithm for Topological Sorting

## 📘 Pengertian
**Kahn’s Algorithm** adalah metode **topological sorting** pada graf berarah **tanpa siklus (Directed Acyclic Graph/DAG)**. Algoritma ini digunakan untuk menentukan **urutan eksekusi simpul (nodes)** berdasarkan **ketergantungan (dependency)** antar simpul.

Algoritma ini berbasis pada prinsip **Breadth-First Search (BFS)**, dengan memanfaatkan struktur **in-degree** (jumlah sisi masuk ke simpul) dan **antrian (queue)**.

---

## 🔧 Prinsip Dasar Kahn’s Algorithm
Untuk setiap **edge u → v**, simpul `u` harus muncul **sebelum** `v` dalam urutan topologis.

### Langkah-langkah Algoritma:
1. Hitung **in-degree** (jumlah sisi masuk) untuk setiap simpul.
2. Tambahkan semua simpul dengan **in-degree = 0** ke dalam queue.
3. Selama queue tidak kosong:
   - Ambil simpul dari depan queue dan tambahkan ke urutan hasil.
   - Kurangi in-degree semua tetangga simpul tersebut.
   - Jika in-degree tetangga menjadi 0, masukkan ke queue.
4. Jika semua simpul telah diproses → **tidak ada siklus**.
   Jika tidak → graf **mengandung siklus**.

---

## 💻 Contoh Kasus

### Studi Kasus: Mata Kuliah
```text
A dan B adalah prasyarat untuk C
C adalah prasyarat untuk D
```

```text
Tugas: A, B, C, D, E, F
- A sebelum D
- F sebelum A dan B
- B sebelum D
- D sebelum C
```

## 💻 Contoh Implementasi C++ (Kahn's Algorithm)

```cpp
#include <iostream>
#include <unordered_map>
#include <vector>
#include <queue>
using namespace std;

void kahnTopologicalSort(int V, unordered_map<int, vector<int>>& adj) {
    vector<int> inDegree(V, 0);

    // Hitung in-degree
    for (auto& pair : adj) {
        for (int neighbor : pair.second)
            inDegree[neighbor]++;
    }

    queue<int> q;
    for (int i = 0; i < V; i++)
        if (inDegree[i] == 0)
            q.push(i);

    vector<int> result;
    while (!q.empty()) {
        int node = q.front();
        q.pop();
        result.push_back(node);

        for (int neighbor : adj[node]) {
            inDegree[neighbor]--;
            if (inDegree[neighbor] == 0)
                q.push(neighbor);
        }
    }

    if (result.size() != V) {
        cout << "Graf mengandung siklus.\n";
    } else {
        cout << "Urutan Topologis: ";
        for (int node : result)
            cout << node << " ";
        cout << endl;
    }
}

int main() {
    int V = 6;
    unordered_map<int, vector<int>> adj;
    // F (5) → A (0), B (1)
    // A (0) → D (3)
    // B (1) → D (3)
    // D (3) → C (2)

    adj[5] = {0, 1};
    adj[0] = {3};
    adj[1] = {3};
    adj[3] = {2};

    kahnTopologicalSort(V, adj);
    return 0;
}

```

# 📝 Kesimpulan

## 🔄 Kahn’s Algorithm
**Kahn’s Algorithm** digunakan untuk melakukan **topological sorting** pada **Directed Acyclic Graph (DAG)**. Algoritma ini berbasis pada prinsip **Breadth-First Search (BFS)** dan menggunakan struktur **in-degree** untuk memastikan simpul-simpul diproses dalam urutan yang valid sesuai dengan ketergantungannya. Kahn’s Algorithm sangat berguna dalam aplikasi yang melibatkan dependency seperti penjadwalan tugas, kompilasi program, dan alokasi sumber daya.

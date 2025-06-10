---
title :  Dijkstra’s Algorithm
date : 2025-06-03
categories : [Summary Portfolio Material]
tags : [Portfolio Desain & Analisis Algoritma]
---

# 📍 Dijkstra's Algorithm

---

## 📘 Apa itu Dijkstra’s Algorithm?

**Dijkstra's Algorithm** adalah metode untuk mencari **jalur terpendek** antara dua titik dalam **graf berbobot non-negatif**. Graf terdiri dari simpul (nodes) dan sisi (edges) dengan bobot (weight) tertentu. Algoritma ini digunakan dalam berbagai aplikasi seperti navigasi, jaringan komputer, dan logistik.

---

## 🔧 Cara Kerja Dijkstra’s Algorithm

1. Buat tabel untuk menyimpan jarak minimum dari simpul awal ke setiap simpul.
2. Pilih simpul awal, tetapkan jaraknya = 0, dan sisanya = ∞.
3. Tandai simpul yang telah dikunjungi.
4. Dari simpul saat ini, perbarui jarak semua tetangganya jika jalur baru lebih pendek.
5. Pilih simpul dengan jarak minimum yang belum dikunjungi sebagai simpul baru.
6. Ulangi hingga semua simpul telah dikunjungi atau simpul tujuan ditemukan.

---

## 💻 Ilustrasi dan Contoh Kasus

### Tujuan:
Carilah jalur terpendek dari simpul **A ke F**

```text
Graf:
A —1→ B
A —5→ C
B —2→ E
B —1→ D
D —2→ F
E —3→ F
```

## Implementasi Sederhana Dijkstra dalam C++

```cpp
#include <iostream>
#include <vector>
#include <queue>
using namespace std;

const int INF = 1e9;

void dijkstra(int start, vector<vector<pair<int, int>>>& adj, vector<int>& dist) {
    priority_queue<pair<int, int>, vector<pair<int, int>>, greater<>> pq;
    dist[start] = 0;
    pq.push({0, start});

    while (!pq.empty()) {
        auto [d, u] = pq.top();
        pq.pop();

        if (d > dist[u]) continue;

        for (auto [v, w] : adj[u]) {
            if (dist[u] + w < dist[v]) {
                dist[v] = dist[u] + w;
                pq.push({dist[v], v});
            }
        }
    }
}

int main() {
    int n = 6;
    vector<vector<pair<int, int>>> adj(n);

    // A=0, B=1, C=2, D=3, E=4, F=5
    adj[0].push_back({1, 1}); // A→B
    adj[0].push_back({2, 5}); // A→C
    adj[1].push_back({4, 2}); // B→E
    adj[1].push_back({3, 1}); // B→D
    adj[3].push_back({5, 2}); // D→F
    adj[4].push_back({5, 3}); // E→F

    vector<int> dist(n, INF);
    dijkstra(0, adj, dist);

    cout << "Jarak terpendek dari A ke F: " << dist[5] << endl;
    return 0;
}

```

# 📝 Kesimpulan

## 🛣️ Dijkstra’s Algorithm
**Dijkstra’s Algorithm** digunakan untuk menemukan **jalur terpendek** antara dua simpul dalam graf berbobot non-negatif. Dengan menggunakan **greedy approach**, Dijkstra selalu memilih jalur yang paling pendek pada setiap langkah. Algoritma ini banyak digunakan dalam aplikasi **routing jaringan**, **navigasi GPS**, dan **sistem pemetaan** untuk menemukan jalur terpendek dengan efisien.

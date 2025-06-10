---
title : Breadth-First Search (BFS)
date : 2025-05-27
categories : [Summary Portfolio Material]
tags : [Portfolio Desain & Analisis Algoritma]
---

# 🌐 Breadth-First Search (BFS)

## 📘 Pengertian
**Breadth-First Search (BFS)** adalah algoritma pencarian dalam struktur **graf atau pohon** yang menjelajahi simpul-simpul berdasarkan **jaraknya dari simpul awal (start node)**. BFS bekerja secara **level-order traversal**, yaitu mengeksplorasi semua simpul pada satu tingkat/lapisan sebelum berpindah ke tingkat berikutnya.

Ilustrasi: Mencari ruang kelas di gedung kampus 3 lantai — kamu akan memeriksa semua ruangan di lantai 1 terlebih dahulu sebelum naik ke lantai 2.

---

## 🔧 Konsep Dasar
1. Menggunakan **struktur data queue (antrian)**.
2. Menjelajah semua simpul tetangga sebelum berpindah ke tetangga dari simpul-simpul tersebut.
3. Memastikan semua simpul pada tingkat yang sama dikunjungi sebelum masuk ke tingkat berikutnya.

---

## 📍 Langkah-Langkah Algoritma BFS
1. Tentukan simpul awal (start node).
2. Masukkan simpul awal ke dalam **queue** dan tandai sebagai **visited**.
3. Selama queue tidak kosong:
   - Ambil simpul terdepan dari queue.
   - Periksa apakah itu simpul tujuan.
   - Tambahkan semua tetangganya yang belum dikunjungi ke dalam queue dan tandai sebagai visited.
4. Ulangi sampai simpul tujuan ditemukan atau queue kosong.

---

## 💻 Representasi dan Contoh Proses BFS

### Struktur Graf:

```text
        S
       / \
      A   B
     / \   \
    C   D   E
       / \
      F   H
           \
            G
```


```text 
Langkah     Queue              Aktif     Visited
1           S                  S         S
2           A, B              A         S, A
3           B, C, D           B         S, A, B
4           C, D, E, F        C         S, A, B, C
5           D, E, F           D         ...
...
```

## 💻 Contoh Implementasi C++ BFS

```cpp
#include <iostream>
#include <vector>
#include <queue>
using namespace std;

void bfs(int start, vector<vector<int>>& adjList, int n) {
    vector<bool> visited(n, false);
    queue<int> q;

    visited[start] = true;
    q.push(start);

    while (!q.empty()) {
        int current = q.front();
        q.pop();
        cout << current << " ";

        for (int neighbor : adjList[current]) {
            if (!visited[neighbor]) {
                visited[neighbor] = true;
                q.push(neighbor);
            }
        }
    }
}

int main() {
    int n = 6; // jumlah simpul
    vector<vector<int>> adjList(n);

    // contoh graf tidak berarah
    adjList[0] = {1, 2}; // S
    adjList[1] = {0, 3, 4}; // A
    adjList[2] = {0, 5}; // B
    adjList[3] = {1}; // C
    adjList[4] = {1}; // D
    adjList[5] = {2}; // E

    bfs(0, adjList, n); // mulai dari simpul 0 (S)
    return 0;
}
```

# 📝 Kesimpulan

## 🌐 Breadth-First Search (BFS)
**Breadth-First Search (BFS)** adalah algoritma penelusuran graf yang bekerja dengan mengunjungi semua simpul yang paling dekat terlebih dahulu sebelum melanjutkan ke simpul yang lebih jauh. BFS menggunakan **queue** dan cocok digunakan untuk pencarian jalur terpendek di graf tak berbobot. BFS banyak diterapkan dalam aplikasi seperti penelusuran jaringan sosial, GPS, dan sistem pencarian.


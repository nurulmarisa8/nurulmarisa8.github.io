---
title : Rat in a Maze
date : 2025-05-27
categories : [Summary Portfolio Material]
tags : [Portfolio Desain & Analisis Algoritma]
---

# 🐭 Rat in a Maze Problem

## 📘 Definisi
**Rat in a Maze** adalah masalah algoritmik klasik yang melibatkan seekor tikus yang harus menemukan jalan keluar dari labirin persegi (maze) yang direpresentasikan sebagai **matriks/grid 2D**. Sel bernilai `1` berarti **bisa dilewati**, sedangkan `0` berarti **terhalang**.

Solusi ditemukan dengan algoritma **backtracking**: mencoba langkah demi langkah ke setiap arah yang valid, dan **mundur (backtrack)** jika jalan buntu ditemukan.

---

## 🧠 Prinsip Kerja
1. Tikus mulai dari titik awal `(0, 0)`.
2. Ia mencoba bergerak ke satu dari 4 arah:
   - **U** (Up / Atas)
   - **D** (Down / Bawah)
   - **L** (Left / Kiri)
   - **R** (Right / Kanan)
3. Jika sel tujuan valid (tidak keluar dari grid dan bukan tembok), lanjut ke sel tersebut.
4. Jika tidak ada jalan keluar, tikus akan kembali ke posisi sebelumnya dan mencoba arah lain (backtracking).

---

## 🧪 Contoh Maze

```text
Matriks Maze (N x N):

1 0 0 0
1 1 0 1
1 1 0 0
0 1 1 1

Titik awal: (0, 0)
Tujuan akhir: (3, 3)
```

## 💻 Implementasi C++ (Backtracking)

```cpp 
#include <iostream>
#include <vector>
using namespace std;

bool isSafe(int x, int y, vector<vector<int>>& maze, vector<vector<bool>>& visited, int n) {
    return (x >= 0 && x < n && y >= 0 && y < n &&
            maze[x][y] == 1 && !visited[x][y]);
}

void solve(int x, int y, vector<vector<int>>& maze, int n, vector<string>& paths, string path, vector<vector<bool>>& visited) {
    if (x == n - 1 && y == n - 1) {
        paths.push_back(path);
        return;
    }

    visited[x][y] = true;

    // Down
    if (isSafe(x + 1, y, maze, visited, n)) {
        solve(x + 1, y, maze, n, paths, path + 'D', visited);
    }
    // Left
    if (isSafe(x, y - 1, maze, visited, n)) {
        solve(x, y - 1, maze, n, paths, path + 'L', visited);
    }
    // Right
    if (isSafe(x, y + 1, maze, visited, n)) {
        solve(x, y + 1, maze, n, paths, path + 'R', visited);
    }
    // Up
    if (isSafe(x - 1, y, maze, visited, n)) {
        solve(x - 1, y, maze, n, paths, path + 'U', visited);
    }

    visited[x][y] = false; // backtrack
}

vector<string> findPaths(vector<vector<int>>& maze, int n) {
    vector<string> paths;
    vector<vector<bool>> visited(n, vector<bool>(n, false));

    if (maze[0][0] == 1) {
        solve(0, 0, maze, n, paths, "", visited);
    }

    return paths;
}

int main() {
    vector<vector<int>> maze = {
        {1, 0, 0, 0},
        {1, 1, 0, 1},
        {1, 1, 0, 0},
        {0, 1, 1, 1}
    };

    vector<string> solutions = findPaths(maze, 4);
    for (const string& path : solutions) {
        cout << path << endl;
    }

    return 0;
}
```

# 📝 Kesimpulan

## 🐭 Rat in a Maze
**Rat in a Maze** adalah masalah pencarian jalur yang melibatkan algoritma **backtracking** untuk menemukan jalan keluar dari labirin. Dengan cara menyelam sedalam mungkin ke dalam cabang, algoritma ini mengeksplorasi semua jalur hingga menemukan jalan keluar atau kembali ke jalur sebelumnya jika tidak ditemukan solusi. Algoritma ini sangat efektif dalam pemecahan masalah labirin dan permainan berbasis graf.

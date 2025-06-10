---
title : N-Queens Problem
date : 2025-05-20
categories : [Summary Portfolio Material]
tags : [Portfolio Desain & Analisis Algoritma]
---

# ♛ N-Queens Problem

## 📚 Definisi Masalah
**N-Queens** adalah masalah klasik dalam ilmu komputer dan matematika kombinatorik yang melibatkan penempatan **N buah ratu** pada papan catur berukuran **N × N**. Tujuannya adalah **tidak ada dua ratu yang saling menyerang** secara horizontal, vertikal, maupun diagonal.

Contoh paling terkenal: **8-Queens**, menempatkan 8 ratu di papan 8x8.

---

## 🎯 Tujuan
1. Menemukan semua konfigurasi penempatan ratu yang **tidak saling menyerang**.
2. Menguji dan mengembangkan algoritma pencarian: **backtracking**, DFS, heuristic, atau genetika.
3. Melatih logika pemrograman dan memahami **Constraint Satisfaction Problem (CSP)**.

---

## 🔎 Pentingnya N-Queens
- ✅ Studi kasus dalam AI dan algoritma pencarian (Backtracking, Branch and Bound, Heuristic).
- ✅ Model dari CSP yang memuat variabel (baris/kolom) dan constraint (larangan saling menyerang).
- ✅ Aplikasi nyata: penjadwalan tugas, penempatan modul dalam sirkuit, alokasi sumber daya.
- ✅ Kompleksitas eksponensial → cocok untuk evaluasi performa algoritma skala besar.

---

## 🤖 Mengapa Menggunakan Backtracking?
- Proses bertahap: menempatkan satu ratu per baris dan memeriksa validitas posisi.
- Jika tidak valid → **backtrack** (kembali ke langkah sebelumnya).
- Relevan dengan **pohon pencarian solusi** dan **penelusuran rekursif**.
- Teknik **brute-force yang sistematis dan efisien**.

---

## 🧩 Langkah-langkah Backtracking
1. **Decision Choice**: Pilih kolom untuk tiap baris.
2. **Constraint Check**: Cek apakah aman (tidak diserang).
3. **Recursive Exploration**: Jika valid, lanjut ke baris berikutnya.
4. **Backtrack**: Jika tidak ada pilihan aman, kembali ke langkah sebelumnya.
5. **Base Case**: Jika semua ratu telah ditempatkan → solusi ditemukan.

---

## 💡 Studi Kasus Permutasi (Analog)
Permutasi dari `[1,2,3]`:
- Proses mirip rekursi & backtrack → coba semua kemungkinan kombinasi, dan mundur jika jalan buntu.

Solusi akhir:
```text
[[1,2,3], [1,3,2], [2,1,3], [2,3,1], [3,1,2], [3,2,1]]
```


## 💻 Contoh Kode C++

```cpp
#define N 8
#include <iostream>
using namespace std;

void printBoard(int board[N][N]) {
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < N; j++)
            cout << (board[i][j] ? "Q " : ". ");
        cout << endl;
    }
    cout << "--------" << endl;
}

bool isSafe(int board[N][N], int row, int col) {
    for (int i = 0; i < row; i++)
        if (board[i][col]) return false;
    for (int i = row - 1, j = col - 1; i >= 0 && j >= 0; i--, j--)
        if (board[i][j]) return false;
    for (int i = row - 1, j = col + 1; i >= 0 && j < N; i--, j++)
        if (board[i][j]) return false;
    return true;
}

void solve(int board[N][N], int row) {
    if (row == N) {
        printBoard(board);
        return;
    }
    for (int col = 0; col < N; col++) {
        if (isSafe(board, row, col)) {
            board[row][col] = 1;
            solve(board, row + 1);
            board[row][col] = 0; // backtrack
        }
    }
}

int main() {
    int board[N][N] = {0};
    solve(board, 0);
    return 0;
}
```

# 📝 Kesimpulan

## ♛ N-Queens Problem
**N-Queens** adalah masalah klasik dalam algoritma dan matematika kombinatorik yang melibatkan penempatan **N buah ratu** pada papan catur berukuran **N × N**, dengan tujuan agar **tidak ada dua ratu yang saling menyerang** baik secara horizontal, vertikal, maupun diagonal. Masalah ini sering diselesaikan menggunakan **backtracking**, yang memanfaatkan pendekatan eksplorasi dan kembali (recursive) untuk menemukan solusi valid. Algoritma ini berguna dalam memahami teknik pencarian solusi dengan memeriksa semua kemungkinan solusi yang ada.

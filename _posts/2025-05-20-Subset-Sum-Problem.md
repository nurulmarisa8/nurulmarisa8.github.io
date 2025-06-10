---
title : Subset Sum Problem
date : 2025-05-20
categories : [Summary Portfolio Material]
tags : [Portfolio Desain & Analisis Algoritma]
---


# 🧮 Subset Sum Problem (SSP)

## 📘 Definisi
**Subset Sum Problem** adalah masalah algoritmik klasik dalam kategori **NP-Complete**, di mana kita ingin mengetahui apakah dari suatu himpunan bilangan bulat, terdapat subset yang jumlah totalnya **sama dengan nilai target tertentu**. SSP sangat penting dalam konteks pemrograman dinamis, kecerdasan buatan, hingga pengelolaan sumber daya.

---

## 🔄 Variasi Subset Sum

1. **Bounded SSP** – Elemen hanya digunakan satu kali.
2. **Unbounded SSP** – Elemen boleh digunakan berulang kali.
3. **Exact k Elements SSP** – Subset harus terdiri dari tepat *k* elemen.
4. **Partition Problem** – Membagi himpunan menjadi dua subset dengan jumlah sama.
5. **Multi-Target SSP** – Harus memenuhi banyak kriteria (misal: nilai dan berat).
6. **Approximate SSP** – Tidak ada subset tepat, cari yang mendekati target.

---

## 🧠 Pendekatan Penyelesaian

### 🔁 1. Rekursif Sederhana
- Coba semua kombinasi subset.
- Kompleksitas waktu: **O(2ⁿ)** → tidak efisien jika *n* besar (> 20).

### 🧠 2. Dynamic Programming

#### A. Top-Down (Memoization)
- Simpan hasil dari subproblem dalam `dp[n][sum]`.
- Menghindari perhitungan ulang yang sama.

#### B. Bottom-Up (Tabulasi)
- Iteratif, mulai dari subset kosong hingga mencapai target.
- Inisialisasi:
  - `dp[i][0] = true` → sum 0 bisa dari subset kosong.
  - `dp[0][j ≠ 0] = false` → tanpa elemen tidak bisa mencapai sum > 0.

#### C. Space Optimization
- Gunakan dua array 1D: `prev[]` dan `curr[]`.
- Hemat ruang dari **O(n × sum)** menjadi **O(sum)**.

---

## 💻 Implementasi C++ (Bottom-Up DP)

```cpp
#include <iostream>
#include <vector>
using namespace std;

bool isSubsetSum(vector<int>& arr, int target) {
    int n = arr.size();
    vector<vector<bool>> dp(n + 1, vector<bool>(target + 1, false));

    // Inisialisasi: subset kosong bisa membentuk sum 0
    for (int i = 0; i <= n; i++)
        dp[i][0] = true;

    // Proses DP
    for (int i = 1; i <= n; i++) {
        for (int sum = 1; sum <= target; sum++) {
            if (arr[i - 1] > sum)
                dp[i][sum] = dp[i - 1][sum];
            else
                dp[i][sum] = dp[i - 1][sum] || dp[i - 1][sum - arr[i - 1]];
        }
    }

    return dp[n][target];
}

int main() {
    vector<int> arr = {3, 34, 4, 12, 5, 2};
    int target = 9;

    if (isSubsetSum(arr, target))
        cout << "YA, subset dengan jumlah " << target << " ditemukan.\n";
    else
        cout << "TIDAK, tidak ada subset dengan jumlah " << target << ".\n";

    return 0;
}
```

# 📝 Kesimpulan

## 🔢 Subset Sum Problem (SSP)
**Subset Sum Problem** adalah masalah di mana kita diberikan sebuah himpunan bilangan bulat dan sebuah nilai target, dan tujuan kita adalah **menentukan apakah ada subset** dari himpunan yang jumlahnya sama dengan target. Algoritma **dynamic programming** atau **backtracking** sering digunakan untuk menyelesaikan masalah ini dengan lebih efisien. Dalam **dynamic programming**, solusi optimal ditemukan dengan memecah masalah menjadi submasalah yang lebih kecil dan menyimpannya untuk menghindari perhitungan ulang. **Subset Sum Problem** banyak diterapkan dalam analisis data dan pengalokasian sumber daya di berbagai bidang, seperti keuangan dan optimasi logistik.

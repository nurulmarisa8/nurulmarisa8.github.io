---
title : Activity Selection Problem
date : 2025-05-06
categories : [Summary Portfolio Material]
tags : [Portfolio Desain & Analisis Algoritma]
---


# 📌 Activity Selection Problem

## 🧠 Pengertian
**Activity Selection Problem (ASP)** adalah masalah optimasi klasik dalam ilmu komputer. Tujuannya adalah memilih sebanyak mungkin aktivitas yang **tidak tumpang tindih** berdasarkan waktu mulai dan selesai masing-masing aktivitas.

> Dua aktivitas dikatakan **kompatibel** jika salah satu selesai sebelum yang lainnya dimulai.

---

## 🧩 Strategi Penyelesaian: Algoritma Greedy
Algoritma Greedy digunakan untuk menyelesaikan masalah ini karena bersifat efisien dan memberikan solusi optimal dalam kasus sederhana.

### Langkah-Langkah:
1. **Urutkan aktivitas berdasarkan waktu selesai (finish time)**
2. **Pilih aktivitas pertama (paling awal selesai)**
3. **Iterasi aktivitas berikutnya:**
   - Pilih jika waktu mulai ≥ waktu selesai aktivitas sebelumnya yang dipilih

---

## 💻 Pseudocode

```text
ACTIVITY-SELECTOR(s, f, n)
    A = {a1}
    j = 1
    for i = 2 to n
        if s[i] >= f[j]
            A = A ∪ {ai}
            j = i
    return A
```


### 🔹 Activity Selection Problem
Masalah ini berfokus pada **pemilihan aktivitas sebanyak mungkin** tanpa terjadi konflik waktu (tumpang tindih). Strategi greedy yang digunakan adalah dengan selalu memilih aktivitas dengan **waktu selesai paling awal**, karena hal ini memberikan ruang waktu terbesar untuk aktivitas-aktivitas selanjutnya. Hasilnya, solusi yang diperoleh bersifat optimal untuk kasus tanpa batasan tambahan.

## 💻 Implementasi C++

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

// Struktur untuk aktivitas
struct Activity {
    int start, finish;
};

// Fungsi pembanding untuk pengurutan berdasarkan waktu selesai
bool compare(Activity a1, Activity a2) {
    return a1.finish < a2.finish;
}

// Fungsi untuk memilih aktivitas yang kompatibel
vector<Activity> activitySelection(vector<Activity>& activities) {
    // Urutkan aktivitas berdasarkan waktu selesai
    sort(activities.begin(), activities.end(), compare);

    // Pilih aktivitas pertama
    vector<Activity> selectedActivities;
    selectedActivities.push_back(activities[0]);

    // Pilih aktivitas yang tidak tumpang tindih
    int lastIndex = 0;
    for (int i = 1; i < activities.size(); i++) {
        if (activities[i].start >= activities[lastIndex].finish) {
            selectedActivities.push_back(activities[i]);
            lastIndex = i;
        }
    }

    return selectedActivities;
}

int main() {
    // Daftar aktivitas (waktu mulai, waktu selesai)
    vector<Activity> activities = {
        {1, 3}, {3, 5}, {0, 6}, {5, 7}, {3, 8}, {5, 9}, {6, 10}
    };

    // Menyelesaikan masalah Activity Selection
    vector<Activity> selected = activitySelection(activities);

    // Menampilkan aktivitas yang terpilih
    cout << "Aktivitas yang terpilih:\n";
    for (auto& activity : selected) {
        cout << "Start: " << activity.start << ", Finish: " << activity.finish << endl;
    }

    return 0;
}
```

# 📝 Kesimpulan

## 📚 Activity Selection Problem
**Activity Selection Problem** adalah masalah optimasi yang bertujuan memilih aktivitas sebanyak mungkin tanpa saling tumpang tindih. Dengan menggunakan **algoritma greedy**, solusi optimal dapat ditemukan dengan memilih aktivitas yang memiliki waktu selesai paling awal. Pendekatan ini efisien dan cocok digunakan dalam berbagai aplikasi seperti penjadwalan ruang kelas, proses CPU, dan logistik.

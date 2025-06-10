---
title : Huffman Coding
date : 2025-05-20
categories : [Summary Portfolio Material]
tags : [Portfolio Desain & Analisis Algoritma]
---

# 🧠 Huffman Coding

## 📚 Definisi
**Huffman Coding** adalah algoritma kompresi data **lossless** yang ditemukan oleh David A. Huffman pada tahun 1952. Algoritma ini digunakan untuk **mengurangi ukuran data** dengan mengganti karakter yang sering muncul dengan kode biner yang lebih pendek, dan karakter yang jarang muncul dengan kode yang lebih panjang.

> Umumnya digunakan pada format ZIP, JPEG, MP3, dan berbagai sistem kompresi lainnya.

---

## 🧩 Konsep Dasar
- Berdasarkan **frekuensi kemunculan karakter**.
- Karakter **sering muncul → kode lebih pendek**.
- Karakter **jarang muncul → kode lebih panjang**.
- Representasi dalam bentuk **pohon biner**.

---

## ⚙️ Langkah-langkah Huffman Coding
1. Hitung frekuensi tiap karakter dalam data.
2. Buat simpul untuk tiap karakter.
3. Gabungkan dua simpul dengan frekuensi terkecil.
4. Ulangi hingga terbentuk satu **pohon Huffman**.
5. Tetapkan kode biner: **0 ke kiri**, **1 ke kanan**.

---

## 💻 Simulasi
Contoh string: `"ABBCCCDDDD"`

- Frekuensi:
  - A: 1
  - B: 2
  - C: 3
  - D: 4
- Hasil kode Huffman (contoh):
  - D = `0`
  - C = `10`
  - B = `110`
  - A = `111`
- Ukuran bit:
  - ASCII: 8 bit × 10 karakter = **80 bit**
  - Huffman: **lebih hemat**, misalnya 45 bit saja

---

## 🛠️ Contoh Simulasi Lain
Pesan: `BCCABBDDAECCBBAEDDCC`

- ASCII: 8 bit × 20 karakter = **160 bit**
- Huffman:
  - Setelah proses penggabungan node & penandaan sisi pohon → hanya **45 bit**
- **Efisiensi ruang meningkat drastis**

---

## 💻 Pseudocode Huffman Coding

```text
1. Buat priority queue berdasarkan frekuensi karakter.
2. Selama ada lebih dari satu node:
   - Ambil dua node dengan frekuensi terkecil
   - Gabungkan jadi satu node baru (parent)
   - Masukkan kembali ke queue
3. Lakukan traversal pohon:
   - kiri = 0, kanan = 1
   - Tetapkan kode ke setiap karakter (daun)
```


## 💻 Implementasi C++

```cpp
#include <iostream>
#include <queue>
#include <unordered_map>
#include <vector>
using namespace std;

// Struktur untuk node Huffman
struct HuffmanNode {
    char ch;
    int freq;
    HuffmanNode* left;
    HuffmanNode* right;

    HuffmanNode(char c, int f) : ch(c), freq(f), left(nullptr), right(nullptr) {}
};

// Fungsi pembanding untuk priority queue
struct Compare {
    bool operator()(HuffmanNode* a, HuffmanNode* b) {
        return a->freq > b->freq;
    }
};

// Fungsi rekursif untuk menghasilkan kode Huffman
void generateCodes(HuffmanNode* root, string code, unordered_map<char, string>& huffmanCodes) {
    if (!root) return;

    // Jika leaf node
    if (!root->left && !root->right) {
        huffmanCodes[root->ch] = code;
    }

    generateCodes(root->left, code + "0", huffmanCodes);
    generateCodes(root->right, code + "1", huffmanCodes);
}

// Fungsi utama untuk membangun pohon Huffman dan menghasilkan kode
void huffmanEncoding(string text) {
    unordered_map<char, int> freq;

    // Hitung frekuensi karakter
    for (char c : text) {
        freq[c]++;
    }

    // Bangun priority queue
    priority_queue<HuffmanNode*, vector<HuffmanNode*>, Compare> pq;

    for (auto pair : freq) {
        pq.push(new HuffmanNode(pair.first, pair.second));
    }

    // Bangun pohon Huffman
    while (pq.size() > 1) {
        HuffmanNode* left = pq.top(); pq.pop();
        HuffmanNode* right = pq.top(); pq.pop();

        HuffmanNode* newNode = new HuffmanNode('\0', left->freq + right->freq);
        newNode->left = left;
        newNode->right = right;
        pq.push(newNode);
    }

    // Hasilkan kode Huffman
    HuffmanNode* root = pq.top();
    unordered_map<char, string> huffmanCodes;
    generateCodes(root, "", huffmanCodes);

    // Cetak kode hasil
    cout << "Huffman Codes:\n";
    for (auto pair : huffmanCodes) {
        cout << pair.first << " : " << pair.second << "\n";
    }

    // Tampilkan string terkompresi
    string encoded = "";
    for (char c : text) {
        encoded += huffmanCodes[c];
    }

    cout << "\nOriginal string: " << text << endl;
    cout << "Encoded string : " << encoded << endl;
}

int main() {
    string input = "ABBCCCDDDD";
    huffmanEncoding(input);
    return 0;
}
```

# 📝 Kesimpulan

## 📈 Huffman Coding
**Huffman Coding** adalah algoritma kompresi data lossless yang menggunakan pohon biner untuk menghasilkan kode biner yang efisien berdasarkan frekuensi kemunculan karakter. Dengan pendekatan **greedy**, algoritma ini mengurangi ukuran data dengan mengganti karakter yang sering muncul dengan kode bit lebih pendek. Huffman Coding banyak digunakan dalam format kompresi seperti ZIP, JPEG, dan MP3.


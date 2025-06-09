---
title: FRACTIONAL KNAPSACK
date: 2025-05-06
categories: [DESAIN ANALISIS ALGORITMA, GREEDY ALGORITHM]
tags: [daa, algorithm, greedy]     # TAG names should always be lowercase
---


**Pengantar**

Presentasi ini akan membahas "Fractional Knapsack", sebuah masalah optimasi yang penting dalam ilmu komputer. Kami akan mendalami definisi masalah, perbedaannya dengan 0/1 Knapsack, karakteristiknya, serta strategi penyelesaian menggunakan algoritma greedy. Selain itu, kami juga akan menganalisis kompleksitas waktu, melihat beberapa aplikasi dunia nyata, memahami konsep dasar algoritma greedy itu sendiri, dan melihat contoh implementasi kode.

**Anggota Kelompok**

Presentasi ini dibuat oleh Kelompok 2, yang terdiri dari anggota-anggota berikut:
* Zalfa Syauqiyah Hamka
* Davidzen
* Maisyah Mahdiyyah
* Muhammad Fadel Aryasatya Makkulau
* Hezekiah Reynard Tikupadang

**Knapsack Problem dan Fractional Knapsack**

Knapsack Problem adalah masalah optimasi di mana kita harus memilih barang-barang dari sekumpulan item agar nilai totalnya maksimal tanpa melebihi kapasitas berat ransel yang tersedia. Ada dua variasi utama dari masalah ini, yaitu 0/1 Knapsack dan Fractional Knapsack. Pada 0/1 Knapsack, kita hanya bisa memilih seluruh barang atau tidak sama sekali, sehingga barang tidak boleh dipotong-potong. Sedangkan pada Fractional Knapsack, kita diperbolehkan mengambil sebagian dari barang tersebut, sehingga barang bisa dipotong sesuai kebutuhan agar mendapatkan nilai maksimal. Perbedaan ini membuat 0/1 Knapsack menjadi lebih kompleks dan biasanya diselesaikan menggunakan metode pemrograman dinamis, sementara Fractional Knapsack dapat diselesaikan dengan algoritma greedy yang lebih sederhana dan efisien.

**Definisi dan Karakteristik Fractional Knapsack**

Fractional Knapsack adalah sebuah permasalahan optimisasi dalam bidang algoritma dan struktur data, di mana tujuannya adalah untuk memaksimalkan nilai total barang yang dimasukkan ke dalam sebuah knapsack (tas) dengan kapasitas tertentu, dengan kemungkinan mengambil sebagian (fraksi) dari barang.

Karakteristik Fractional Knapsack meliputi:
* Setiap barang memiliki berat (weight) dan nilai (value).
* Kapasitas tas adalah terbatas.
* Barang boleh dipotong atau diambil sebagian (misalnya 0.5 bagian dari barang A).
* Masalah ini dapat diselesaikan secara greedy karena tidak memerlukan pencarian kombinasi semua kemungkinan seperti pada 0/1 Knapsack.

**Strategi Penyelesaian Fractional Knapsack**

Untuk menyelesaikan Fractional Knapsack, digunakan pendekatan Greedy Algorithm:
1. Hitung *value per unit weight* untuk setiap item (value/weight).
2. Urutkan item berdasarkan nilai tersebut secara menurun.
3. Ambil sebanyak mungkin dari item dengan rasio tertinggi, hingga tas penuh.
4. Jika tidak bisa mengambil seluruh item karena kapasitas tersisa, ambil sebagian dari item terakhir.

**Kompleksitas Waktu**

* $O(n \log n)$ untuk mengurutkan item berdasarkan rasio value/weight.
* $O(n)$ untuk memasukkan item ke dalam tas.

**Aplikasi Fractional Knapsack**

Fractional Knapsack memiliki beberapa aplikasi praktis, di antaranya:
1. Penjadwalan tugas dengan sumber daya terbatas.
2. Investasi dana ke beberapa proyek.
3. Pengalokasian bandwidth di jaringan.
4. Optimisasi logistik.

**Algoritma Greedy**

Algoritma Greedy adalah sebuah pendekatan atau strategi dalam merancang algoritma yang membuat pilihan yang tampak terbaik pada saat itu (pilihan optimal lokal) dengan harapan bahwa pilihan tersebut akan mengarah pada solusi optimal global.

Karakteristik Utama Algoritma Greedy:
* **Pilihan Lokal Optimal**: Di setiap langkah, algoritma memilih opsi yang paling menguntungkan atau "greedy" saat itu.
* **Tidak Melihat ke Depan**: Keputusan dibuat berdasarkan informasi yang tersedia saat ini saja, tanpa mempertimbangkan sub-masalah yang akan muncul setelah keputusan tersebut dibuat.
* **Sederhana dan Cepat**: Algoritma greedy seringkali sangat sederhana untuk diimplementasikan dan memiliki kompleksitas waktu yang rendah dibandingkan pendekatan lain seperti pemrograman dinamis.

Algoritma greedy sangat efektif dan sering digunakan untuk masalah-masalah tertentu di mana pilihan optimal lokal memang mengarah ke solusi optimal global. Namun, kelemahan utama algoritma greedy adalah tidak selalu menghasilkan solusi optimal global untuk semua jenis masalah. Ada masalah di mana pilihan terbaik saat ini justru menghalangi tercapainya solusi terbaik secara keseluruhan.

**Implementasi C++ (Permasalahan 4)**

Meskipun detail spesifik dari "Permasalahan 4" tidak disertakan dalam presentasi, implementasi C++ untuk Fractional Knapsack biasanya melibatkan struktur data untuk item (berat dan nilai), fungsi untuk menghitung rasio nilai per berat, fungsi perbandingan untuk pengurutan, dan logika utama untuk mengisi knapsack secara greedy. Berikut adalah contoh umum dari implementasi C++ untuk Fractional Knapsack:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

// Struktur untuk merepresentasikan sebuah item
struct Item {
    int value;
    int weight;
    double ratio; // value per unit weight
};

// Fungsi perbandingan untuk mengurutkan item berdasarkan rasio secara menurun
bool compareItems(Item a, Item b) {
    return a.ratio > b.ratio;
}

// Fungsi untuk menyelesaikan Fractional Knapsack Problem
double fractionalKnapsack(int capacity, std::vector<Item>& items) {
    // Hitung rasio value/weight untuk setiap item
    for (int i = 0; i < items.size(); ++i) {
        items[i].ratio = (double)items[i].value / items[i].weight;
    }

    // Urutkan item berdasarkan rasio secara menurun
    std::sort(items.begin(), items.end(), compareItems);

    double totalValue = 0.0;
    int currentWeight = 0;

    // Iterasi melalui item yang sudah diurutkan
    for (int i = 0; i < items.size(); ++i) {
        // Jika item bisa diambil seluruhnya
        if (currentWeight + items[i].weight <= capacity) {
            currentWeight += items[i].weight;
            totalValue += items[i].value;
        } else {
            // Jika item hanya bisa diambil sebagian
            int remainingCapacity = capacity - currentWeight;
            totalValue += items[i].ratio * remainingCapacity;
            break; // Knapsack sudah penuh
        }
    }

    return totalValue;
}

int main() {
    int capacity = 50; // Kapasitas knapsack
    std::vector<Item> items = {
        {60, 10}, // Item 1: value=60, weight=10
        {100, 20}, // Item 2: value=100, weight=20
        {120, 30}  // Item 3: value=120, weight=30
    };

    double maxValue = fractionalKnapsack(capacity, items);
    std::cout << "Nilai maksimum yang bisa diambil: " << maxValue << std::endl;

    return 0;
}
```
**Kesimpulan**

Fractional Knapsack adalah salah satu variasi dari Knapsack Problem yang dapat diselesaikan secara efisien menggunakan algoritma greedy. Dalam versi ini, barang boleh diambil sebagian (fraksional), berbeda dengan 0/1 Knapsack yang hanya membolehkan pengambilan penuh atau tidak sama sekali. Dengan menghitung rasio nilai terhadap berat (value/weight) untuk setiap barang, lalu mengambil barang dengan rasio tertinggi hingga kapasitas tas penuh, kita bisa mendapatkan solusi optimal secara cepat dan sederhana. Pendekatan greedy ini bekerja efektif karena pilihan optimal lokal (berdasarkan rasio) juga mengarah pada solusi optimal global dalam kasus Fractional Knapsack.
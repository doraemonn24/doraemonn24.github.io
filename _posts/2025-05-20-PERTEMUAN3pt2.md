---
title: N-QUEENS PROBLEM
date: 2025-05-20
categories: [DESAIN ANALISIS ALGORITMA, BACKTRACKING]
tags: [daa, algorithm, backtracking]     # TAG names should always be lowercase
---


**Pengantar**

Presentasi ini akan membahas "N-Queens Problem", sebuah masalah klasik dalam ilmu komputer dan matematika kombinatorik. Kami akan mendalami definisi masalah, tujuannya, serta bagaimana masalah ini diselesaikan menggunakan algoritma *backtracking*. Kami juga akan menganalisis prinsip kerja *backtracking* dalam konteks N-Queens, melihat contoh penyelesaian 4-Queens, menganalisis kompleksitas waktu, dan meninjau implementasi kodenya.

**Anggota Kelompok**

Presentasi ini dibuat oleh Kelompok 4, yang terdiri dari anggota-anggota berikut:
* Aditya Hisbul Bahri (H071241069)
* Jonas Ba'ka (H071241031)
* Akhmad Hidayat (H071241003)
* As'sviekril Fikran Sarda (H071241083)
* M. Fadhil Mulyadi (H071241011)

**N-Queens Problem: Definisi Masalah**

Masalah N-Queens adalah permasalahan klasik yang melibatkan penempatan N buah ratu catur pada sebuah papan catur berukuran $N \times N$ sedemikian rupa sehingga tidak ada dua ratu yang saling menyerang. Dalam aturan catur, seorang ratu dapat bergerak secara horizontal (baris), vertikal (kolom), dan diagonal. Oleh karena itu, solusi dari masalah ini harus memastikan bahwa tidak ada dua ratu yang berada pada baris, kolom, atau diagonal yang sama. Contoh paling terkenal adalah masalah 8-Queens, yaitu menempatkan 8 ratu di papan $8 \times 8$.

Tujuan utama dari masalah N-Queens adalah:
1. Menemukan semua konfigurasi penempatan ratu yang memenuhi syarat tidak saling menyerang.
2. Mengembangkan algoritma efisien untuk menemukan solusi tersebut.

**N-Queens dan Algoritma Backtracking**

Algoritma *backtracking* adalah teknik umum untuk menyelesaikan masalah yang melibatkan pencarian solusi dari ruang keadaan yang besar. Konsepnya adalah membangun solusi secara bertahap. Jika pada suatu titik ditemukan bahwa solusi parsial tidak dapat diperluas menjadi solusi lengkap yang valid, algoritma akan "mundur" (backtrack) dan mencoba jalur lain.

**Prinsip Kerja Backtracking pada N-Queens:**
1. **Pendekatan Rekursif:** Masalah ini dipecah menjadi sub-masalah yang lebih kecil, yaitu menempatkan satu ratu per kolom.
2. **Pengecekan Keamanan:** Sebelum menempatkan ratu pada suatu posisi $(baris, kolom)$, algoritma memeriksa apakah posisi tersebut aman (tidak ada ratu lain yang menyerang pada baris, kolom, atau diagonal yang sama).
3. **Mencoba dan Mundur (Trial and Error):**
    * Jika posisi aman, ratu ditempatkan, dan algoritma melanjutkan secara rekursif untuk kolom berikutnya.
    * Jika rekursi tidak berhasil (tidak ditemukan solusi di kolom berikutnya dari posisi saat ini), ratu dihapus (backtrack), dan algoritma mencoba posisi lain di kolom saat ini.
4. **Basis Kasus:** Ketika semua N ratu berhasil ditempatkan (yaitu, berhasil menempatkan ratu di kolom terakhir), sebuah solusi valid ditemukan.

**Contoh Penyelesaian 4-Queens**

Untuk masalah 4-Queens, kita akan menempatkan 4 ratu di papan $4 \times 4$.

**Langkah-langkah Penempatan:**

* **Kolom 0 (Q1):**
    * Coba Q1 di (0,0). Aman. Lanjutkan ke Kolom 1.
* **Kolom 1 (Q2):**
    * Coba Q2 di (0,1), (1,1). Tidak aman.
    * Coba Q2 di (2,1). Aman. Lanjutkan ke Kolom 2.
* **Kolom 2 (Q3):**
    * Coba Q3 di (0,2), (1,2), (2,2), (3,2). Tidak aman.
    * **Backtrack ke Kolom 1.**
* **Kolom 1 (Q2, Lanjutan):**
    * Q2 di (2,1) tadi tidak berhasil. Coba Q2 di (3,1). Aman. Lanjutkan ke Kolom 2.
* **Kolom 2 (Q3):**
    * Coba Q3 di (0,2), (1,2). Tidak aman.
    * Coba Q3 di (2,2). Aman. Lanjutkan ke Kolom 3.
* **Kolom 3 (Q4):**
    * Coba Q4 di (0,3), (1,3), (2,3), (3,3). Tidak aman.
    * **Backtrack ke Kolom 2.**
* **Kolom 2 (Q3, Lanjutan):**
    * Q3 di (2,2) tidak berhasil. Coba Q3 di (3,2). Aman. Lanjutkan ke Kolom 3.
* **Kolom 3 (Q4):**
    * Coba Q4 di (0,3). Aman.
        * **Solusi Pertama Ditemukan:** Q1:(0,0), Q2:(3,1), Q3:(2,2), Q4:(0,3) - *ini contoh saja, biasanya bukan ini solusi pertama yang ditemukan, tapi ilustrasi proses*.

Proses ini terus berlanjut hingga semua solusi ditemukan atau semua kemungkinan telah dicoba.

**Analisis Kompleksitas Waktu**

* **Pencarian ruang solusi:** Secara teoritis, ada $N^N$ kemungkinan cara menempatkan N ratu di papan $N \times N$. Namun, karena adanya batasan (tidak saling menyerang), banyak jalur yang langsung dipangkas oleh backtracking.
* **Kompleksitas yang lebih realistis:** Meskipun sulit untuk menentukan kompleksitas waktu yang tepat untuk N-Queens karena sifatnya yang memangkas pohon pencarian, batas atasnya adalah $O(N!)$ karena kita menempatkan satu ratu per baris, dan ada $N$ pilihan untuk baris pertama, $N-1$ untuk baris kedua, dan seterusnya. Ini adalah kompleksitas faktorial yang sangat besar.
* **Faktor K:** Untuk $N$ yang lebih besar, algoritma ini menjadi sangat lambat. Kompleksitasnya mendekati $O(k^N)$, di mana $k$ adalah konstanta antara 2 dan 3.

**Implementasi C++**

Berikut adalah implementasi C++ untuk N-Queens Problem menggunakan algoritma *backtracking*. Kode ini akan menemukan dan mencetak semua solusi yang valid untuk N ratu.

```cpp
#include <iostream>
#include <vector>

// Ukuran papan catur
int N;

// Papan catur: board[row][col] = 1 jika ada ratu, 0 jika kosong
std::vector<std::vector<int>> board;

// Fungsi untuk mencetak solusi papan
void printSolution() {
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < N; j++) {
            std::cout << board[i][j] << " ";
        }
        std::cout << std::endl;
    }
    std::cout << std::endl;
}

// Fungsi untuk memeriksa apakah aman menempatkan ratu di board[row][col]
bool isSafe(int row, int col) {
    int i, j;

    // Periksa baris ini di sisi kiri
    for (i = 0; i < col; i++) {
        if (board[row][i]) {
            return false;
        }
    }

    // Periksa diagonal atas di sisi kiri
    for (i = row, j = col; i >= 0 && j >= 0; i--, j--) {
        if (board[i][j]) {
            return false;
        }
    }

    // Periksa diagonal bawah di sisi kiri
    for (i = row, j = col; i < N && j >= 0; i++, j--) {
        if (board[i][j]) {
            return false;
        }
    }

    return true;
}

// Fungsi rekursif untuk menyelesaikan N-Queens dengan backtracking
// 'col' adalah kolom yang sedang dipertimbangkan untuk menempatkan ratu
void solveNQueensUtil(int col) {
    // Basis kasus: Jika semua ratu sudah ditempatkan (sampai kolom N-1)
    if (col >= N) {
        printSolution();
        return;
    }

    // Coba tempatkan ratu di setiap baris dalam kolom saat ini
    for (int i = 0; i < N; i++) {
        // Periksa apakah ratu bisa ditempatkan di board[i][col]
        if (isSafe(i, col)) {
            // Tempatkan ratu
            board[i][col] = 1;

            // Rekursi untuk kolom berikutnya
            solveNQueensUtil(col + 1);

            // Backtrack: Jika penempatan ini tidak mengarah ke solusi,
            // hapus ratu dari board[i][col] (mundur)
            board[i][col] = 0; 
        }
    }
}

// Fungsi utama untuk menyelesaikan N-Queens
void solveNQueens() {
    // Inisialisasi papan kosong dengan ukuran N x N
    board = std::vector<std::vector<int>>(N, std::vector<int>(N, 0));

    // Mulai pencarian solusi dari kolom 0
    solveNQueensUtil(0);
}

int main() {
    std::cout << "Masukkan ukuran papan N: ";
    std::cin >> N;

    if (N <= 0) {
        std::cout << "Ukuran papan harus positif." << std::endl;
        return 1;
    }

    std::cout << "Solusi untuk " << N << "-Queens Problem:\n";
    solveNQueens();

    return 0;
}
```

**Penjelasan Kode:**
* **Global Variable `N` dan `board`**: `N` menyimpan ukuran papan, dan `board` adalah representasi papan catur menggunakan `std::vector<std::vector<int>>`. `1` berarti ada ratu, `0` berarti kosong.
* **`printSolution()`**: Fungsi ini mencetak konfigurasi papan saat solusi ditemukan.
* **`isSafe(int row, int col)`**: Fungsi kunci dalam backtracking. Ini memeriksa tiga arah (horizontal kiri, diagonal atas kiri, diagonal bawah kiri) dari posisi yang diberikan `(row, col)` untuk memastikan tidak ada ratu yang menyerang. Karena kita mengisi kolom per kolom dari kiri ke kanan, kita hanya perlu memeriksa sisi kiri.
* **`solveNQueensUtil(int col)`**: Ini adalah fungsi rekursif inti.
    * **Basis Kasus**: Jika `col >= N`, berarti kita sudah berhasil menempatkan ratu di semua kolom, jadi solusi ditemukan dan dicetak.
    * **Rekursi**: Untuk setiap baris `i` di kolom `col` saat ini, ia memeriksa apakah `(i, col)` aman (`isSafe`).
        * Jika aman, ratu ditempatkan (`board[i][col] = 1`).
        * Kemudian, fungsi memanggil dirinya sendiri untuk kolom berikutnya (`solveNQueensUtil(col + 1)`).
        * **Backtrack**: Setelah panggilan rekursif kembali (baik itu menemukan solusi atau menemui jalan buntu), ratu dihapus (`board[i][col] = 0`). Ini penting untuk memungkinkan jalur pencarian alternatif.
* **`solveNQueens()`**: Fungsi pembungkus yang menginisialisasi papan kosong dan memulai proses rekursif dari kolom 0.
* **`main()`**: Meminta input `N` dari pengguna dan memanggil `solveNQueens()`.

**Kesimpulan**

N-Queens Problem adalah tantangan klasik yang menunjukkan kekuatan algoritma *backtracking*. Dengan pendekatan ini, kita secara sistematis mencari solusi dengan membangunnya langkah demi langkah dan "mundur" ketika jalur yang diambil tidak lagi menjanjikan. Meskipun kompleksitas waktunya bisa sangat tinggi ($O(N!)$ secara umum), *backtracking* secara efektif memangkas ruang pencarian yang sangat besar, menjadikannya metode yang praktis untuk menemukan semua konfigurasi valid penempatan ratu di papan catur.
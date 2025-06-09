---
title: SUBSET SUM PROBLEM
date: 2025-05-20
categories: [DESAIN ANALISIS ALGORITMA, BACKTRACKING]
tags: [daa, algorithm, backtracking]     # TAG names should always be lowercase
---


**Pengantar**

Presentasi ini akan membahas "Subset Sum Problem" (SSP), sebuah masalah klasik dalam ilmu komputer yang termasuk dalam kategori NP-Complete. Kami akan mendalami definisi masalah, berbagai variasinya, serta strategi penyelesaian menggunakan pendekatan rekursif dan pemrograman dinamis. Selain itu, kami juga akan menganalisis kompleksitas, melihat beberapa aplikasi dunia nyata, dan meninjau implementasi kodenya.

**Anggota Kelompok**

Presentasi ini dibuat oleh Kelompok 5 DAA A, yang terdiri dari anggota-anggota berikut:
* Ishmah Nurwasilah (H071241019)
* Trivania Buli Karoma (H071241039)
* Diani Annisah (H071241043)
* Diesty Mendila Tappo (H071241077)
* Muhammad Fathir Syabhan (H071241091)

**Konsep Subset Sum Problem**

**Apa itu Subset Sum Problem (SSP)?**
Subset Sum Problem adalah masalah klasik dalam ilmu komputer yang termasuk dalam kategori NP-Complete. Diberikan sebuah himpunan bilangan bulat dan sebuah nilai target, tugasnya adalah menentukan apakah ada subset dari himpunan tersebut yang jumlah elemennya sama dengan nilai target.

**Definisi Formal:**
* Input: Himpunan bilangan bulat $S = \{s_1, s_2, \ldots, s_n\}$ dan nilai target $T$.
* Output: True jika terdapat subset $S' \subseteq S$ sehingga $\sum_{x \in S'} x = T$. False jika tidak ada.

**Contoh:**
* Input: `arr = [1, 2, 3]`, `target_sum = 3`
* Output: `True`
* Penjelasan: Terdapat subset `{1, 2}` yang jumlahnya 3.

**Variasi Subset Sum Problem**

Subset Sum Problem memiliki beberapa variasi, yang masing-masing cocok untuk skenario yang berbeda:
1.  **Bounded Subset Sum:** Setiap elemen dalam himpunan hanya dapat digunakan paling banyak sekali. Ini adalah variasi paling umum.
2.  **Unbounded Subset Sum:** Setiap elemen dalam himpunan dapat digunakan berkali-kali. Ini mirip dengan masalah koin atau perubahan.
3.  **Exact K-Elements Subset Sum:** Membutuhkan subset yang jumlahnya sama dengan target, dan subset tersebut harus memiliki tepat $K$ elemen.
4.  **Partition Problem:** Ini adalah kasus khusus SSP di mana target sum adalah setengah dari total jumlah semua elemen dalam himpunan. Tujuannya adalah membagi himpunan menjadi dua subset dengan jumlah yang sama.
5.  **Multi-Target Subset Sum:** Mencari subset yang jumlahnya sesuai dengan salah satu dari beberapa nilai target.
6.  **Approximate Subset Sum:** Digunakan ketika menemukan solusi eksak terlalu mahal secara komputasi. Algoritma ini mencari solusi yang mendekati nilai target.

**Pendekatan untuk Menyelesaikan Subset Sum Problem**

SSP dapat diselesaikan dengan berbagai pendekatan:

1.  **Pendekatan Rekursif Sederhana:**
    * **Ide Dasar:** Untuk setiap elemen, ada dua pilihan: memasukkannya ke dalam subset atau tidak. Algoritma secara rekursif memeriksa semua kemungkinan kombinasi.
    * **Base Case:**
        * Jika `target_sum` menjadi 0, berarti kita menemukan subset yang jumlahnya target.
        * Jika kita mencapai akhir himpunan (`n == 0`) dan `target_sum` masih bukan 0, berarti tidak ada solusi.
    * **Rekurensi:**
        * Jika elemen saat ini (`arr[n-1]`) lebih besar dari `target_sum`, maka elemen ini tidak bisa dimasukkan.
        * Jika tidak, kita punya dua opsi:
            * Sertakan elemen: `subsetSum(arr, n-1, target_sum - arr[n-1])`
            * Jangan sertakan elemen: `subsetSum(arr, n-1, target_sum)`

    * **Kompleksitas Waktu:** $O(2^n)$, karena setiap elemen memiliki dua kemungkinan (diambil atau tidak). Ini menjadi sangat tidak efisien untuk `n` yang besar.
    * **Kompleksitas Ruang:** $O(n)$ untuk kedalaman tumpukan rekursi.

2.  **Pendekatan Pemrograman Dinamis (Dynamic Programming - DP):**
    * **Ide Dasar:** Membangun tabel (biasanya 2D) untuk menyimpan hasil sub-masalah yang tumpang tindih, sehingga tidak perlu menghitung ulang.
    * **Tabel DP:** `dp[i][j]` adalah `true` jika jumlah `j` dapat dibentuk dari `i` elemen pertama, dan `false` jika tidak.
    * **Inisialisasi:** `dp[0][0] = true` (jumlah 0 dapat dibentuk dengan 0 elemen).
    * **Pengisian Tabel:**
        `dp[i][j] = dp[i-1][j]` (tidak termasuk `arr[i-1]`)
        JIKA `j >= arr[i-1]`, MAKA `dp[i][j] = dp[i-1][j] OR dp[i-1][j - arr[i-1]]` (termasuk `arr[i-1]`)
    * **Kompleksitas Waktu:** $O(n \cdot target\_sum)$, karena kita mengisi tabel $n \times target\_sum$.
    * **Kompleksitas Ruang:** $O(n \cdot target\_sum)$ untuk tabel DP.

**Implementasi C++ (Dynamic Programming)**

Berikut adalah contoh implementasi C++ untuk Subset Sum Problem menggunakan pendekatan pemrograman dinamis.

```cpp
#include <iostream>
#include <vector>
#include <numeric> // Untuk std::accumulate

// Fungsi untuk menyelesaikan Subset Sum Problem menggunakan Dynamic Programming
bool isSubsetSum(const std::vector<int>& arr, int n, int sum) {
    // Buat tabel boolean DP.
    // dp[i][j] akan bernilai true jika jumlah j dapat dibentuk dari i elemen pertama.
    std::vector<std::vector<bool>> dp(n + 1, std::vector<bool>(sum + 1));

    // Inisialisasi baris pertama:
    // dp[0][0] adalah true karena jumlah 0 dapat dibentuk dengan 0 elemen.
    dp[0][0] = true;

    // Inisialisasi kolom pertama:
    // Untuk j > 0, dp[0][j] adalah false karena jumlah positif tidak dapat dibentuk dengan 0 elemen.
    for (int j = 1; j <= sum; j++) {
        dp[0][j] = false;
    }

    // Isi tabel dp secara bottom-up
    for (int i = 1; i <= n; i++) { // Iterasi melalui setiap item
        for (int j = 0; j <= sum; j++) { // Iterasi melalui setiap kemungkinan jumlah
            // Kasus 1: Jangan sertakan item saat ini (arr[i-1])
            // Jika jumlah j sudah bisa dibentuk tanpa item ini, maka dp[i][j] adalah true
            dp[i][j] = dp[i-1][j];

            // Kasus 2: Sertakan item saat ini (arr[i-1])
            // Jika item saat ini tidak melebihi jumlah j dan
            // jika (jumlah j - berat item saat ini) bisa dibentuk tanpa item ini,
            // maka dp[i][j] juga true
            if (j >= arr[i-1]) {
                dp[i][j] = dp[i][j] || dp[i-1][j - arr[i-1]];
            }
        }
    }

    // Hasil akhir berada di dp[n][sum]
    return dp[n][sum];
}

int main() {
    std::vector<int> arr = {3, 34, 4, 12, 5, 2};
    int sum = 9;
    int n = arr.size();

    if (isSubsetSum(arr, n, sum)) {
        std::cout << "Ditemukan subset dengan jumlah " << sum << std::endl;
    } else {
        std::cout << "Tidak ditemukan subset dengan jumlah " << sum << std::endl;
    }

    std::vector<int> arr2 = {1, 2, 3};
    int sum2 = 3;
    int n2 = arr2.size();

    if (isSubsetSum(arr2, n2, sum2)) {
        std::cout << "Ditemukan subset dengan jumlah " << sum2 << std::endl;
    } else {
        std::cout << "Tidak ditemukan subset dengan jumlah " << sum2 << std::endl;
    }

    std::vector<int> arr3 = {1, 2, 3, 5};
    int sum3 = 11;
    int n3 = arr3.size();

    if (isSubsetSum(arr3, n3, sum3)) {
        std::cout << "Ditemukan subset dengan jumlah " << sum3 << std::endl;
    } else {
        std::cout << "Tidak ditemukan subset dengan jumlah " << sum3 << std::endl;
    }

    return 0;
}
```

**Penjelasan Kode:**
1.  **`isSubsetSum(const std::vector<int>& arr, int n, int sum)`**: Fungsi ini mengambil himpunan bilangan bulat (`arr`), ukurannya (`n`), dan nilai target (`sum`).
2.  **Tabel DP (`dp`)**: Sebuah `std::vector<std::vector<bool>>` berukuran `(n+1) x (sum+1)` digunakan. `dp[i][j]` akan `true` jika jumlah `j` dapat dibentuk menggunakan `i` elemen pertama dari `arr`, dan `false` jika tidak.
3.  **Inisialisasi**:
    * `dp[0][0] = true`: Jumlah 0 selalu bisa dibentuk dengan tidak mengambil elemen apa pun.
    * `dp[0][j] = false` untuk `j > 0`: Jumlah positif tidak bisa dibentuk dengan 0 elemen.
4.  **Pengisian Tabel Iteratif**:
    * Loop luar (`for (int i = 1; i <= n; i++)`) merepresentasikan jumlah elemen yang dipertimbangkan.
    * Loop dalam (`for (int j = 0; j <= sum; j++)`) merepresentasikan nilai jumlah yang ingin dibentuk.
    * `dp[i][j] = dp[i-1][j]`: Defaultnya, jika `j` bisa dibentuk dengan `i-1` elemen, maka `j` juga bisa dibentuk dengan `i` elemen (dengan tidak mengambil elemen ke-`i`).
    * `if (j >= arr[i-1]) { dp[i][j] = dp[i][j] || dp[i-1][j - arr[i-1]]; }`: Jika elemen ke-`i` (`arr[i-1]`) kurang dari atau sama dengan `j`, kita juga bisa mencoba mengambil elemen ini. Jika `j - arr[i-1]` bisa dibentuk dengan `i-1` elemen, maka `j` bisa dibentuk dengan `i` elemen (dengan mengambil elemen ke-`i`). Operator `||` (OR) digunakan karena kita perlu `true` jika salah satu dari kedua kasus tersebut menghasilkan `true`.
5.  **Hasil Akhir**: Nilai `dp[n][sum]` akan menjadi `true` jika ada subset dengan jumlah target, dan `false` jika tidak.

**Aplikasi Dunia Nyata**

Subset Sum Problem memiliki banyak aplikasi praktis di berbagai bidang:
1.  **Kriptografi dan Keamanan Data:** Dasar dari beberapa algoritma kriptografi yang mengandalkan kesulitan SSP untuk keamanan.
2.  **Keuangan dan Pengelolaan Anggaran:** Menentukan apakah sejumlah item (investasi, pengeluaran) dapat mencapai anggaran atau target tertentu.
3.  **Genetika dan Bioinformatika:** Digunakan untuk menganalisis kombinasi gen atau fragmen DNA dengan total ekspresi atau panjang tertentu.
4.  **Keuangan dan Investasi:** Membantu menentukan apakah target investasi dapat dicapai dengan memilih kombinasi aset yang tepat.
5.  **Perancangan Permainan dan Teka-Teki:** Muncul dalam permainan atau teka-teki yang melibatkan pencarian kombinasi angka sesuai skor target.

**Kesimpulan**

Subset Sum Problem (SSP) adalah masalah dalam ilmu komputer yang bertujuan untuk menentukan apakah terdapat subset dari sekumpulan bilangan bulat yang jumlahnya sama dengan nilai target tertentu. Masalah ini tergolong dalam kategori NP-Complete dan memiliki berbagai variasi, seperti bounded, unbounded, exact k elements, partition, multi-target, hingga approximate subset sum, yang masing-masing memiliki aplikasi dan batasan berbeda.

Untuk menyelesaikan SSP, digunakan pendekatan rekursif yang sederhana namun kurang efisien, serta dynamic programming yang lebih optimal baik dari segi waktu maupun ruang. Subset Sum memiliki aplikasi nyata dalam bidang kriptografi, keuangan, pengelolaan sumber daya, hingga kecerdasan buatan, menjadikannya masalah penting yang tidak hanya teoritis, tetapi juga relevan dalam dunia praktis.


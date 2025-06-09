---
title: DEPTH FIRST SEARCH (DFS)
date: 2025-05-27
categories: [DESAIN ANALISIS ALGORITMA, DFS, BACKTRACKING]
tags: [daa, algorithm, dfs, backtracking]     # TAG names should always be lowercase
---



**Pengantar**

Presentasi ini akan membahas "Depth-First Search" (DFS), sebuah algoritma fundamental dalam ilmu komputer untuk menelusuri atau mencari di dalam struktur data graf atau pohon. Berbeda dengan BFS yang menjelajah secara meluas, DFS menjelajah secara mendalam. Kami akan mendalami pengertian dan konsep dasarnya, termasuk bagaimana ia memanfaatkan struktur data tumpukan (stack) atau rekursi. Kemudian, kita akan melihat prinsip utama cara kerjanya, menganalisis kompleksitas waktu dan ruang, mengidentifikasi kelebihan dan kekurangannya, melihat beberapa aplikasi dunia nyata, serta meninjau implementasi kodenya.

**Anggota Kelompok**

Presentasi ini dibuat oleh Kelompok 8, yang terdiri dari anggota-anggota berikut:
* BISMILLAH GHANIYYU PUTRA DARMIN (H071241057)
* MAYNOVA CHRISTIN GABRYELA SIMAMORA (H071241001)
* NABILA SALSABILA (H071241023)
* MOCH. ICHWANUL MUSLIMIN MAYANG (H071241027)

**Depth-First Search (DFS)**

Depth-First Search (DFS) adalah algoritma pencarian atau penelusuran pada struktur data graf atau pohon yang bekerja dengan menjelajahi satu cabang sedalam mungkin sebelum mundur (*backtrack*) dan melanjutkan ke cabang berikutnya.

**Prinsip Utama**

DFS beroperasi berdasarkan prinsip tumpukan (Stack), yang bekerja dengan metode **Last-In, First-Out (LIFO)**.
1.  **Masukkan Simpul Akar ke dalam Stack:** Proses dimulai dengan menempatkan simpul awal (atau simpul akar, jika ini pohon) ke dalam tumpukan.
2.  **Ambil dan Kunjungi:** Selama tumpukan tidak kosong:
    * Ambil simpul teratas dari tumpukan.
    * Jika simpul tersebut belum dikunjungi, tandai sebagai dikunjungi dan proses (misalnya, cetak).
    * Kemudian, masukkan semua tetangga (anak) yang belum dikunjungi dari simpul tersebut ke dalam tumpukan.
3.  **Kembali (Backtrack):** Ketika tidak ada lagi tetangga yang belum dikunjungi dari simpul saat ini, algoritma secara implisit "mundur" ke simpul yang ditambahkan terakhir ke tumpukan (karena LIFO), yang memungkinkan eksplorasi cabang lain.

**Mekanisme Kerja**

DFS memiliki dua mekanisme kerja utama:
1.  **Iteratif (menggunakan Stack eksplisit):**
    * Inisialisasi stack kosong dan set `visited` untuk melacak simpul yang sudah dikunjungi.
    * Dorong simpul awal ke stack dan tandai sebagai `visited`.
    * Selama stack tidak kosong:
        * Pop simpul dari stack.
        * Proses simpul tersebut.
        * Untuk setiap tetangga simpul yang belum dikunjungi, dorong ke stack dan tandai sebagai `visited`.
2.  **Rekursif (menggunakan Stack implisit):**
    * Ini adalah cara yang paling umum dan seringkali lebih elegan untuk mengimplementasikan DFS. Stack di sini adalah *call stack* dari fungsi rekursif itu sendiri.
    * Fungsi rekursif akan menerima simpul saat ini dan graf.
    * Tandai simpul saat ini sebagai dikunjungi dan proses.
    * Untuk setiap tetangga simpul yang belum dikunjungi, panggil fungsi rekursif pada tetangga tersebut.

**Kompleksitas Waktu dan Ruang**

* **Kompleksitas Waktu:** $O(V+E)$, di mana $V$ adalah jumlah simpul (vertices) dan $E$ adalah jumlah sisi (edges). Ini karena setiap simpul dan setiap sisi di graf akan dikunjungi tepat sekali.
* **Kompleksitas Ruang:** $O(V)$, untuk menyimpan status `visited` dari simpul dan untuk *call stack* rekursif (dalam kasus terburuk, stack bisa mencapai kedalaman $V$, seperti pada graf linier atau pohon yang sangat dalam).

**Kelebihan dan Kekurangan**

* **Kelebihan:**
    * **Hemat Memori:** Untuk graf yang sangat lebar (banyak simpul di satu level), DFS seringkali lebih hemat memori dibandingkan BFS karena hanya perlu menyimpan jalur saat ini di stack.
    * **Deteksi Siklus:** Dapat dengan mudah mendeteksi siklus dalam graf.
    * **Pencarian Jalur:** Baik untuk menemukan jalur (bukan tentu jalur terpendek) dan eksplorasi yang mendalam.
* **Kekurangan:**
    * **Tidak Optimal untuk Jalur Terpendek:** DFS tidak menjamin ditemukannya jalur terpendek dalam graf tak berbobot karena ia akan terus menjelajah ke bawah sedalam mungkin, bahkan jika ada jalur yang lebih pendek di level yang lebih tinggi.
    * **Masalah Loop Tak Terbatas:** Pada graf dengan siklus, jika tidak ada mekanisme `visited` yang tepat, DFS bisa terjebak dalam *infinite loop*.
    * **Jalur Suboptimal:** Dapat menemukan jalur yang sangat panjang sebelum menemukan jalur yang diinginkan atau solusi.

**Aplikasi Dunia Nyata**

1.  **Pencarian Jalur (Pathfinding):**
    * Digunakan dalam algoritma pencarian jalur seperti menemukan jalan keluar dari labirin (Rat in a Maze) atau memecahkan teka-teki tertentu.
2.  **Deteksi Siklus dalam Graf:**
    * Sangat efektif untuk mengidentifikasi apakah suatu graf memiliki siklus (misalnya, dalam deteksi *deadlock* pada sistem operasi).
3.  **Pencarian Komponen Terhubung:**
    * Menemukan semua simpul yang terhubung dalam graf yang tidak terhubung penuh.
4.  **Topological Sorting:**
    * Mengurutkan simpul-simpul dalam graf terarah asiklik (DAG) sedemikian rupa sehingga untuk setiap sisi dari `u` ke `v`, `u` selalu muncul sebelum `v` dalam urutan.
5.  **Pencarian di Pohon (Tree Traversal):**
    * Pre-order, In-order, dan Post-order traversals adalah bentuk-bentuk DFS yang digunakan untuk memproses simpul-simpul pohon.

**Implementasi C++ (Rekursif)**

Berikut adalah contoh implementasi C++ sederhana untuk DFS pada graf menggunakan pendekatan rekursif. Graf direpresentasikan menggunakan *adjacency list*.

```cpp
#include <iostream>
#include <vector>
#include <map> // Menggunakan map untuk adjacency list agar lebih fleksibel dengan node ID

// Fungsi rekursif untuk melakukan Depth-First Search
// u: Simpul saat ini yang sedang dikunjungi
// adj: Adjacency list yang merepresentasikan graf
// visited: Vektor boolean untuk melacak simpul yang sudah dikunjungi
void DFS(int u, const std::map<int, std::vector<int>>& adj, std::map<int, bool>& visited) {
    // Tandai simpul saat ini sebagai sudah dikunjungi
    visited[u] = true;
    // Cetak simpul yang dikunjungi
    std::cout << u << " ";

    // Jelajahi semua tetangga dari simpul saat ini
    // Pastikan simpul 'u' ada di adjacency list
    if (adj.count(u)) {
        for (int v : adj.at(u)) {
            // Jika tetangga belum dikunjungi, panggil DFS secara rekursif
            if (!visited[v]) {
                DFS(v, adj, visited);
            }
        }
    }
}

int main() {
    // Jumlah simpul
    int n = 6;

    // Representasi graf menggunakan adjacency list (map)
    // Map ini memungkinkan kita menggunakan ID simpul apa pun (misalnya, 0, 1, 2, ... atau 10, 20, 30, ...)
    std::map<int, std::vector<int>> graph;

    // Tambahkan sisi-sisi (edges) graf
    graph[0].push_back(1); // 0 terhubung ke 1
    graph[0].push_back(2); // 0 terhubung ke 2

    graph[1].push_back(0); // 1 terhubung ke 0
    graph[1].push_back(3); // 1 terhubung ke 3
    graph[1].push_back(4); // 1 terhubung ke 4

    graph[2].push_back(0); // 2 terhubung ke 0
    graph[2].push_back(5); // 2 terhubung ke 5

    graph[3].push_back(1); // 3 terhubung ke 1
    graph[4].push_back(1); // 4 terhubung ke 1
    graph[5].push_back(2); // 5 terhubung ke 2

    // Map untuk melacak simpul yang sudah dikunjungi
    // Inisialisasi semua simpul yang ada di graf menjadi 'false'
    std::map<int, bool> visited;
    for (auto const& [node, neighbors] : graph) {
        visited[node] = false;
        // Pastikan juga tetangga diinisialisasi
        for (int neighbor : neighbors) {
            if (visited.find(neighbor) == visited.end()) {
                visited[neighbor] = false;
            }
        }
    }

    std::cout << "DFS traversal dimulai dari simpul 0: ";
    DFS(0, graph, visited);
    std::cout << std::endl;

    // Menginisialisasi ulang visited untuk traversal baru
    // Reset semua node yang sebelumnya dikunjungi menjadi false
    for (auto const& [node, val] : visited) {
        visited[node] = false;
    }

    std::cout << "DFS traversal dimulai dari simpul 2: ";
    DFS(2, graph, visited);
    std::cout << std::endl;

    return 0;
}
```

**Penjelasan Kode:**

1.  **`std::map<int, std::vector<int>> graph`**: Ini adalah representasi *adjacency list* dari graf. Kunci `int` adalah simpul, dan `std::vector<int>` adalah daftar tetangga dari simpul tersebut. Penggunaan `std::map` memungkinkan simpul dengan ID non-sequential dan lebih fleksibel.
2.  **`std::map<int, bool> visited`**: Sebuah peta untuk melacak apakah setiap simpul sudah dikunjungi atau belum dalam traversal saat ini. Ini penting untuk mencegah pemrosesan berulang dan *infinite loop* pada graf yang memiliki siklus. Inisialisasi awal dilakukan untuk semua simpul yang ada dalam `graph` map.
3.  **`DFS(int u, const std::map<int, std::vector<int>>& adj, std::map<int, bool>& visited)`**: Ini adalah fungsi rekursif inti yang mengimplementasikan DFS.
    * **Tandai dan Proses**: Simpul `u` saat ini ditandai sebagai `visited[u] = true` dan kemudian dicetak.
    * **Eksplorasi Tetangga**: Kode kemudian mengiterasi semua tetangga `v` dari `u`.
    * **Panggilan Rekursif**: Jika tetangga `v` belum dikunjungi (`!visited[v]`), fungsi `DFS` akan dipanggil secara rekursif dengan `v` sebagai simpul saat ini. Ini yang mendorong eksplorasi ke "kedalaman".
4.  **`main()`**: Mendefinisikan contoh graf dan memanggil fungsi `DFS` dua kali dengan simpul awal yang berbeda untuk mendemonstrasikan perilakunya. Setiap kali `DFS` dipanggil ulang dari simpul baru, `visited` perlu direset jika kita ingin melihat traversal dari simpul yang berbeda di graf yang sama tanpa pengaruh dari traversal sebelumnya.

**Kesimpulan**

Depth-First Search (DFS) adalah algoritma penelusuran pada struktur data graf atau pohon yang menjelajahi simpul sedalam mungkin sebelum kembali (*backtracking*) dan melanjutkan ke simpul lainnya. Proses penelusuran ini dilakukan secara rekursif atau menggunakan tumpukan (stack) eksplisit. DFS efektif untuk deteksi siklus, pencarian komponen terhubung, dan *topological sorting*. Meskipun tidak menjamin jalur terpendek, keunggulannya dalam eksplorasi mendalam dan efisiensi memori membuatnya menjadi alat yang sangat berharga dalam berbagai aplikasi ilmu komputer.
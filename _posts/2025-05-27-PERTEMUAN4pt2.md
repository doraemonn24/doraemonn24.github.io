---
title: BREADTH-FIRST SEARCH (BFS)
date: 2025-05-27
categories: [DESAIN ANALISIS ALGORITMA, BFS, BACKTRACKING]
tags: [daa, algorithm, bfs, backtracking]     # TAG names should always be lowercase
---


**Pengantar**

Presentasi ini akan membahas "Breadth-First Search" (BFS), sebuah algoritma fundamental dalam ilmu komputer untuk menelusuri atau mencari di dalam struktur data pohon atau graf. Kami akan mendalami pengertian dan konsep dasarnya, termasuk bagaimana ia memanfaatkan struktur data antrean. Kemudian, kita akan melihat langkah-langkah detail cara kerjanya, menganalisis kompleksitas waktu dan ruang, mengidentifikasi kelebihan dan kekurangannya, melihat beberapa aplikasi dunia nyata, serta meninjau implementasi kodenya.

**Anggota Kelompok**

Presentasi ini dibuat oleh Kelompok 7, yang terdiri dari anggota-anggota berikut:
* Muh. Hanif Durmahdin (H071241033)
* Kevin Anugrah Somakila' (H071241005)
* Moch. Syech Yusuf. M (H071241093)
* Raihan Ramadhan (H071241021)

**Pengertian Breadth-First Search (BFS)**

Breadth-First Search (BFS) adalah metode untuk menjelajahi graf atau pohon dengan menelusuri simpul-simpul berdasarkan jaraknya dari titik awal. Secara sederhana, BFS akan mengeksplorasi semua simpul yang paling dekat terlebih dahulu, baru kemudian beralih ke simpul yang lebih jauh. Jadi, pendekatannya menyebar ke seluruh arah secara merata dari pusat. Sebagai ilustrasi, bayangkan kita sedang mencari ruang kelas di sebuah gedung kampus berlantai 3. Kita pasti akan memeriksa seluruh ruangan dari lantai pertama sebelum lanjut ke lantai atas. Itulah cara kerja BFS: menjelajah secara mendatar. BFS banyak digunakan dalam berbagai aplikasi, mulai dari pencarian rute tercepat dalam game, penelusuran jaringan sosial, hingga pencarian jalur optimal dalam sistem navigasi dan peta digital.

**Konsep Dasar BFS**

1.  **Penggunaan Queue (Antrean):** BFS menggunakan struktur data *queue* (antrean). Simpul yang baru ditemukan (dan belum dikunjungi) ditambahkan ke bagian belakang antrean, dan simpul yang akan diproses selanjutnya diambil dari bagian depan antrean. Ini memastikan simpul-simpul pada "level" yang sama (jarak yang sama dari simpul awal) diproses terlebih dahulu.
2.  **Penjelajahan Berjenjang:** Algoritma ini menjelajahi graf atau pohon lapis demi lapis atau level demi level. Dimulai dari simpul awal, ia mengunjungi semua tetangga langsung, lalu semua tetangga dari tetangga tersebut, dan seterusnya.
3.  **Catatan Kunjungan:** BFS menggunakan sebuah mekanisme (biasanya array boolean atau set) untuk melacak simpul mana saja yang sudah dikunjungi. Ini penting untuk mencegah pemrosesan simpul yang sama berulang kali dan untuk menghindari *infinite loop* pada graf yang memiliki siklus.
4.  **Jalur Terpendek:** BFS menjamin ditemukannya jalur terpendek (dalam jumlah *edge*) antara simpul awal dan simpul lainnya pada graf tak berbobot (atau graf dengan bobot *edge* yang seragam).

**Cara Kerja BFS**

Berikut adalah langkah-langkah bagaimana algoritma BFS bekerja:
1.  **Mulai:** Pilih simpul awal (start node) dan masukkan ke dalam antrean. Tandai simpul awal tersebut sebagai telah dikunjungi.
2.  **Loop Utama:** Selama antrean tidak kosong, ulangi langkah-langkah berikut:
    a.  **Dequeue:** Ambil simpul pertama dari antrean (dequeue).
    b.  **Proses/Kunjungi:** Lakukan proses yang diperlukan pada simpul tersebut (misalnya, mencetaknya).
    c.  **Temukan Tetangga:** Periksa semua tetangga dari simpul yang baru saja diproses.
    d.  **Enqueue Tetangga:** Untuk setiap tetangga yang belum dikunjungi:
        * Tandai tetangga tersebut sebagai telah dikunjungi.
        * Masukkan tetangga tersebut ke dalam antrean (enqueue).
3.  **Selesai:** Ketika antrean kosong, semua simpul yang dapat dijangkau dari simpul awal telah dikunjungi.

**Kompleksitas BFS**

* **Kompleksitas Waktu ($O(V+E)$):**
    * $V$ adalah jumlah simpul (vertices).
    * $E$ adalah jumlah sisi (edges).
    * Setiap simpul dan setiap sisi di graf akan dikunjungi paling banyak sekali.
* **Kompleksitas Ruang ($O(V)$):**
    * Dalam kasus terburuk, antrean mungkin menyimpan semua simpul di satu level sebelum beralih ke level berikutnya. Pada graf yang sangat padat, ini bisa berarti menyimpan sebagian besar simpul.
    * Ruang tambahan juga dibutuhkan untuk melacak simpul yang sudah dikunjungi.

**Kelebihan dan Kekurangan**

* **Kelebihan:**
    * Menjamin ditemukannya solusi yang paling baik (komplit dan optimal) dalam mencari jalur terpendek pada graf tak berbobot.
    * Sederhana dan mudah diimplementasikan.
* **Kekurangan:**
    * Membutuhkan memori yang cukup banyak, terutama untuk graf yang lebar (banyak simpul di satu level).
    * Bisa membutuhkan waktu yang cukup banyak untuk graf yang sangat besar, karena harus menjelajahi semua simpul yang dapat dijangkau di setiap level.

**Aplikasi Dunia Nyata BFS**

1.  **Pencarian Jalur Terpendek:**
    * Digunakan dalam algoritma *pathfinding* pada *game* untuk menemukan jalur terpendek antara dua titik.
    * Aplikasi seperti Google Maps, Grab, atau Gojek menggunakan BFS (atau variannya seperti Dijkstra yang merupakan perluasan BFS) untuk menemukan rute terpendek, terutama jika semua *edge* diasumsikan memiliki bobot yang sama (misalnya, jumlah jalan terpendek, bukan jarak).
2.  **Sistem Jaringan Komputer:**
    * Memetakan semua perangkat (PC, server, router) dalam jaringan. Dimulai dari router utama, BFS menelusuri perangkat yang terhubung per level (Level 1: Switch, Level 2: PC/server yang terhubung ke switch).
3.  **Media Sosial:**
    * Platform seperti Facebook atau LinkedIn menggunakan BFS untuk menemukan teman atau koneksi dalam jarak tertentu (misal: "Orang yang mungkin Anda kenal"). Ini menelusuri teman langsung (level 1), lalu temannya teman (level 2), dan seterusnya.
4.  **Web Crawling:**
    * Mesin pencari seperti Google menggunakan BFS untuk meng-*crawl* halaman web, menjelajahi tautan dari satu halaman ke halaman lain.

**Implementasi C++**

Berikut adalah contoh implementasi C++ sederhana untuk BFS pada graf. Graf direpresentasikan menggunakan *adjacency list*.

```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <map>

// Fungsi untuk melakukan Breadth-First Search
// adj: Adjacency list yang merepresentasikan graf
// startNode: Simpul awal untuk memulai penelusuran
void bfs(const std::map<int, std::vector<int>>& adj, int startNode) {
    // Queue untuk menyimpan simpul yang akan dikunjungi
    std::queue<int> q;

    // Map untuk melacak simpul yang sudah dikunjungi
    std::map<int, bool> visited;

    // Inisialisasi: Tandai semua simpul sebagai belum dikunjungi
    for (auto const& [node, neighbors] : adj) {
        visited[node] = false;
    }

    // Masukkan simpul awal ke queue dan tandai sebagai sudah dikunjungi
    q.push(startNode);
    visited[startNode] = true;

    std::cout << "BFS traversal dimulai dari simpul " << startNode << ":\n";

    // Loop utama BFS
    while (!q.empty()) {
        // Ambil simpul dari depan queue
        int currentNode = q.front();
        q.pop();

        // Proses simpul saat ini (misalnya, cetak)
        std::cout << currentNode << " ";

        // Kunjungi semua tetangga dari simpul saat ini
        // Pastikan currentNode ada di adjacency list
        if (adj.count(currentNode)) {
            for (int neighbor : adj.at(currentNode)) {
                // Jika tetangga belum dikunjungi, masukkan ke queue dan tandai
                if (!visited[neighbor]) {
                    visited[neighbor] = true;
                    q.push(neighbor);
                }
            }
        }
    }
    std::cout << std::endl;
}

int main() {
    // Contoh graf menggunakan adjacency list:
    // 0 -- 1
    // |  / |
    // | /  |
    // 2 -- 3 -- 4
    std::map<int, std::vector<int>> graph;

    // Tambahkan sisi-sisi graf
    graph[0].push_back(1);
    graph[0].push_back(2);

    graph[1].push_back(0);
    graph[1].push_back(2);
    graph[1].push_back(3);

    graph[2].push_back(0);
    graph[2].push_back(1);
    graph[2].push_back(3);

    graph[3].push_back(1);
    graph[3].push_back(2);
    graph[3].push_back(4);

    graph[4].push_back(3);

    // Jalankan BFS dari simpul 0
    bfs(graph, 0); // Output: 0 1 2 3 4

    // Contoh lain, mulai dari simpul 4
    std::cout << "\n";
    bfs(graph, 4); // Output: 4 3 1 2 0

    return 0;
}
```

**Penjelasan Kode:**

1.  **`std::map<int, std::vector<int>> adj`**: Ini adalah representasi *adjacency list* dari graf. Kunci `int` adalah simpul, dan `std::vector<int>` adalah daftar tetangga dari simpul tersebut. Menggunakan `std::map` memungkinkan simpul dengan ID non-sequential.
2.  **`std::queue<int> q`**: Antrean digunakan untuk menyimpan simpul yang akan dikunjungi. Prinsip FIFO (First-In, First-Out) antrean sangat penting untuk BFS.
3.  **`std::map<int, bool> visited`**: Sebuah peta untuk melacak apakah setiap simpul sudah dikunjungi atau belum. Ini mencegah pemrosesan berulang dan siklus.
4.  **`bfs(const std::map<int, std::vector<int>>& adj, int startNode)`**:
    * Inisialisasi `visited` untuk semua simpul dalam graf menjadi `false`.
    * Masukkan `startNode` ke `q` dan tandai sebagai `true` di `visited`.
    * Loop `while (!q.empty())` terus berjalan selama ada simpul di antrean.
    * Di dalam loop, `currentNode` diambil dari depan antrean (`q.front()`, `q.pop()`).
    * `currentNode` diproses (dalam kasus ini, hanya dicetak).
    * Kemudian, semua tetangga `currentNode` diperiksa. Jika tetangga belum dikunjungi, ia ditandai `visited` dan dimasukkan ke `q`.
5.  **`main()`**: Mendefinisikan contoh graf dan memanggil fungsi `bfs` dua kali dengan simpul awal yang berbeda untuk mendemonstrasikan perilakunya.

**Kesimpulan**

Breadth-First Search (BFS) adalah algoritma penelusuran graf atau pohon yang menjelajahi simpul secara berlapis, dimulai dari simpul awal. Ia menggunakan struktur data antrean untuk memastikan semua simpul dengan jarak terdekat dijelajahi lebih dulu. BFS cocok untuk mencari jalur terpendek pada graf tak berbobot dan sangat efektif digunakan dalam berbagai aplikasi dunia nyata, mulai dari sistem navigasi, jaringan komputer, hingga media sosial. Meskipun membutuhkan memori yang cukup banyak, kelebihannya dalam menjamin solusi optimal pada kasus jalur terpendek menjadikannya algoritma yang fundamental dan banyak digunakan.
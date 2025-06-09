---
title: DIJKSTRA'S ALGORITHM
date: 2025-05-27
categories: [DESAIN ANALISIS ALGORITMA, DIJKSTRA'S ALGORITHM]
tags: [daa, algorithm, dijkstra, backtracking]     # TAG names should always be lowercase
---


**Pengantar**

Presentasi ini akan membahas "Dijkstra's Algorithm", sebuah algoritma fundamental dalam ilmu komputer yang digunakan untuk menemukan jalur terpendek dalam graf berbobot dengan sisi non-negatif. Kami akan mendalami pengertian algoritma ini, prinsip kerjanya langkah demi langkah, menganalisis kompleksitas waktu dan ruang, mengidentifikasi kelebihan dan kekurangannya, melihat beberapa aplikasi dunia nyata, serta meninjau implementasi kodenya. Dijkstra's Algorithm adalah salah satu algoritma *pathfinding* yang paling dikenal dan banyak diterapkan dalam berbagai bidang.

**Anggota Kelompok**

Presentasi ini dibuat oleh Kelompok 10, yang terdiri dari anggota-anggota berikut:
* AKMAL (H071241065)
* MUHAMMAD ARLIS (H071241047)
* MUHAMMAD HAIRI (H071241055)
* ZAHRA AULIA PUTRI (H071241025)

**Apa itu Dijkstra's Algorithm?**

Dijkstra's Algorithm adalah sebuah metode yang digunakan untuk mencari jalur terpendek antara dua titik (simpul) dalam sebuah graf. Graf ini bisa berupa jaringan yang terdiri dari simpul (titik) dan sisi (hubungan antar titik) dengan bobot tertentu pada sisi-sisinya. Algoritma ini membantu kita menentukan jalur terpendek dari titik awal (sumber) ke semua titik tujuan lainnya.

**Cara Kerja Dijkstra's Algorithm**

Dijkstra's Algorithm bekerja dengan pendekatan *greedy*, yaitu selalu memilih pilihan terbaik pada setiap langkah dengan harapan akan mengarah pada solusi optimal secara keseluruhan. Berikut adalah langkah-langkahnya:

1.  **Inisialisasi Jarak:**
    * Buat sebuah tabel atau array untuk menyimpan jarak terpendek dari simpul sumber ke setiap simpul lainnya. Inisialisasi jarak simpul sumber ke 0, dan jarak semua simpul lainnya ke tak hingga (`infinity`).
    * Buat sebuah set atau array boolean untuk melacak simpul mana saja yang sudah "dikunjungi" atau telah memiliki jarak terpendek final.
2.  **Pilih Simpul Terdekat:** Dari semua simpul yang belum dikunjungi, pilih simpul dengan jarak terpendek yang saat ini diketahui dari simpul sumber.
3.  **Perbarui Jarak Tetangga:** Untuk simpul yang baru dipilih:
    * Tandai simpul tersebut sebagai sudah dikunjungi.
    * Untuk setiap tetangganya:
        * Hitung jarak baru dari simpul sumber melalui simpul yang baru dipilih ini.
        * Jika jarak baru ini lebih kecil dari jarak yang saat ini tercatat untuk tetangga tersebut, perbarui jaraknya.
4.  **Ulangi:** Ulangi langkah 2 dan 3 sampai semua simpul telah dikunjungi atau semua simpul yang dapat dijangkau telah diproses.

**Kompleksitas Dijkstra's Algorithm**

* **Kompleksitas Waktu:**
    * **Dengan Array/List Biasa:** $O(V^2)$, di mana $V$ adalah jumlah simpul. Ini terjadi karena pada setiap iterasi, kita mencari simpul dengan jarak minimum dari $V$ simpul.
    * **Dengan Priority Queue (Heap):** $O((V+E) \log V)$, di mana $V$ adalah jumlah simpul dan $E$ adalah jumlah sisi. Ini adalah implementasi yang lebih efisien untuk graf yang besar atau jarang. Setiap operasi *extract-min* pada priority queue membutuhkan $O(\log V)$, dan ada $V$ operasi tersebut. Setiap operasi *decrease-key* (pembaruan jarak) membutuhkan $O(\log V)$, dan ada hingga $E$ operasi tersebut.
* **Kompleksitas Ruang:** $O(V+E)$, untuk menyimpan graf (adjacency list/matrix), array jarak, array `visited`, dan priority queue.

**Kelebihan Dijkstra's Algorithm**

* **Menjamin Jalur Terpendek:** Untuk graf dengan bobot sisi non-negatif, Dijkstra's Algorithm selalu menemukan jalur terpendek yang optimal dari simpul sumber ke semua simpul lainnya.
* **Efisiensi:** Dengan implementasi menggunakan *priority queue*, algortima ini sangat efisien untuk berbagai ukuran graf.
* **Kesederhanaan Konseptual:** Konsep dasar algoritma ini cukup mudah dipahami.
* **Aplikasi Luas:** Dapat diterapkan dalam berbagai masalah dunia nyata yang melibatkan pencarian jalur terpendek.

**Kekurangan Dijkstra's Algorithm**

* **Tidak Bekerja dengan Bobot Negatif:** Kekurangan terbesar Dijkstra adalah ketidakmampuannya menangani sisi dengan bobot negatif. Jika ada sisi negatif, algoritma bisa memberikan hasil yang salah. Untuk kasus ini, algoritma Bellman-Ford atau Floyd-Warshall lebih cocok.
* **Kurang Efisien untuk Graf Sangat Besar dan Jarang (Sparse):** Meskipun $O((V+E) \log V)$ efisien, pada graf yang sangat besar dan jarang terhubung (sedikit sisi), kompleksitas ini mungkin masih kurang optimal dibandingkan beberapa algoritma lain dalam skenario sangat spesifik, tetapi ini jarang menjadi masalah utama.
* **Perhitungan Bisa Terlalu Luas:** Jika tujuan kita hanya mencari jalur terpendek dari titik A ke titik B, Dijkstra tetap menghitung jarak terpendek dari A ke semua titik yang dapat dijangkau. Dalam kasus seperti ini, algoritma $A^*$ (A-Star) bisa lebih baik karena mempertimbangkan heuristik untuk mengarahkan pencarian ke tujuan, membuatnya lebih cepat.

**Aplikasi Dunia Nyata**

1.  **Sistem Navigasi/Peta:** Algoritma ini digunakan oleh aplikasi peta seperti Google Maps untuk menemukan rute terpendek antara dua lokasi, dengan bobot sisi yang mewakili jarak atau waktu tempuh.
2.  **Jaringan Komputer:**
    * **Routing Data:** Digunakan dalam protokol routing jaringan untuk menentukan jalur terbaik bagi paket data agar mencapai tujuannya dengan waktu tunda minimum.
    * **Internet:** Digunakan oleh router untuk menemukan jalur terpendek ke tujuan dalam jaringan, terutama dalam protokol *Open Shortest Path First (OSPF)*.
3.  **Pengiriman Logistik:** Perusahaan pengiriman menggunakan Dijkstra untuk mengoptimalkan rute pengiriman, mengurangi waktu dan biaya.
4.  **Analisis Jaringan Sosial:** Menemukan jarak "pertemanan" terpendek antar individu dalam jaringan sosial.

**Implementasi C++**

Berikut adalah implementasi Dijkstra's Algorithm dalam C++ menggunakan *priority queue* untuk efisiensi yang lebih baik.

```cpp
vector<pair<int, int>> graph[MAX]; // adjacency list
bool visited[MAX];                // track nodes visited
int distance[MAX];                // distance from source

void dijkstra(int start, int n) {
    for (int i = 0; i < n; i++) {
        distance[i] = INF;
        visited[i] = false;
    }

    distance[start] = 0;
    priority_queue<pair<int, int>, vector<pair<int, int>>, greater<>> pq;
    pq.push({0, start});

    while (!pq.empty()) {
        int u = pq.top().second;
        pq.pop();

        if (visited[u]) continue;
        visited[u] = true;

        for (auto [v, w] : graph[u]) {
            if (distance[u] + w < distance[v]) {
                distance[v] = distance[u] + w;
                pq.push({distance[v], v});
            }
        }
    }
}


**Penjelasan Kode:**

1.  **`std::vector<std::vector<Pair>> graph`**: Ini adalah representasi *adjacency list* dari graf. Setiap elemen `graph[u]` adalah sebuah vektor dari `Pair`s. Setiap `Pair` `{v, weight}` berarti ada sisi dari simpul `u` ke simpul `v` dengan bobot `weight`.
2.  **`std::vector<int> dist(V, std::numeric_limits<int>::max())`**: Vektor ini menyimpan jarak terpendek yang diketahui dari `start_node` ke setiap simpul. Awalnya, semua jarak disetel ke nilai maksimum integer (tak hingga) kecuali untuk `start_node` itu sendiri.
3.  **`std::priority_queue<Pair, std::vector<Pair>, std::greater<Pair>> pq`**: Ini adalah *min-priority queue*. Ia menyimpan pasangan `{jarak, simpul}`. `std::greater<Pair>` digunakan untuk mengubah perilaku default `priority_queue` dari *max-heap* menjadi *min-heap*, sehingga elemen dengan jarak terkecil selalu berada di bagian atas.
4.  **`dijkstra(const ..., int V, int start_node)` Function**:
    * **Inisialisasi**: Jarak `start_node` disetel ke 0 dan dimasukkan ke `pq`.
    * **Loop Utama (`while (!pq.empty())`)**:
        * Mengambil simpul `u` dengan jarak `d` terpendek dari `pq`.
        * **Optimisasi (`if (d > dist[u]) continue;`)**: Ini adalah cek penting. Jika jarak `d` yang baru saja diambil dari `pq` lebih besar dari `dist[u]` yang sudah ada, berarti kita sudah menemukan jalur yang lebih pendek ke `u` sebelumnya. Jadi, kita bisa melewati pemrosesan ini untuk menghindari perhitungan yang tidak perlu.
        * **Relaksasi Sisi**: Untuk setiap tetangga `v` dari `u`:
            * Jika `dist[u] + weight` (jarak dari sumber ke `u` ditambah bobot sisi `u` ke `v`) lebih kecil dari `dist[v]` saat ini, maka jalur baru ini lebih pendek.
            * `dist[v]` diperbarui, dan pasangan `{dist[v], v}` dimasukkan ke `pq`.
5.  **`main()` Function**:
    * Mendefinisikan graf contoh (`V=5` simpul) menggunakan *adjacency list*.
    * Memanggil `dijkstra` dari `start_node = 0`.
    * Mencetak hasil jarak terpendek dari simpul awal ke semua simpul lainnya.

**Kesimpulan**

Algoritma Dijkstra merupakan salah satu algoritma pencarian jalur terpendek yang paling efisien dan banyak digunakan dalam teori graf. Algoritma ini bekerja dengan cara mencari jalur terpendek dari satu simpul sumber ke semua simpul lainnya dalam graf berbobot non-negatif. Melalui pendekatan *greedy*, Dijkstra memastikan bahwa setiap langkahnya mendekatkan solusi menuju hasil optimal. Keunggulan utama algoritma ini terletak pada keakuratannya dan efisiensinya, terutama jika dikombinasikan dengan struktur data seperti *priority queue* atau *min-heap*. Dalam implementasi praktis, algoritma Dijkstra sangat berguna dalam berbagai bidang seperti jaringan komputer, sistem navigasi, dan pemodelan transportasi.
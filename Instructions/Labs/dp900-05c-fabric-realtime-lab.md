---
lab:
  title: Jelajahi analitik real-time di Microsoft Fabric
  module: Explore real-time analytics in Microsoft Fabric
---

# Jelajahi analitik real-time di Microsoft Fabric

Microsoft Fabric menyediakan Real-Time Intelligence, memungkinkan Anda membuat solusi analitik untuk aliran data real time. Dalam latihan ini, Anda akan menggunakan kemampuan Real-Time Intelligence di Microsoft Fabric untuk mencerna, menganalisis, dan memvisualisasikan aliran data real time dari perusahaan taksi.

Lab ini membutuhkan waktu sekitar **30** menit untuk menyelesaikannya.

> **Catatan**: Anda memerlukan [penyewa](https://learn.microsoft.com/fabric/get-started/fabric-trial) Microsoft Fabric untuk menyelesaikan latihan ini.

## Membuat ruang kerja

Sebelum bekerja dengan data di Fabric, Anda perlu membuat ruang kerja dengan kapasitas Fabric diaktifkan.

1. Navigasi ke [beranda](https://app.fabric.microsoft.com/home?experience=fabric) Microsoft Fabric di `https://app.fabric.microsoft.com/home?experience=fabric` browser, dan masuk dengan kredensial Fabric Anda.
1. Pada bilah menu di sebelah kiri, pilih **Ruang Kerja** (ikon terlihat mirip dengan ).
1. Buat ruang kerja baru dengan nama pilihan Anda, pilih mode lisensi yang mencakup kapasitas Fabric (*Uji Coba*, *Premium*, atau *Fabric*).
1. Saat ruang kerja baru Anda terbuka, ruang kerja harus kosong.

    ![Cuplikan layar ruang kerja kosong di Fabric.](./images/new-workspace.png)

## Membuat eventstream

Sekarang Anda siap untuk menemukan dan menyerap data real-time dari sumber streaming. Untuk melakukan ini, Anda akan mulai di Fabric Real-Time Hub.

> **Tips**: Saat pertama kali Anda menggunakan Hub Real-Time, beberapa *tips memulai* mungkin ditampilkan. Anda dapat menutup ini.

1. Di bilah menu di sebelah kiri, pilih **hub Real-Time** .

    Hub real time menyediakan cara mudah untuk menemukan dan mengelola sumber data streaming.

    ![Cuplikan layar hub real time di Fabric.](./images/real-time-hub.png)

1. Di hub real time, di bagian **Sambungkan ke** , pilih **Sumber data**.
1. **Temukan sumber data sampel taksi** kuning dan pilih **Sambungkan**. Kemudian di wizard Sambungkan **, beri nama sumber `taxi` dan edit nama eventstream default untuk mengubahnya menjadi `taxi-data`.** Aliran default yang terkait dengan data ini akan secara otomatis diberi nama *taxi-data-stream*:

    ![Cuplikan layar eventstream baru.](./images/name-eventstream.png)

1. Pilih **Berikutnya** dan tunggu sumber dan eventstream dibuat, lalu pilih **Buka eventstream**. Eventstream akan menampilkan **sumber taksi** dan **aliran** data taksi di kanvas desain:

   ![Cuplikan layar kanvas eventstream.](./images/new-taxi-stream.png)

## Membuat eventhouse

Eventstream menyerap data stok real-time, tetapi saat ini tidak melakukan apa pun dengannya. Mari kita buat eventhouse tempat kita dapat menyimpan data yang diambil dalam tabel.

1. Pada bilah menu di sebelah kiri, pilih **Buat**. Di halaman *Baru* , di bawah bagian *Inteligensi* Real-Time, pilih **Eventhouse**. Beri nama unik pilihan Anda.

    >**Catatan**: Jika **opsi Buat** tidak disematkan ke bar samping, Anda perlu memilih opsi elipsis (**...**) terlebih dahulu.

    Tutup tips atau perintah apa pun yang ditampilkan hingga Anda melihat eventhouse kosong baru Anda.

    ![Cuplikan layar eventhouse baru](./images/create-eventhouse.png)

1. Di panel sebelah kiri, perhatikan bahwa eventhouse Anda berisi database KQL dengan nama yang sama dengan eventhouse. Anda dapat membuat tabel untuk data real time Anda dalam database ini, atau membuat database tambahan seperlunya.
1. Pilih database, dan perhatikan bahwa ada set* kueri terkait*. File ini berisi beberapa contoh kueri KQL yang bisa Anda gunakan untuk mulai mengkueri tabel dalam database Anda.

    Namun, saat ini tidak ada tabel untuk dikueri. Mari kita atasi masalah tersebut dengan mendapatkan data dari eventstream ke dalam tabel baru.

1. Di halaman utama database KQL Anda, pilih **Dapatkan data**.
1. Untuk sumber data, pilih **Eventstream Eventstream**** > ** Yang Ada.
1. Di panel **Pilih atau buat tabel** tujuan, buat tabel baru bernama `taxi`. Kemudian di panel **Konfigurasikan sumber** data, pilih ruang kerja Anda dan **eventstream data** taksi dan beri nama koneksi `taxi-table`.

   ![Cuplikan layar konfigurasi untuk memuat tabel dari eventstream.](./images/configure-destination.png)

1. Gunakan tombol **Berikutnya** untuk menyelesaikan langkah-langkah untuk memeriksa data lalu menyelesaikan konfigurasi. Kemudian tutup jendela konfigurasi untuk melihat eventhouse Anda dengan tabel stok.

   ![Cuplikan layar dan eventhouse dengan tabel.](./images/eventhouse-with-table.png)

    Koneksi antara aliran dan tabel telah dibuat. Mari kita verifikasi bahwa dalam eventstream.

1. Di bilah menu di sebelah kiri, pilih **hub Real-Time** lalu lihat **halaman Aliran** data saya. **Di menu ...** untuk **aliran aliran** taksi-data, pilih **Buka eventstream**.

    Eventstream sekarang menampilkan tujuan untuk aliran:

   ![Cuplikan layar eventstream dengan tujuan.](./images/eventstream-destination.png)

    > **Tips**: Pilih tujuan pada kanvas desain, dan jika tidak ada pratinjau data yang ditampilkan di bawahnya, pilih **Refresh**.

    Dalam latihan ini, Anda telah membuat eventstream yang sangat sederhana yang menangkap data real-time dan memuatnya ke dalam tabel. Dalam soltuion nyata, Anda biasanya akan menambahkan transformasi untuk mengagregasi data melalui jendela temporal (misalnya, untuk menangkap harga rata-rata setiap saham selama periode lima menit).

    Sekarang mari kita jelajahi bagaimana Anda bisa mengkueri dan menganalisis data yang diambil.

## Mengkueri data yang diambil

Eventstream menangkap data tarif taksi real time dan memuatnya ke dalam tabel di database KQL Anda. Anda bisa mengkueri tabel ini untuk melihat data yang diambil.

1. Di bilah menu di sebelah kiri, pilih database eventhouse Anda.
1. Pilih set *kueri* untuk database Anda.
1. Di panel kueri, ubah contoh kueri pertama seperti yang diperlihatkan di sini:

    ```kql
    taxi
    | take 100
    ```

1. Pilih kode kueri dan jalankan untuk melihat 100 baris data dari tabel.

    ![Cuplikan layar kueri KQL.](./images/kql-stock-query.png)

1. Tinjau hasilnya, lalu ubah kueri untuk memperlihatkan jumlah pengambilan taksi untuk setiap jam:

    ```kql
    taxi
    | summarize PickupCount = count() by bin(todatetime(tpep_pickup_datetime), 1h)
    ```

1. Sorot kueri yang dimodifikasi dan jalankan untuk melihat hasilnya.
1. Tunggu beberapa detik dan jalankan lagi, mencatat bahwa jumlah pengambilan berubah saat data baru ditambahkan ke tabel dari aliran real-time.

## Membersihkan sumber daya

Dalam latihan ini, Anda telah membuat eventhouse, menyerap data real time menggunakan eventstream, mengkueri data yang diserap dalam tabel database KQL, membuat dasbor real time untuk memvisualisasikan data real time, dan mengonfigurasi pemberitahuan menggunakan Activator.

Jika Anda telah selesai menjelajahi Real-Time Intelligence di Fabric, Anda dapat menghapus ruang kerja yang Anda buat untuk latihan ini.

1. Di bilah di sebelah kiri, pilih ikon untuk ruang kerja Anda.
2. Di toolbar, pilih **Pengaturan** ruang kerja.
3. Di bagian **Umum** , pilih **Hapus ruang** kerja ini.

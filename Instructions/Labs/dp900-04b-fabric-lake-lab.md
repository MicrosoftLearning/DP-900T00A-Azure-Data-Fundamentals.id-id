---
lab:
  title: Menjelajahi analitik data di Microsoft Fabric
  module: Explore fundamentals of large-scale data analytics
---

# Menjelajahi analitik data di Microsoft Fabric

Dalam latihan ini Anda akan menjelajahi penyerapan dan analitik data di Microsoft Fabric Lakehouse.

Membutuhkan waktu sekitar **25** menit untuk menyelesaikan lab ini.

> **Catatan**: Anda memerlukan lisensi Microsoft Fabric untuk menyelesaikan latihan ini. Lihat [Mulai menggunakan Fabric](https://learn.microsoft.com/fabric/get-started/fabric-trial) untuk detail tentang cara mengaktifkan lisensi uji coba Fabric gratis. Anda akan memerlukan akun *sekolah* atau *kerja* Microsoft untuk melakukan ini. Jika tidak memilikinya, Anda dapat [mendaftar untuk uji coba Microsoft Office 365 E3 atau yang lebih tinggi](https://www.microsoft.com/microsoft-365/business/compare-more-office-365-for-business-plans).

## Membuat ruang kerja

Sebelum bekerja dengan data di Fabric, buat ruang kerja dengan uji coba Fabric diaktifkan.

1. Masuk ke [Microsoft Fabric](https://app.fabric.microsoft.com) di `https://app.fabric.microsoft.com`.
2. Di bilah menu di sebelah kiri, pilih **Ruang Kerja** (ikon terlihat mirip dengan &#128455;).
3. Buat ruang kerja baru dengan nama pilihan Anda, memilih mode lisensi di bagian **Tingkat Lanjut** yang mencakup kapasitas Fabric (*Uji Coba*, *Premium*, atau *Fabric*).
4. Saat ruang kerja baru Anda terbuka, ruang kerja harus kosong.

    ![Cuplikan layar ruang kerja kosong di Power BI.](./images/new-workspace.png)

## Membuat lakehouse

Sekarang setelah Anda memiliki ruang kerja, saatnya untuk beralih ke pengalaman *Rekayasa* data di portal dan membuat data lakehouse untuk file data Anda.

1. Di kiri bawah portal, beralihlah ke pengalaman **Rekayasa Data**.

    ![Cuplikan layar menu pengalih pengalaman.](./images/fabric-switcher.png)

    Beranda rekayasa data menyertakan petak peta untuk membuat aset rekayasa data yang umum digunakan.

2. Di beranda **Rekayasa** data, buat **Lakehouse** baru dengan nama pilihan Anda.

    Setelah satu menit atau lebih, lakehouse baru akan dibuat:

    ![Cuplikan layar lakehouse baru.](./images/new-lakehouse.png)

3. Lihat lakehouse baru, dan perhatikan bahwa panel **penjelajah Lakehouse** di sebelah kiri memungkinkan Anda menelusuri tabel dan file di lakehouse:
    - **Folder Tabel** berisi tabel yang bisa Anda kueri menggunakan SQL. Tabel dalam Microsoft Fabric lakehouse didasarkan pada format file *Delta Lake* sumber terbuka, yang umumnya digunakan dalam Apache Spark.
    - Folder **File** berisi file data di penyimpanan OneLake untuk lakehouse yang tidak terkait dengan tabel delta terkelola. Anda juga dapat membuat *pintasan* di folder ini untuk mereferensikan data yang disimpan secara eksternal.

    Saat ini, tidak ada tabel atau file di lakehouse.

## Serap data

Cara sederhana untuk menyerap data adalah dengan menggunakan aktivitas **Salin Data** dalam alur untuk mengekstrak data dari sumber dan menyalinnya ke file di lakehouse.

1. Pada halaman **Beranda** untuk lakehouse Anda, di menu **Dapatkan data** , pilih **Alur data baru**, dan buat alur data baru bernama **Ingest Sales Data**.
1. Di wizard **Salin Data** , pada halaman **Pilih sumber data** , pilih himpunan data sampel **Model Data Ritel dari Wide World Importers** .

    ![Cuplikan layar halaman Pilih sumber data.](./images/choose-data-source.png)

1. Pilih **Berikutnya** dan tampilkan tabel di sumber data di halaman **Sambungkan ke sumber data** .
1. Pilih tabel **dimension_stock_item** , yang berisi rekaman produk. Lalu pilih **Berikutnya** untuk melanjutkan ke halaman **Pilih tujuan data** .
1. Pada halaman **Pilih tujuan data** , pilih lakehouse Anda yang sudah ada. Lalu pilih **Berikutnya**.
1. Atur opsi tujuan data berikut, lalu pilih **Berikutnya**:
    - **Folder akar**: Tabel
    - **Pengaturan muat**: Muat ke tabel baru
    - **Nama tabel tujuan**: dimension_stock_item
    - **Pemetaan kolom**: *Biarkan pemetaan default apa adanya*
    - **Aktifkan partisi**: *Tidak dipilih*
1. Pada halaman **Tinjau + simpan** , pastikan bahwa opsi **Mulai transfer data segera** dipilih, lalu pilih **Simpan + Jalankan**.

    Alur baru yang berisi aktivitas **Salin Data** dibuat, seperti yang diperlihatkan di sini:

    ![Cuplikan layar alur dengan aktivitas Salin Data.](./images/copy-data-pipeline.png)

    Saat alur mulai berjalan, Anda dapat memantau statusnya di panel **Output** di bawah perancang alur. Gunakan ikon **&#8635;** (Refresh) untuk *menyegarkan* status, dan tunggu hingga berhasil.

1. Di bilah menu hub di sebelah kiri, pilih lakehouse Anda.
1. Pada halaman **Beranda** , di panel **penjelajah Lakehouse** , perluas **Tabel** dan verifikasi bahwa tabel **dimension_stock_item** telah dibuat.

    > **Catatan**: Jika tabel baru tercantum sebagai *tidak dikenal*, gunakan tombol **Refresh** di toolbar lakehouse untuk me-refresh tampilan.

1. Pilih tabel **dimension_stock_item** untuk menampilkan isinya.

    ![Cuplikan layar tabel dimension_stock_item.](./images/dimProduct.png)

## Mengkueri data di lakehouse

Sekarang setelah Anda menyerap data ke dalam tabel di lakehouse, Anda bisa menggunakan SQL untuk mengkuerinya.

1. Di kanan atas halaman Lakehouse, beralihlah ke **titik akhir SQL** untuk lakehouse Anda.

    ![Cuplikan layar menu titik akhir SQL.](./images/endpoint-switcher.png)

1. Di toolbar, pilih **Kueri SQL baru**. Kemudian masukkan kode SQL berikut ke editor kueri:

    ```sql
    SELECT Brand, COUNT(StockItemKey) AS Products
    FROM dimension_stock_item
    GROUP BY Brand
    ```

1. Pilih tombol **&#9655; Jalankan** untuk menjalankan kueri dan meninjau hasilnya, yang harus mengungkapkan bahwa ada dua nilai merek (*N/A* dan *Northwind*) dan memperlihatkan jumlah produk di masing-masing produk.

    ![Cuplikan layar kueri SQL.](./images/sql-query.png)

## Memvisualisasikan data di lakehouse

Microsoft Fabric lakehouses mengatur semua tabel dalam model data, yang dapat Anda gunakan untuk membuat visualisasi dan laporan.

1. Di kiri bawah halaman, di bawah panel **Explorer** , pilih tab **Model** untuk melihat model data untuk tabel di lakehouse (dalam hal ini hanya ada satu tabel).

    ![Cuplikan layar halaman model di Fabric lakehouse.](./images/fabric-model.png)

1. Di toolbar, pilih **Laporan baru** untuk membuka tab browser baru yang berisi perancang laporan Power BI.
1. Di perancang laporan:
    1. Di panel **Data** , perluas tabel **dimension_stock_item** dan pilih bidang **Brand** dan **StockItemKey** .
    1. Di panel **Visualisasi** , pilih visualisasi **bagan batang Tumpuk** (ini adalah yang pertama tercantum). Kemudian pastikan bahwa **sumbu Y** berisi bidang **Merek** dan ubah agregasi di **sumbu X** menjadi **Hitungan** sehingga berisi bidang **Jumlah StockItemKey** . Terakhir, mengubah ukuran visualisasi di kanvas laporan untuk mengisi ruang yang tersedia.

        ![Cuplikan layar laporan Power BI.](./images/fabric-report.png)

    > **Tips**: Anda dapat menggunakan **>>** ikon untuk menyembunyikan panel perancang laporan untuk melihat laporan dengan lebih jelas.

1. Pada menu **File** , pilih **Simpan** untuk menyimpan laporan sebagai **Laporan Kuantitas Merek** di ruang kerja Fabric Anda.

    Anda sekarang dapat menutup tab browser yang melanjutkan laporan untuk kembali ke lakehouse Anda. Anda dapat menemukan laporan di halaman untuk ruang kerja Anda di portal Microsoft Fabric.

## Membersihkan sumber daya

Jika Anda telah selesai menjelajahi Microsoft Fabric, Anda dapat menghapus ruang kerja yang Anda buat untuk latihan ini.

1. Di bilah di sebelah kiri, pilih ikon untuk ruang kerja Anda untuk melihat semua item yang ada di dalamnya.
2. Di menu **...** pada toolbar, pilih **Pengaturan ruang kerja**.
3. Di bagian **Lainnya** , pilih **Hapus ruang kerja ini**.

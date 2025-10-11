---
lab:
  title: Menjelajahi Azure SQL Database
  module: Explore relational data in Azure
---

# Menjelajahi Azure SQL Database

Di lab ini, Anda akan mempelajari cara memprovisikan Azure SQL Database dan berinteraksi dengannya menggunakan kueri SQL. Anda akan menggunakan database sampel Microsoft AdventureWorks, yang menyediakan tabel dan data yang telah diisi sebelumnya, sehingga Anda dapat fokus menjelajahi dan mengkueri data relasional tanpa perlu membuat skema Anda sendiri atau menyisipkan rekaman sampel. Pendekatan ini membuat semuanya mudah dan memungkinkan Anda berkonsentrasi pada pemahaman konsep database inti dan sintaks SQL.

Membutuhkan waktu sekitar **15** menit untuk menyelesaikan lab ini.

## Sebelum memulai

Anda memerlukan [langganan Azure](https://azure.microsoft.com/free) dengan akses tingkat administratif.

## Memprovisikan sumber daya Azure SQL Database

1. [Di portal Azure](https://portal.azure.com?azure-portal=true), pilih **&#65291; Buat sumber daya** dari sudut kiri atas dan cari `Azure SQL`. Lalu, di halaman **Azure SQL** yang dihasilkan, pilih **Buat**.

    ![Cuplikan layar Portal Microsoft Azure memperlihatkan Azure SQL di marketplace](images/azure-sql-marketplace.png)

1. Tinjau opsi Azure SQL yang tersedia, lalu di petak peta **Database SQL**, pastikan **Database tunggal** di pilih, lalu pilih **Buat**.

    ![Cuplikan layar portal Microsoft Azure yang menunjukkan halaman Azure SQL.](images/azure-sql-portal.png)

    > _**Tips**: Database tunggal adalah yang paling sederhana dan tercepat untuk disiapkan untuk lab ini. Opsi lain menambahkan pengaturan yang belum Anda perlukan._

1. Masukkan nilai berikut ini di halaman **Buat SQL Database**, dan biarkan semua properti lain dengan pengaturan default:
    - **Langganan**: Pilih langganan Azure Anda.
    - **Grup sumber daya**: Buat grup sumber daya baru dengan nama pilihan Anda.
    - **Nama database**: `AdventureWorks`
    - **Server**: Pilih **Buat baru** dan buat server baru dengan nama unik di lokasi yang tersedia. Gunakan **Autentikasi SQL** dan tentukan nama Anda sebagai proses masuk admin server dan kata sandi yang cukup rumit (ingat kata sandi - Anda akan membutuhkannya nanti!)
    - **Ingin menggunakan kumpulan elastis SQL?**: *Tidak*
    - **Lingkungan beban kerja**: Pengembangan
    - **Komputasi + penyimpanan**: Jangan ubah
    - **Redundansi penyimpanan cadangan**: *Penyimpanan cadangan redundan lokal*

    > _**Tips**: Autentikasi SQL cepat disiapkan untuk yang terakhir (tidak ada langkah-langkah ID Microsoft Entra tambahan). Default pengembangan lebih murah dan cepat. Pencadangan lokal adalah pilihan bernilai rendah dan halus untuk database praktik sementara._

1. Pada halaman **Buat SQL Database**, pilih **Berikutnya :Jaringan >**, dan pada halaman **Jaringan**, di bagian **Konektivitas jaringan**, pilih **Titik akhir publik**. Lalu, pilih **Ya** untuk kedua opsi di bagian **Aturan firewall** untuk mengizinkan akses ke server database Anda dari layanan Azure dan alamat IP klien Anda saat ini.

    ![Cuplikan layar Portal Microsoft Azure memperlihatkan pengaturan jaringan untuk database SQL](images/sql-database-network.png)

    > _**Tips**: Titik akhir publik + yang memungkinkan IP Anda langsung terhubung. Bagus untuk lab pendek. Dalam proyek nyata Anda biasanya mengunci akses lebih banyak._

1. Pilih **Berikutnya: Keamanan >** dan atur opsi **Aktifkan Microsoft Defender untuk SQL** ke **Tidak sekarang**.

    > _**Tips**: Defender adalah add-on keamanan berbayar. Kami melewatinya di sini untuk menjaga hal-hal sederhana dan menghindari biaya dalam latihan singkat._

1. Pilih **Berikutnya: Pengaturan Tambahan >** dan pada tab **Pengaturan tambahan**, atur opsi **Gunakan data yang ada** ke **Sampel** (opsi ini akan membuat database sampel yang dapat Anda jelajahi nanti).

    > _**Tips**: Data sampel memberi Anda tabel dan baris siap pakai sehingga Anda bisa langsung mulai mengkueri._

1. Pilih **Tinjau + Buat**, lalu pilih **Buat** untuk membuat database Azure SQL Anda.

1. Tunggu hingga penerapan selesai. Lalu, buka sumber daya yang sudah disebarkan, yang akan terlihat seperti ini:

    ![Cuplikan layar portal Microsoft Azure yang menunjukkan halaman SQL Database.](images/sql-database-portal.png)

1. Pada panel di sisi kiri laman, pilih **Editor kueri (pratinjau)**, lalu masuk menggunakan info masuk dan sandi administrator yang Anda tentukan untuk server Anda.
    
    >**Catatan**: Jika pesan kesalahan yang menyatakan bahwa alamat IP klien tidak diizinkan ditampilkan, pilih **tautan Allowlist IP ...** di akhir pesan untuk mengizinkan akses dan mencoba masuk lagi (sebelumnya Anda menambahkan alamat IP klien komputer Anda sendiri ke aturan firewall, tetapi editor kueri dapat terhubung dari alamat yang berbeda tergantung pada konfigurasi jaringan Anda.)
    
    Editor kueri terlihat seperti ini:
    
    ![Cuplikan layar portal Microsoft Azure yang menunjukkan editor kueri.](images/query-editor.png)

1. Perluas folder **Tables** untuk melihat tabel dalam database.

1. Di panel **Kueri 1**, masukkan kode SQL berikut:

    ```sql
   SELECT * FROM SalesLT.Product;
    ```

    > _**Tips**: SELECT * dengan cepat memperlihatkan setiap kolom dan beberapa nilai. (Dalam aplikasi nyata Anda biasanya menghindarinya dan hanya memilih kolom yang Anda butuhkan.)_

1. Pilih **&#9655; Jalankan** di atas kueri untuk menjalankannya dan melihat hasilnya, yang harus menyertakan semua kolom untuk semua baris dalam tabel **SalesLT.Product** seperti yang ditunjukkan di sini:

    ![Cuplikan layar portal Microsoft Azure yang menunjukkan editor kueri dengan hasil kueri.](images/sql-query-results.png)

1. Ganti pernyataan SELECT dengan kode berikut, lalu pilih **&#9655; Jalankan** untuk menjalankan kueri baru dan tinjau hasilnya (yang hanya menyertakan kolom **ProductID**, **Name**, **ListPrice**, **ProductCategoryID**):

    ```sql
   SELECT ProductID, Name, ListPrice, ProductCategoryID
   FROM SalesLT.Product;
    ```

    > _**Tips**: Hanya mencantumkan kolom yang Anda butuhkan agar hasilnya lebih kecil dan dapat berjalan lebih cepat._

1. Sekarang coba kueri berikut, yang menggunakan JOIN untuk mendapatkan nama kategori dari tabel **SalesLT.ProductCategory**:

    ```sql
    SELECT 
        p.ProductID, 
        p.Name AS ProductName,
        c.Name AS Category, 
        p.ListPrice
    FROM SalesLT.Product AS p
    INNER JOIN SalesLT.ProductCategory AS c 
        ON p.ProductCategoryID = c.ProductCategoryID;
    ```

    > _**Tips**: JOIN memperlihatkan cara menarik data terkait (nama kategori) dari tabel lain menggunakan ID yang cocok._

1. Tutup panel editor kueri, dengan membuang hasil editan Anda.

> _**Tips**: Jika Anda telah selesai menjelajahi Azure SQL Database, Anda dapat menghapus grup sumber daya yang Anda buat dalam latihan ini. Menghapus grup sumber daya akan menghapus semua sumber daya dalam satu langkah. Ini juga meminimalkan biaya._

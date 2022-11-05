---
lab:
  title: Jelajahi Azure Cosmos DB
  module: Explore fundamentals of Azure Cosmos DB
---
# <a name="explore-azure-cosmos-db"></a>Jelajahi Azure Cosmos DB

Dalam latihan ini Anda akan memprovisikan database Azure Cosmos DB di langganan Azure Anda, dan menjelajahi berbagai cara Anda dapat menggunakannya untuk menyimpan data non-relasional.

Membutuhkan waktu sekitar **15** menit untuk menyelesaikan lab ini.

## <a name="before-you-start"></a>Sebelum Anda memulai

Anda memerlukan [langganan Azure](https://azure.microsoft.com/free) dengan akses tingkat administratif.

## <a name="create-a-cosmos-db-account"></a>Membuat akun Cosmos DB

Untuk menggunakan Cosmos DB, Anda harus menyediakan akun Cosmos DB di langganan Azure Anda. Dalam latihan ini, Anda akan menyediakan akun Cosmos DB yang menggunakan Azure Cosmos DB untuk NoSQL.

1. Di portal Microsoft Azure, pilih **+ Buat sumber daya** di kiri atas, dan cari *Azure Cosmos DB*.  Di hasil, pilih **Azure Cosmos DB** dan pilih **Buat**.
1. Di petak **Azure Cosmos DB untuk NoSQL**, pilih **Buat**.
1. Masukkan detail berikut, lalu pilih **Tinjau + Buat**:
    - **Langganan**: Jika Anda menggunakan kotak pasir, pilih *Langganan Concierge*. Atau, pilih langganan Azure.
    - **Grup sumber daya**: Jika Anda menggunakan kotak pasir, pilih grup sumber daya yang ada (yang akan diberi nama seperti *learn-xxxx...* ). Jika tidak, buat grup sumber daya baru dengan nama pilihan Anda.
    - **Nama Akun**: Masukkan nama unik
    - **Lokasi**: Pilih lokasi yang disarankan
    - **Mode kapasitas**: Throughput yang disediakan
    - **Terapkan Diskon Tingkat Gratis**: Pilih Terapkan jika tersedia
    - **Batasi total throughput akun**: Tidak dipilih
1. Ketika konfigurasi telah divalidasi, pilih **Buat**.
1. Tunggu hingga penerapan selesai. Lalu pergi ke sumber daya yang disebarkan.

## <a name="create-a-sample-database"></a>Membuat database sampel

*Sepanjang prosedur ini, tutup semua tips yang ditampilkan di portal*.

1. Pada halaman akun Cosmos DB baru Anda, di panel sebelah kiri, pilih **Data Explorer**.
1. Di halaman **Data Explorer**, pilih **Luncurkan mulai cepat**.
1. Di tab **Kontainer baru**, tinjau pengaturan yang telah diisi sebelumnya untuk database sampel, lalu pilih **OK**.
1. Amati status di panel di bagian bawah layar hingga database **SampleDB** dan kontainer **SampleContainer** telah dibuat (yang mungkin memerlukan waktu sekitar satu menit).

## <a name="view-and-create-items"></a>Melihat dan membuat item

1. Di halaman Data Explorer, luaskan database **SampleDB** dan kontainer **SampleContainer**, lalu pilih **Item** untuk melihat daftar item dalam kontainer. Item mewakili alamat, masing-masing dengan id unik dan properti lainnya.
1. Pilih salah satu item dalam daftar untuk melihat representasi JSON dari data item.
1. Di bagian atas halaman, pilih **Item Baru** untuk membuat item kosong baru.
1. Ubah JSON untuk item baru sebagai berikut, lalu pilih **Simpan**.

    ```json
    {
        "address": "1 Any St.",
        "id": "123456789"
    }
    ```

1. Setelah menyimpan item baru, perhatikan bahwa properti metadata tambahan ditambahkan secara otomatis.

## <a name="query-the-database"></a>Mengkueri database

1. Di halaman **Data Explorer**, pilih ikon **Kueri SQL Baru**.
1. Di editor Kueri SQL, tinjau kueri default (`SELECT * FROM c`) dan gunakan tombol `SELECT * FROM c` untuk menjalankannya.
1. Tinjau hasilnya, yang mencakup representasi JSON lengkap dari semua item.
1. Ubah kueri sebagai berikut:

    ```sql
    SELECT c.id, c.address
    FROM c
    WHERE CONTAINS(c.address, "Any St.")
    ```

1. Gunakan tombol **Jalankan Kueri** untuk menjalankan kueri yang direvisi dan tinjau hasilnya, yang mencakup entitas JSON untuk item apa pun dengan bidang **alamat** yang berisi teks "Any St.".
1. Tutup editor Kueri SQL, buang perubahan Anda.

    Anda telah melihat cara membuat dan mengkueri entitas JSON dalam database Cosmos DB menggunakan antarmuka penjelajah data di portal Microsoft Azure. Di kehidupan nyata, pengembang aplikasi akan menggunakan salah satu dari banyak kit pengembangan perangkat lunak (SDK) khusus bahasa pemrograman untuk memanggil NoSQL API dan bekerja dengan data dalam database.

> **Tips**: Setelah selesai menjelajahi Azure Cosmos DB, Anda dapat menghapus grup sumber daya yang dibuat dalam latihan ini.

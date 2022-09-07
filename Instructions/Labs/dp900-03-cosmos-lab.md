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

To use Cosmos DB, you must provision a Cosmos DB account in your Azure subscription. In this exercise, you'll provision a Cosmos DB account that uses the core (SQL) API.

1. In the Azure portal, select <bpt id="p1">**</bpt>+ Create a resource<ept id="p1">**</ept> at the top left, and search for <bpt id="p2">*</bpt>Azure Cosmos DB<ept id="p2">*</ept>.  In the results, select <bpt id="p1">**</bpt>Azure Cosmos DB<ept id="p1">**</ept> and select  <bpt id="p2">**</bpt>Create<ept id="p2">**</ept>.
1. Di petak **Core (SQL) - Disarankan**, pilih **Buat**.
1. Masukkan detail berikut, lalu pilih **Tinjau + Buat**:
    - <bpt id="p1">**</bpt>Subscription<ept id="p1">**</ept>: If you're using a sandbox, select <bpt id="p2">*</bpt>Concierge Subscription<ept id="p2">*</ept>. Otherwise, select your Azure subscription.
    - **Grup sumber daya**: Jika Anda menggunakan kotak pasir, pilih grup sumber daya yang ada (yang akan diberi nama seperti *learn-xxxx...* ). Jika tidak, buat grup sumber daya baru dengan nama pilihan Anda.
    - **Nama Akun**: Masukkan nama unik
    - **Lokasi**: Pilih lokasi yang disarankan
    - **Mode kapasitas**: Throughput yang disediakan
    - **Terapkan Diskon Tingkat Gratis**: Pilih Terapkan jika tersedia
    - **Batasi total throughput akun**: Tidak dipilih
1. Ketika konfigurasi telah divalidasi, pilih **Buat**.
1. Wait for deployment to complete. Then go to the deployed resource.

## <a name="create-a-sample-database"></a>Membuat database sampel

*Sepanjang prosedur ini, tutup semua tips yang ditampilkan di portal*.

1. Pada halaman akun Cosmos DB baru Anda, di panel sebelah kiri, pilih **Data Explorer**.
1. Di halaman **Data Explorer**, pilih **Luncurkan mulai cepat**.
1. Di tab **Kontainer baru**, tinjau pengaturan yang telah diisi sebelumnya untuk database sampel, lalu pilih **OK**.
1. Amati status di panel di bagian bawah layar hingga database **SampleDB** dan kontainer **SampleContainer** telah dibuat (yang mungkin memerlukan waktu sekitar satu menit).

## <a name="view-and-create-items"></a>Melihat dan membuat item

1. In the Data Explorer page, expand the <bpt id="p1">**</bpt>SampleDB<ept id="p1">**</ept> database and the <bpt id="p2">**</bpt>SampleContainer<ept id="p2">**</ept> container, and select <bpt id="p3">**</bpt>Items<ept id="p3">**</ept> to see a list of items in the container. The items represent addresses, each with a unique id and other properties.
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

    You've seen how to create and query JSON entities in a Cosmos DB database by using the data explorer interface in the Azure portal. In a real scenario, an application developer would use one of the many programming language specific software development kits (SDKs) to call the core (SQL) API and work with data in the database.

> **Tips**: Setelah selesai menjelajahi Azure Cosmos DB, Anda dapat menghapus grup sumber daya yang dibuat dalam latihan ini.

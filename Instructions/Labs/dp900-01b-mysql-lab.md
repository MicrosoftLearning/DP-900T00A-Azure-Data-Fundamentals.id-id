---
lab:
  title: Jelajahi Azure Database for MySQL
  module: Explore relational data in Azure
---

# <a name="explore-azure-database-for-mysql"></a>Jelajahi Azure Database for MySQL

Dalam latihan ini Anda akan menyediakan sumber daya Azure Database for MySQL di langganan Azure Anda.

Membutuhkan waktu sekitar **5** menit untuk menyelesaikan lab ini.

## <a name="before-you-start"></a>Sebelum Anda memulai

Anda memerlukan [langganan Azure](https://azure.microsoft.com/free) dengan akses tingkat administratif.

## <a name="provision-an-azure-database-for-mysql-resource"></a>Memprovisikan sumber daya Azure Database for MySQL

Dalam latihan ini, Anda akan memprovisikan sumber daya Azure Database for MySQL.

1. In the Azure portal, select <bpt id="p1">**</bpt>&amp;#65291; Create a resource<ept id="p1">**</ept> from the upper left-hand corner and search for <bpt id="p2">*</bpt>Azure Database for MySQL<ept id="p2">*</ept>. Then in the resulting <bpt id="p1">**</bpt>Azure Database for MySQL<ept id="p1">**</ept> page, select <bpt id="p2">**</bpt>Create<ept id="p2">**</ept>.

1. Tinjau opsi Azure Database for MySQL yang tersedia, biarkan **Jenis sumber daya** sebagai  dan pilih **Buat**.

    ![Cuplikan layar opsi penyebaran Azure Database for MySQL](images/mysql-options.png)

1. Masukkan nilai berikut di halaman **Buat SQL Database**:
    - **Langganan**: Pilih langganan Azure Anda.
    - **Grup sumber daya**: Buat grup sumber daya baru dengan nama pilihan Anda.
    - **Nama server**: Masukkan nama unik.
    - **Wilayah**: Setiap lokasi yang tersedia di dekat Anda.
    - **Versi MySQL**: Biarkan tidak berubah.
    - **Jenis beban kerja**: Untuk proyek pengembangan atau hobi.
    - **Komputasi + penyimpanan**: Biarkan tidak berubah.
    - **Zona ketersediaan**: Biarkan tidak berubah.
    - **Aktifkan ketersediaan tinggi**: Biarkan tidak berubah.
    - **Nama pengguna admin**: Nama Anda
    - **Kata sandi** dan **Konfirmasi kata sandi**: Kata sandi yang cukup rumit

1. Pilih **Berikutnya: Jaringan**.

1. Di bagian **Aturan firewall**, pilih **&#65291; Tambahkan alamat IP klien saat ini**.

1. Pilih **Tinjau + Buat**, lalu pilih **Buat** untuk membuat database Azure MySQL Anda.

1. Wait for deployment to complete. Then go to the resource that was deployed, which should look like this:

    ![Cuplikan layar portal Microsoft Azure yang menampilkan halaman Azure Database for MySQL.](images/mysql-portal.png)

1. Tinjau opsi untuk mengelola sumber daya Azure Database for MySQL Anda.

> **Tips**: Setelah selesai menjelajahi Azure Database for MySQL, Anda dapat menghapus grup sumber daya yang dibuat dalam latihan ini.

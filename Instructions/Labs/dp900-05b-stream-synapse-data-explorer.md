---
lab:
  title: Menjelajahi Azure Synapse Data Explorer
  module: Explore fundamentals of real-time analytics
---

# <a name="explore-azure-synapse-data-explorer"></a>Menjelajahi Azure Synapse Data Explorer

Dalam latihan ini, Anda akan menggunakan Azure Synapse Data Explorer untuk menganalisis data deret waktu.

Membutuhkan waktu sekitar **25** menit untuk menyelesaikan lab ini.

## <a name="before-you-start"></a>Sebelum Anda memulai

Anda memerlukan [langganan Azure](https://azure.microsoft.com/free) dengan akses tingkat administratif.

## <a name="provision-a-synapse-analytics-workspace"></a>Memprovisikn ruang kerja Azure Synapse Analytics

> **Tips**: Jika sudah memiliki Ruang Kerja Azure Synapse dari latihan sebelumnya, lewati bagian ini dan langsung buka **[Buat kumpulan Data Explorer](#create-a-data-explorer-pool)** .

1. Buka portal Microsoft Azure di [https://portal.azure/com](https://portal.azure.com?azure-portal=true), dan masuk menggunakan info masuk yang terkait dengan langganan Azure Anda.

    >                 **Catatan**: Pastikan untuk menggunakan direktori yang berisi langganan Anda - terletak di kanan atas di bawah ID pengguna. Jika tidak, pilih ikon pengguna dan ubah direktori.

1. Di portal Microsoft Azure, di halaman **Beranda**, gunakan **&#65291; Buat ikon sumber daya** untuk membuat sumber daya baru.
1. Cari *Azure Synapse Analytics*, dan buat sumber daya **Azure Synapse Analytics** yang baru dengan pengaturan berikut:
    - **Langganan**: *Langganan Azure Anda*
        - **Grup sumber daya**: *Buat grup sumber daya baru dengan nama yang sesuai, seperti "synapse-rg"*
        - **Kelompok sumber daya terkelola**: *Masukkan nama yang sesuai, misalnya "synapse-managed-rg"*.
    - **Nama ruang kerja**: *Masukkan nama ruang kerja yang unik, misalnya "synapse-ws-<your_name>*.
    - **Wilayah**: *Pilih wilayah yang tersedia*.
    - **Pilih Data Lake Storage Gen 2**: Dari langganan
        - **Nama akun**: *Buat akun baru dengan nama unik, misalnya "datalake<your_name>"*.
        - **Nama sistem file**: *Buat sistem file baru dengan nama yang unik, misalnya "fs<your_name>"*.

    >                 **Catatan**: Ruang kerja Synapse Analytics memerlukan dua grup sumber daya dalam langganan Azure; satu untuk sumber daya yang dibuat secara eksplisit, dan satu lagi untuk sumber daya terkelola yang digunakan oleh layanan. Hal ini juga memerlukan akun penyimpanan Data Lake untuk menyimpan data, skrip, dan artefak lainnya.

1. Saat Anda memasukkan detail ini, pilih **Tinjau + buat**, lalu pilih **Buat** untuk membuat ruang kerja.
1. Tunggu hingga ruang kerja selesai dibuat - mungkin memerlukan waktu lima menit atau lebih.
1. Saat penyebaran selesai, buka grup sumber daya yang dibuat dan perhatikan bahwa grup tersebut berisi ruang kerja Synapse Analytics Anda dan akun penyimpanan Data Lake.
1. Pilih ruang kerja Synapse Anda, dan di halaman **Gambaran umum**, di kartu **Buka Synapse Studio**, pilih **Buka** untuk membuka Synapse Studio di tab browser baru. Synapse Studio adalah antarmuka berbasis web yang dapat digunakan untuk bekerja dengan ruang kerja Synapse Analytics Anda.
1. Di sisi kiri Synapse Studio, gunakan ikon **&rsaquo;&rsaquo;** untuk meluaskan menu - tindakan ini akan menampilkan berbagai halaman dalam Synapse Studio yang akan digunakan untuk mengelola sumber daya dan melakukan tugas analitik data

## <a name="create-a-data-explorer-pool"></a>Membuat kumpulan Data Explorer

1. Di Synapse Studio, pilih halaman **Kelola**.
1. Pilih tab **kumpulan Data Explorer**, lalu gunakan tab **&#65291; Ikon** baru untuk membuat kumpulan baru dengan pengaturan berikut:
    - **Nama kumpulan Data Explorer**: dxpool
    - **Beban kerja**: Dioptimalkan untuk komputasi
    - **Ukuran**: Ekstra Kecil (2 inti)
1. Pilih **Berikutnya: Pengaturan Tambahan >** dan aktifkan pengaturan **Penyerapan streaming** - pengaturan ini memungkinkan Data Explorer menyerap data baru dari sumber streaming, seperti Azure Event Hubs.
1. Pilih **Tinjau dan buat** untuk membuat kumpulan Data Explorer, lalu tunggu hingga kumpulan tersebut disebarkan (yang mungkin memerlukan waktu 15 menit atau lebih lama - statusnya akan berubah dari *Membuat* menjadi *Online*).

## <a name="create-a-database-and-ingest-data"></a>Membuat database dan menyerap data

1. Di Synapse Studio, pilih halaman **Data**.
1. Pastikan tab **Ruang Kerja** dipilih, dan jika perlu, pilih **&#8635;** di kiri atas halaman untuk merefresh tampilan sehingga **database Data Explorer**  terdaftar.
1. Perluas **Database Data Explorer** dan verifikasi bahwa **dxpool** dicantumkan.
1. Di panel **Data**, gunakan **&#65291;** untuk membuat **database Data Explorer** baru di kumpulan **dxpool** dengan nama **iot-data**.
1. Sambil menunggu database dibuat, unduh **devices.csv** dari [https://github.com/MicrosoftLearning/DP-900T00A-Azure-Data-Fundamentals/raw/master/streaming/data/devices.csv](https://github.com/MicrosoftLearning/DP-900T00A-Azure-Data-Fundamentals/raw/master/streaming/data/devices.csv?azure-portal=true), simpan di folder mana pun di komputer lokal Anda.
1. Di Synapse Studio, tunggu database dibuat jika perlu, lalu di menu **...** untuk database **iot-data** baru, pilih **Buka di Azure Data Explorer**.
1. Di tab browser baru yang berisi Azure Data Explorer, pada tab **Data**, pilih **Serap data baru**.
1. Di halaman **Tujuan**, pilih pengaturan berikut:
    - **Kluster**: *Kumpulan Data Explorer **dxpool** di ruang kerja Azure Synapse Anda*
    - **Database**: iot-data
    - **Tabel**: Buat tabel baru bernama **perangkat**
1. Pilih **Berikutnya: Sumber** dan pada halaman **Sumber**, pilih opsi berikut:
    - **Jenis sumber**: File
    - **File**: Unggah file **devices.csv** dari komputer lokal Anda.
1. Pilih **Berikutnya: Skema** dan pada halaman **Skema**, pastikan pengaturan berikut sudah benar:
    - **Jenis pemadatan**: Tidak dipadatkan
    - **Format data**: CSV
    - **Abaikan catatan pertama**: dipilih
    - **Pemetaan**: devices_mapping
1. Pastikan tipe data kolom telah diidentifikasi dengan benar sebagai *Waktu (waktu (tanggalwaktu)*, *Perangkat (string)*, dan *Nilai (panjang)*). Kemudian pilih **Berikutnya: Mulai Penyerapan**.
1. Saat penyerapan selesai, pilih **Tutup**.
1. Di Azure Data Explorer, pada tab **Kueri**, pastikan database **iot-data** dipilih, lalu di panel kueri, masukkan kueri berikut.

    ```kusto
    devices
    ```

1. Pada bilah alat, pilih **&#9655; Jalankan** untuk menjalankan kueri, dan tinjau hasilnya, yang akan terlihat seperti ini:

    | Waktu | Perangkat | Nilai |
    | --- | --- | --- |
    | 2022-01-01T00:00:00Z | Dev1 | 7 |
    | 2022-01-01T00:00:01Z | Dev2 | 4 |
    | ... | ... | ... |

    Jika hasil cocok dengan ini, Anda telah berhasil membuat tabel **perangkat** dari data dalam file.

    >                 **Tips**: Dalam contoh ini, Anda mengimpor sejumlah kecil data batch dari satu file, yang dapat dilakukan untuk tujuan latihan ini. Pada kenyataannya, Anda dapat menggunakan Data Explorer untuk menganalisis volume data yang jauh lebih besar; dan karena Anda mengaktifkan penyerapan streaming, Anda juga dapat mengonfigurasi Data Explorer untuk menyerap data ke dalam tabel dari sumber streaming seperti Azure Event Hubs.

## <a name="use-kusto-query-language-to-query-the-table-in-synapse-studio"></a>Gunakan bahasa kueri Kusto untuk membuat kueri tabel di Synapse Studio

1. Tutup tab browser Azure Data Explorer dan kembali ke tab yang berisi Synapse Studio.
1. Pada halaman **Data**, luaskan database **iot-data** dan folder **Tabel**-nya. Kemudian di menu **...** untuk tabel **perangkat**, pilih **Skrip KQL Baru** > **Ambil 1000 baris**.
1. Tinjau kueri yang dihasilkan dan hasilnya. Kueri harus berisi kode berikut:

    ```kusto
    devices
    | take 1000
    ```

    Hasil kueri berisi 1000 baris data pertama.

1. Ubah kueri sebagai berikut:

    ```kusto
    devices
    | where Device == 'Dev1'
    ```

1. Pilih **&#9655; Jalankan** untuk menjalankan kueri. Kemudian tinjau hasilnya, yang seharusnya hanya berisi baris untuk perangkat *Dev1*.

1. Ubah kueri sebagai berikut:

    ```kusto
    devices
    | where Device == 'Dev1'
    | where Time > datetime(2022-01-07)
    ```

1. Jalankan kueri dan tinjau hasilnya, yang seharusnya hanya berisi baris untuk perangkat *Dev1* setelah tanggal 7 Januari 2022.

1. Ubah kueri sebagai berikut:

    ```kusto
    devices
    | where Time between (datetime(2022-01-01 00:00:00) .. datetime(2022-07-01 23:59:59))
    | summarize AvgVal = avg(Value) by Device
    | sort by Device asc
    ```

1. Jalankan kueri dan tinjau hasilnya, yang seharusnya berisi nilai perangkat rata-rata yang tercatat antara tanggal 1 Januari dan 7 Januari 2022 dalam urutan nama perangkat yang menaik.

1. Tutup tab kueri KQL, buang perubahan Anda.

## <a name="delete-azure-resources"></a>Menghapus sumber daya Azure

Setelah selesai menjelajahi Azure Synapse Analytics, Anda harus menghapus sumber daya yang dibuat untuk menghindari biaya Azure yang tidak perlu.

1. Tutup tab browser Synapse Studio, tanpa menyimpan perubahan apa pun, dan kembali ke portal Microsoft Azure.
1. Di portal Microsoft Azure, pada halaman **Beranda**, pilih **Grup sumber daya**.
1. Pilih grup sumber daya untuk ruang kerja Synapse Analytics Anda (bukan grup sumber daya terkelola), dan verifikasi bahwa grup tersebut berisi ruang kerja Synapse, akun penyimpanan, dan kumpulan Data Explorer untuk ruang kerja Anda (jika Anda menyelesaikan latihan sebelumnya, grup tersebut juga akan berisi kumpulan Spark).
1. Di bagian atas halaman **Gambaran Umum** untuk grup sumber daya, pilih **Hapus grup sumber daya**.
1. Masukkan nama grup sumber daya untuk mengonfirmasi bahwa Anda ingin menghapusnya, dan pilih **Hapus**.

    Setelah beberapa menit, ruang kerja Azure Synapse Anda dan ruang kerja terkelola yang terkait dengannya akan dihapus.

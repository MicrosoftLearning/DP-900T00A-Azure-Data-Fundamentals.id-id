---
lab:
  title: Menjelajahi Spark Streaming di Azure Synapse Analytics
  module: Explore fundamentals of real-time analytics
---

# <a name="explore-spark-streaming-in-azure-synapse-analytics"></a>Menjelajahi Spark Streaming di Azure Synapse Analytics

Dalam latihan ini, Anda akan menggunakan *Aliran Terstruktur Spark* dan *tabel delta* di Azure Synapse Analytics untuk memproses data aliran.

Membutuhkan waktu sekitar **15** menit untuk menyelesaikan lab ini.

## <a name="before-you-start"></a>Sebelum Anda memulai

Anda memerlukan [langganan Azure](https://azure.microsoft.com/free) dengan akses tingkat administratif.

## <a name="provision-a-synapse-analytics-workspace"></a>Memprovisikn ruang kerja Azure Synapse Analytics

Untuk menggunakan Synapse Analytics, Anda harus memprovisikan sumber daya Ruang Kerja Synapse Analytics di langganan Azure Anda.

1. Buka portal Azure di [portal Azure](https://portal.azure.com?azure-portal=true), dan masuk menggunakan info masuk yang terkait dengan langganan Azure Anda.

    > <bpt id="p1">**</bpt>Note<ept id="p1">**</ept>: Ensure you are working in the directory containing your own subscription - indicated at the top right under your user ID. If not, select the user icon and switch directory.

2. Di portal Microsoft Azure, di halaman **Beranda**, gunakan **&#65291; Buat ikon sumber daya** untuk membuat sumber daya baru.
3. Cari *Azure Synapse Analytics*, dan buat sumber daya **Azure Synapse Analytics** yang baru dengan pengaturan berikut:
    - **Langganan**: *Langganan Azure Anda*
        - **Grup sumber daya**: *Buat grup sumber daya baru dengan nama yang sesuai, seperti "synapse-rg"*
        - **Kelompok sumber daya terkelola**: *Masukkan nama yang sesuai, misalnya "synapse-managed-rg"*.
    - **Nama ruang kerja**: *Masukkan nama ruang kerja yang unik, misalnya "synapse-ws-<your_name>*.
    - **Wilayah**: *Pilih wilayah yang tersedia*.
    - **Pilih Data Lake Storage Gen 2**: Dari langganan
        - **Nama akun**: *Buat akun baru dengan nama unik, misalnya "datalake<your_name>"*.
        - **Nama sistem file**: *Buat sistem file baru dengan nama yang unik, misalnya "fs<your_name>"*.

    > <bpt id="p1">**</bpt>Note<ept id="p1">**</ept>: A Synapse Analytics workspace requires two resource groups in your Azure subscription; one for resources you explicitly create, and another for managed resources used by the service. It also requires a Data Lake storage account in which to store data, scripts, and other artifacts.

4. Saat Anda memasukkan detail ini, pilih **Tinjau + buat**, lalu pilih **Buat** untuk membuat ruang kerja.
5. Tunggu hingga ruang kerja selesai dibuat - mungkin memerlukan waktu lima menit atau lebih.
6. Saat penyebaran selesai, buka grup sumber daya yang dibuat dan perhatikan bahwa grup tersebut berisi ruang kerja Synapse Analytics Anda dan akun penyimpanan Data Lake.
7. Pilih ruang kerja Synapse Anda, dan di halaman **Gambaran umum**, di kartu **Buka Synapse Studio**, pilih **Buka** untuk membuka Synapse Studio di tab browser baru. Synapse Studio adalah antarmuka berbasis web yang dapat digunakan untuk bekerja dengan ruang kerja Synapse Analytics Anda.
8. Di sisi kiri Synapse Studio, gunakan ikon **&rsaquo;&rsaquo;** untuk memperluas menu - tindakan ini akan menampilkan halaman berbeda dalam Synapse Studio yang akan Anda gunakan untuk mengelola sumber daya dan melakukan tugas analisis data, seperti ditampilkan di sini:

    ![Synapse Studio](images/synapse-studio.png)

## <a name="create-a-spark-pool"></a>Membuat kumpulan Spark

Untuk menggunakan Spark guna memproses data aliran, Anda perlu menambahkan kumpulan Spark ke ruang kerja Azure Synapse Anda.

1. Di Synapse Studio, pilih halaman **Kelola**.
2. Pilih tab **Kumpulan Apache Spark**, lalu gunakan ikon **&#65291; Baru** untuk membuat kumpulan Spark baru dengan pengaturan berikut:
    - **Nama kumpulan Apache Spark**: sparkpool
    - **Kelompok ukuran node**: Memori Dioptimalkan
    - **Ukuran node**: Kecil (4 vCore/32 GB)
    - **Skala otomatis**: Diaktifkan
    - **Jumlah node** 3----3
3. Tinjau dan buat kumpulan Spark, lalu tunggu sampai digunakan (yang mungkin memakan waktu beberapa menit).

## <a name="explore-stream-processing"></a>Mempelajari pemrosesan aliran

Untuk mempelajari pemrosesan aliran dengan Spark, Anda akan menggunakan notebook yang berisi kode Python dan catatan untuk membantu Anda melakukan beberapa pemrosesan aliran dasar dengan Aliran Terstruktur Spark dan tabel delta.

1. Unduh notebook [Structured Streaming and Delta Tables.ipynb](https://github.com/MicrosoftLearning/DP-900T00A-Azure-Data-Fundamentals/raw/master/streaming/Spark%20Structured%20Streaming%20and%20Delta%20Tables.ipynb) ke komputer lokal Anda (jika notebook dibuka sebagai file teks di browser Anda, simpan ke folder lokal; harap diingat untuk menyimpannya sebagai **Structured Streaming and Delta Tables.ipynb**, bukan sebagai file .txt)
2. Di Synapse Studio, pilih halaman **Kembangkan**.
3. Pada menu **&#65291;**, pilih **&#8612; Impor**, dan pilih file **Structured Streaming and Delta Tables.ipynb** di komputer lokal Anda.
4. Ikuti petunjuk di buku catatan untuk melampirkannya ke kumpulan Spark Anda dan menjalankan sel kode didalamnya guna mempelajari berbagai cara menggunakan Spark untuk pemrosesan aliran.

## <a name="delete-azure-resources"></a>Menghapus sumber daya Azure

> <bpt id="p1">**</bpt>Note<ept id="p1">**</ept>: If you intend to complete other exercises that use Azure Synapse Analytics, you can skip this section. Otherwise, follow the steps below to avoid unnecessary Azure costs.

1. Tutup tab browser Synapse Studio, tanpa menyimpan perubahan apa pun, dan kembali ke portal Microsoft Azure.
1. Di portal Microsoft Azure, pada halaman **Beranda**, pilih **Grup sumber daya**.
1. Pilih grup sumber daya untuk ruang kerja Synapse Analytics Anda (bukan grup sumber daya terkelola), dan verifikasi bahwa grup tersebut berisi ruang kerja Synapse, akun penyimpanan, dan kumpulan Data Explorer untuk ruang kerja Anda (jika Anda menyelesaikan latihan sebelumnya, grup tersebut juga akan berisi kumpulan Spark).
1. Di bagian atas halaman **Gambaran Umum** untuk grup sumber daya, pilih **Hapus grup sumber daya**.
1. Masukkan nama grup sumber daya untuk mengonfirmasi bahwa Anda ingin menghapusnya, dan pilih **Hapus**.

    Setelah beberapa menit, ruang kerja Azure Synapse Anda dan ruang kerja terkelola yang terkait dengannya akan dihapus.

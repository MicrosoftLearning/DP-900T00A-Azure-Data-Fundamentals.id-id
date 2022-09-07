---
lab:
  title: Menjelajahi Azure Storage
  module: Explore Azure Storage for non-relational data
---

# <a name="explore-azure-storage"></a>Menjelajahi Azure Storage

Dalam latihan ini Anda akan memprovisikan akun Azure Storage di langganan Azure, dan menjelajahi berbagai cara agar dapat menggunakannya untuk menyimpan data.

Membutuhkan waktu sekitar **15** menit untuk menyelesaikan lab ini.

## <a name="before-you-start"></a>Sebelum Anda memulai

Anda memerlukan [langganan Azure](https://azure.microsoft.com/free) dengan akses tingkat administratif.

## <a name="provision-an-azure-storage-account"></a>Memprovisikan akun Azure Storage

Langkah pertama dalam menggunakan Azure Storage adalah memprovisikan akun Azure Storage di langganan Azure Anda.

1. Jika Anda belum memprovisikannya, masuk ke [portal Microsoft Azure](https://portal.azure.com?azure-portal=true).
1. On the Azure portal home page, select <bpt id="p1">**</bpt>&amp;#65291; Create a resource<ept id="p1">**</ept> from the upper left-hand corner and search for <bpt id="p2">*</bpt>Storage account<ept id="p2">*</ept>. Then in the resulting <bpt id="p1">**</bpt>Storage account<ept id="p1">**</ept> page, select <bpt id="p2">**</bpt>Create<ept id="p2">**</ept>.
1. Masukkan nilai berikut pada halaman **Buat akun penyimpanan**:
    - <bpt id="p1">**</bpt>Subscription<ept id="p1">**</ept>: If you're using a sandbox, select <bpt id="p2">*</bpt>Concierge Subscription<ept id="p2">*</ept>. Otherwise, select your Azure subscription.
    - **Grup sumber daya**: Jika Anda menggunakan kotak pasir, pilih grup sumber daya yang ada (yang akan diberi nama seperti *learn-xxxx...* ). Jika tidak, buat grup sumber daya baru dengan nama pilihan Anda.
    - **Nama akun penyimpanan**: Masukkan nama unik untuk akun penyimpanan Anda menggunakan huruf kecil dan angka.
    - **Wilayah**: Pilih lokasi yang tersedia.
    - **Kinerja**: *Standar*
    - **Redundansi**: *Penyimpanan yang redundan secara lokal (LRS)*

1. Select <bpt id="p1">**</bpt>Next: Advanced &gt;<ept id="p1">**</ept> and view the advanced configuration options. In particular, note that this is where you can enable hierarchical namespace to support Azure Data Lake Storage Gen2. Leave this option <bpt id="p1">**</bpt><bpt id="p2">&lt;u&gt;</bpt>unselected<ept id="p2">&lt;/u&gt;</ept><ept id="p1">**</ept> (you'll enable it later), and then select <bpt id="p3">**</bpt>Next: Networking &gt;<ept id="p3">**</ept> to view the networking options for your storage account.
1. Select <bpt id="p1">**</bpt>Next: Data protection &gt;<ept id="p1">**</ept> and then in the <bpt id="p2">**</bpt>Recovery<ept id="p2">**</ept> section, <bpt id="p3">&lt;u&gt;</bpt>de<ept id="p3">&lt;/u&gt;</ept>select all of the <bpt id="p4">**</bpt>Enable soft delete...<ept id="p4">**</ept> options. These options retain deleted files for subsequent recovery, but can cause issues later when you enable hierarchical namespace.
1. Lanjutkan melalui halaman **Berikutnya >** yang ada tanpa mengubah pengaturan default apa pun, lalu pada halaman **Tinjau + Buat**, tunggu hingga pilihan Anda divalidasi dan pilih **Buat** untuk membuat akun Azure Storage.
1. Wait for deployment to complete. Then go to the resource that was deployed.

## <a name="explore-blob-storage"></a>Menjelajahi penyimpanan blob

Sekarang setelah memiliki akun Azure Storage, Anda dapat membuat kontainer untuk data blob.

1. Unduh file JSON [product1.json](https://aka.ms/product1.json?azure-portal=true) dari `https://aka.ms/product1.json` dan simpan di komputer (Anda dapat menyimpannya di folder mana pun - Anda akan mengunggahnya ke penyimpanan blob nanti).

    *Jika file JSON ditampilkan di browser Anda, simpan halaman sebagai **product1.json**.*

1. Di halaman portal Azure untuk kontainer penyimpanan Anda, di sisi kiri, pada bagian **Penyimpanan data**, pilih **Kontainer**.
1. Di halaman **Kontainer**, pilih **&#65291; Kontainer** dan tambahkan kontainer baru bernama **data** dengan tingkat akses publik **Privat (tanpa akses anonim)** .
1. Setelah kontainer **data** dibuat, verifikasi bahwa kontainer tersebut tercantum di halaman **Kontainer**.
1. In the pane on the left side, in the top section, select **Storage browser **. This page provides a browser-based interface that you can use to work with the data in your storage account.
1. Di halaman browser penyimpanan, pilih **Kontainer blob** dan verifikasi bahwa kontainer **data** Anda dicantumkan.
1. Pilih kontainer **data**, dan perhatikan bahwa kontainer tersebut kosong.
1. Pilih **&#65291; Tambahkan Direktori** dan baca informasi tentang folder sebelum membuat direktori baru bernama **produk**.
1. Di penjelajah penyimpanan, verifikasi bahwa tampilan saat ini menunjukkan konten folder **produk** yang baru saja dibuat - perhatikan bahwa "breadcrumbs" di bagian atas halaman menampilkan jalur **Kontainer blob > data > produk**.
1. Di breadcrumb, pilih **data** untuk beralih ke kontainer **data**, dan perhatikan bahwa kontainer tersebut <u>tidak</u> berisi folder bernama **produk**.

    Folders in blob storage are virtual, and only exist as part of the path of a blob. Since the <bpt id="p1">**</bpt>products<ept id="p1">**</ept> folder contained no blobs, it isn't really there!

1. Gunakan tombol **&#10514; Unggah** untuk membuka panel **Unggah blob**.
1. In the <bpt id="p1">**</bpt>Upload blob<ept id="p1">**</ept> panel, select the <bpt id="p2">**</bpt>product1.json<ept id="p2">**</ept> file you saved on your local computer previously. Then in the <bpt id="p1">**</bpt>Advanced<ept id="p1">**</ept> section, in the <bpt id="p2">**</bpt>Upload to folder<ept id="p2">**</ept> box, enter <bpt id="p3">**</bpt>product_data<ept id="p3">**</ept> and select the <bpt id="p4">**</bpt>Upload<ept id="p4">**</ept> button.
1. Tutup panel **Unggah blob** jika masih terbuka, dan verifikasi bahwa folder virtual **product_data** telah dibuat di kontainer **data**.
1. Pilih folder **product_data** dan verifikasi bahwa folder tersebut berisi blob **product1.json** yang Anda unggah.
1. Di sisi kiri, di bagian **Penyimpanan data**, pilih **Kontainer**.
1. Buka kontainer **data**, dan verifikasi bahwa folder **product_data** yang Anda buat dicantumkan.
1. Select the <bpt id="p1">**</bpt>&amp;#x2027;&amp;#x2027;&amp;#x2027;<ept id="p1">**</ept> icon at the right-end of the folder, and note that it doesn't display any options. Folders in a flat namespace blob container are virtual, and can't be managed.
1. Gunakan ikon **X** di kanan atas halaman **data** untuk menutup halaman dan kembali ke halaman **Kontainer**.

## <a name="explore-azure-data-lake-storage-gen2"></a>Menjelajahi Azure Data Lake Storage Gen2

Azure Data Lake Store Gen2 support enables you to use hierarchical folders to organize and manage access to blobs. It also enables you to use Azure blob storage to host distributed file systems for common big data analytics platforms.

1. Unduh file JSON [product2.json](https://aka.ms/product2.json?azure-portal=true) dari `https://aka.ms/product2.json` dan simpan di komputer Anda di folder yang sama tempat Anda mengunduh **product1.json** sebelumnya - Anda akan mengunggahnya ke penyimpanan blob nanti ).
1. Di halaman portal Microsoft Azure untuk akun penyimpanan Anda, di sisi kiri, gulir ke bawah ke bagian **Pengaturan**, dan pilih **Peningkatan Azure Data Lake Gen2**.
1. Di beranda portal Microsoft Azure, pilih **&#65291; Buat sumber daya** dari sudut kiri atas dan cari *Akun penyimpanan*.
1. Setelah peningkatan selesai, pada panel sisi kiri, di bagian atas, pilih **Browser penyimpanan** dan navigasikan kembali ke akar kontainer blob **data** Anda, yang masih berisi folder **product_data**.
1. Pilih folder **product_data**, dan pastikan folder tersebut masih berisi file **product1.json** yang Anda unggah sebelumnya.
1. Gunakan tombol **&#10514; Unggah** untuk membuka panel **Unggah blob**.
1. Kemudian di halaman **Akun penyimpanan** yang dihasilkan, pilih **Buat**.
1. Tutup panel **Unggah blob** jika masih terbuka, dan verifikasi bahwa folder **product_data** sekarang berisi file **product2.json**.
1. Di sisi kiri, di bagian **Penyimpanan data**, pilih **Kontainer**.
1. Buka kontainer **data**, dan verifikasi bahwa folder **product_data** yang Anda buat dicantumkan.
1. Pilih ikon **&#x2027;&#x2027;&#x2027;** di ujung kanan folder, dan perhatikan bahwa saat namespace hierarkis diaktifkan, Anda dapat mengerjakan tugas konfigurasi di tingkat folder; termasuk mengganti nama folder dan mengatur izin.
1. Gunakan ikon **X** di kanan atas halaman **data** untuk menutup halaman dan kembali ke halaman **Kontainer**.

## <a name="explore-azure-files"></a>Menjelajahi Azure Files

Azure Files menyediakan cara untuk membuat berbagi berbasis cloud.

1. Di halaman portal Azure untuk kontainer penyimpanan Anda, di sisi kiri, di bagian **Penyimpanan data**, pilih **Berbagi**.
1. Di halaman Berbagi file, pilih **&#65291; Berbagi file** dan tambahkan berbagi file baru bernama **file** menggunakan tingkat **Transaksi yang dioptimalkan**.
1. Di **Berbagi**, buka **berbagi** baru Anda.
1. At the top of the page, select <bpt id="p1">**</bpt>Connect<ept id="p1">**</ept>. Then in the <bpt id="p1">**</bpt>Connect<ept id="p1">**</ept> pane, note that there are tabs for common operating systems (Windows, Linux, and macOS) that contain scripts you can run to connect to the shared folder from a client computer.
1. Tutup panel **Hubungkan** lalu tutup halaman **file** guna kembali ke halaman **Berbagi** untuk akun penyimpanan Azure Anda.

## <a name="explore-azure-tables"></a>Menjelajahi Azure Table

Azure Table menyediakan penyimpanan kunci/nilai untuk aplikasi yang perlu menyimpan nilai data, tetapi tidak memerlukan fungsionalitas dan struktur penuh dari database hubungan.

1. Di halaman portal Azure untuk kontainer penyimpanan Anda, di sisi kiri, di bagian **Penyimpanan data**, pilih **Tabel**.
1. Pada halaman **Tabel**, pilih **&#65291; Tabel** dan buat tabel baru bernama **produk**.
1. Setelah tabel **produk** dibuat, pada panel di sebelah kiri, di bagian atas, pilih **Browser penyimpanan**.
1. Di penjelajah penyimpanan, pilih **Tabel** dan verifikasi bahwa tabel **produk** dicantumkan.
1. Pilih tabel **produk**.
1. Di halaman **produk**, pilih **&#65291; Tambahkan entitas**.
1. Di panel **Tambahkan entitas**, masukkan nilai kunci berikut:
    - **PartitionKey**: 1
    - **RowKey**: 1
1. Pilih **Tambahkan properti**, dan buat properti baru dengan nilai berikut:

    |Nama properti | Jenis | Nilai |
    | ------------ | ---- | ----- |
    | Nama | String | Widget |

1. Tambahkan properti kedua dengan nilai berikut:

    |Nama properti | Jenis | Nilai |
    | ------------ | ---- | ----- |
    | Harga | Ganda | 2,99 |

1. Pilih **Sisipkan** untuk menyisipkan baris entitas baru ke dalam tabel.
1. Di browser penyimpanan, verifikasi bahwa baris telah ditambahkan ke tabel **produk**, dan kolom **Stempel waktu** telah dibuat untuk menunjukkan kapan baris terakhir diubah.
1. Tambahkan entitas lain ke tabel **produk** dengan properti berikut:

    |Nama properti | Jenis | Nilai |
    | ------------ | ---- | ----- |
    | PartitionKey | Untai (karakter) | 1 |
    | RowKey | Untai | 2 |
    | Nama | String | Kniknak |
    | Harga | Ganda | 1,99 |
    | Dihentikan | Boolean | TRUE |

1. Setelah menyisipkan entitas baru, verifikasi bahwa baris yang berisi produk yang dihentikan ditampilkan dalam tabel.

    You have manually entered data into the table using the storage browser interface. In a real scenario, application developers can use the Azure Storage Table API to build applications that read and write values to tables, making it a cost effective and scalable solution for NoSQL storage.

> **Tips**: Setelah menjelajahi Azure Storage, Anda dapat menghapus grup sumber daya yang dibuat dalam latihan ini.

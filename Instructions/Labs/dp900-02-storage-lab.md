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
1. Di beranda portal Microsoft Azure, pilih **&#65291; Buat sumber daya** dari sudut kiri atas dan cari *Akun penyimpanan*. Kemudian di halaman **Akun penyimpanan** yang dihasilkan, pilih **Buat**.
1. Masukkan nilai berikut pada halaman **Buat akun penyimpanan**:
    - **Langganan**: Pilih langganan Azure Anda.
    - **Grup sumber daya**: Buat grup sumber daya baru dengan nama pilihan Anda.
    - **Nama akun penyimpanan**: Masukkan nama unik untuk akun penyimpanan Anda menggunakan huruf kecil dan angka.
    - **Wilayah**: Pilih lokasi yang tersedia.
    - **Kinerja**: *Standar*
    - **Redundansi**: *Penyimpanan yang redundan secara lokal (LRS)*

1. Pilih **Berikutnya: Tingkat Lanjut >** dan lihat opsi konfigurasi tingkat lanjut. Secara khusus, perhatikan bahwa ini adalah tempat Anda dapat mengaktifkan namespace layanan hierarkis untuk mendukung Azure Data Lake Storage Gen2. Biarkan opsi ini tetap **<u>tidak dipilih</u>** (Anda dapat mengaktifkannya nanti), lalu pilih **Berikutnya: Jaringan >** guna menampilkan opsi jaringan untuk akun penyimpanan.
1. Pilih **Berikutnya: Perlindungan data >** , lalu di bagian **Pemulihan**, <u>batalkan</u> pilihan semua opsi **Aktifkan penghapusan sementara...** . Opsi ini mempertahankan file yang dihapus untuk pemulihan berikutnya, tetapi dapat menyebabkan masalah nanti saat Anda mengaktifkan namespace layanan hierarkis.
1. Lanjutkan melalui halaman **Berikutnya >** yang ada tanpa mengubah pengaturan default apa pun, lalu pada halaman **Tinjau + Buat**, tunggu hingga pilihan Anda divalidasi dan pilih **Buat** untuk membuat akun Azure Storage.
1. Tunggu hingga penerapan selesai. Lalu buka sumber daya yang disebarkan.

## <a name="explore-blob-storage"></a>Menjelajahi penyimpanan blob

Sekarang setelah memiliki akun Azure Storage, Anda dapat membuat kontainer untuk data blob.

1. Unduh file JSON [product1.json](https://aka.ms/product1.json?azure-portal=true) dari `https://aka.ms/product1.json` dan simpan di komputer (Anda dapat menyimpannya di folder mana pun - Anda akan mengunggahnya ke penyimpanan blob nanti).

    *Jika file JSON ditampilkan di browser Anda, simpan halaman sebagai **product1.json**.*

1. Di halaman portal Azure untuk kontainer penyimpanan Anda, di sisi kiri, pada bagian **Penyimpanan data**, pilih **Kontainer**.
1. Di halaman **Kontainer**, pilih **&#65291; Kontainer** dan tambahkan kontainer baru bernama **data** dengan tingkat akses publik **Privat (tanpa akses anonim)** .
1. Setelah kontainer **data** dibuat, verifikasi bahwa kontainer tersebut tercantum di halaman **Kontainer**.
1. Di panel sebelah kiri, di bagian atas, pilih **Browser penyimpanan**. Halaman ini menyediakan antarmuka berbasis browser yang dapat Anda gunakan untuk bekerja dengan data di akun penyimpanan.
1. Di halaman browser penyimpanan, pilih **Kontainer blob** dan verifikasi bahwa kontainer **data** Anda dicantumkan.
1. Pilih kontainer **data**, dan perhatikan bahwa kontainer tersebut kosong.
1. Pilih **&#65291; Tambahkan Direktori** dan baca informasi tentang folder sebelum membuat direktori baru bernama **produk**.
1. Di browser penyimpanan, verifikasi bahwa tampilan saat ini menunjukkan konten folder **produk** yang baru saja dibuat - perhatikan bahwa "breadcrumbs" di bagian atas halaman menampilkan jalur **Kontainer blob > data > produk**.
1. Di breadcrumb, pilih **data** untuk beralih ke kontainer **data**, dan perhatikan bahwa kontainer tersebut <u>tidak</u> berisi folder bernama **produk**.

    Folder dalam penyimpanan blob adalah virtual, dan hanya ada sebagai bagian dari jalur blob. Karena folder **produk** tidak berisi blob, itu tidak benar-benar ada!

1. Gunakan tombol **&#10514; Unggah** untuk membuka panel **Unggah blob**.
1. Di panel **Unggah blob**, pilih file **product1.json** yang sebelumnya Anda simpan di komputer lokal. Kemudian di bagian **Tingkat Lanjut**, di kotak **Unggah ke folder**, masukkan **product_data** dan pilih tombol **Unggah**.
1. Tutup panel **Unggah blob** jika masih terbuka, dan verifikasi bahwa folder virtual **product_data** telah dibuat di kontainer **data**.
1. Pilih folder **product_data** dan verifikasi bahwa folder tersebut berisi blob **product1.json** yang Anda unggah.
1. Di sisi kiri, di bagian **Penyimpanan data**, pilih **Kontainer**.
1. Buka kontainer **data**, dan verifikasi bahwa folder **product_data** yang Anda buat dicantumkan.
1. Pilih ikon **&#x2027;&#x2027;&#x2027;** di ujung kanan folder, dan perhatikan bahwa ikon tersebut tidak menampilkan opsi sama sekali. Folder dalam kontainer blob namespace datar bersifat virtual, serta tidak dapat dikelola.
1. Gunakan ikon **X** di kanan atas halaman **data** untuk menutup halaman dan kembali ke halaman **Kontainer**.

## <a name="explore-azure-data-lake-storage-gen2"></a>Menjelajahi Azure Data Lake Storage Gen2

Dukungan Azure Data Lake Store Gen2 memungkinkan Anda menggunakan folder hierarkis untuk mengatur dan mengelola akses ke blob. Ini juga memungkinkan Anda menggunakan penyimpanan blob Azure untuk menghosting sistem file terdistribusi untuk platform analitik big data yang umum.

1. Unduh file JSON [product2.json](https://aka.ms/product2.json?azure-portal=true) dari `https://aka.ms/product2.json` dan simpan di komputer Anda di folder yang sama tempat Anda mengunduh **product1.json** sebelumnya - Anda akan mengunggahnya ke penyimpanan blob nanti ).
1. Di halaman portal Microsoft Azure untuk akun penyimpanan Anda, di sisi kiri, gulir ke bawah ke bagian **Pengaturan**, dan pilih **Peningkatan Azure Data Lake Gen2**.
1. Di halaman ****Peningkatan Azure Data Lake Gen2****, perluas dan selesaikan setiap langkah untuk meningkatkan akun penyimpanan Anda guna mengaktifkan namespace hierarkis dan mendukung Azure Data Lake Storage Gen 2. Ini mungkin memakan waktu.
1. Setelah peningkatan selesai, pada panel sisi kiri, di bagian atas, pilih **Browser penyimpanan** dan navigasikan kembali ke akar kontainer blob **data** Anda, yang masih berisi folder **product_data**.
1. Pilih folder **product_data**, dan pastikan folder tersebut masih berisi file **product1.json** yang Anda unggah sebelumnya.
1. Gunakan tombol **&#10514; Unggah** untuk membuka panel **Unggah blob**.
1. Di panel **Unggah blob**, pilih file **product2.json** yang Anda simpan di komputer lokal. Kemudian pilih tombol **Unggah**.
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
1. Di bagian atas halaman, pilih **Hubungkan**. Kemudian di panel **Hubungkan**, perhatikan bahwa ada tab untuk sistem operasi umum (Windows, Linux, dan macOS) yang berisi skrip yang dapat Anda jalankan untuk menghubungkan ke folder bersama dari komputer klien.
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
    | RowKey | Untai | 2. |
    | Nama | String | Kniknak |
    | Harga | Ganda | 1,99 |
    | Dihentikan | Boolean | TRUE |

1. Setelah menyisipkan entitas baru, verifikasi bahwa baris yang berisi produk yang dihentikan ditampilkan dalam tabel.

    Anda telah memasukkan data secara manual ke dalam tabel menggunakan antarmuka browser penyimpanan. Dalam skenario nyata, pengembang aplikasi dapat menggunakan Azure Storage Table API untuk membangun aplikasi yang membaca dan menulis nilai ke tabel, menjadikannya solusi yang hemat biaya dan scalable untuk penyimpanan NoSQL.

> **Tips**: Setelah menjelajahi Azure Storage, Anda dapat menghapus grup sumber daya yang dibuat dalam latihan ini.

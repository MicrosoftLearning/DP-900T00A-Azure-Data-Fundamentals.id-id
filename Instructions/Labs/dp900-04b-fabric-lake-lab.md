---
lab:
  title: Menjelajahi analitik data di Microsoft Fabric
  module: Explore fundamentals of large-scale data analytics
---

# Menjelajahi analitik data di Microsoft Fabric

Dalam latihan ini Anda akan menjelajahi penyerapan dan analitik data di Microsoft Fabric Lakehouse.

Membutuhkan waktu sekitar **25** menit untuk menyelesaikan lab ini.

> **Catatan**: Anda memerlukan lisensi Microsoft Fabric untuk menyelesaikan latihan ini. Lihat [Mulai menggunakan Fabric](https://learn.microsoft.com/fabric/get-started/fabric-trial) untuk detail cara mengaktifkan lisensi uji coba Fabric gratis. Anda akan memerlukan akun *sekolah*atau *kerja* Microsoft untuk melakukan ini. Jika Anda tidak memilikinya, Anda bisa [mendaftar untuk uji coba Microsoft Office 365 E3 atau yang lebih tinggi](https://www.microsoft.com/microsoft-365/business/compare-more-office-365-for-business-plans).

*Pertama kali Anda menggunakan fitur Microsoft Fabric apa pun, perintah dengan tips mungkin muncul. Tutup ini.*

## Membuat ruang kerja

Sebelum mengerjakan data di Fabric, buat ruang kerja dengan uji coba Fabric diaktifkan.

1. Masuk ke [Microsoft Fabric](https://app.fabric.microsoft.com) di `https://app.fabric.microsoft.com`.
1. Di bilah menu, di kiri bawah, beralihlah ke **pengalaman Rekayasa Data**.

    ![Cuplikan layar menu pengalih pengalaman.](./images/fabric-switcher.png)

1. Pada bilah menu di sebelah kiri, pilih **Ruang Kerja** (ikon terlihat mirip dengan ).
1. Buat ruang kerja baru dengan nama pilihan Anda, pilih mode lisensi di bagian **Tingkat Lanjut** yang mencakup kapasitas Fabric (*Uji Coba*, *Premium*, atau *Fabric*).
1. Saat ruang kerja baru Anda terbuka, ruang kerja harus kosong.

    ![Cuplikan layar ruang kerja kosong di Power BI.](./images/new-workspace.png)

## Membuat lakehouse

Sekarang setelah Anda memiliki ruang kerja, saatnya untuk membuat data lakehouse untuk file data Anda.

1. Di beranda ruang kerja, buat Lakehouse** baru **dengan nama pilihan Anda.

    Setelah satu menit atau lebih, lakehouse baru akan dibuat:

    ![Cuplikan layar lakehouse baru.](./images/new-lakehouse.png)

1. Lihat lakehouse baru, dan perhatikan bahwa panel **Penjelajah lakehouse** di sebelah kiri memungkinkan Anda menelusuri tabel dan file di lakehouse:
    - Folder **Tabel** berisi tabel yang bisa Anda kueri menggunakan SQL. Tabel di lakehouse Microsoft Fabric didasarkan pada format file *Delta Lake* sumber terbuka, yang umum digunakan dalam Apache Spark.
    - Folder **File** berisi file data di penyimpanan OneLake untuk lakehouse yang tidak terkait dengan tabel delta terkelola. Anda juga dapat membuat *pintasan* di folder ini untuk mereferensikan data yang disimpan secara eksternal.

    Saat ini, tidak ada tabel atau file di lakehouse.

## Menyerap data

Cara sederhana untuk menyerap data adalah dengan menggunakan aktivitas **Salin Data** dalam alur untuk mengekstrak data dari sumber dan menyalinnya ke file di lakehouse.

1. Pada halaman **Beranda** untuk lakehouse Anda, di **menu Dapatkan data** , pilih **Alur** data baru, dan buat alur data baru bernama **Ingest Data**.
1. **Di wizard Salin Data**, pada **halaman Pilih sumber** data, pilih **Sampel data** lalu pilih **himpunan data sampel Taksi - Hijau** NYC.

    ![Cuplikan layar halaman Pilih sumber data.](./images/choose-data-source.png)

1. Pada halaman **Sambungkan ke sumber** data, lihat tabel di sumber data. Harus ada satu meja yang berisi detail perjalanan taksi di New York City. Lalu pilih **Berikutnya** untuk melanjutkan ke halaman **Pilih tujuan data**.
1. Pada halaman **Pilih tujuan data**, pilih lakehouse Anda yang sudah ada. Kemudian pilih **Berikutnya**.
1. Atur opsi tujuan data berikut, lalu pilih **Berikutnya**:
    - **Folder akar**: Tabel
    - **Memuat pengaturan**: Muat ke tabel baru
    - **Nama** tabel tujuan: taxi_rides *(Anda mungkin perlu menunggu pratinjau pemetaan kolom ditampilkan sebelum Anda dapat mengubahnya)*
    - **Pemetaan kolom**: *Biarkan pemetaan default apa adanya*
    - **Aktifkan partisi**: *Tidak dipilih*
1. Pada halaman **Tinjau + simpan** , pastikan bahwa opsi **Mulai transfer data segera** dipilih, lalu pilih **Simpan + Jalankan**.

    Alur baru yang berisi aktivitas **Salin Data **dibuat, seperti yang ditunjukkan di sini:

    ![Cuplikan layar alur dengan aktivitas Salin Data.](./images/copy-data-pipeline.png)

    Saat alur mulai berjalan, Anda dapat memantau statusnya di panel **Output** di bawah perancang alur. **Gunakan ikon &#8635;** (*Refresh) untuk menyegarkan* status, dan tunggu hingga berhasil (yang mungkin memakan waktu 10 menit atau lebih).

1. Di bilah menu hub di sebelah kiri, pilih lakehouse Anda.
1. Pada halaman **Beranda** , di **panel penjelajah** Lakehouse, di **menu ...** untuk simpul **Tabel** , pilih **Refresh** lalu perluas **Tabel** untuk memverifikasi bahwa **tabel taxi_rides** telah dibuat.

    > **Catatan**: Jika tabel baru tercantum sebagai *tidak* dikenal, gunakan **opsi menu Refresh** untuk me-refresh tampilan.

1. **Pilih tabel taxi_rides** untuk menampilkan kontennya.

    ![Cuplikan layar tabel taxi_rides.](./images/dimProduct.png)

## Melakukan kueri data di lakehouse

Sekarang setelah Anda menyerap data ke dalam tabel di lakehouse, Anda dapat menggunakan SQL untuk melakukan kueri.

1. Di kanan atas halaman Lakehouse, beralihlah dari **tampilan Lakehouse** ke **titik** akhir analitik SQL untuk lakehouse Anda.

1. Di bilah toolbar, pilih **Kueri SQL Baru**. Masukkan kode SQL berikut ke dalam editor kueri:

    ```sql
    SELECT  DATENAME(dw,lpepPickupDatetime) AS Day,
            AVG(tripDistance) As AvgDistance
    FROM taxi_rides
    GROUP BY DATENAME(dw,lpepPickupDatetime)
    ```

1. **Pilih &#9655; Tombol Jalankan** untuk menjalankan kueri dan meninjau hasilnya, yang harus menyertakan jarak perjalanan rata-rata untuk setiap hari dalam seminggu.

    ![Cuplikan layar kueri SQL.](./images/sql-query.png)

## Memvisualisasikan data di lakehouse

Lakehouse Microsoft Fabric mengatur semua tabel dalam model data semantik, yang dapat Anda gunakan untuk membuat visualisasi dan laporan.

1. Di kiri bawah halaman, di bawah panel **Explorer** , pilih tab **Model** untuk melihat model data untuk tabel di lakehouse (ini termasuk tabel sistem serta **tabel taxi_rides** ).
1. Di toolbar, pilih **Laporan** baru untuk membuat laporan baru berdasarkan **taxi_rides**.
1. Di perancang laporan:
    1. Di panel **Data** , perluas **tabel taxi_rides** dan pilih **bidang lpepPickupDatetime** dan **passengerCount** .
    1. Di panel **Visualisasi**, pilih visualisasi Bagan garis****. Kemudian pastikan sumbu **** X berisi **bidang lpepPickupDatetime** dan **sumbu Y** berisi **Jumlah passengerCount**.

        ![Cuplikan layar laporan Power BI.](./images/fabric-report.png)

    > **Tips**: Anda dapat menggunakan ikon **>>** untuk menyembunyikan panel perancang laporan untuk melihat laporan dengan lebih jelas.

1. Pada menu **File** , pilih **Simpan** untuk menyimpan laporan sebagai **Laporan** Naik Taksi di ruang kerja Fabric Anda.

    Anda sekarang dapat menutup tab browser yang berisi laporan untuk kembali ke lakehouse Anda. Anda dapat menemukan laporan di halaman untuk ruang kerja Anda di portal Microsoft Fabric.

## Membersihkan sumber daya

Jika Anda telah selesai menjelajahi Microsoft Fabric, Anda dapat menghapus ruang kerja yang Anda buat untuk latihan ini.

1. Di bilah di sebelah kiri, pilih ikon untuk ruang kerja Anda untuk melihat semua item yang ada di dalamnya.
2. Di menu **...** pada toolbar, pilih **Pengaturan ruang kerja**.
3. Di bagian **Lainnya** , pilih **Hapus ruang kerja ini**.

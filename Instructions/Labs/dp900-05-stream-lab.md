---
lab:
  title: Mempelajari Azure Stream Analytics
  module: Explore fundamentals of real-time analytics
---

# <a name="explore-azure-stream-analytics"></a>Mempelajari Azure Stream Analytics

Dalam latihan ini, Anda akan memprovisikan pekerjaan Azure Stream Analytics di langganan Azure Anda, dan menggunakannya untuk memproses aliran data real-time.

Membutuhkan waktu sekitar **15** menit untuk menyelesaikan lab ini.

## <a name="before-you-start"></a>Sebelum Anda memulai

Anda memerlukan [langganan Azure](https://azure.microsoft.com/free) dengan akses tingkat administratif.

## <a name="create-azure-resources"></a>Membuat sumber daya Azure

1. Masuk ke langganan Azure di [portal Microsoft Azure](https://portal.azure.com), menggunakan kredensial langganan Azure Anda.

1. Gunakan tombol **[\>_]** di sebelah kanan bilah pencarian di bagian atas halaman untuk membuat Cloud Shell baru di portal Azure, dengan memilih lingkungan ***Bash*** dan membuat penyimpanan jika diminta. Shell cloud menyediakan antarmuka baris perintah di panel di bagian bawah portal Azure, seperti yang ditunjukkan di sini:

    ![Portal Azure dengan panel cloud shell](./images/cloud-shell.png)

1. Di Azure Cloud Shell, masukkan perintah berikut untuk mengunduh file yang Anda perlukan untuk latihan ini.

    ```bash
    git clone https://github.com/MicrosoftLearning/DP-900T00A-Azure-Data-Fundamentals dp-900
    ```

1. Tunggu hingga perintah selesai, lalu masukkan perintah berikut untuk mengubah direktori saat ini ke folder yang berisi file untuk latihan ini.

    ```bash
    cd dp-900/streaming
    ```

1. Masukkan perintah berikut untuk menjalankan skrip yang membuat sumber daya Azure yang Anda perlukan dalam latihan ini.

    ```bash
    bash setup.sh
    ```

    Tunggu selagi skrip berjalan dan lakukan tindakan berikut:

    1. Menginstal ekstensi Azure CLI yang diperlukan untuk membuat sumber daya (*Anda dapat mengabaikan peringatan apa pun tentang ekstensi eksperimental*)
    1. Mengidentifikasi grup sumber daya Azure yang disediakan untuk latihan ini.
    1. Membuat sumber daya *Azure IoT Hub*, yang akan digunakan untuk menerima aliran data dari perangkat simulasi.
    1. Membuat *Akun Azure Storage*, yang akan digunakan untuk menyimpan data yang diproses.
    1. Membuat pekerjaan *Azure Stream Analytics*, yang akan memproses data perangkat yang masuk secara real time, dan menulis hasilnya ke akun penyimpanan.

## <a name="explore-the-azure-resources"></a>Mempelajari sumber daya Azure

1. Di [portal Microsoft Azure](https://portal.azure.com?azure-portal=true), di beranda, pilih **Grup sumber daya** untuk melihat grup sumber daya dalam langganan Anda. Grup ini harus menyertakan **learn*xxxxxxxxxxxxxxxxxx...** * grup sumber daya yang diidentifikasi oleh skrip penyiapan.
2. Pilih **learn*xxxxxxxxxxxxxxxxxx...** * grup sumber daya, dan tinjau sumber daya di dalamnya, yang harus menyertakan:
    - *IoT Hub* bernama **iothub*xxxxxxxxxxxxx***, yang digunakan untuk menerima data perangkat yang masuk.
    - *Akun penyimpanan* bernama **store*xxxxxxxxxxxx***, tempat hasil pemrosesan data akan ditulis.
    - *Pekerjaan Azure Stream Analytics* bernama **stream*xxxxxxxxxxxxx***, yang akan digunakan untuk memproses data aliran.

    Jika ketiga sumber ini tidak tercantum, klik tombol **&#8635; Refresh** hingga sumber muncul.

    > **Catatan**: Jika Anda menggunakan kotak pasir Microsoft learn, grup sumber daya juga dapat berisi *Akun penyimpanan* kedua bernama **cloudshell*xxxxxxxxx***, yang digunakan untuk menyimpan data untuk Azure Cloud Shell yang digunakan untuk menjalankan skrip penyiapan.

3. Pilih pekerjaan Azure Stream Analytics **stream*xxxxxxxxxxxxx*** dan lihat informasinya di halaman **Ringkasan**, dengan memperhatikan detail berikut:
    - Pekerjaan memiliki satu *input* bernama **iotinput**, dan satu *output* bernama **bloboutput**. Ini merujuk pada IoT Hub dan akun Penyimpanan yang dibuat oleh skrip penyiapan.
    - Pekerjaan memiliki *kueri*, yang membaca data dari input **iotinput**, dan menggabungkannya dengan menghitung jumlah pesan yang diproses setiap 10 detik; menulis hasilnya ke output **bloboutput**.

## <a name="use-the-resources-to-analyze-streaming-data"></a>Gunakan sumber daya untuk menganalisis data aliran

1. Di bagian atas halaman **Ringkasan** untuk pekerjaan Azure Stream Analytics, pilih opsi **&#9655; Mulai**, lalu di panel **Mulai pekerjaan**, pilih **Mulai** untuk memulai pekerjaan.
2. Tunggu pemberitahuan bahwa pekerjaan aliran berhasil dimulai.
3. Kembali ke Azure Cloud Shell, dan masukkan perintah berikut untuk mensimulasikan perangkat yang mengirim data ke IoT Hub.

    ```
    bash iotdevice.sh
    ```

4. Tunggu simulasi hingga memulai, yang akan ditunjukkan oleh output seperti ini:

    ```
    Device simulation in progress: 6%|#    | 7/120 [00:08<02:21, 1.26s/it]
    ```

5. Saat simulasi sedang berjalan, kembali ke portal Microsoft Azure, dan kembali ke halaman untuk grup sumber daya **learn*xxxxxxxxxxxxxxxxxx...** *, dan pilih akun penyimpanan **store*xxxxxxxxxxxx***.
6. Di panel di sebelah kiri panel akun penyimpanan, pilih tab **Kontainer**.
7. Buka kontainer **data**.
8. Dalam kontainer **data**, navigasikan melalui hierarki folder, yang mencakup folder untuk tahun ini, dengan subfolder untuk bulan, hari, dan jam.
9. Dalam folder jam, pilih file yang telah dibuat, yang memiliki nama mirip dengan **0_xxxxxxxxxxxxxxxx.json**.
10. Pada halaman file, pilih **Edit**, dan tinjau konten file; yang harus terdiri dari catatan JSON untuk setiap periode 10 detik, menunjukkan jumlah pesan yang diterima dari perangkat IoT, seperti ini:

    ```
    {"starttime":"2021-10-23T01:02:13.2221657Z","endtime":"2021-10-23T01:02:23.2221657Z","device":"iotdevice","messages":2}
    {"starttime":"2021-10-23T01:02:14.5366678Z","endtime":"2021-10-23T01:02:24.5366678Z","device":"iotdevice","messages":3}
    {"starttime":"2021-10-23T01:02:15.7413754Z","endtime":"2021-10-23T01:02:25.7413754Z","device":"iotdevice","messages":4}
    ...
    ```

11. Gunakan **&#8635; Refresh** untuk merefresh file, dengan mencatat bahwa hasil tambahan ditulis ke file saat pekerjaan Azure Stream Analytics memproses data perangkat secara real time saat dialirkan dari perangkat ke IoT Hub.
12. Kembali ke Azure Cloud Shell dan tunggu simulasi perangkat selesai (harus berjalan sekitar 3 menit).
13. Kembali ke portal Microsoft Azure, refresh file sekali lagi untuk melihat hasil lengkap yang dihasilkan selama simulasi.
14. Kembali ke grup sumber daya **learn*xxxxxxxxxxxxxxxxxx...** *, dan buka kembali pekerjaan Azure Stream Analytics **stream*xxxxxxxxxxxxx***.
15. Di bagian atas halaman pekerjaan Azure Stream Analytics, gunakan **&#11036; Tombol Berhenti** untuk menghentikan pekerjaan, mengonfirmasi saat diminta.

> **Catatan**: Jika Anda telah selesai menjelajahi solusi streaming, hapus grup sumber daya yang dibuat dalam latihan ini.

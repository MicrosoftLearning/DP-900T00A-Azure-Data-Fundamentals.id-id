---
lab:
  title: Menjelajahi dasar-dasar visualisasi data dengan Power BI
  module: Explore fundamentals of data visualization
---

# <a name="explore-fundamentals-of-data-visualization-with-power-bi"></a>Menjelajahi dasar-dasar visualisasi data dengan Power BI

Dalam latihan ini Anda akan menggunakan Microsoft Power BI Desktop untuk membuat model data dan laporan yang berisi visualisasi data interaktif.

Membutuhkan waktu sekitar **20** menit untuk menyelesaikan lab ini.

## <a name="before-you-start"></a>Sebelum Anda memulai

Anda memerlukan [langganan Azure](https://azure.microsoft.com/free) dengan akses tingkat administratif.

### <a name="install-power-bi-desktop"></a>Menginstal Power BI Desktop

Jika Microsoft Power BI Desktop belum terinstal di komputer Windows, Anda dapat mengunduh dan menginstalnya secara gratis.

1. Unduh penginstal Power BI Desktop dari [https://aka.ms/power-bi-desktop](https://aka.ms/power-bi-desktop?azure-portal=true).
1. When the file has downloaded, open it, and use the setup wizard to install Power BI Desktop on your computer. This insatllation may take a few minutes.

## <a name="import-data"></a>Impor data

1. Open Power BI Desktop. The application interface should look similar to this:

    ![Cuplikan layar yang menunjukkan beranda Power BI Desktop.](images/power-bi-start.png)

    Sekarang Anda siap mengimpor data untuk laporan Anda.

1. Pada layar selamat datang Power BI Desktop, pilih **Dapatkan data**, lalu dalam daftar sumber data, pilih **Web** lalu pilih **Hubungkan**.

    ![Cuplikan layar yang menunjukkan cara memilih sumber data web di Power BI.](images/web-source.png)

1. Di kotak dialog **Dari web**, masukkan URL berikut, lalu pilih **OK**:

    ```
    https://github.com/MicrosoftLearning/DP-900T00A-Azure-Data-Fundamentals/raw/master/power-bi/customers.csv
    ```

1. Di dialog konten Access Web, pilih **Hubungkan**.

1. Verify that the URL opens a dataset containing customer data, as shown below. Then select <bpt id="p1">**</bpt>Load<ept id="p1">**</ept> to load the data into the data model for your report.

    ![Cuplikan layar yang menunjukkan himpunan data pelanggan yang ditampilkan di Power BI.](images/customers.png)

1. Di jendela utama Power BI Desktop, di menu Data, pilih **Dapatkan data**, lalu pilih **Web**:

    ![Cuplikan layar yang menunjukkan menu Dapatkan data di Power BI.](images/get-data.png)

1. Di kotak dialog **Dari web**, masukkan URL berikut, lalu pilih **OK**:

    ```
    https://github.com/MicrosoftLearning/DP-900T00A-Azure-Data-Fundamentals/raw/master/power-bi/products.csv
    ```

1. Di dialog, pilih **Muat** untuk memuat data produk dalam file ini ke dalam model data.

1. Ulangi tiga langkah sebelumnya untuk mengimpor himpunan data ketiga yang berisi data pesanan dari URL berikut:

    ```
    https://github.com/MicrosoftLearning/DP-900T00A-Azure-Data-Fundamentals/raw/master/power-bi/orders.csv
    ```

## <a name="explore-a-data-model"></a>Menjelajahi model data

Tiga tabel data yang telah Anda impor telah dimuat ke dalam model data, yang sekarang akan Anda jelajahi dan perbaiki.

1. In Power BI Desktop, on the left-side edge, select the <bpt id="p1">**</bpt>Model<ept id="p1">**</ept> tab, and then arrange the tables in the model so you can see them. You can hide the panes on the right side by using the <bpt id="p1">**</bpt><ph id="ph1">&gt;&gt;</ph><ept id="p1">**</ept> icons:

    ![Cuplikan layar yang menunjukkan tab Model di Power BI.](images/model-tab.png)

1. Di tabel **pesanan**, pilih bidang **Pendapatan**, lalu di panel **Properti**, atur properti **Format** ke **Mata Uang**:

    ![Cuplikan layar yang menunjukkan cara mengatur format Pendapatan ke Mata Uang di Power BI.](images/revenue-currency.png)

    Langkah ini dapat memastikan bahwa nilai pendapatan ditampilkan sebagai mata uang dalam visualisasi laporan.

1. In the products table, right-click the <bpt id="p1">**</bpt>Category<ept id="p1">**</ept> field (or open its <bpt id="p2">**</bpt><ph id="ph1">&amp;vellip;</ph><ept id="p2">**</ept> menu) and select <bpt id="p3">**</bpt>Create hierarchy<ept id="p3">**</ept>. This step creates a hierarchy named <bpt id="p1">**</bpt>Category Hierarchy<ept id="p1">**</ept>. You may need to expand or scroll in the <bpt id="p1">**</bpt>products<ept id="p1">**</ept> table to see this - you can also see it in the <bpt id="p2">**</bpt>Fields<ept id="p2">**</ept> pane:

    ![Cuplikan layar yang menunjukkan cara menambahkan Hierarki Kategori di Power BI.](images/category-hierarchy.png)

1. In the products table, right-click the <bpt id="p1">**</bpt>ProductName<ept id="p1">**</ept> field (or open its <bpt id="p2">**</bpt><ph id="ph1">&amp;vellip;</ph><ept id="p2">**</ept> menu) and select <bpt id="p3">**</bpt>Add to hierarchy<ept id="p3">**</ept><ph id="ph2"> &gt; </ph><bpt id="p4">**</bpt>Category Hierarchy<ept id="p4">**</ept>. This adds the <bpt id="p1">**</bpt>ProductName<ept id="p1">**</ept> field to the hierarchy you created previously.
1. In the <bpt id="p1">**</bpt>Fields<ept id="p1">**</ept> pane, right-click <bpt id="p2">**</bpt>Category Hierarchy<ept id="p2">**</ept> (or open its <bpt id="p3">**</bpt>...<ept id="p3">**</ept> menu) and select <bpt id="p4">**</bpt>Rename<ept id="p4">**</ept>. Then rename the hierarchy to <bpt id="p1">**</bpt>Categorized Product<ept id="p1">**</ept>.

    ![Cuplikan layar yang menunjukkan cara mengganti nama hierarki di Power BI.](images/rename-hierarchy.png)

1. Di tepi kiri, pilih tab **Data**, lalu di panel **Bidang**, pilih tabel **pelanggan**.
1. Pilih header kolom **Kota**, lalu atur properti **Kategori Data** ke **Kota**:

    ![Cuplikan layar yang menunjukkan cara mengatur kategori data di Power BI.](images/data-category.png)

    Langkah ini dapat memastikan bahwa nilai dalam kolom ini diinterpretasikan sebagai nama kota, yang berguna jika Anda ingin menyertakan visualisasi peta.

## <a name="create-a-report"></a>Membuat laporan

Now you're almost ready to create a report. First you need to check some settings to ensure all visualizations are enabled.

1. On the <bpt id="p1">**</bpt>File<ept id="p1">**</ept> menu, select <bpt id="p2">**</bpt>Options and Settings<ept id="p2">**</ept>. Then select <bpt id="p1">**</bpt>Options<ept id="p1">**</ept>, and in the <bpt id="p2">**</bpt>Security<ept id="p2">**</ept> section, ensure that <bpt id="p3">**</bpt>Use Map and Filled Map visuals<ept id="p3">**</ept> is enabled and select <bpt id="p4">**</bpt>OK<ept id="p4">**</ept>.

    ![Cuplikan layar yang menunjukkan cara mengatur properti visual Gunakan Peta dan Peta Terisi di PowerBI.](images/set-options.png)

    Pengaturan ini memastikan bahwa Anda dapat menyertakan visualisasi peta dalam laporan.

1. Di tepi kiri, pilih tab **Laporan** dan lihat antarmuka desain laporan.

    ![Cuplikan layar yang menunjukkan tab laporan di Power BI.](images/report-tab.png)

1. In the ribbon, above the report design surface, select <bpt id="p1">**</bpt>Text Box<ept id="p1">**</ept> and add a text box containing the text <bpt id="p2">**</bpt>Sales Report<ept id="p2">**</ept> to the report. Format the text to make it bold with a font size of 32.

    ![Cuplikan layar yang menunjukkan cara menambahkan kotak teks di Power BI.](images/text-box.png)

1. Ketika file telah diunduh, buka, dan gunakan wizard penyiapan untuk menginstal Power BI Desktop di komputer Anda.

    ![Cuplikan layar yang menunjukkan cara menambahkan tabel produk yang dikategorikan ke laporan di Power BI.](images/categorized-products-table.png)

1. Penginstalan ini mungkin membutuhkan waktu beberapa menit.

    The revenue is formatted as currency, as you specified in the model. However, you didn't specify the number of decimal places, so the values include fractional amounts. It won't matter for the visualizations you're going to create, but you could go back to the <bpt id="p1">**</bpt>Model<ept id="p1">**</ept> or <bpt id="p2">**</bpt>Data<ept id="p2">**</ept> tab and change the decimal places if you wish.

    ![Cuplikan layar yang menunjukkan tabel produk yang dikategorikan dengan pendapatan dalam laporan.](images/revenue-column.png)

1. With the table still selected, in the <bpt id="p1">**</bpt>Visualizations<ept id="p1">**</ept> pane, select the <bpt id="p2">**</bpt>Stacked column chart<ept id="p2">**</ept> visualization. The table is changed to a column chart showing revenue by category.

    ![Cuplikan layar yang menunjukkan bagan kolom bertumpuk dari produk yang dikategorikan dengan pendapatan dalam laporan.](images/stacked-column-chart.png)

1. Buka Power BI Desktop.

    ![Cuplikan layar yang menunjukkan bagan kolom penelusuran mendetail untuk melihat produk dalam kategori.](images/drill-down.png)

1. Antarmuka aplikasi akan terlihat seperti ini:
1. Select a blank area of the report, and then in the <bpt id="p1">**</bpt>Fields<ept id="p1">**</ept> pane, select the <bpt id="p2">**</bpt>Quantity<ept id="p2">**</ept> field in the <bpt id="p3">**</bpt>orders<ept id="p3">**</ept> table and the <bpt id="p4">**</bpt>Category<ept id="p4">**</ept> field in the <bpt id="p5">**</bpt>products<ept id="p5">**</ept> table. This step results in another column chart showing sales quantity by product category.
1. Dengan bagan kolom baru yang dipilih, di panel **Visualisasi**, pilih **Bagan pai** lalu ubah ukuran bagan dan posisikan di sebelah bagan kolom pendapatan berdasarkan kategori.

    ![Cuplikan layar yang menampilkan diagram lingkaran yang menunjukkan kuantitas penjualan berdasarkan kategori.](images/category-pie-chart.png)

1. Select a blank area of the report, and then in the <bpt id="p1">**</bpt>Fields<ept id="p1">**</ept> pane, select the <bpt id="p2">**</bpt>City<ept id="p2">**</ept> field in the <bpt id="p3">**</bpt>customers<ept id="p3">**</ept> table and then select the <bpt id="p4">**</bpt>Revenue<ept id="p4">**</ept> field in the <bpt id="p5">**</bpt>orders<ept id="p5">**</ept> table. This results in a map showing sales revenue by city. Rearrange and resize the visualizations as needed:

    ![Cuplikan layar peta yang menunjukkan pendapatan berdasarkan kota.](images/revenue-map.png)

1. In the map, note that you can drag, double-click, use a mouse-wheel, or pinch and drag on a touch screen to interact. Then select a specific city, and note that the other visualizations in the report are modified to highlight the data for the selected city.

    ![Cuplikan layar peta yang menunjukkan pendapatan berdasarkan kota dan berfokus pada data kota yang dipilih.](images/selected-data.png)

1. On the <bpt id="p1">**</bpt>File<ept id="p1">**</ept> menu, select <bpt id="p2">**</bpt>Save<ept id="p2">**</ept>. Then save the file with an appropriate .pbix file name. You can open the file and explore data modeling and visualization further at your leisure.

Jika Anda memiliki langganan [layanan Power BI](https://www.powerbi.com/?azure-portal=true), Anda dapat masuk ke akun dan menerbitkan laporan ke ruang kerja Power BI. 

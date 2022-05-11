---
lab:
  title: Mempelajari Azure Stream Analytics
  module: Explore data analytics in Azure
ms.openlocfilehash: 925607333098d0774839d705d4e055a78e32de27
ms.sourcegitcommit: e73a39e323ef061919b58561ff1afdca876ad2b5
ms.translationtype: HT
ms.contentlocale: id-ID
ms.lasthandoff: 04/07/2022
ms.locfileid: "141493691"
---
## <a name="explore-azure-stream-analytics"></a>Mempelajari Azure Stream Analytics

Dalam latihan ini, Anda akan memprovisikan pekerjaan Azure Stream Analytics di langganan Azure Anda, dan menggunakannya untuk memproses aliran data real-time.

> **Catatan**: Latihan ini merupakan bagian dari modul di Microsoft Learn, dan mencakup opsi untuk menggunakan langganan Azure *kotak pasir*. Namun, jika Anda menyelesaikan latihan ini sebagai bagian dari kelas yang dipandu instruktur, Anda harus menggunakan langganan Azure yang disediakan sebagai bagian dari kelas, bukan kotak pasir.

Sebelum memulai latihan di Microsoft Learn, Anda harus menyiapkan lingkungan cloud shell untuk langganan Azure Anda.

1. Masuk ke langganan Azure Anda di [portal Azure](https://portal.azure.com) di `https://portal.azure.com`, menggunakan info masuk langganan Azure Anda.
2. Gunakan tombol **[\>_]** di sebelah kanan bilah pencarian di bagian atas halaman untuk membuat Cloud Shell baru di portal Azure, dengan memilih lingkungan **_Bash_** dan membuat penyimpanan jika diminta. Shell cloud menyediakan antarmuka baris perintah di panel di bagian bawah portal Azure, seperti yang ditunjukkan di sini:

    ![Portal Azure dengan panel cloud shell](./images/cloud-shell.png)

3. Perhatikan bahwa Anda dapat mengubah ukuran cloud shell dengan menyeret bilah pemisah di bagian atas panel, atau menggunakan ikon **&#8212;** , **&#9723;** , dan **X** di kanan atas panel untuk meminimalkan, memaksimalkan, dan menutup panel. Untuk informasi selengkapnya tentang menggunakan Azure Cloud Shell, lihat [dokumentasi Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview).

4. Sekarang Anda siap untuk menyelesaikan latihan di Microsoft Learn - gunakan saja cloud shell di portal Azure Anda, bukan yang (kosong) di modul Learn (yang disediakan untuk pelajar mandiri yang menggunakan langganan kotak pasir).

    Gunakan tautan di bawah ini untuk membuka latihan di Microsoft Learn.

    **[Buka Microsoft Learn](https://docs.microsoft.com/learn/modules/explore-fundamentals-stream-processing/5-exercise-stream-analytics#create-azure-resources)**

> **Pembelajaran lebih lanjut**: Jika Anda punya waktu nanti, Anda mempertimbangkan untuk kembali ke modul Microsoft Learn ini dan mencoba latihan lain yang ada di dalamnya, termasuk menjelajahi Spark Streaming dan Azure Synapse Data Explorer.

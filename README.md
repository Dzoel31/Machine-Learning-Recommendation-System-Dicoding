# Laporan Proyek Machine Learning - Dzulfikri Adjmal

## Project Overview

Kemajuan zaman telah membawa perubahan dalam berbagai aspek kehidupan, termasuk dalam bidang pariwisata. Pariwisata merupakan salah satu sektor yang sangat penting bagi perekonomian suatu negara. Kegiatan ini sudah menjadi kebutuhan manusia, kesibukan sehari-hari yang membuat manusia merasa lelah dan jenuh, sehingga membutuhkan waktu untuk berlibur.

Pesatnya perkembangan teknologi informasi khususnya pada bidang pariwisata membantu para wisatawan dalam mencari informasi mengenai tempat wisata yang akan dikunjungi. Salah satu penerapan teknologi informasi dalam bidang pariwisata adalah sistem rekomendasi tempat wisata. Sistem rekomendasi tempat wisata memberikan rekomendasi berdasarkan rating yang diberikan oleh pengunjung sebelumnya.

Penelitian yang dilakukan oleh Siska, et al (2024) dengan judul Sistem Rekomendasi Wisata Magelang Menggunakan Metode Collaborative Filtering menunjukkan bahwa sistem rekomendasi dapat membantu pengguna menemukan destinasi wisata yang sesuai dengan kebutuhan dan preferensi mereka. Penelitian ini juga menyimpulkan potensi penggunaan sistem rekomendasi dalam meningkatkan pengalaman wisata dan pengembangan sektor wisata di Magelang.

Proyek ini bertujuan untuk mengembangkan sebuah sistem rekomendasi yang dapat membantu para wisatawan dalam menemukan destinasi wisata yang sesuai dengan kebutuhan dan preferensi mereka khususnya di 5 kota besar di Indonesia, yaitu Jakarta, Bandung, Surabaya, Semarang, dan Yogyakarta. Dengan adanya sistem rekomendasi ini diharapkan dapat meningkatkan pengalaman wisata para wisatawan dan membantu dalam pengembangan sektor pariwisata di Indonesia.

## Business Understanding

### Problem Statements

Dari latar belakang yang telah dijelaskan di atas, maka dapat dirumuskan pernyataan masalah sebagai berikut:

- Bagaimana cara mengembangkan sistem rekomendasi destinasi wisata yang dapat membantu para wisatawan dalam menemukan destinasi wisata yang sesuai dengan kebutuhan dan preferensi mereka?

### Goals

Proyek ini memiliki tujuan sebagai berikut:

- Mengembangkan sistem rekomendasi destinasi wisata yang dapat membantu para wisatawan dalam menemukan destinasi wisata yang sesuai berdasarkan rating yang telah diberikan oleh pengunjung sebelumnya.

### Solution statements

- Mengembangkan sistem rekomendasi destinasi wisata berbasis algoritma collaborative filtering.

## Data Understanding

Data yang digunakan merupakan data yang diambil dari [Indonesia Tourism Destination](https://www.kaggle.com/datasets/aprabowo/indonesia-tourism-destination) yang berisi mengenai destinasi wisata di 5 kota besar di Indonesia, yaitu Jakarta, Bandung, Surabaya, Semarang, dan Yogyakarta. Dataset ini terdiri dari 4 file csv, yaitu:

- tourism_with_id.csv: berisi mengenai data destinasi wisata di 5 kota besar di Indonesia.
- user.csv: berisi mengenai data pengunjung yang memberikan rating pada destinasi wisata.
- tourism_rating.csv: berisi mengenai data rating yang diberikan oleh pengunjung pada destinasi wisata.
- package_tourism.csv: berisi mengenai data paket wisata.

### Variabel-variabel pada Dataset

1. tourism_with_id.csv terdiri dari 437 baris dan 13 kolom, yaitu:
    - Place_Id: ID destinasi wisata.
    - Place_Name: Nama destinasi wisata.
    - Description: Deskripsi destinasi wisata.
    - Category: Kategori destinasi wisata, antara lain: Budaya, Taman Hiburan, Cagar Alam, Bahari, Pusat Perbelanjaan, Tempat Ibadah.
    - City: Kota destinasi wisata.
    - Price: Harga tiket masuk destinasi wisata.
    - Rating: Rating destinasi wisata.
    - Time_Minutes: Waktu tempuh dari pusat kota ke destinasi wisata dalam menit.
    - Coordinates: Koordinat destinasi wisata.
    - Lat (Latitude): Garis lintang destinasi wisata.
    - Long (Longitude): Garis bujur destinasi wisata.
    - Unnamed: 11: Kolom yang tidak memiliki nama.
    - Unnamed: 12: Kolom yang tidak memiliki nama.

2. user.csv terdiri dari 300 baris dan 3 kolom, yaitu:
    - User_Id: ID pengunjung.
    - Location: Lokasi pengunjung.
    - Age: Usia pengunjung.

3. tourism_rating.csv terdiri dari 10000 baris dan 3 kolom, yaitu:
    - User_Id: ID pengunjung.
    - Place_Id: ID destinasi wisata.
    - Rating: Rating yang diberikan oleh pengunjung pada destinasi wisata.

4. package_tourism.csv terdiri dari 100 baris dan 6 kolom, yaitu:
    - Package: ID paket wisata.
    - City: Kota paket wisata.
    - Place_Tourism1: Destinasi wisata 1.
    - Place_Tourism2: Destinasi wisata 2.
    - Place_Tourism3: Destinasi wisata 3.
    - Place_Tourism4: Destinasi wisata 4.
    - Place_Tourism5: Destinasi wisata 5.

### Exploratory Data Analysis (EDA)

Untuk lebih mengenali dataset yang digunakan dan mengetahui karakteristik dari data, dilakukan eksplorasi data dengan beberapa metode berikut:

- Melihat jumlah kategori wisata di setiap kota.
- Melihat wisata dengan rating tertinggi di setiap kota.

#### Jumlah Kategori Wisata di Setiap Kota

![jumlah kategori wisata tiap kota](https://github.com/Dzoel31/Machine-Learning-Recommendation-System-Dicoding/blob/main/assets/jumlah_kategori_wisata_tiap_kota.png?raw=true)

Dari grafik di atas dapat dilihat bahwa tiap daerah memiliki kategori wisata yang paling banyak dari daerah lainnya. Kategori wisata yang paling banyak di setiap daerah dapat dilihat pada tabel berikut.

| Kota       | Kategori Wisata | Jumlah |
|------------|-----------------|--------|
| Bandung    | Cagar Alam   | 1230     |
| Jakarta    | Budaya   | 719     |
| Semarang   | Cagar Alam   | 456     |
| Surabaya   | Budaya   | 402     |
| Yogyakarta | Taman Hiburan   | 801     |

#### Wisata dengan Rating Tertinggi di Setiap Kota

![wisata rating tertinggi tiap kota](https://github.com/Dzoel31/Machine-Learning-Recommendation-System-Dicoding/blob/main/assets/wisata_rating_tertinggi_tiap_kota.png?raw=true)

Dari grafik di atas dapat dilihat bahwa tiap daerah memiliki destinasi wisata dengan rating yang paling tinggi. Yogyakarta memiliki destinasi wisata dengan rating tertinggi, yaitu Desa Wisata Sungai Code Jogja Kota. Surabaya memiliki destinasi wisata dengan rating tertinggi kedua, yaitu Masjid Nasional Al-Akbar. Semarang memiliki destinasi wisata dengan rating tertinggi ketiga, yaitu Gua Maria Kerep Ambarawa. Jakarta memiliki destinasi wisata dengan rating tertinggi keempat, yaitu Wisata Kuliner Pecenongan. Bandung memiliki destinasi wisata dengan rating tertinggi kelima, yaitu Gereja Tiberias Indonesia Bandung.

## Data Preparation

Data preparation merupakan tahapan yang penting dalam proses pembuatan model sistem rekomendasi. Pada tahapan ini, data akan dipersiapkan agar dapat digunakan dalam proses pemodelan. Beberapa tahapan yang dilakukan dalam data preparation adalah sebagai berikut:

- Penghapusan kolom yang tidak diperlukan.

    Penghapusan kolom yang tidak diperlukan dilakukan untuk mengurangi dimensi data dan mempercepat proses pemodelan.

- Penggabungan data.

    Penggabungan data dilakukan untuk menggabungkan data yang memiliki hubungan satu sama lain. Penggabungan data melibatkan data user, data rating, dan data destinasi wisata.

### Content-Based Filtering

- Pengecekan missing value.

    Pengecekan missing value dilakukan untuk mengetahui apakah terdapat missing value pada dataset. Missing value dapat mempengaruhi model yang akan dibuat.

- Pengecekan duplikasi data.

    Pengecekan duplikasi data dilakukan untuk mengetahui apakah terdapat duplikasi data pada dataset. Duplikasi data dapat mempengaruhi hasil rekomendasi yang diberikan oleh model.

- Seleksi fitur.

    Seleksi fitur dilakukan untuk memilih fitur yang akan digunakan dalam proses pemodelan. Fitur yang dipilih adalah fitur yang memiliki hubungan dengan target yang akan diprediksi.

### Collaborative Filtering

- Encoding data.

    Encoding data dilakukan untuk mengubah data kategorikal menjadi data numerik. Data kategorikal perlu diubah menjadi data numerik agar dapat digunakan dalam proses pemodelan.

- Pembagian data menjadi data latih dan data uji.

    Pembagian data menjadi data latih dan data uji dilakukan untuk melatih model dan menguji model yang telah dilatih. Pembagian data ini dilakukan dengan proporsi 80% data latih dan 20% data uji.

## Modeling

Pada proyek ini, akan digunakan dua pendekatan dalam membangun sistem rekomendasi, yaitu content-based filtering dan collaborative filtering.

### Content-Based Filtering: Cosine Similarity

Content-Based Filtering berfokus pada kesamaan antara item berdasarkan fitur yang dimiliki oleh item tersebut. Dalam kasus ini, perhitungan Cosine Similarity digunakan untuk menghitung kesamaan tag dari destinasi wisata. Tag Tersebut terdiri dari kategori dan tempat wisata.

Keuntungan:

- Dapat memberikan rekomendasi yang sesuai dengan preferensi pengguna.
- Item baru dapat direkomendasikan tanpa memerlukan rating dari pengguna.

Kekurangan:

- Hasil rekomendasi yang diberikan kurang beragam.

Hasil:

![content based check](https://github.com/Dzoel31/Machine-Learning-Recommendation-System-Dicoding/blob/main/assets/content_based_check.png?raw=true)

![content based result](https://github.com/Dzoel31/Machine-Learning-Recommendation-System-Dicoding/blob/main/assets/content_based_result.png?raw=true)

### Collaborative Filtering: User-Based RecommenderNet

Collaborative Filtering berfokus pada kesamaan antara pengguna berdasarkan rating yang diberikan oleh pengguna pada item. Dalam kasus ini, model User-Based RecommenderNet digunakan untuk memberikan rekomendasi destinasi wisata berdasarkan rating yang diberikan oleh pengguna sebelumnya.

Keuntungan:

- Sangat personal karena berdasarkan rating yang diberikan oleh pengguna.
- Dapat memberikan rekomendasi yang beragam.

Kekurangan:

- Memerlukan data rating yang lengkap.
- Masalah cold start, yaitu ketika pengguna baru tidak memiliki data rating.

Hasil:

![user review](https://github.com/Dzoel31/Machine-Learning-Recommendation-System-Dicoding/blob/main/assets/user_review_collaborative_filtering.png?raw=true)

![model recommendation](https://github.com/Dzoel31/Machine-Learning-Recommendation-System-Dicoding/blob/main/assets/model_recommendation.png?raw=true)

## Evaluation

### Content-Based Filtering

Hasil dari 10 teratas rekomendasi terhadap destinasi wisata Museum Nasional yang memiliki tag Budaya dan Jakarta adalah sebagai berikut:

![content based result](https://github.com/Dzoel31/Machine-Learning-Recommendation-System-Dicoding/blob/main/assets/content_based_result.png?raw=true)

Berdasarkan hasil rekomendasi di atas, dapat dilihat bahwa destinasi wisata yang direkomendasikan memiliki tag yang sama dengan destinasi wisata Museum Nasional, yaitu tag Budaya dan Jakarta. Hal ini menunjukkan bahwa sistem rekomendasi sudah mencapai nilai presisi 100% (10/10).

Nilai presisi dihitung dengan rumus berikut:

$$ \text{Precision} = \frac{\text{Jumlah rekomendasi yang relevan}}{\text{Jumlah rekomendasi dari model}} $$

- Jumlah rekomendasi yang relevan: Jumlah destinasi wisata yang direkomendasikan oleh model yang relevan dengan preferensi pengguna.
- Jumlah rekomendasi dari model: Jumlah destinasi wisata yang direkomendasikan oleh model yang tidak relevan dengan preferensi pengguna.

### Collaborative Filtering

![user review](https://github.com/Dzoel31/Machine-Learning-Recommendation-System-Dicoding/blob/main/assets/user_review_collaborative_filtering.png?raw=true)

![model recommendation](https://github.com/Dzoel31/Machine-Learning-Recommendation-System-Dicoding/blob/main/assets/model_recommendation.png?raw=true)

Untuk mengevaluasi model Collaborative Filtering, dilakukan perhitungan presisi dan RMSE (Root Mean Squared Error) pada data uji. RMSE digunakan untuk mengukur seberapa baik model dalam memprediksi rating yang diberikan oleh pengguna pada destinasi wisata.

Presisi dihitung dengan rumus berikut:

$$ \text{Precision} = \frac{\text{Jumlah rekomendasi yang relevan}}{\text{Jumlah rekomendasi dari model}} $$

- Jumlah rekomendasi yang relevan: Jumlah destinasi wisata yang direkomendasikan oleh model yang relevan dengan preferensi pengguna.
- Jumlah rekomendasi dari model: Jumlah destinasi wisata yang direkomendasikan oleh model yang tidak relevan dengan preferensi pengguna.

Dari hasil rekomendasi di atas, dapat dilihat bahwa model Collaborative Filtering memberikan rekomendasi yang relevan dengan preferensi pengguna. Hal ini menunjukkan bahwa model Collaborative Filtering sudah mencapai nilai presisi 100% (10/10).

RMSE dihitung dengan rumus berikut:

$$ \text{RMSE} = \sqrt{\frac{1}{n} \sum_{i=1}^{n} (y_i - \hat{y}_i)^2} $$

- $n$: Jumlah data.
- $y_i$: Rating yang diberikan oleh pengguna pada destinasi wisata ke-$i$.
- $\hat{y}_i$: Rating yang diprediksi oleh model pada destinasi wisata ke-$i$.

![hasil rmse](https://github.com/Dzoel31/Machine-Learning-Recommendation-System-Dicoding/blob/main/assets/hasil_rmse.png?raw=true)

Berdasarkan hasil perhitungan RMSE di atas, dapat dilihat bahwa model Collaborative Filtering memiliki rata rata RMSE sebesar 0.3294 pada data latih dan 0.3483 pada data uji.

Kedua pendekatan, yaitu Content-Based Filtering dan Collaborative Filtering, memberikan hasil yang sangat baik dalam memberikan rekomendasi destinasi wisata yang sesuai dengan preferensi pengguna. Content-Based filtering cocok untuk kondisi dimana informasi terkait tentang kategori atau tag dari destinasi wisata sudah tersedia. Sedangkan Collaborative Filtering cocok untuk kondisi dimana informasi terkait rating yang diberikan oleh pengguna sudah tersedia.
Secara keseluruhan, kedua pendekatan ini dapat digunakan untuk memberikan rekomendasi destinasi wisata yang sesuai dengan preferensi pengguna.

## Daftar Pustaka

- Siska, S., Fajri, I. N., Rayhan, R., Pratama, A., & Rohman, A. N. (2024). Sistem Rekomendasi Wisata Magelang Menggunakan Metode Collaborative Filtering. Jurnal Eksplora Informatika, 14(1), 63-70. <https://doi.org/10.30864/eksplora.v14i1.1084>


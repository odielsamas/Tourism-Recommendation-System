# Laporan Proyek Machine Learning Sistem Rekomendasi - Odi Elsamas


## Project Overview
Pariwisata di Indonesia merupakan sektor ekonomi yang penting di Indonesia. Di tahun 2019, pariwisata menduduki peringkat ke-tiga dalam hal penerimaan devisa setelah komoditas gas dan minyak bumi serta minyak kelapa sawit. Berdasarkan data tahun 2016, jumlah wisatawan mancanegara yang datang ke Indonesia sebesar 11.525.963 juta lebih atau tumbuh sebesar 10,79% dibandingkan tahun sebelumnya. Kekayaan alam dan budaya adalah komponen penting dalam pariwisata di Indonesia. Indonesia juga merupakan negara kepulauan terbesar dan berpenduduk terbanyak di dunia.

Dari latar belakang diatas, proyek ini saya buat dengan tujuan memanfaatkan potensi-potensi tempat wisata yang ada di seluruh Indonesia. Semakin banyak orang-orang yang tau tempat-tempat wisata yang ada, maka akan semakin meningkat perekonomian yang ada di Indonesia.


## Business Understanding
Dari project overview di atas, sistem rekomendasi ini dikembangkan untuk menjawab pertanyaan berikut:

#### Problem Statement
- Bagaimana memberikan rekomendasi tempat wisata dengan rating yang paling tertinggi.

#### Goals
- Menghasilkan sistem rekomendasi yang akurat yang mengacu pada rating preferensi pengunjung sebelumnya.
 
#### Solution Approch

Solusi yang saya buat yaitu dengan menggunakan 2 algoritma Machine Learning sistem rekomendasi, yaitu :

- _Content Based Filtering_ adalah algoritma yang merekomendasikan item serupa dengan apa yang disukai pengguna, berdasarkan tindakan mereka sebelumnya atau umpan balik eksplisit.
- _Collaborative Filtering_ adalah algoritma yang bergantung pada pendapat komunitas pengguna. Dia tidak memerlukan atribut untuk setiap itemnya.

Modelling dengan _Content Based Filtering_ digunakan untuk merekemondesikan tempat wisata berdasarkan preferensi pengguna sebelumnya, sedangkan _Collaborative Filltering_ digunakan untuk merekomendasikan tempat wisata berdasarkan rating tertinggi.

## Data Understanding
Dataset yang digunakan pada proyek sistem rekomendasi ini yaitu data Indonesia Tourism Destination yang didapatkan dari situs kaggle. Informasi dataset dapat dilihat pada [Indonesia Tourism Destination](https://www.kaggle.com/datasets/aprabowo/indonesia-tourism-destination). Pada dataset terdapat beberapa atribut yang tidak diperlukan sehingga nantinya perlu menghapus beberapa atribut. Serta terdapat data yang kosong yang nantiya akan ditangani pada proses data preparation.

Dataset ini juga terdiri dari 4 file, yaitu:
1. tourism_ dengan _id.csv yang berisi informasi tempat wisata di 5 kota besar di Indonesia. Berikut detail masing-masing fitur:
    - Place_Id : Id tempat wisata
    - Place_Name : Nama tempat wisata
    - Description : Informasi mengenai tempat wisata	
    - Category : Kategori tempat wisata	
    - City : Kota tempat wisata
    - Price : Harga tempat wisata	
    - Rating : Rating tempat wisata	
    - Time_Minutes : Lama waktu tempat wisata	
    - Coordinate : Letak geografis tempat wisata
2. user.csv yang berisi data pengguna dummy untuk membuat fitur rekomendasi berdasarkan pengguna. Berikut detail dari masing-masing fitur:
    - User_Id : Id pada pengunjung
    - Location : Lokasi yang pernah dikunjungi
    - Age : Umur pengunjung
3. tourism_rating.csv berisi 3 kolom yaitu user, place, dan rating yang diberikan, berfungsi untuk membuat sistem rekomendasi berdasarkan rating. Berikut detail dari masing-masing fitur:
    - User_Id : Id pada user
    - Place_Id : Id Pada tempat wisata
    - Place_Rating : Nilai pada tempat wisata
4. package_tourism.csv berisi rekomendasi tempat terdekat berdasarkan waktu, biaya, dan rating. Berikut detail dari masing-masing fitur:
    - Package : identifier data
    - City : kota tempat wisata
    - Place_Tourism1 : Tempat Wisata
    - Place_Tourism2 : Tempat Wisata
    - Place_Tourism3 : Tempat Wisata
    - Place_Tourism4 : Tempat Wisata	
    - Place_Tourism5 : Tempat Wisata

## Data Preparation
Tahapan data preparation yang saya lakukan diantaranya:

##### Menangani Missing Value
Tahap ini dilakukan untuk mengecek apakah ada nilai yang kosong atau tidak. Pada dataset yang ada ternyata menunjukan bahwa tidak ada nilai yang kosong.

##### Mengurutkan Data
Tahap ini dilakukan untuk mengurutkan data berdasarkan Place_Id secara asceding dengan fungsi sort_values() dan memasukkannya ke dalam variabel fix_tourism.

##### Menangani Duplikasi Data
Tahap ini dilakukan untuk menangani data nilai yang sama. Cara melakukannya dengan menggunakan fungsi drop_duplicates(). Hasil akhir nya yaitu terdapat 437 jumlah data.

##### Konversi Data Menjadi List
Tahap ini yaitu mengkonversi data menjadi list menggunakan fungsi tolist() dari library numpy. Fitur yang diubah yaitu Place_Name, Place_Id, Description, City.

## Modeling
Pada tahap modelling, saya menggunakan algoritma Content Based filtering dan Collaborative Filtering

#### Content Based Filtering
_Content based filtering_ menggunakan informasi tentang beberapa item/data untuk merekomendasikan kepada pengunjung sebagai referensi mengenai informasi yang digunakan sebelumnya. Tujuan dari content based filtering adalah untuk memprediksi persamaan sejumlah informasi yang didapat dari pengguna.

Untuk menghitung derajat kesamaan (similarity degree) antar tempat wisata dengan teknik cosine similarity.

Berikut hasil top 5 rekomendasi tempat wisata:
|tourism_name|city|
|:-----------|:---|
|Puncak Pinus Becici|Yogyakarta|
|Kampung Wisata Taman Sari|Yogyakarta|
|Situs Warungboto|Yogyakarta|
|Keraton Yogyakarta|Yogyakarta|
|Sindu Kusuma Edupark (SKE)|Yogyakarta|

Dari hasil rekomendasi di atas, diketahui bahwa Pantai Graweng termasuk ke dalam kategori Yogyakarta. Dari 5 item yang direkomendasikan, 5 item memiliki kategori Yogyakarta (similar). Artinya, precision sistem kita sebesar 5/5 atau 100%.

Precision = #of recommendation that are relevant/#of item we recommend.
Pada contoh rekomendasi tempat wisata di atas:
Precission = 5/5.
Jadi presisinya = 100%

#### Collaborative Filtering
Pada algoritma ini saya menggunakan tingkat rating tempat wisata tersebut.

Top 5 rating tertinggi tempat wisata:
|tourism_name|city|
|:-----------|:---|
|Dunia Fantasi|Jakarta|
|Hutan Pinus Pengger|Yogyakarta|
|Watu Goyang|Yogyakarta|
|Wisata Alam Wana Wisata Penggaron|Semarang|
|Air Terjun Semirang|Semarang|

Top 10 tempat wisata yang direkomendasikan: 
|tourism_name|city|
|:-----------|:---|
|Museum Tekstil|Jakarta|
|Sumur Gumuling|Yogyakarta|
|Nonumen Yogya Kembali|Yogyakarta|
|The World Landmarks - Merapi Park Yogyakarta|Yogyakarta|
|Puncak Gunung Api Purba - Nglanggeran|Yogyakarta|
|Pantai Baron|Yogyakarta|
|Pintoe Langit Dahromo|Yogyakarta|
|Kebun Teh Nglinggo|Yogyakarta|
|Geoforest Watu Payung Turunan|Yogyakarta|
|Keraton Surabaya|Surabaya|
 
Dari hasil rekomendasi, Semarang dan Yogyakarta menjadi top 5 kota yang paling tinggi ratingnya, dan top 10 tempat wisata yang direkomendasikan oleh sistem adalah kota Yogyakarta.

## Evaluation
Pada tahap data training dan validasi kita bagi data train dan validasi dengan komposisi 80:20.

#### Evaluation Content Based Filtering
![This is an image](https://github.com/odielsamas/Sistem-Rekomendasi-Tempat-Wisata/blob/main/result4.png?raw=true)
![This is an image](https://github.com/odielsamas/Sistem-Rekomendasi-Tempat-Wisata/blob/main/result2.png?raw=true)

Dari hasil rekomendasi di atas, diketahui bahwa Pantai Graweng termasuk ke dalam kategori Yogyakarta. Dari 5 item yang direkomendasikan, 5 item memiliki kategori Yogyakarta (similar). Artinya, precision sistem kita sebesar 5/5 atau 100%.

#### Evaluation Collaborative filtering
Hasil dari model evaluasi visualisasi matriks adalah sebagai berikut :
![Plot](https://github.com/odielsamas/Sistem-Rekomendasi-Tempat-Wisata/blob/main/plot.png?raw=true)

Perhatikanlah, proses training model cukup smooth dan model konvergen pada epochs sekitar 100. Dari proses ini, kita memperoleh nilai error akhir sebesar sekitar 0.31 dan error pada data validasi sebesar 0.36. 

Kesimpulannya dari output yang dihasilkan yaitu dari hasil rekomendasi, Semarang dan Yogyakarta menjadi kota yang paling tinggi ratingnya, dan top 10 tempat wisata yang direkomendasikan oleh sistem adalah kota Yogyakarta.

REFERENCES
Vol. 16 No. 1 (2022): Jurnal Kepariwisataan Indonesia: Jurnal Penelitian dan Pengembangan Kepariwisataan Indonesia

---Ini adalah bagian akhir laporan---

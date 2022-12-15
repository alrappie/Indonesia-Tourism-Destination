# Laporan Proyek Machine Learning - Al'Ravie Mutiar Mahesa

## Domain Proyek

### Latar Belakang

Objek wisata merupakan tempat atau keadaan alam yang memiliki sumber daya
wisata yang dibangun dan dikembangkan sehingga mempunyai daya tarik dan
diusahakan sebagai tempat yang dikunjungi wisatawan [1]. Destinasi wisata Indonesia
cukup berhasil menarik perhatian para wisatawan lokal maupun wisatawan asing.
Menurut data Kementrian Pariwisata, jumlah kunjungan wisata mancanegara dari
bulan Januari sampai Agustus 2018 berjumlah 10.577.289 kunjungan, angka tersebut
mengalami pertumbuhan 12,30 % dari tahun sebelumnya [2].

Indonesia mempunyai objek wisata yang cukup beragam mulai dari wisata sejarah
seperti candi atau museum, wisata religi seperti makam atau tempat beribadah, wisata
pendidikan atau edukasi, serta wisata alam seperti pantai atau pegunungan. Jawa
Barat adalah salah satu wilayah yang mempunyai kekayaan alam yang mempesona.
Objek wisata di Jawa Barat cukup banyak diketahui masyarakat mulai dari wisata
pantai, laut, pegunungan, cagar alam, air terjun juga wisata lainnya. Namun wisatawan tidak mengetahui tempat objek wisata yang berada di Indonesia sehingga wisatawan hanya mengunjungi tempat - tempat yang biasa dikunjungi oleh banyak orang saja / populer.

Berdasarkan hal tersebut, lebih baik jika terdapat sebuah sistem yang dapat memberikan rekomendasi wisata bagi wisatawan. Sehingga wisatawan dapat dengan mudah untuk melanjutkan perjalanannya menuju jenis tempat wisata yang disukainya. Oleh karena itu untuk memberikan kemudahan bagi wisatawan dilakukannya pembuatan sistem rekomendasi bagi wisatawan yang ingin menikmati perjalannya di Indonesia.

## Business Understanding

### Problem Statement 
* Bagaimana wisatawan dapat mengetahui objek wisata tempat lain yang memiliki jenis yang sama atau yang disukai oleh wisatawan?
  
### Goals
* Memberikan sebuah sistem rekomendasi untuk wisatawan yang sedang berkunjung ke Indonesia sehingga wisatawan dapat menikmati jenis objek wisata yang digemarinya.
  
### Solution Approach
* Memberikan 2 algoritma yang digunakan, yaitu *content based filtering* dan *collaborative filtering* kepada para wisatawan.

## Data Understanding 
Dataset yang digunakan untuk proyek ini adalah [Indonesia *Tourism Destination*](https://www.kaggle.com/datasets/aprabowo/indonesia-tourism-destination?select=package_tourism.csv).

Pada dataset yang terdapat sebanyak 4 file csv, yaitu : tourism_rating.csv, tourism_with_id.csv, package_tourism.csv, dan user.csv.

Pada dataset tourism_rating.csv menjelaskan tentang penilaian user terhadap tempat wisata.

Pada dataset tourism_with_id.csv menjelaskan mengenai deskripsi tempat wisata 

Pada package_tourism menjelaskan paket tour wisatawan

Pada dataset user.csv menjelaskan mengenai deskripsi wisatawan.

Pada dataset tersebut hanya 3 dataset saja yang digunakan, yaitu : user.csv, tourism_with_id.csv, dan tourism_rating.csv

Variabel pada dataset user sebagai berikut:

1. *User_Id* : Berupa ID user
2. *Location* : Lokasi user
3. *Age* : Umur User

Variabel pada dataset tourism_rating sebagai berikut:

1. *User_Id* : Berupa ID user
2. *Place_Id* : tempat ID wisata
3. *Place_Ratings* : Penliaian terhadap tempat tersebut

Variabel pada dataset tourism_with_id sebagai berikut:

1. *Place_Id* : Berupa ID wisata
2. *Place_Name* : Nama tempat wisata
3. *Description* : Deskripsi Wisata
4. *Category* : Kategori wisata
5. *City* : Tempat kota wisata
6. *Price* : Harga wisata
7. *Rating* : Penilaian tempat wisata
8. *Time_Minutes* : Lamanya kedatangan
9. *Coordinate* : Koordinat tempat wisata
10. *Lat* : *Latitude*
11. *Long* : *Longitude*

### Visualisasi Variabel 
#### Univariate

* Age
![](https://lh3.googleusercontent.com/d/1Ak6jypmZViQ-27qP6dwloeHpWw5q_2gu)

  Gambar 1. Distribusi Age (Umur)

  Pada gambar 1, memiliki distribusi age yang normal karena skewness tidak melebihi treshold, umur terkecil adalah 18 tahun dan umur tertinggi adalah 40 tahun.

* City
  
  ![](https://lh3.googleusercontent.com/d/1aKf-aBtpyc12mwLAf_MpnZjJeD_qgYi6)

  Gambar 2. Perbandingan Kota yang sering dikunjungi oleh *tourism*

  Pada gambar 2, Wisatawan sering mengunjungi Yogyakarta dan Bandung sebagai tujuan destinasi wisata.

#### Multivariative 

* Tempat Wisata per Rating User

  ![](https://lh3.googleusercontent.com/d/1Eyt4RLgKNBlW4nj9H7H4FSgOuzag_8u-)

    Gambar 4. 10 Destinasi Wisata berdasarkan *rating tourism*

    Pada gambar 4, wisata keraton surabaya memiliki rating paling tinggi, yaitu 3.9 menurut rata-rata para wisatawan yang sudah berkunjung.

### Data Preparation

* Melihat *missing values* pada setiap variabel di data
  
    Untuk Melihat *missing values* pada masing-masing variabel dapat dilakukan dengan menuliskan *method* *isna()* dan *sum()* pada *dataframe* maka akan memberikan informasi terkait banyaknya isi variabel yang memiliki nilai kosong. Setelah menerapkan ke seluruh dataset, tidak ditemukan data yang memiliki nilai yang kosong.

    Tujuan : Hal ini dilakukan bertujuan karena tidak semua model pada machine learning dapat menerima data yang kosong dan dengan data yang kosong kita juga bisa melakukan imputasi agar nilai error bisa lebih di minimalkan.

* Melihat tipe data pada setiap variabel di data
    
    untuk melihat tipe data pada setiap variabel di dataset dapat dilakukan dengan menggunakan *method* *info()* maka akan memberikan informasi terkait banyaknya isi dari setiap variabel yang memiliki nilai kosong beserta dengan tipe data pada masing-masing variabel.

    Tujuan : Hal ini bertujuan untuk mengetahui tipe data pada variabel secara keseluruhan sehingga dapat dengan mudah memberikan informasi untuk dilakukannya data preprocessing.

* Menghapus *column* dan menyatukan *dataframe* menjadi satu
  
  Untuk menyatukan menghapus *column* dapat dilakukan dengan menuliskan *method* *drop()* pada *dataframe* yang ingin dilakukannya *dropping column*, yaitu *column* *Rating, Time_Minutes, Coordinate, Lat, Long, Unnamed: 11,* dan *Unamed: 12*. Setelah itu untuk menyatukan dataframe dapat dilakukan dengan menggunakan *library* pandas dengan menuliskan *pd.merge()* pada *data_tourism_rating* yang sudah di *groupby* berdasarkan *place_id* lalu di gabungkan dengan *data_tourism_with_id*.

    Tujuan : Hal ini dilakukan bertujuan untuk mempermudah dalam melihat data sekaligus melakukan modeling.

* Membuat *Encode* pada variabel *User_Id* dan *Place_Id*
  
  Untuk melakukan *encode* pada variabel *User_Id* dan *Place_Id* dapat dilakukan dengan menggunakan *looping* pada banyaknya *user_id* dan *place_id* yang terdapat pada data dengan membuat *key and value*. Angka 0 hingga banyaknya *User_Id* menjadi *value* dan nilai asli *User_Id* menjadi *Key*

  Tujuan : Hal ini dilakukan supaya tipe data *User_Id* dan *Place_Id* berbentuk *Integer* sehingga dapat dilakukan tahapan selanjutnya yaitu pemodelan.

* Membuat *Decode* pada Variabel *User_Id* dan *Place_Id*
  
  Untuk melakukan *dencode* pada variabel *User_Id* dan *Place_Id* dapat dilakukan dengan menggunakan *looping* pada banyaknya *user_id* dan *place_id* yang terdapat pada data dengan membuat *key and value*. Angka 0 hingga banyaknya *User_Id* menjadi *Key* dan nilai asli *User_Id* menjadi *Value*
  
  Tujuan : Hal ini dilakukan supaya tipe data yang sudah dilakukan *encode* dapat dikembalikan seperti nilai aslinya.

* Melakukan *Mapping* 
  
  Setelah membuat *encode* maka terapkan kepada dataset dengan membuat column baru, yaitu *user* dan *place* dengan menggunakan *method* *map* pada variabel *encode* yang sudah dibuat.

  Tujuan : Hal ini dilakukan untuk menerapkan *encode* pada dataset sehingga bertipe integer.

* Membagi dataset menjadi data latih dan data val
  
  Untuk membagi dataset menjadi data latih dan data val maka dilakukannya pemisahan terhadap nilai X, yaitu *user* dan *place* dengan y yaitu *place_ratings*. Lalu membagi menjadi 80% data latih dan 20% data validasi menjadi x_train, x_val, y_train, y_val.

  Tujuan : Hal ini dilakukan sehingga data latih digunakan untuk melatih model yang nantinya akan dibuat dan data validasi untuk mengukur perfoma dari model yang sudah dibuat.

## Modeling and Result

Setelah dilakukannya data preparation maka selanjutnya akan dilakukan modeling. Pada modeling dilakukan dengan menggunakan 2 algoritma rekomendasi yaitu *Content Based Filtering* dan *Collaborative Filtering*.

### *Content Based Filtering*

Untuk Model
Pada *Content Based Filtering* menggunakan item-item yang berada pada dataset. Item yang digunakan untuk kasus ini adalah deskripsi dari masing-masing wisata beserta dengan jenis kategori wisata tersebut bertipe data text. Sehingga bila wisatawan ingin sebuah tempat wisata yang mirip dengan pilihan wisatawan maka akan menampilkan 10 rekomendasi tempat wisata yang serupa dengan pilihan wisatawan.

Tahapan yang digunakan untuk modeling adalah 

1. Membuat variabel baru pada dataset, yaitu *tags* yang berisikan *item* yang dapat mendeskripsikan tempat tersebut.
2. Melakukan pembersihan kata, yaitu stemming untuk membuat kata yang diberikan menjadi kata dasar tanpa adanya imbuhan dan *stopwords* untuk menghapus kata yang tidak digunakan, dengan menggunakan *library* sastrawi.
3. Mengubah *text* menjadi *integer* dengan menggunakan *library* *countvectorizer* sehingga dapat dilakukan pemprosessan lebih lanjut. CountVectorizer berkerja menggunakan fungsi TF-IDF untuk mengukur atau menghitung bobot dari setiap kata yang digunakan. Setiap kata yang ada akan dimasukan kedalam *bag of words* (kantong kata) kemudian dibuatkan sebuah array yang berisikan seluruh kata tersebut. Lalu pada setiap document akan dilakukan pengecekan, apakah kata tersebut ada dalam dokumen  atau tidak dan juga membandingkannya dengan dokumen lain sehingga menghasilkan bobot dari kata tersebut.
4. Menerapkan *cosine* *similarity* untuk mengukur kesamaan pada masing - masing *item* pada data. Cosine smiliarity bekerja dengan cara melakukan perkalian skalar antara query (kata yang ingin dilakukan kemiripan) dengan dokumen kemudian dijumlahkan, setelah itu melakukan perkalian antara panjang dokumen dengan panjang query  (kata yang ingin dilakukan kemiripan) yang telah dikuadratkan, lalu dihitung akar pangkat dua.

Contoh hasil Tampilan yang dikeluarkan untuk rekomendasi sebagai berikut :

recommend_by_content_based_filtering('Monumen Nasional')

|Hasil Rekomendasi| 
|---            |
|Monumen Bandung Lautan Api|
|Monumen Selamat Datang|
|Monumen Perjuangan Rakyat Jawa Barat|
|Tugu Muda Semarang|
|Monumen Bambu Runcing Surabaya|
|Monumen Tugu Pahlawan|
|Monumen Sanapati|
|Monumen Yogya Kembali|
|Monumen Palagan Ambarawa|

#### Kelebihan dan Kekurangan 

Kelebihan pada model ini adalah dapat memberikan rekomendasi yang sifatnya baru bagi user dan memberikan rekomendasi terhadap kemiripan tempat wisata yang di sukainya.

Kekurangan pada model ini adalah tidak adanya ide, pendapat dari pengguna lain sehingga rekomendasi yang diberikan belum tentu memiliki tempat yang bagus.

### *Collaborative Filtering*
Pada *Collaborative Filtering* menggunakan item berdasarkan penilaian pengguna sebelumnya yang telah mengunjungi tempat wisata tersebut. Item yang digunakan untuk kasus ini adalah *rating* tempat wisata. Apabila wisatawan ingin sebuah tempat rekomendasi berdasarkan hal yang disukainya dengan pengguna lainnya maka akan menampilkan 10 rekomendasi tempat wisata.

Tahapan yang digunakan untuk modeling adalah 

1. Membuat fungsi recommender dengan menggunakan library dari keras. Fungsi rekomender bekerja dengan cara membuat sebuah layer embedding untuk *user* dan juga layer embedding untuk *place* lalu menambahkan layer embedding bias dari kedua layer tersebut sehingga terdapat 4 layer embedding. layer embedding *user* dan *place* dilakukan perkalian dot setelah itu ditambahkan dengan nilai dari *user* bias dan *place* bias sehingga menghasilkan nilai yang nantinya akan menggunakan aktivasi sigmoid untuk melakukan prediksi.
2. Melakukan inisiasi model dan melakukan fitting pada model dengan memasukan beberapa parameter seperti, embedding_size sebesar 50, learning rate sebesar 0.001, jumlah epoch sebesar 100, dan batch_size sebesar 8.
3. Membuat sebuah fungsi untuk melakukan prediksi pada dataset dengan mengambil contoh user, lalu membuat inisasi variabel baru sebagai tempat yang belum pernah dikunjungi oleh user lalu melakukan prediksi terhadap tempat yang belum pernah dikunjungi sehingga dapat mengeluarkan hasil rekomendasi.

Contoh Hasil rekomendasi yang dikeluarkan untuk rekomendasi sebagai berikut : 

user dengan id 227 menyukai beberapa tempat dengan rating tertinggi, yaitu :

|*Place with High Ratings from User (Sample 5)*| 
|---            |
|Monumen Nasional|
|Kota Tua|
|Alun Alun Selatan Yogyakarta|
|Museum Barli|
|Museum Nike Ardilla|

sehingga dapat diberikan 10 tempat wisata pilihan, yaitu : 

|Hasil Rekomendasi| 
|---            |
|Museum Tekstil|
|The World Landmarks - Merapi Park Yogyakarta|
|Air Terjun Kedung Pedut|
|Pantai Baron|
|Goa Pindul|
|Pantai Depok Jogja|
|Hutan Mangrove Kulon Progo|
|Jogja Bay Pirates Adventure Waterpark|
|Pantai Watu Kodok|
|Desa Wisata Pulesari|

#### Kelebihan dan Kekurangan 

Kelebihan pada model ini adalah dapat memberikan rekomendasi meskipun konten yang
berhubungan dengan item atau wisatawan sangat sedikit atau bahkan tidak ada.

Kekurangan pada model ini adalah tidak dapat diberikan rekomendasi untuk wisatawan baru dikarenakan belum memiliki rating pada wisata yang ada

## Evaluation

### *Collaborative Filtering*

Pada collaborative Filtering menggunakan RMSE (*Root Mean Square Error*) untuk mengukur tingkat ketidaktepatan rekomendasi pada wisatawan. 

  ![](https://lh3.googleusercontent.com/d/1JnMBmWM_fzZDsMNzeK8PocZxtU9_e0M3)

  Gambar 5. Nilai RMSE pada *Collaborative Filtering*

Pada hasil nilai error perbandingan nilai test dengan nilai train berbeda. Nilai train memiliki nilai sekitar 0.31 dan nilai error pada test sekitar 0.36. Hal ini menandakan bahwa model ini  memiliki nilai overfitting yang sedikit. Pada hasil nilai error terkecil data test sebesar 0.36. Hal tersebut cukup bagus untuk memberikan sebuah  sistem rekomendasi kepada wisatawan.

Rumus yang digunakan untuk RMSE : 

$$\sqrt{\frac{\sum_{i=1}^{N} (\hat{y}_i - y_i)} {N}}$$

$\hat{y}$  = merupakan hasil prediksi

$y$ = merupakan hasil aktual

Cara kerja metric : 

Hasil prediksi pada setiap epoch dikurang dengan hasil aktual pada epoch epoch tersebut dan dibagi dengan banyaknya epoch yaitu 100


### *Content Based Filtering*

Pada Content Based Filtering menggunakan ***Smiliarity Metrics*** untuk mengukur tingkat kemiripan hasil rekomendasi pada wisatawan. Jika wisatawan meminta rekomendasi berdasarkan tempat yang mirip dengan Pantai Watu Kodok maka hasil ***Smiliarity Metrics*** berupa : 

|Hasil Rekomendasi| Nilai *Smiliarity Metrics* (Kemiripan)
|---            |---|
|Pantai Kukup|0.5659440531411729|
|Pantai Timang|0.5185433503874808|
|Pantai Drini|0.5034916444153296|
|Pantai Ngandong|0.48939744234953786|
|Pantai Sundak|0.4855410205632307|
|Pantai Ngrawe (Mesra)|0.4655150705971857|
|Pantai Sadranan|0.44906283441167205|
|Pantai Jungwok|0.42546650148837023|
|Pantai Cipta|0.4101023347137378|

Pada hasil tersebut nilai metrics kemiripan tertinggi yaitu 56% dan terendah yaitu 41%.

Rumus yang digunakan untuk *Cosine Smiliarity* : 

$Cos\theta = \frac{\overrightarrow{a} . \overrightarrow{b}} {||\overrightarrow{a}||||\overrightarrow{b}||} = \frac{\sum_{1}^{n} a_ib_i}{\sqrt{\sum_{1}^{n}a_i^{2}}\sqrt{\sum_{1}^{n}b_i^{2}}}$

Cara kerja metric : 

Cosine similarity menghitung kesamaan sebagai dot product yang dinormalisasi dari masukan sampel X dan Y. Semakin mirip kesamaan maka jarak nilai cosine semakin kecil menuju ke angka 1.

## Referensi 
[1] I. Setiawan, "POTENSI DESTINASI WISATA DI INDONESIA MENUJU KEMANDIRIAN," [Online]. Available: https://media.neliti.com/media/publications/173034-ID-potensi-destinasi-wisata-di-indonesia-me.pdf. [Accessed 19 November 2022].

[2] 	"Statistik Kunjungan Wisatawan Mancanegara 2020," kemenparekraf, 3 Desember 2020. [Online]. Available: https://www.kemenparekraf.go.id/statistik-wisatawan-mancanegara/Statistik-Kunjungan-Wisatawan-Mancanegara-2020. [Accessed 19 November 2022].
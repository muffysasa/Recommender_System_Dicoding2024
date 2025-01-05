# Proyek 2 Recommendation System
## 1. Project Overview 

Destinasi wisata adalah tujuan yang dikunjungi baik oleh wisatawan lokal maupun internasional untuk liburan atau menikmati pesona alam, budaya, dan atraksi tertentu. Setiap destinasi memiliki daya tarik dan keunikan tersendiri, seperti keindahan alam, nilai sejarah, atau aktivitas menarik yang dapat menghibur pengunjung.

Indonesia sendiri memiliki ratusan hingga ribuan destinasi wisata alam dan budaya yang kaya, sehingga banyak menarik perhatian wisatawan baik lokal dan mancanegara untuk menikmati khas alam dan budaya di Indonesia. Sektor wisata dengan keragaman alam bidaya di Indonesia dapat meningkatkan perekonomian Indonesia. Sehingga penting bagi pihak destinasi wisata di Indonesia untuk meningkatkan dan mempertahankan wisatawan baik lokal maupun mancanegara menjadikan destinasi wisata di Indonesia merupakan destinasi yang terbaik

Setiap wisatawan memiliki preferensi atraksi atau keunikan yang ingin dinikmati. Banyak calon wisatawan ingin mencoba atau mendatangi wisata yang baru atau memiliki review yang baik. Seringkali calon turis menentukan tujuan destinasinya berdasarkan pengalaman bagi turis yang memiliki riwayat kunjungan ke wisata tersebut. Namun karena banyaknya jenis dan lokasi wisata di Indonesia maka akan terlalu banyak informasi yang didapat dan kurang tepat sasaran pada calon turis sesuai preferensinya tersebut. Dengan perkembangan Machine learning, faktor tersebut dapat dibantu dengan membangun sistem yang dapat menilai atau merekomendasikan tujuan wisata sesuai dengan ciri khas yang diinginkan oleh pengunjung [referensi jurnal](http://jurnal.upnyk.ac.id/index.php/telematika/article/view/3023/2443).


## 2. Business Understanding
**- Problem Statement**

Indonesia memiliki ragam wisata yang didatangi banyak wisatawan. Dengan keragaman wisata dan banyaknya wisatawan dapat menghasilkan Data Mining yang merekam data-data transaksi wisatawan berkunjung di Indonesia. Sehingga, dapat dimanfaatkan untuk membangun sistem rekomendasi bertujuan menggali informasi dan mencari wisatawan baru.
Selain itu, banyak wisatawan mendatangi destinasi wisata sesuai dengan preferensi mereka, agar tujuan yang didatangi dapat memenuhi ekspetasi. Perlu adanya sistem rekomendasi yang dapat membaca preferensi calon wisatawan dan menyesuaikan referensi wisatawan lainnya yang memiliki riwayat menikmati wisata yang sama dengan preferensi calon wisatawan. Sehingga rekomendasi wisata akan menyesuaikan dengan preferensi calon wisatawan, dapat meningkatkan ekspetasi setelah berkunjung sesuai rekomendasi dan juga dapat menaikkan daya tarik wisata yang dapat meningkatkan perekonomian Indonesia.


Berdasarkan latar belakang tersebut project ini memiliki batasan masalah sebagai berikut:
1. **Bagaimana langkah-langkah untuk membuat sistem rekomendasi untuk calon pengunjung berdasarkan referensi riwayat pengunjung?**
  --> Melakukan metode sederhana CRISP-DM (Cross-Industry Standard Process for Data Mining) yaitu mengumpulkan, membersihkan dan menganalisis data. selanjutnya melakukan fitur engineering untuk membangun model sistem rekomendasi.
2. **Bagaimana atribut-atribut referensi pengunjung-pengunjung untuk menentukan destinasi wisata?**
  --> Menganalisis referensi data pengunjung wisata sebagai penilaian destinasi wisata
3. **Bagaimana cara membangun model Machine Learning sebagai solusi untuk merekomendasikan destinasi wisata untuk calon pengunjung berdasarakan preferensi pengunjung tersebut?**
  --> Analisis data dan membangun model menggunakan Deep Learning dengan eksplorasi hyperparameter berdasarkan rating dan ciri khas destinasi wisata melihat pada MSE, MAE dan R2 sebagai parameter model yang memiliki error paling kecil

  
**- Goals**

Sistem rekomendasi destinasi wisata bertujuan bagi calon pengunjung untuk:
1.   **Merekomendasikan tujuan wisata sesuai prefernsinya berdasarkan referensi riwayat pengunjung-pengunjung sebelumnya yang memiliki kesamaan preferensi tujuan wisata**
2.   **Menilai referensi pengunjung untuk menentukan destinasi wisata**,
3.  **Meningkatkan kepuasan para pengunjung wisaata sesuai preferensinya**,
4. **Mengurangi penilaian rendah pada destinasi wisata karena kurang sesuainya terhadap preferensi calon pengunjung**

**- Solution statements**
Menggunakan content based filtering cosine similarity dan kernel Sigmoid, collaborative filtering algoritma recommenderNet dengan library keras dan SVD dengan library surprise yang dapat terukur baik menggunakan RMSE dan MAE

### 3. Data Understanding
Data yang digunakan bersumber [Mendeley Data](https://data.mendeley.com/datasets/h58s544674/1), oleh kontributor *huda, choirul huda (2023), “Tourism Dataset”, Mendeley Data, V1, doi: 10.17632/h58s544674.1*. Data tersebut berisi transaksi turis pada 3 lokasi wisata yang terpopuler di Indonesia yaitu Bali, Malang dan Yogyakarta dari riwayat turis yang direkam oleh website TripAdvisor rentang waktu Oktober 2022 - January 2023. Data terdapat 9 data format xlsx. Berikut penjelasan kolom-kolom pada masing-masing data:

1. Data City.xlsx -> master data kota persona turis. [9143 baris, 3 kolom]
  - CityId : integer berisi identifikasi unik merepresentasikan sebuah kota | 9143 non-null
  - CityName : string berisi informasi nama kota | 9142 non-null
  - CountryId : integer berisi identifikasi unik merepresentasikan sebuah negara |9143 non-null

  Data terdapat nilai null, namun tabel ini tidak diperlukan drop data karena akan digunakan referensi dari penggabungan data.
2. Data Continent.xlsx -> master data benua persona turis. [6 kolom, 2 baris]
  - ContenetId : integer berisi identifikasi unik merepresentasikan sebuah benua | 6 non-null
  - Contenent : string berisi informasi nama benua | 6 non-null

  Tidak ada nilai null
3. Data Country.xlsx -> master data negara persona turis. [165 baris, 3 kolom]
  - CountryId : integer berisi identifikasi unik merepresentasikan sebuah negara | 165 non-null
  - Country : sting berisi informasi nama wilayah | 165 non-null
  - RegionId : integer berisi identifikasi unik merepresentasikan sebuah wilayah | 165 non-null

  Tidak ada nilai null
4. Data Item.xlsx -> master data destinasi wisata. [30 baris, 5 kolom
  - Attractionid : integer berisi identifikasi unik merepresentasikan sebuah wisata | 30 non-null
  - AttractionCityId : integer berisi identifikasi unik merepresentasikan sebuah lokasi kota wisata | 30 non-null
  - AttractionTypeId : integer berisi identifikasi unik merepresentasikan sebuah tipe wisata | 30 non-null
  - Attraction : string berisi informasi nama wisata |  30 non-null
  - AttractionAddress : string berisi informasi alamat wisata | 30 non-null

  Tidak ada nilai null
5. Data Mode.xlsx -> master data jenis kunjungan turis. [6 baris, 2 kolom]
  - VisitModeId : integer berisi identifikasi unik merepresentasikan sebuah jenis kunjungan wisatawan | 6 non-null
  - VisitMode : string berisi informasi jenis kunjungan wisatawan |  6 non-null

  Tidak ada nilai null, namun pada visit mode terdapat nilai tidak konsisten yaitu nilai "-". Hal ini tidak perlu di drop karena akan digunakan referensi penggabungan data
6. Data Region.xlsx -> master data daerah persona turis. [22 baris, 3 kolom]
  - Region : string berisi informasi nama negara | 22 non-null
  - RegionId : integer berisi identifikasi unik merepresentasikan sebuah negara | 22 non-null
  - ContentId : integer berisi identifikasi unik merepresentasikan sebuah benua | 22 non-null

  Tidak ada nilai null
7. Data Transaction.xlsx -> data transaksi turis. [52930 baris,7 kolom]
  - TransactionId : integer berisi identifikasi unik merepresentasikan sebuah transaksi | 52930 non-null
  - UserId : integer berisi identifikasi unik merepresentasikan sebuah user/wisatawan | 52930 non-null
  - VisitYear : datetime informasi waktu tahun kunjungan wisatawan | 52930 non-null
  - VisitMonth : datetime informasi waktu bulan kunjungan wisatawan | 52930 non-null
  - VisitMode : string berisi informasi jenis kunjungan wisatawan | 52930 non-null
  - AttractionId : integer berisi identifikasi unik merepresentasikan sebuah wisata | 52930 non-null
  - Rating : integer berisi informasi rating wisatawan terhadap tempat wisata (ordinal)| 52930 non-null

  Tidak ada nilai null
8. Data Type.xlsx -> master data tipe wisata. [17 baris, 2 kolom]
  - AttractionTypeId : integer berisi identifikasi unik merepresentasikan sebuah jenis wisata | 7 non-null
  - AttractionType : string berisi informasi nama jenis wisata | 7 non-null

  Tidak ada nilai null
9. Data User.xlsx -> data referesni persona turis. [33530 baris, 5 kolom]
  - UserId : integer berisi identifikasi unik merepresentasikan sebuah user/wisatawan |33530 non-null
  - ContenentId : integer berisi identifikasi unik merepresentasikan sebuah benua | 33530 non-null
  - RegionId : integer berisi identifikasi unik merepresentasikan sebuah wilayah | 33530 non-null
  - CountryId : integer berisi identifikasi unik merepresentasikan sebuah negara | 33530 non-null
  - CityId : integer berisi identifikasi unik merepresentasikan sebuah kota |33526 non-null
  
  Data terdapat nilai null, namun tabel ini tidak diperlukan drop data karena akan digunakan referensi dari penggabungan data.


Pada informasi masing-masing data terdapat nilai null. Pembersihan data/drop data akan dilakukan setelah penggabungan data/merge data

#### 3. 1 Merge data/penggabungan data untuk persiapan data content-based dan collaborative based

Berdasarkan data understanding bahwa folder Tourism_Dataset terdapat 9 file. Pada tahap ini, akan dilakukan proses penggabungan data menampilkan informasi yang konsisten. Sesuai kebutuhan projek ini, input dan output yang akan digunakan adalah atribut-atribut pada destinasi wisata. Maka akan dilakukan
merge data destinasi wisata yang  berisi informasi tujuan wisata berdasarkan lokasi, type wisata, kunjungan dsb

Data yang akan digunakan adalah data merge destinasi wisata terdiri gabungan data Item.xlsx, Type.xlsx, Transaction.xlsx, Terdiri kolom-kolom:
|No|Nama Kolom|Jumlah Baris non_null|Tipe Data|
|--|----------|---------------------|---------|
 0|   TransactionId|      52930 non-null|  int64 
 1|   UserId|             52930 non-null|  int64 
 2|   VisitYear|          52930 non-null|  int64 
 3|   VisitMonth|         52930 non-null|  int64 
 4|   VisitModeId|        52930 non-null|  int64 
 5|   AttractionId|       52930 non-null|  int64 
 6|   Rating|             52930 non-null|  int64 
 7|   AttractionCityId|   52930 non-null|  int64 
 8|   AttractionTypeId|   52930 non-null|  int64 
 9|   Attraction|         52930 non-null|  object
 10|  AttractionAddress|  52930 non-null|  object
 11|  AttractionType|     52930 non-null|  object
 12|  VisitMode|          52930 non-null|  object
 
 Berdasarkan tabel informasi diatas setiap kolom memiliki jumlah baris non-null dapat diartikan tidak ada nilai masing-masing kolom yang bernilai Null
 
#### 3. 2 Pembersihan data
Berdasarkan informasi data, data tidak terdapat Null dan tidak ada duplikat

#### 3. 3 EDA data detinasi wisata di Indonesia
Berdasarkan EDA data destinasi selama Oktober 2022 hingga January 2023 menunjukkan
1. 5 terbanyak destinasi wisata dengan jumlah pengunjung wisata terdapat pada tempat wisata Bali":
- Sacred Monkey Forest Sactuary = ±13000 pengunjung
- Waterbom Bali = ±7000 pengunjung
- Tegalalang Rice Terrace = ±5800 pengunjung
- Uluwatu temple = ±3800 pengunjung
- Tanah Lot Temple = ±3800 pengunjung

2. Wisata dengan rating >= 3
- Sacred Monkey Forest Sactuary 
- Waterbom Bali 
- Tegalalang Rice Terrace 
- Uluwatu temple 
- Tanah Lot Temple 

3. Jenis kunjungan di Indonesia
- Pada kunjungan wisata Bali sebanyak 43.4% couples (family, friends)
- Pada kunjungan wisata Malang sebanyak 39.6% friends (family, couple)
- Pada kunjungna wisata Yogyakarta sebanyak 30.1% friends (couple, family)

4. Jenis kunjungan pada wisata 5 jenis di I
- Nature Wilds Area -> couple
- Beaches -> couple
- Religious Sites -> couple
- Water Parks -> Family
- Points of Interest and Landmarks -> couple

Summary Visualisasi Data dalam rentang waktu Oktober 2022 - January 2023: Wisata berlokasi di Bali merupakan tujuan wisatawan terbanyak dibandingkan lokasi Malang Jawa Timur dan Yogyakarta area DI Yogyakarta. Wisata di Bali didominasi wisatawan adalah jenis wisata Nature & Wildlife Areas, Water Parks, Points of Interest & Landmarks, Religious Sites. Selain itu banyak pengunjung dengan tujuan daerah Bali dengan pengunjung Couple disusul pengunjung Familiy dan Friends. Sacred Monkey Forest Sactuary merupakan wisata Nature & Wildlife Areas terfavorit wisatawan dengan rating lebih dari 3 dari wisata di Bali lainnya.


### 4. Data Preparation
#### 4. 1 Data Preparation Modelling for Content Based -> Cosine Similarity dan Kernel Sigmoid
1. Text Cleaning : Pada value kolom yang akan digunakan NewAttraction dan NewAttractionType setiap kata terdapat spasi, jika dilakukan mapping Vectorizer akan menampilkan value kolom yang tidak sesuai. Sehingga perlu cleaning teks pada simbol-simbol dan mengganti spasi dengan underscore
2. Nilai unik pada pada item yang digunakan berjumlah 148, maka saat di vektorisasi akan 148x148
3. Membuang kolom yang tidak digunakan
4. Melakukan feture Engineering TF-IDF Vectorizer
- membuat fitur kolom
- transformasi matriks dai sparse (banyak 0) ke dense (lebih padat)

#### 4. 2 Data Preparation Modelling for Collaborative -> Neural Network
1. Mengkonversi encoding pada kolom 'UserId' dan 'AttractionId'-> jumlah unik UserId 33530 dan Attraction 30
2. Standarisasi nilai kolom 'Rating' menjadi range 0-1
3. Data splitting dengan rasio 80:20

#### 4. 3 Data Preparation Modelling for Collaborative -> SVD
1. Menginstall library surprise
2. Mempersiapkan data yang akan digunakan
3. Mengkonversi data ke format laten dengan mengubah DataFrame menjadi format standar library Suprise dan membuat skala rating 1-5

## 5. Build Model
#### 5. 1 Content Based Cosine Similarity

1. Menghitung kesamaan antar item
Cosine similarity mengukur kesamaan antara dua vektor dan menentukan apakah kedua vektor tersebut menunjuk ke arah yang sama. Ia menghitung sudut cosinus antara dua vektor. Semakin kecil sudut cosinus, semakin besar nilai cosine similarity. cosine similarity digunakan untuk mengukur kesamaan nama wisata sesuai mode kunjungan dan jenis wisata sesuai mode kunjungan. Sehingga wisata memiliki kesamaan pada jenis wisata dan mode kunjungan satu antar lainnya
2. Implementasi hasil model
    Input wisata -> 'Sanur Beach'

**=== Recommendation System Content Based-Cosine Similarity ===**


======= 10 places to go based on item --> Sanur Beach ========
1 Balekambang Beach : Malang District
2 Goa Cina Beach : Dusun Trowotratih, Desa Sitiarjo Kecamatan Sumbermanjing Wetan, Malang 65111 Indonesia
3 Kuta Beach  Bali : Kuta
4 Seminyak Beach : Seminyak
5 Nusa Dua Beach : Semenanjung Nusa Dua, Nusa Dua 80517 Indonesia
6 Sempu Island : Sumber Manjing Wetan, Malang 65111 Indonesia
7 Jodipan Colorful Village : Gang 1 Jodipan, Kesatrian, Kec. Blimbing, Malang 65126 Indonesia
8 Mount Semeru Volcano : Malang Lumajang
9 Bromo Tengger Semeru National Park : Asrikaton - Pakis, Malang 65100 Indonesia
10 Waterbom Bali : Jl. Kartika Plaza, Kuta 80361 Indonesia

#### 5. 2 Collaborative Based NN

1. Setting parameter model
Kode class RecommenderNet ini terinspirasi dari tutorial dalam situs Keras dengan beberapa adaptasi sesuai kasus sistem rekomendasi. Menggunakan embedding_size = 35, embedding_initializer = 'he_normal', embeddings_regularizer = L2 norm, aktivasi = sigmoid.
Model ini menggunakan Binary Crossentropy untuk menghitung loss function, Adam (Adaptive Moment Estimation) sebagai optimizer, dan root mean squared error (RMSE) sebagai metrics evaluation. 
2. Training model
- Batch_size=32 
- epochs=15
3. Melihat grafik MSE
 proses training model cukup smooth dan model konvergen pada epochs sekitar 15. Dari proses ini, kita memperoleh nilai error akhir sebesar sekitar 0.19 dan error pada data validasi sebesar 0.34.

Nilai RMSE menunjukkan 0.2 dimana selama training nilai RMSE menurun dapat diartikan error semakin kecil

4. Hasil implementasi model
   
**=== Recommendation System Collaborative Based-Neural Network RecommenderNet ===**

->Showing recommendations for users: 9409

->Recent destinattion with high ratings from user
    - [ Points of Interest & Landmarks ] Tegalalang Rice Terrace : Jalan Raya Ceking, Tegalalang 80517 Indonesia
    - [ Waterfalls ] Tegenungan Waterfall : Jl. Raya Tegenungan, Kemenuh, Ubud 80581 Indonesia
    - [ Beaches ] Kuta Beach - Bali : Kuta
    
10 places to go - recommended
1 [ Nature & Wildlife Areas ] Sacred Monkey Forest Sanctuary : Jl. Monkey Forest, Ubud 80571 Indonesia
2 [ Water Parks ] Waterbom Bali : Jl. Kartika Plaza, Kuta 80361 Indonesia
3 [ Beaches ] Nusa Dua Beach : Semenanjung Nusa Dua, Nusa Dua 80517 Indonesia
4 [ Religious Sites ] Uluwatu Temple : Jl. Raya Uluwatu Southern part of Bali, Pecatu 80361 Indonesia
5 [ Religious Sites ] Tanah Lot Temple : Kecamatan Kediri, Kabupaten Tabanan, Beraban 82121 Indonesia
6 [ National Parks ] Bromo Tengger Semeru National Park : Asrikaton - Pakis, Malang 65100 Indonesia
7 [ Volcanos ] Mount Semeru Volcano : Malang Lumajang
8 [ Spas ] Khayangan Reflexology & Massage : Malang
9 [ Caverns & Caves ] Jomblang Cave : Jetis Wetan, Pacarejo, Semanu 55581 Indonesia
10 [ History Museums ] Ullen Sentalu Museum : Jl. Boyong Taman Wisata, 55581 Indonesia

#### 5. 3 Collaborative Based SVD
1. Training with Cross Validation 10 folds
Proses implementasi model menggunalakn algoritma SVD menggunakan crsoo-validation menjadi 10 folds. Nilai metrik yang akan digunakan adalah MSE dan MAE pada tiap folds apakah menunjukkan perbedaan signifikan (melihat nilai Standar Deviasi) dan besar nilai keduanya.

Berdasarkan nilai RMSE dari folds 1-10 menunjukkan nilai kecil yaitu 0.9 (dibawah 1, jika semakin besar cth 2.xx/5.xx maka buruk) dapat dikatakan prediksi baik. Dan nilai MAE yang kecil. Nilai STD menunjukkan nilai kecil sehingga hasil nilai MSE dan MAE masing-masing folds konsisten.

2. Hasil Implementasi Model

    Showing recent for users: 9409
    - [ Waterfalls ] Tegenungan Waterfall : Jl. Raya Tegenungan, Kemenuh, Ubud 80581 Indonesia
    - [ Points of Interest & Landmarks ] Tegalalang Rice Terrace : Jalan Raya Ceking, Tegalalang 80517 Indonesia
    - [ Beaches ] Kuta Beach - Bali : Kuta
   
10 places to go - probably you sholud like
1 [ Volcanos ] Mount Semeru Volcano : Malang Lumajang
2 [ Water Parks ] Waterbom Bali : Jl. Kartika Plaza, Kuta 80361 Indonesia
3 [ National Parks ] Bromo Tengger Semeru National Park : Asrikaton - Pakis, Malang 65100 Indonesia
4 [ Caverns & Caves ] Jomblang Cave : Jetis Wetan, Pacarejo, Semanu 55581 Indonesia
5 [ History Museums ] Ullen Sentalu Museum : Jl. Boyong Taman Wisata, 55581 Indonesia
6 [ Religious Sites ] Tanah Lot Temple : Kecamatan Kediri, Kabupaten Tabanan, Beraban 82121 Indonesia
7 [ Spas ] Khayangan Reflexology & Massage : Malang
8 [ Nature & Wildlife Areas ] Sempu Island : Sumber Manjing Wetan, Malang 65111 Indonesia
9 [ Neighborhoods ] Jodipan Colorful Village : Gang 1 Jodipan, Kesatrian, Kec. Blimbing, Malang 65126 Indonesia
10 [ Speciality Museums ] Museum Malang Tempo Doeloe : Jl. Gajahmada no. 2, Malang 65119 Indonesia

## 6. Evaluasi
Metrik pada model sistem rekomendasi berfokus pada RMSE dan MAE. RMSE merupakan mengukur akar dari rata-rata kuadrat selisih antara nilai prediksi dan nilai aktual, sehingga dapat menekankan kesalahan yang lebih besar, karena nilai kesalahan dikuadratkan. Sehingga dengan nilai RMSE kecil menunjukkan nilai error yang kecil juga
Selain itu metrik MAE digunakan untuk mengukur kesalahan dengan nilai rata-rata absolut antara nilai prediksi dan nilai aktual. MAE membantu mengukur seberapa besar rata-rata perbedaan antara nilai aktual dan nilai prediksi. Dengan nilai MAE yang semakin kecil menunjukkan nilai kedua tersebut memiliki error yang kecil

1. Content based
Berdasarkan 2 teknik untuk menemukan pola hubungan antar item, penggunaan cosine_similarity dapat menunjukkan item yang memiliki kesamaan dengan item yang diinput. Cosine similarity merupakan metrik untuk mengukur kemiripan antara 2 vector dimana berdasarkan sudut kosinus. Pada atribut yang memiliki nilai 1 merupakan atribut yang memilki kesamaan sedangkan nilai 0 atribut tidak memiliki kesamaan
Kernel sigmoid menggunakan fungsi sigmoid dalam menghitung kesamaan antara dua vektor dalam ruang fitur. Pada umumnya fungsi ini digunakan pada pendekatan hubungan yang non-linear.
Hasil pengembangan menggunakan kedua metode dapat menunjukkan 10 rekomendasi yang relate dengan input. Metode cosine similarity lebih memiliki kesamaan yang lebih dekat karena menggunakan skor kesamaan berbasis vektor dan kedua atribut memiliki hubungan/lineraritas (jenis wisata dan tempat wisata)


2. Collaborative based
Hasil penggunaan 2 algoritma adalah model dapat merekomendasi destinasi wisata. Pada penggunaan Neural Network menunjukkan nilai error MAE dan RMSE yang semakin rendah sekitar 0.19 sedangkan algoritma SVD sekitar 0.9-0.7. Algoritma NN dapat menunjukkan 10 rekomendasi teratas menyesuaikan jenis wisata yang mirip, frekuensi destinasi wisata yang banyak dikunjungi wisatawan dan rating detinasi wisata (membandingkan melihat hasil EDA-seperti jenis wisata yang sering muncul)
Pada algoritma SVD 10 rekomendasi teratas berdasarkan prediksi baru dari perhitungan fitur laten rating dan destinasi wisata. Sehingga rekomendasi menunjukkan destinasi wisata dengan kemiripan wisata yang tesembunyi (tidak terlalu menonjol dapat dilihat dengan perbandingan EDA) dan menghasilkan prediksi rating baru yang kemungkinan akan mirip dengan riwayat destinasi wisatawan. Sehingga model ini cocok untuk mengenalkan wisata baru.
Pada projek ini hasil sistem rekomendasi penggunaan algoritma NN menunjukkan nilai RMSE dan MAE lebih rendah dibandingkan menggunakan algoritma SVD. Selain itu hasil algoritma NN mendekati dengan hasil EDA dimana dengan jenis wisata dan destinasi wisata yang direkomendasikan sering muncul dan mendekati dengan jumlah rating yang tingga pada data, sesuai banyaknya riwayat kunjungan tiap pengunjung. Sedangkan SVD perlu dievaluasi kembali dan eksplore lagi pada proses training model karna saat ini menggunakan cross-validaton dan pengkonversian data yang menggunakan library surprise dan fitur laten.







# Laporan Proyek Machine Learning - Jody Irawan

## Project Overview

Perkembangan terus terjadi pada dunia teknologi. Hal ini dibuktikan dengan terus meningkatnya pengguna internet pada kehidupan di masyarakat. Konten hiburan seperti perfilman juga mengalami perkembangan pesat. Sekarang orang-orang tidak selalu harus pergi kebioskop atau tempat layar tancap ataupun di tv. Untuk menikmati film dijaman sekarang banyak aplikasi pemutar film maupun web yang mudah didapatkan dengan banyak list film didalamnya. Hal tersebut berakibat semakin banyaknya orang untuk menonton film yang mereka suka. Tetapi Tidak jarang seseorang yang ingin menonton film menjadi kebingungan karena terlalu banyak film yang tersedia di internet. Oleh karena itu, dibutuhkan sebuah sistem yang dapat membantu memberikan informasi terkait film yang sesuai dengan keinginan pengguna. Sistem tersebut sering disebut dengan sistem rekomendasi.

Untuk itu, disini saya akan membuat sistem rekomendasi film yang berguna untuk merekomendasikan film yang bisa ditonton pengguna berdasarkan film yang mereka suka. Pada proyek sistem rekomendasi ini, disini saya menggunakan dataset data film yang terdiri dari data informasi movie dan data informasi user rating lalu model development yang digunakan yaitu model development dengan Collaborative Filtering. Diharapkan solusi Collaborative Filtering dapat memberikan solusi yang tepat dalam merekomendasikan sebuah film pada user.

## Business Understanding

Tujuan pada proyek ini yaitu merekomendasikan film berdasarkan film yang mereka sukai dengan membuat sistem rekomendasi dengan menggunakan dataset film dan menggunakan model development dengan Collaborative Filtering.

### Problem Statements
Berikut adalah problem statement dari proyek ini:
- Bagaimana membuat sistem rekomendasi yang dapat memberikan referensi film yang mungkin disukai oleh pengguna?

### Goals

Menjelaskan tujuan proyek yang menjawab pernyataan masalah:
- memberikan rekomendasi film berdasarkan film yang disukai pengguna berdasarkan rating yang telah diberikan sebelumnya.

### Solution Approach
solusi permasalahan yang dapat diberikan :
- Membagi dataset menjadi data latih (train) dan data uji (test) dengan rasio 80% untuk data latih dan 20% untuk data uji.
- Melakukan pengembangkan model dengan Collaborative Filtering. Collaborative Filtering memberi rekomendasi bedasarkan penilaian komunitas pengguna atau biasa disebut dengan rating.kekurangan dalam model ini yaitu membutuhkan parameter rating. Dimana jika suatu film tidak memiliki rating karena film tersebut baru atau memang kurang tidak akan direkomendasikan oleh sistem.

## Data Understanding
Data yang saya gunakan untuk proyek ini adalah [dataset rekomendasi movie](https://www.kaggle.com/uttam94/recommendation), dimana dataset ini terdapat informasi mengenai film-film tua hingga yang terbaru dengan kategori dan rating berdasarkan user berikan. dataset ini saya unduh dari kaggle. Dataset ini terdiri dari 2 file yaitu 'movies.csv' dan 'ratings.csv'. Pada masing-masing file tersebut terdapat beberapa variable atau kolom dengan rincian sebagai berikut:

Variabel-variabel pada 'movies.csv' adalah sebagai berikut:
- movieId : merupakan id movie yang mengidentifikasi judul film.
- title : merupakan judul film.
- gendres : daftar genre/kategori yang dipisahkan dengan garis tegak.

![movie_csv](https://github.com/jodyirawan/Proyek-Sistem-Rekomendasi/blob/main/Data%20Gambar%20Proyek%20Akhir%20MLT/MoviesVariable.png?raw=true)

Variabel-variabel pada 'ratings.csv' adalah sebagai berikut:
- userId : Merupakan user id yang dibuat secara berurut dan tidak terdefinisi.
- movieId :merupakan id movie yang mengidentifikasi judul film.
- rating : skor penilaian film penilaian dari 1 (terendah) hingga 5 (tertinggi)
- timestamp : Stempel waktu informasi riwayat waktu user memberikan data.

![rating_csv](https://github.com/jodyirawan/Proyek-Sistem-Rekomendasi/blob/main/Data%20Gambar%20Proyek%20Akhir%20MLT/RatingVariable.png?raw=true)

Disini saya juga menggunakan visualisasi data untuk melihat film paling populer yang paling banyak user tonton dan disukai. Visualisasi ini menggunakan barplot dimana data diambil dari gabungan dataset movies dan ratings. Terlihat pada gambar dibawah bahwa film Forrest Gump (1994) menjadi film yang paling populer.
![MoviePopuler](https://github.com/jodyirawan/Proyek-Sistem-Rekomendasi/blob/main/Data%20Gambar%20Proyek%20Akhir%20MLT/MoviePopuler.png?raw=true)

## Data Preparation
Data preparation bertujuan untuk menyiapkan data sebelum masuk ke proses modeling. Selain itu, data preparation juga berguna untuk meningkatkan akurasi saat training data. Pada tahap ini dilakukan proses data preparation yaitu sebagai berikut :
- Membuat variabel preparation yang berisi dataframe movies_one kemudian mengurutkan berdasarkan movieId.
- Membuang data duplikat pada variabel preparation.
- konversi data series menjadi list menggunakan fungsi tolist() dari library numpy..
- membuat dictionary untuk menentukan pasangan key-value pada data movie_id dan movie_name.
- Membagi dataset menjadi data latih (train) dan data uji (test) dengan rasio 80% untuk data latih dan 20% untuk data uji.

## Modeling
Pada proyek ini saya menggunakan pendekatan Collaborative Filtering.Collaborative Filtering melakukan penyeleksian pada sistem rekomendasi yang memanfaatkan kesamaan antara pengguna dan item secara bersamaan untuk memberi rekomendasi. Olehkarena itu teknik ini cocok dipakai pada proyek ini karena teknik ini membutuhkan data rating dari user. Proses dari model ini terdiri dari :
- melakukan proses embedding untuk menghitung skor kecocokan user pengguna dan movie lalu melakukan operasi perkalian dot product antara embedding user dan movie.
- lakukan proses compile terhadap model. Model ini menggunakan Binary Crossentropy untuk menghitung loss function, Adam (Adaptive Moment Estimation) sebagai optimizer, dan root mean squared error (RMSE) sebagai metrics evaluation. 
- mulailah proses training dengan model.fit.
- Mendapatkan Rekomendasi film yang belum user tonton dan cocok berdasarkan rating yang diberikan sebelumnya.

Berikut ini adalah hasil dari rekomendasi film menggunakan Collaborative Filtering:
![HasilRekomendsasi](https://github.com/jodyirawan/Proyek-Sistem-Rekomendasi/blob/main/Data%20Gambar%20Proyek%20Akhir%20MLT/HasilRekomendasi.png?raw=true)
Dapat dilihat pada gambar hasil prediksi bahwa user dengan id '482' dengan film favoritnya berdasarkan rating yang user berikan yaitu salah satunya film 'Back to the Future (1985)'. Maka dari itu sistem dapat merekomendasikan film yang mirip dengan user tersebut. Beberapa film rekomendasi user tersebut seperti film 'Band of Brothers (2001)', 'Trial, The (Procès, Le) (1962)' dan 'Paths of Glory (1957)'.

## Evaluation

Model ini menggunakan Binary Crossentropy untuk menghitung loss function, Adam (Adaptive Moment Estimation) sebagai optimizer, dan root mean squared error (RMSE) sebagai metrics evaluation. Root mean squared error (RMSE) adalah matrik yang berfungsi untuk menghitung kuadrat dari rata-rata selisih kuadrat antara nilai taksiran dan nilai sebenarnya dari variabel/fitur. Dengan demikian semakin rendahnya nilai RMSE makan semakin baik model tersebut dalam melakukan prediksi. Berikut rumus dari RMSE:
![RumusMSE](https://github.com/jodyirawan/Proyek-Sistem-Rekomendasi/blob/main/Data%20Gambar%20Proyek%20Akhir%20MLT/RMSE.png?raw=true)

Berikut visualisasi (RMSE) dari metriks yang digunakan :
![VisualisasiRMSE](https://github.com/jodyirawan/Proyek-Sistem-Rekomendasi/blob/main/Data%20Gambar%20Proyek%20Akhir%20MLT/VisualisasiMetrik.png?raw=true)
Metriks yang digunakan RMSE dapat memberikan prediksi yang cukup akurat. Dapat dilihat visualisasi dari metriks yang digunakan, kita memperoleh nilai error akhir sebesar sekitar 0.17 dan error pada data validasi sebesar 0.20. Nilai tersebut cukup bagus untuk sistem rekomendasi.

Berdasarkan proses yang sudah dilakukan sebelumnya maka dapat disumpulkan bahwa dari pembuatan sistem rekomendasi movie dengan model Collaborative Filtering berhasil membuat sistem rekomendasi film. Sistem dapat merekomendasikan judul film yang kepada user berdasarkan film yang mereka suka berdasarkan film yang telah user berikan rating sebelumnya.
 


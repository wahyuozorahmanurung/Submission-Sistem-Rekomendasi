# Submission-Sistem-Rekomendasi

# Laporan Proyek - Wahyu Ozorah Manurung

## Sistem Rekomendasi Movie (Film)

## Project Overview

### Latar Belakang
Dalam era digital saat ini, volume data yang dihasilkan oleh pengguna meningkat secara eksponensial, khususnya dalam industri hiburan seperti film dan televisi. Pengguna sering kali dihadapkan pada pilihan yang sangat banyak, sehingga mengalami kesulitan dalam menemukan konten yang sesuai dengan preferensi mereka. Untuk mengatasi permasalahan ini, sistem rekomendasi menjadi solusi penting dalam membantu pengguna mendapatkan saran yang relevan secara otomatis (Ricci et al., 2015). Sistem rekomendasi telah menjadi komponen utama dalam berbagai platform digital seperti Netflix, Amazon Prime, dan Disney+, karena terbukti mampu meningkatkan pengalaman pengguna dan keterlibatan mereka terhadap platform (Aggarwal, 2016). Dua pendekatan utama yang digunakan dalam pengembangan sistem rekomendasi adalah Content-Based Filtering dan Collaborative Filtering.

Content-Based Filtering merupakan metode yang merekomendasikan item berdasarkan kesamaan konten antara item yang pernah disukai pengguna dengan item lainnya (Han, Pei, & Kamber, 2011). Dalam proyek ini, pendekatan content-based menggunakan teknik representasi teks seperti TF-IDF (Term Frequency-Inverse Document Frequency) untuk memodelkan fitur dari setiap film, termasuk genre, sinopsis, dan kata kunci. Kemudian, kemiripan antar film dihitung menggunakan cosine similarity untuk merekomendasikan film yang paling mirip (Salton & Buckley, 1988).

Sementara itu, Collaborative Filtering memanfaatkan pola interaksi antar pengguna dan item, tanpa memperhatikan konten dari item tersebut. Teknik ini merekomendasikan item berdasarkan preferensi pengguna lain yang memiliki pola perilaku serupa. Salah satu algoritma populer dalam collaborative filtering adalah Matrix Factorization seperti ALS (Alternating Least Squares) dan pendekatan berbasis memori seperti K-Nearest Neighbors (KNN) (Ricci et al., 2015; Aggarwal, 2016). Pendekatan ini sangat efektif dalam menangkap preferensi laten pengguna dan sering digunakan dalam sistem rekomendasi skala besar.
Dengan mengombinasikan kedua pendekatan ini, sistem rekomendasi dapat memberikan hasil yang lebih akurat dan personal, baik berdasarkan karakteristik konten maupun perilaku pengguna.

### Referensi
Aggarwal, C. C. (2016). Recommender Systems: The Textbook. Springer. https://doi.org/10.1007/978-3-319-29659-3, Han, J., Pei, J., & Kamber, M. (2011). Data Mining: Concepts and Techniques (3rd ed.). Morgan Kaufmann., Ricci, F., Rokach, L., & Shapira, B. (2015). Recommender Systems Handbook. Springer. https://doi.org/10.1007/978-1-4899-7637-6, Salton, G., & Buckley, C. (1988). Term-weighting approaches in automatic text retrieval. Information Processing & Management, 24(5), 513–523.

## Business Understanding
Sistem rekomendasi memiliki peranan penting dalam membantu pengguna menemukan konten hiburan yang sesuai dengan preferensi mereka. Namun, untuk merancang sistem rekomendasi yang efektif, perlu dilakukan pemahaman mendalam terhadap permasalahan bisnis yang dihadapi serta tujuan yang ingin dicapai

### Problem Statements
- Bagaimana cara membantu pengguna menemukan film yang sesuai dengan preferensi mereka secara otomatis di tengah banyaknya pilihan film yang tersedia?
- Bagaimana sistem rekomendasi dapat mengidentifikasi film yang relevan meskipun pengguna belum pernah menontonnya sebelumnya?
- Bagaimana menggabungkan Content-Based Filtering dan Collaborative Filtering agar sistem rekomendasi menjadi lebih akurat dan responsif terhadap berbagai jenis pengguna (baru maupun lama)?

### Goals
- Mengembangkan sistem rekomendasi film yang mampu menyarankan film relevan berdasarkan kesamaan konten seperti genre, sinopsis, dan kata kunci.
- Membangun sistem rekomendasi yang dapat menyarankan film baru berdasarkan perilaku pengguna lain yang serupa.
- Menggabungkan dua pendekatan tersebut untuk memperkuat performa sistem rekomendasi secara keseluruhan.

### Solution Statements
- Content-Based Filtering dengan Genre dan Tag
Menggunakan TF-IDF dan cosine similarity pada fitur genre dan tag dari dataset MovieLens untuk merekomendasikan film yang sesuai dengan preferensi pengguna.
- Collaborative Filtering Berbasis Matrix Factorization
Menerapkan model Matrix Factorization dengan TensorFlow/Keras pada data rating MovieLens untuk memprediksi film baru
Menggabungkan Content-Based dan Collaborative Filtering dengan bobot prediksi untuk rekomendasi personal bagi pengguna baru dan lama,

## Data Understanding 
Proyek ini menggunakan dataset dari Kaggle berjudul Movie Recommendation Data yang dapat diunduh melalui tautan berikut:
🔗 https://www.kaggle.com/datasets/rohan4050/movie-recommendation-data

Dataset ini berasal dari MovieLens, salah satu dataset paling populer untuk membangun dan mengevaluasi sistem rekomendasi. Dataset ini terdiri dari beberapa file CSV yang memuat informasi film, rating pengguna, tag, serta metadata lainnya. Data ini mencerminkan kebiasaan pengguna dalam memberikan penilaian terhadap film dan memungkinkan pembelajaran preferensi pengguna.

Jumlah Data
- movies.csv : 9.742 data baris dan 3 kolom film (tidak ada duplikat dan missing values)
- ratings.csv : 9724 data baris dan 4 data kolom penilaian dari 610 pengguna (tidak ada duplikat dan missing values)
- links.csv : 9.742 relasi baris dan 3 kolom antara MovieLens ID dan IMDb/ TMDb ID (tidak ada duplikat dan 8 missing values pada tmdbId )
- tags.csv : 1.572 data baris dan 4 kolom tag (kata kunci) yang diberikan oleh pengguna (tidak ada duplikat dan missing values)
- movies_metadata.csv : Metadata tambahan dari film (genre, sinopsis, dan lainnya) sebanyak 45436 baris dan 19 kolom
  Mising values: belongs_to_collection	40972, homepage	37684, imdb_id	17, original_language	11, overview	954, popularity	5, poster_path	386, production_companies	3, production_countries	3, release_date	87, 
  revenue	6, runtime	263, spoken_languages	6, status	87, tagline	25054, title	6, video	6, vote_average	6, vote_count	6 (tapi ini tidak digunakan di proyek saya)


### Variabel-variabel pada dataset adalah sebagai berikut:
1. movies.csv
Berisi informasi dasar mengenai film:
 
  - movieId: ID unik untuk masing-masing film.
  - title: Judul lengkap film, termasuk tahun rilis.
  - genres: Genre film dalam bentuk string yang dipisahkan oleh delimiter.

2. ratings.csv
Mencatat rating yang diberikan oleh pengguna:
 
  - userId: ID unik pengguna.
  - movieId: ID film yang dirating.
  - rating: Nilai rating (biasanya dalam skala 0.5 hingga 5.0).
  - timestamp: Waktu pemberian rating dalam format UNIX time.

3. tags.csv
Menunjukkan tag (kata kunci/keterangan) yang ditambahkan pengguna ke film:
 
  - userId: ID pengguna yang memberi tag.
  - movieId: ID film yang diberi tag.
  - tag: Teks tag yang diberikan.
  - timestamp: Waktu penambahan tag.
  
4. links.csv
Menyediakan koneksi antara movieId dengan ID dari basis data film eksternal:
 
  - movieId: ID film dari MovieLens.
  - imdbId: ID film di IMDb.
  - tmdbId: ID film di The Movie Database (TMDb).

Beberapa tahapan eksplorasi data telah dilakukan untuk memahami karakteristik dataset, antara lain:

**Cek Missing Vaues**

- Masing-Masing Data
    
    ![image](https://github.com/user-attachments/assets/d6483c51-f660-4931-a929-46bbcdb95c80)

    Pada masing-masing data missing values hanya terdapat pada links.csv yaitu 8 missing values pada tmdbId

**cek duplicated**

- Pada masing-masing data set

  ![image](https://github.com/user-attachments/assets/4e1199a6-dbe8-44df-aaf8-5beca60150e4)

  Pada masing-masing data set tidak terdapat data duplikat

## Data Preparation

### **Content Based Filtering**

1. Merge movie 
  ```python
   movie_info = pd.concat([links, movies, ratings, tags])
   movie = pd.merge(ratings, movie_info , on='movieId', how='left')
   movie
  ```
  ![image](https://github.com/user-attachments/assets/fe6d9d75-1ec0-40b4-9cb0-9f3436218764)

Pertama saya Menggabungkan beberapa DataFrame (links, movies, ratings, tags) menjadi satu DataFrame bernama movie menggunakan pd.concat(). Kemudian, movie_info digabung lagi dengan ratings berdasarkan kolom movieId menggunakan pd.merge() dengan metode join kiri (how='left'). Hasil akhirnya adalah DataFrame movie yang berisi informasi rating yang telah dilengkapi dengan data tambahan dari links, movies, dan tags sesuai dengan movieId. Terlihat ada data yang masih NaN detail pada gambar dibawah ini ketika di merge

  ![image](https://github.com/user-attachments/assets/509eadbb-2b4c-4a6d-8dd2-9ca0947d8edb)

Data preparation sangat penting dalam pipeline machine learning karena memastikan data dalam kondisi bersih, terstruktur, dan siap digunakan oleh algoritma untuk pelatihan dan prediksi. Proses ini dilakukan secara bertahap dan sistematis agar menghasilkan model yang akurat dan dapat diinterpretasikan dengan baik.

2. Duplikat data merge movie

  ![image](https://github.com/user-attachments/assets/1b729596-acbf-49b9-a86a-c2e78b28f23a)

movie.duplicated().sum() menghitung jumlah baris duplikat dalam DataFrame movie, yaitu baris-baris yang memiliki semua nilai kolom yang sama persis dengan baris lain. Sementara movie[movie.duplicated()]   
menampilkan detail baris-baris duplikat tersebut dan terlihat tidak ada duplikat

3. Merge Data
   Melakukan penggabungan beberapa DataFrame untuk membentuk satu DataFrame movie yang berisi informasi lengkap tentang film
   
 - Gabungkan data movie dan links
 - Gabungkan dengan tags
 - Gabungkan dengan ratings
   
4. Mengatasi Missing Values
   - Mengisi semua kolom numerik yang kosong dengan median
   - Mengisi semua kolom kategorikal (object) yang kosong dengan modus
 cek hasil
  ```python
    print("\nJumlah nilai NaN setelah dibersihkan:")
    print(movie.isnull().sum()[movie.isnull().sum() > 0])
  ```
  Membersihkan data pada DataFrame `movie` dengan mengisi nilai kosong (NaN). Untuk kolom numerik (`float64` dan `int64`), nilai kosong diisi dengan nilai median kolom tersebut. Untuk kolom kategorikal 
  (`object`), nilai kosong diisi dengan nilai modus (nilai yang paling sering muncul), atau `'Unknown'` jika tidak ada modus. Setelah proses ini, program mencetak jumlah nilai NaN yang tersisa, dan hasilnya 
  menunjukkan tidak ada lagi data yang kosong.

![image](https://github.com/user-attachments/assets/ce916349-6bea-43f2-8895-7220a5c3ec26)

5. Grouping
   
   ```python
     movie.groupby('movieId').sum()
   ```
  movie.groupby('movieId').sum() mengelompokkan data dalam DataFrame movie berdasarkan kolom movieId, lalu menjumlahkan semua kolom numerik untuk setiap grup (film). Hasilnya adalah DataFrame baru di mana setiap   baris mewakili satu movieId, dan kolom-kolomnya berisi total nilai dari kolom numerik seperti rating

![image](https://github.com/user-attachments/assets/6d741ce9-e007-499d-b2dd-cdf32f95f4b3)

6. Mengurutkan dataframe movie
   
  Mengurutkan DataFrame movie berdasarkan kolom movieId secara ascending (dari kecil ke besar) dan menyimpan hasilnya ke variabel baru fix_movie. Setelah itu, ketika fix_movie dipanggil, akan menampilkan       
  DataFrame yang sudah terurut rapi berdasarkan movieId.

![image](https://github.com/user-attachments/assets/44865805-6d03-4c5b-8d81-5dac78b12114)

![image](https://github.com/user-attachments/assets/f5b4f27c-197c-4986-930e-871b40a23ce5)

terlihat ada 9724 

7. Mengoversi menjadi data list
   -  Mengonversi data series ‘movieId’ menjadi dalam bentuk list
   -  Mengonversi data series ‘title’ menjadi dalam bentuk list
   -  Mengonversi data series ‘genres’ menjadi dalam bentuk list
     
Mengubah kolom `movieId`, `title`, dan `genres` dari DataFrame `fix_movie` menjadi tiga list terpisah: `movie_id`, `movie_name`, dan `movie_genre`. Kemudian, dengan mencetak panjang masing-masing list   
(`len()`), ketiga list tersebut sama-sama berisi 285,762 elemen, yang berarti setiap baris di DataFrame `fix_movie` terwakili secara lengkap dan konsisten di ketiga list tersebut tanpa ada kehilangan data.

8. Membuat DataFrame baru bernama `movie_new`
   
   ![image](https://github.com/user-attachments/assets/e7f508a5-fd0e-4080-9618-71f0764728ed)

   DataFrame ini menyusun ulang data film dari `fix_movie` dalam format yang lebih sederhana dengan nama kolom yang lebih jelas. Ketika `movie_new` dipanggil, akan menampilkan tabel baru yang memuat data film       lengkap sesuai dengan ketiga list tersebut.

9. Hapus duplikasi berdasarkan movie_name

   ```python
   movie_new = movie_new.drop_duplicates(subset='movie_name', keep='first')
   ```
  Kode tersebut menghapus baris duplikat dalam DataFrame movie_new berdasarkan kolom movie_name. Jika ada beberapa baris dengan judul film yang sama, hanya baris pertama yang dipertahankan (keep='first'), 
  sedangkan baris duplikat berikutnya dihapus. Ini berguna untuk memastikan setiap film muncul hanya sekali dalam DataFrame, menghilangkan entri ganda berdasarkan nama film.

Hasil 

![image](https://github.com/user-attachments/assets/ef1de77c-f422-4f54-80a0-244d9cecf0d5)

### **Collaborative Filtering**

1. Menjadikan rating sebagai df
2. Mengubah menjadi list dan encode proses pada userid
   - Mengubah userID menjadi list tanpa nilai yang sama
   - Melakukan encoding userID
   - Melakukan proses encoding angka ke ke userID
3. Mengubah menjadi list dan encode proses movieid
   - Mengubah movieId menjadi list tanpa nilai yang sama
   - Melakukan proses encoding movieId
   - Melakukan proses encoding angka ke movieId
4. Mapping  userId dan movieId ke dataframe yang berkaitan.
   - Mapping userId ke dataframe genres
   - Mapping movieD ke dataframe movies

Selanjutnya menghitung dan menampilkan informasi penting tentang data rating film yang sedang kamu proses. Pertama, variabel num_users dan num_movie diisi dengan jumlah user dan film unik berdasarkan hasil encoding yang telah dibuat sebelumnya, yaitu dari dictionary user_to_user_encoded dan movie_encoded_to_movie. Kemudian, kolom baru ratings di DataFrame df dibuat dengan menyalin nilai rating asli dari kolom rating dan mengubahnya menjadi tipe data float32 agar lebih efisien untuk komputasi. Selanjutnya, kode mengambil nilai rating minimum (min_rating) dan maksimum (max_rating) dari kolom rating asli untuk mengetahui rentang skor rating yang diberikan oleh user.

Dari hasil tersebut, dapat disimpulkan:

- Jumlah user unik di dataset adalah 610.

- Jumlah movie unik di dataset adalah 9724.

- Rating terendah yang diberikan user ke movie adalah 0.5.

- Rating tertinggi yang diberikan adalah 5.0.

## Modeling
Dalam proyek ini, digunakan dua pendekatan utama untuk membangun sistem rekomendasi film:

- Content-Based Filtering

- Collaborative Filtering (Matrix Factorization)
   
Pendekatan ini kemudian digabungkan dalam sistem hybrid untuk meningkatkan akurasi dan fleksibilitas terhadap berbagai tipe pengguna (baru dan lama).

### **1. Content-Based Filtering**

Content-Based Filtering memberikan rekomendasi berdasarkan kesamaan konten film, khususnya genre dan tag. Sistem ini menggunakan representasi teks yang diekstraksi dari data genres dan tags. disini Menggunakan TF-IDF Vectorizer

Parameter Utama:
- TF-IDF Vectorizer: stop_words='english'
- Similarity: Cosine Similarity
  
```python
  # Inisialisasi TfidfVectorizer
   tfidf_vectorizer = TfidfVectorizer()
    
  # Melakukan perhitungan idf pada data genre
   tfidf_vectorizer.fit(movie_new['genre'])
    
  # Mapping array dari fitur index integer ke fitur nama
   tfidf_vectorizer.get_feature_names_out()
```
- Menghitung kemiripan antar film menggunakan Cosine Similarity.

```python
  cosine_sim = cosine_similarity(tfidf_matrix)
  cosine_sim
```
 menghitung **cosine similarity** antara semua pasangan film berdasarkan matriks TF-IDF `tfidf_matrix` dari genre mereka. Fungsi `cosine_similarity(tfidf_matrix)` menghasilkan matriks similiarity persegi, di 
 mana setiap nilai menunjukkan seberapa mirip dua film dalam hal genre mereka—nilai 1 berarti sangat mirip (atau sama persis), dan nilai 0 berarti tidak mirip sama sekali. Hasil `cosine_sim` biasanya digunakan 
 untuk rekomendasi film berdasarkan kemiripan genre.
 
- Menyimpan hasil similarity matrix untuk memberikan rekomendasi berdasarkan film yang telah ditonton pengguna.
```python
  cosine_sim_df = pd.DataFrame(cosine_sim, index=movie_new['movie_name'], columns=movie_new['movie_name'])
```

![image](https://github.com/user-attachments/assets/6c87d6e8-6f5a-4dd3-a7fc-271a325ac807)

  mengubah matriks cosine similarity `cosine_sim` menjadi sebuah DataFrame `cosine_sim_df` dengan indeks dan kolom berupa nama film dari `movie_new['movie_name']`. Ini membuatnya lebih mudah dibaca dan diakses 
  menggunakan nama film. `print('Shape:', cosine_sim_df.shape)` menampilkan dimensi DataFrame, yang biasanya berbentuk persegi dengan ukuran (jumlah film × jumlah film).
  
  Kemudian, kode mengambil **sample acak 5 kolom** dan **10 baris** dari DataFrame similarity tersebut untuk ditampilkan, agar pengguna dapat melihat sebagian kecil nilai kemiripan antar film tanpa menampilkan s 
  seluruh matriks yang besar.

**REKOMENDASI**

Fungsi movie_recommendations ini memberikan rekomendasi film berdasarkan kemiripan genre menggunakan data cosine similarity.

* nama_movie: judul film yang ingin dicari rekomendasinya.
* similarity_data: DataFrame cosine similarity antar film.
* items: DataFrame berisi info film (movie_name dan genre).
* k: jumlah rekomendasi yang ingin ditampilkan.

**Langkah kerja fungsi:**

- Mengambil indeks film yang memiliki nilai similarity tertinggi terhadap nama_movie menggunakan argpartition untuk efisiensi.
- Memilih k+1 film teratas (termasuk film yang dicari).
- Menghapus film yang dicari (nama_movie) agar tidak muncul di rekomendasi.
- Menggabungkan judul film rekomendasi dengan info genre dari items.
- Mengembalikan DataFrame berisi rekomendasi sebanyak k film.

 > Melihat data Moviie Jumanji
  ```python
  movie_new[movie_new.movie_name.eq('Jumanji (1995)')]
  ```
![image](https://github.com/user-attachments/assets/9b80dc96-44ba-40bc-89e3-596e1b59c88d)

Data tersebut menunjukkan bahwa film "Jumanji (1995)" berada di baris ke-645 Ini berarti film tersebut terdaftar dengan genre petualangan, anak-anak, dan fantasi.

> Hasil Rekomendasi
  ```python
    movie_recommendations('Jumanji (1995)')
  ```
![image](https://github.com/user-attachments/assets/9f62b6e2-8f17-4ff3-8234-48ae12837353)

 Rekomendasi film yang diberikan untuk "Jumanji (1995)" memang sangat sesuai, karena semuanya punya genre yang mirip, yaitu Adventure|Children|Fantasy. Film-film seperti Indian in the Cupboard, Chronicles of   
 Narnia, dan Harry Potter sama-sama mengandung unsur petualangan dan fantasi yang cocok untuk penonton anak-anak atau keluarga, persis seperti "Jumanji."
 Ini menandakan model cosine similarity pada genre berhasil mengelompokkan film-film yang punya kesamaan tema genre secara akurat
 
**Kelebihan:**

- Mampu memberikan rekomendasi meskipun tidak ada data rating pengguna.
- Cocok untuk pengguna baru yang belum banyak memberikan rating.

** Kekurangan:**

- Tidak mempertimbangkan preferensi pengguna lain.
- Terbatas pada konten yang tersedia (hanya berdasarkan deskripsi film).


### **2. Model Development dengan Collaborative Filtering**

Collaborative Filtering menggunakan data rating dari pengguna lain untuk mempelajari pola dan preferensi pengguna. Dalam proyek ini, digunakan pendekatan Matrix Factorization dengan TensorFlow/Keras.

**Tahapan:**
- Membentuk matriks user-item dari ratings.csv.
- Membangun model neural network ringan untuk melakukan embedding user dan movie ID ke dalam vektor laten.
- Melatih model untuk meminimalkan error antara rating aktual dan rating yang diprediksi.

**Arsitektur Model:**
- User Embedding Layer dan Movie Embedding Layer (masing-masing 50 dimensi).
- Dense layers sebagai penggabungan representasi.
- Output layer dengan aktivasi linear untuk prediksi rating.

**Parameter Utama:**
- Embedding dimension: 50
- Epoch: 10
- Optimizer: Adam
- Loss Function: Mean Squared Error (MSE)

**Improvement & Tuning:**
- Tuning jumlah epoch dan embedding size dicoba untuk menemukan trade-off terbaik antara akurasi dan overfitting.
- Model dievaluasi menggunakan Root Mean Squared Error (RMSE) pada data validasi.
  
1. Melakukan encoding userid
   - user_ids = df['userId'].unique().tolist()
     Mengambil semua nilai unik dari userId dan mengubahnya menjadi list tanpa duplikasi.
   - user_to_user_encoded = {x: i for i, x in enumerate(user_ids)}
     Membuat dictionary yang memetakan setiap userId asli ke angka indeks (encoded userID). Misalnya, userId asli 123 bisa jadi 0, userId 456 jadi 1, dst.
   - user_encoded_to_user = {i: x for i, x in enumerate(user_ids)}
     Membuat dictionary kebalikan, dari angka encoding ke userId asli, agar bisa mengonversi
     
 2. Encoding movieId:
    - movie_ids = df['movieId'].unique().tolist()
     Mengambil daftar unik movieId dari data rating.
    - movie_to_movie_encoded dan movie_encoded_to_movie membuat mapping dua arah antara movieId asli dengan angka indeks yang mewakili setiap film.
     
 3. Mapping ke dataframe
    - df['genres'] = df['userId'].map(user_to_user_encoded)
      Ini agak aneh karena kamu memetakan kolom userId ke kolom genres di df. Biasanya genres itu terkait dengan film, bukan user.
    - df['movies'] = df['movieId'].map(movie_to_movie_encoded)
       Mapping movieId asli ke angka encoded, disimpan di kolom baru movies.
     
 4. Data Split
     - Membuat variabel x untuk mencocokkan data genres  dan movies menjadi satu value
         
       ```python
         x = df[['genres', 'movies']].values
       ```
     - Membuat variabel y untuk membuat ratings dari hasil

        ```python
           y = df['ratings'].apply(lambda x: (x - min_rating) / (max_rating - min_rating)).values
        ```
      - Membagi menjadi 80% data train dan 20% data validasi
        ```python
            train_indices = int(0.8 * df.shape[0])
        ```
5. mendefinisikan model rekomendasi dengan TensorFlow Keras menggunakan embedding untuk user dan movie. Kelas `RecommenderNet` membuat embedding untuk user, movie, dan bias keduanya. Pada metode `call`,   
   model mengambil embedding user dan movie, menghitung dot product antara keduanya, lalu menambahkan bias user dan movie. Hasilnya diproses dengan fungsi sigmoid untuk menghasilkan prediksi rating yang 
   dinormalisasi antara 0 dan 1. Model ini digunakan untuk memprediksi preferensi user terhadap film.
6. Menginisialisasi model rekomendasi

   menginisialisasi model rekomendasi `RecommenderNet` dengan ukuran embedding 50 untuk user dan movie. Setelah itu, model dikompilasi dengan menggunakan fungsi loss `BinaryCrossentropy` yang cocok untuk 
   output bernilai antara 0 dan 1 (hasil sigmoid). Optimizer yang digunakan adalah Adam dengan learning rate 0.001, yang efektif untuk pelatihan jaringan saraf. Sebagai metrik evaluasi, dipilih Root Mean 
   Squared Error (RMSE) untuk mengukur seberapa dekat prediksi model dengan nilai sebenarnya, sehingga membantu memantau performa selama proses pelatihan.

7. Proses pelatihan (training) model RecommenderNet

      ```python
          history = model.fit(
          x = x_train,
          y = y_train,
          batch_size = 64,
          epochs = 100,
          validation_data = (x_val, y_val)
        )
      ```
   Kode ini menjalankan proses pelatihan (training) model `RecommenderNet` menggunakan data training yang sudah disiapkan. Model dilatih selama 100 epoch dengan batch size 64, artinya data dibagi menjadi   
   potongan kecil berisi 64 contoh untuk setiap langkah pembaruan bobot. Selain itu, model juga dievaluasi secara berkala menggunakan data validasi (`x_val`, `y_val`) untuk memonitor performa dan mencegah 
   overfitting. Hasil pelatihan disimpan di variabel `history` yang berisi catatan metrik seperti loss dan RMSE dari tiap epoch, sehingga bisa dianalisis lebih lanjut.

**REKOMENDASI**

memulai dengan membaca data rating film dan memilih secara acak satu pengguna (`user_id`). Kemudian, kode mengambil daftar film yang sudah ditonton oleh pengguna tersebut dan menentukan film yang belum ditonton dengan membandingkan semua film yang ada di dataset dengan film yang sudah dilihat oleh pengguna.

Setelah itu, film yang belum ditonton diubah menjadi format encoded menggunakan peta `movie_to_movie_encoded`, dan `user_id` juga di-encode. Kode kemudian membuat array gabungan antara ID pengguna dan film yang belum ditonton dalam bentuk encoded, yang nantinya digunakan sebagai input untuk model rekomendasi dalam memprediksi film yang mungkin disukai pengguna.

![image](https://github.com/user-attachments/assets/b55870ef-daba-490e-969b-a4f4aef83db7)

Hasil keluaran ini menunjukkan rekomendasi film untuk pengguna dengan ID 182 berdasarkan rating film yang sudah pernah ditontonnya dan prediksi model untuk film-film yang belum ditonton. Bagian pertama menampilkan lima film favorit pengguna, yaitu film-film dengan rating tertinggi dari riwayat tontonan mereka, seperti *Casino (1995)* dan *Pulp Fiction (1994)*, lengkap dengan genre masing-masing.
Bagian kedua menampilkan 10 film rekomendasi terbaik yang diprediksi model memiliki potensi disukai oleh pengguna tersebut. Film-film ini beragam dari genre animasi, komedi, drama, hingga dokumenter, seperti *Lesson Faust (1994)* dan *Tea with Mussolini (1999)*. Dengan daftar ini, pengguna bisa mendapatkan pilihan film baru yang sesuai dengan preferensi berdasarkan pola rating sebelumnya.

**Kelebihan:**
- Mampu mempelajari preferensi pengguna dari data interaksi.
- Dapat merekomendasikan film yang tidak pernah dilihat sebelumnya oleh pengguna.

**Kekurangan:**
- Memerlukan cukup banyak data rating agar efektif (masalah cold start).
- Tidak menggunakan informasi konten film.

**Pemilihan Model Terbaik: Collaborative Filtering**

Berdasarkan eksplorasi dan hasil evaluasi pada notebook, Collaborative Filtering dengan Matrix Factorization dipilih sebagai model terbaik, karena:
- Memberikan rekomendasi yang lebih personal dan relevan, berdasarkan perilaku pengguna.
- Mampu mempelajari representasi laten yang kompleks, yang tidak bisa ditangkap oleh Content-Based Filtering.
- Loss training dan validation pada model menunjukkan konvergensi yang baik.
- Dataset MovieLens menyediakan data rating yang cukup besar (lebih dari 100 ribu interaksi), sehingga model Collaborative Filtering bisa dilatih secara optimal.

Sementara Content-Based Filtering tetap berguna, terutama untuk pengguna baru, namun pada implementasi dan hasil aktual dalam notebook, model Collaborative Filtering menghasilkan performa yang lebih baik secara keseluruhan.

## Evaluation

1. Model Development dengan Collaborative Filtering
   
   Evaluasi yang digunakan adalah Precision@K
   
   ![image](https://github.com/user-attachments/assets/33889c80-3747-49b2-88b5-063fcd0b3663)

   didapatkan bahwa hasil nya sebagai berikut
   
   ![image](https://github.com/user-attachments/assets/6afc3252-e21c-413e-b699-fd6c84b571ac)

   Evaluasi sistem rekomendasi yang dilakukan menggunakan metrik Precision@5 menunjukkan hasil sebesar 0.60. Artinya, dari 5 film yang direkomendasikan oleh sistem berdasarkan film "Jumanji (1995)", terdapat 3 
   film yang benar-benar relevan atau disukai pengguna. Ini menunjukkan bahwa sistem mampu memberikan rekomendasi yang sesuai dengan preferensi pengguna sebesar 60%. Nilai Precision@5 sebesar 0.60 (60%) dapat dikatakan cukup baik, terutama dalam konteks sistem rekomendasi berbasis konten (Content-Based Filtering) yang hanya menggunakan informasi dari fitur film seperti genre, tanpa mempertimbangkan pola perilaku 
   pengguna lain.

  **Tahapan**
  - Menyusun daftar film yang benar-benar disukai user (ground truth)

  - Menjalankan fungsi rekomendasi → ambil top-K film

  - Evaluasi menggunakan metrik
    
2. Model Development dengan Collaborative Filtering
   
![image](https://github.com/user-attachments/assets/0c2b4bdc-1596-449e-b5f5-df3a16f7d422)

![image](https://github.com/user-attachments/assets/ac1f09b0-442b-43c0-925f-ebf7d3b345d2)

yi: nilai sebenarnya
y^i: nilai prediksi

**Cara Kerja RMSE**
RMSE menghitung selisih antara nilai aktual dan prediksi, mengkuadratkannya (agar tidak negatif), menghitung rata-ratanya, lalu diakarkan agar kembali ke satuan aslinya.
Metrik ini memberi penalti yang lebih besar terhadap kesalahan prediksi yang besar, karena adanya kuadrat pada selisih.

Grafik menunjukkan RMSE model dari epoch 0 hingga 100, dengan garis biru untuk data latih dan oranye untuk data uji. Awalnya, RMSE tinggi (0,26 untuk uji, 0,22 untuk latih), lalu turun drastis hingga epoch 20 (uji ~0,23, latih ~0,19). Setelah itu, RMSE latih stabil di 0,19, sementara RMSE uji tetap di 0,23, menandakan pembelajaran baik tapi ada tanda overfitting.

**Evaluasi Terhadap Business Understanding**

**Menjawab Problem Statement**

   Dalam tahap pemahaman bisnis, tim pengembang telah mengidentifikasi tiga permasalahan utama (problem statements) yang sangat umum dihadapi dalam platform hiburan digital. Ketiga permasalahan ini tidak hanya  
   realistis, tetapi juga strategis karena menyasar tantangan inti dari personalisasi konten untuk pengguna.

  - Problem Statement 1:
    "Bagaimana cara membantu pengguna menemukan film yang sesuai dengan preferensi mereka secara otomatis di tengah banyaknya pilihan film yang tersedia?"
  
     Permasalahan ini dijawab dengan mengimplementasikan metode Content-Based Filtering, yaitu pendekatan yang merekomendasikan film berdasarkan kesamaan genre dan tag dari film yang disukai sebelumnya. 
     Teknologi   
     yang digunakan: TF-IDF Vectorization dan Cosine Similarity untuk membandingkan kemiripan antar film.
  
     Contoh: Jika pengguna menyukai Jumanji (1995), maka sistem akan merekomendasikan film lain dengan genre yang serupa seperti The Chronicles of Narnia atau Harry Potter.

  - Problem Statement 2:
    "Bagaimana sistem rekomendasi dapat mengidentifikasi film yang relevan meskipun pengguna belum pernah menontonnya sebelumnya?"
  
    Masalah ini disebut sebagai cold-start problem untuk item dan berhasil diatasi dengan content-based filtering.Karena pendekatan ini tidak memerlukan data interaksi pengguna sebelumnya, sistem tetap dapat 
    bekerja hanya dengan informasi konten dari film itu sendiri.

  - Problem Statement 3:
   "Bagaimana menggabungkan Content-Based dan Collaborative Filtering agar sistem rekomendasi menjadi lebih akurat dan responsif terhadap berbagai jenis pengguna (baru maupun lama)?"
  
   Jawaban atas masalah ini adalah implementasi sistem hybrid, di mana content-based digunakan untuk pengguna baru dan collaborative filtering untuk pengguna yang sudah memiliki riwayat. Ini memastikan bahwa 
   sistem tetap bekerja optimal dalam berbagai kondisi pengguna.

**Mencapai Goals**

   Tujuan dari proyek ini disusun dengan jelas dan secara logis selaras dengan pernyataan masalah yang telah diidentifikasi sebelumnya. Evaluasi menunjukkan bahwa masing-masing tujuan telah tercapai dengan 
   pendekatan teknis yang tepat.

  - Goal 1:
   "Mengembangkan sistem rekomendasi film yang mampu menyarankan film relevan berdasarkan kesamaan konten seperti genre, sinopsis, dan kata kunci."
  
    Dicapai dengan Content-Based Filtering, menggunakan TF-IDF pada data genre dan tag untuk membentuk representasi vektor konten.
    Sistem mampu memberikan rekomendasi berdasarkan semantik tanpa memerlukan data rating pengguna.
  
  - Goal 2:
   "Membangun sistem rekomendasi yang dapat menyarankan film baru berdasarkan perilaku pengguna lain yang serupa."
  
    Dicapai melalui Collaborative Filtering berbasis Matrix Factorization, dengan neural network sederhana berbasis embedding.
    Model dipelajari dari dataset MovieLens dan menunjukkan hasil evaluasi yang solid (RMSE validasi sekitar 0.23).
  
 - Goal 3:
  "Menggabungkan dua pendekatan tersebut untuk memperkuat performa sistem rekomendasi secara keseluruhan."
  
   Sistem hybrid dirancang dengan baik, memastikan rekomendasi tetap relevan baik untuk pengguna baru maupun lama.
   Fleksibilitas ini penting untuk skalabilitas sistem di lingkungan nyata yang heterogen.

**Dampak dari Solution Statement**

  Setiap solusi teknis yang diusulkan memiliki kontribusi penting terhadap pencapaian tujuan dan penanganan masalah bisnis. Berikut analisis dampaknya:

   - Content-Based Filtering
  
     Kelebihan:
     Tidak bergantung pada data rating, sehingga ideal untuk pengguna baru.
     Memberikan rekomendasi yang dapat dijelaskan secara logis berdasarkan konten.
   
     Dampak:
     Meningkatkan kenyamanan pengguna baru dalam menjelajahi konten yang sesuai dengan preferensi awal.
     Mendorong eksplorasi katalog film dengan genre yang mirip.

   - Collaborative Filtering
     Kelebihan:
     Mampu mempelajari selera pengguna melalui pola rating dan interaksi.
     Hasil rekomendasi lebih personal dan terkadang tak terduga (serendipity).
   
     Dampak:
     Meningkatkan retensi pengguna lama karena mereka merasa sistem “memahami” preferensi mereka.

## Kesimpulan

Proyek sistem rekomendasi ini tidak hanya berhasil menjawab masalah bisnis yang kompleks, tetapi juga memberikan solusi yang scalable dan berdampak langsung terhadap peningkatan kualitas interaksi pengguna dengan platform hiburan digital. Kombinasi pendekatan content-based dan collaborative filtering menunjukkan kesiapan sistem ini untuk diimplementasikan dalam lingkungan produksi nyata.

Proyek ini bertujuan untuk membangun sistem rekomendasi film yang mampu memberikan saran personal kepada pengguna berdasarkan preferensi mereka. Dalam upaya tersebut, dua pendekatan utama digunakan: Content-Based Filtering dan Collaborative Filtering. Dari sisi business understanding, proyek ini berhasil mengidentifikasi dan menjawab masalah utama yang dihadapi pengguna platform hiburan digital, yaitu kesulitan menemukan film yang sesuai di tengah banyaknya pilihan. Pendekatan content-based memungkinkan sistem memberikan rekomendasi kepada pengguna baru yang belum memiliki riwayat interaksi, sementara collaborative filtering efektif mempelajari pola pengguna lama melalui data rating.

Secara teknis, proyek ini menggunakan metode TF-IDF dan cosine similarity untuk menghitung kemiripan antar film berdasarkan konten, serta matrix factorization berbasis neural network embedding untuk mempelajari relasi laten antara pengguna dan film. Evaluasi menggunakan Root Mean Squared Error (RMSE) menunjukkan bahwa model collaborative filtering mampu mencapai akurasi prediksi yang baik, dengan RMSE validasi yang stabil pada ~0.23.

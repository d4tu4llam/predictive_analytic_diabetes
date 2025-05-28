# Laporan Proyek Machine Learning - Hilmi Datu Allam

## Domain Proyek (Kesehatan)

# Domain Proyek
Diabetes adalah penyakit kronis yang terjadi ketika pankreas tidak memproduksi cukup insulin atau ketika tubuh tidak dapat menggunakan insulin secara efektif dan menyebabkan tingginya tingkat gula dalam darah. Pada tahun 2021, diabetes adalah penyebab langsung dari 1.6 juta kematian [1]. Di Indonesia, prevalensi diabetes pada penduduk diatas 15 tahun mencapai 2% atau sekitar 5,7 juta orang [2]. Diabetes memiliki hubungan erat dengan kadar gula darah, di mana kekurangan insulin menyebabkan peningkatan kadar glukosa darah [3]. Obesitas juga merupakan faktor risiko utama, karena dapat menyebabkan resistensi insulin yang memicu diabetes tipe 2 [4]. Selain itu, variabel seperti usia, jenis kelamin, hipertensi, penyakit jantung, riwayat merokok, BMI, kadar HbA1c, dan kadar glukosa darah telah terbukti relevan dalam penelitian diabetes, terutama dalam analitik prediktif untuk mendeteksi risiko dan diagnosis dini [3]. Meningkatnya prevalensi diabetes dan dampaknya terhadap kesehatan masyarakat menunjukkan perlunya pendekatan prediktif berbasis data untuk mengidentifikasi faktor risiko utama dan mendeteksi diabetes secara dini.<br>

Saat ini, perkembangan teknologi berlangsung sangat cepat, termasuk dalam bidang machine learning. Teknologi machine learning telah banyak diterapkan di berbagai sektor, salah satunya adalah bidang kesehatan. Dengan kemampuan dalam mengolah data dan mengenali pola, machine learning dapat dimanfaatkan untuk mendeteksi berbagai jenis penyakit berdasarkan sejumlah parameter atau faktor tertentu, termasuk dalam mendeteksi diabetes. Oleh karena itu, dalam proyek ini, penulis berinisiatif untuk menerapkan machine learning guna melakukan prediksi terhadap penyakit diabetes pada seseorang. Tiga model yang digunakan dalam prediksi ini adalah Logistic Regression, K-Nearest Neighbor, dan Random Forest.

![diabetes](https://github.com/user-attachments/assets/24d7e563-b8e3-417e-9d64-1e657bec310f)

## Business Understanding

### Problem Statements
Rumusan masalah dari masalah latar belakang diatas adalah
  1. Dari berbagai faktor, faktor mana yang merupakan faktor utama terkena diabetes?
  2. Bagaimana cara mendeteksi seseorang memiliki diabetes berdasarkan data rekam medis menggunakan pendekatan analitik prediktif?
  3. Bagaimana akurasi model prediktif dapat ditingkatkan untuk mendeteksi diabetes secara dini ?

### Goals
Berdasarkan problem statements, berikut tujuan dibuatnya proyek ini.
  1. Mengetahui faktor-faktor yang paling berpengaruh terhadap risiko diabetes berdasarkan analisis data seperti usia, jenis kelamin, hipertensi, penyakit jantung, riwayat merokok, BMI, kadar HbA1c, dan kadar glukosa darah.
  2. Menggunakan algoritma machine learning untuk mendeteksi diabetes menggunakan data rekam medis.
  3. Menemukan model terbaik berdasarkan akurasi dan recall tertinggi untuk memprediksi diabetes pada pasien

### Solution Statement

1. Analisis data untuk memahami fitur-fitur yang mempengaruhi orang terkena diabetes, dengan deskripsi statistik data untuk mengetahui korelasi antar fitur dan menerapkan teknik visualisasi data untuk memahami hubungan antara data target dan fitur lainnya.
2. Menggunakan 3 algoritma machine learning yang berbeda, yaitu Random Forest, Logistic Regression dan K-Nearest Neighbor.
3. Menggunakan confusion matrix dan recall score pada masing-masing model machine learning untuk menemukan model terbaik berdasarkan akurasi tertinggi.

## Data Understanding
Dataset yang digunakan untuk memprediksi diabetes pada pasien diambil dari platform [kaggle](https://www.kaggle.com/datasets/iammustafatz/diabetes-prediction-dataset). yang dipublikasikan oleh Mohammed Mustafa. Data ini didapat dari koleksi data medikal pasien. Dataset ini terdiri dari 1 file csv.<br>

### Informasi Keterangan Variabel pada Data
Dataset ini memiliki 9 variabel dengan keterangan sebagai berikut.
Variabel | Keterangan
----------|----------
gender| jenis kelamin
age |  umur dalam decimal
hypertension| 0: tidak hipertensi, 1: hipertensi
heart_disease| 0: tidak ada penyakit jantung, 1: penyakit jantung
smoking_history|6 kategori: not current (tidak merokok saat ini), former (mantan perokok), No Info (tidak ada informasi), current (merokok saat ini), never (tidak pernah merokok), dan ever (pernah merokok).
bmi | ukuran lemak tubuh berdasarkan berat dan tinggi. Rentang BMI dalam dataset adalah 10,16 hingga 71,55.
HbA1c_level| ukuran rata-rata kadar gula darah seseorang selama 2-3 bulan terakhir.
blood_glucose_level | Jumlah glukosa dalam aliran darah pada waktu tertentu.
diabetes | 0: tidak diabetes, 1: diabetes


| Jumlah Baris | Jumlah Kolom |
--------|-------
| 100000 | 9 |

### Deskripsi Statistik dari Data
![deskripsi_statistik](https://github.com/user-attachments/assets/70d656a2-d5cf-4db2-be71-e42948ab73eb)

- Count : Jumlah sampel pada data.
- Mean : Nilai rata-rata.
- Std : Standar deviasi.
- Min : nilai minimum setiap kolom.
- 25% : Kuartil pertama adalah nilai yang menandai batas interval dalam empat bagian sebaran yang sama.
- 50% : Kuartil kedua, atau biasa juga disebut median (nilai tengah).
- 75% : Kuartil ketiga.
- Max : Nilai maksimum.

Dari informasi diatas, disimpulkan bahwa data ini mencakup orang yang berumu 1-80 tahun dengan BMI rentang 10-95. Kadar gula di aliran darah 2-3 bulan terakhir (HbA1c_level) pasien berada di kisaran 3.5 hingga 9 persen, sedangkan kadar gula di aliran saat data ini diambil berada pada kisaran 80 hingga 300 mg/dL

### Univariate Analysis

Berikut merupakan kolom yang termasuk dalam variabel numerikal maupun kategorikal. <br>
Kolom numerik: ['age', 'bmi', 'HbA1c_level', 'blood_glucose_level'] <br>
Kolom kategorik: ['gender', 'smoking_history', 'hypertension', 'heart_disease', 'diabetes'] <br>
Berikut visualisasi kolom kategorik<br>

![analisis_kategorik](https://github.com/user-attachments/assets/d35bf915-ba97-4c78-a9cd-01a6c4cde8dc)


Dari plot-plot diatas didapat informasi:
  1. Dari Plot Gender, pasien mayoritas perempuan dengan sangat sedikit yang menolak menjawab yaitu other
  2. Dari plot Smoking History, mayoritas pasien tidak pernah merokok dan no info. 
  3. Dari plot Hipertensi, mayoritas tidak hipertensi
  4. Dari plot Penyakit Jantung, mayoritas tidak sakit jantung
  5. Dari plot Diabetes, mayoritas tidak diabetes.
  6. Kelas Hipertensi, Penyakit Jantung dan Diabetes sangat imbalance. Untuk kelas target akan dilakukan oversampling nantinya pada tahap data preparation

  Berikut visualisasi kolom numerik<br>
![analisis_numerik](https://github.com/user-attachments/assets/52ce5ee2-e581-4692-8d14-c1f999cb9439)

Dari Gambar didapat informasi: 
1. Plot Histogram dari **HbA1c_level** dan **Age* berdistribusi cukup normal 
2. Plot Histogram dari **Hypertension**, **heart_disease**, **bmi**, **blood_glucose_level** dan **diabetes** berdistribusi miring ke kanan (right skewed)

### Multivariate Analysis

#### 1. Membandingkan diabetes dengan gender

![barplot_gender](https://github.com/user-attachments/assets/b353306e-6499-41fc-906d-2bb436908cd5)

<br>
Dari Plot diatas didapat informasi:
1. Jumlah perempuan tanpa diabetes jauh lebih banyak daripada laki-laki tanpa diabetes.
2. Jumlah perempuan dengan diabetes hampir sama dengan jumlah laki-laki dengan diabetes.

#### 2. Membandingkan diabetes dengan usia

![usia](https://github.com/user-attachments/assets/08c85b12-b11e-4b10-a65d-8a4b2eddccc4)

<br>

Dari gambar diatas:
1. Seluruh pasien non diabates direntang 1-80
2. Seluruh pasien diabetes mulai banyak frekuensinya pada umur 20-80. Dengan beberapa outlier di rentang 1-29

#### 3. Membandingkan diabetes dengan tingkat kadar gula saat ini

![boxplot_glucose](https://github.com/user-attachments/assets/2f6de3d7-82f0-4679-8224-448017db7ff5)

<br>

Dari boxplot diatas:
1. Pasien dengan diabetes memiliki median level glukosa darah yang lebih tinggi dibandingkan pasien tanpa diabetes.
2. Distribusi glukosa pada penderita diabetes lebih melebar dan mencakup nilai yang lebih tinggi hingga 300.
3. Ppasien tanpa diabetes memiliki glukosa darah yang lebih terkonsentrasi di bawah 200.

#### 4. Membandingkan diabetes dengan HbA1c_level (tingkat gula dalam darah 2-3 bulan terakhir)

![Boxplot_HbA1c_level](https://github.com/user-attachments/assets/f87a3d31-0336-4d0c-9790-ace81d8a451b)

<br>
Dari boxplot diatas:
1. Penderita diabetes memiliki HbA1c yang lebih tinggi dibandingkan non-diabetes.
2. Median HbA1c penderita diabetes sekitar 6.5–7.5, sedangkan non-diabetesi sekitar 5.5–6.
3. Hampir seluruh penderita diabetes memiliki HbA1c di atas 6

#### 5. Melihat Korelasi Variabel dengan Menggunakan Heatmap

![Correlation_Matrix](https://github.com/user-attachments/assets/8c049a17-0f60-4a45-88df-b3c56d10b6a9)

<br>

Dari Correlation Matrix Heatmap diatas: 
1. Diabetes memiliki korelasi tinggi dengan blood_glucose_level dan HbA1c_level. Hal ini menunjukkan 2 variabel ini merupakan prediktor yang kuat
2. age, bmi, hypertension dan heart_disease memiliki korelasi positif yang lumayan. Hal ini menandakan bahwa usia yang lebih tua, indeks masa tubuh yang tinggi, hipertensi dan penyakit jantung berkontribusi pada diabetes.


## Data Preparation
### Data Cleaning
### Menghilangkan gender "Other" 
![other](https://github.com/user-attachments/assets/573e74d1-bd72-4a03-adbd-322fa59be594)<br>
Data yang memiliki gender "Other" Sangat kecil 

#### mengecek data duplikasi
![duplikat](https://github.com/user-attachments/assets/e1a3412e-d58f-4e80-b6e9-40b3927673af)
<br>

Terdapat 6001 data duplikat, kemudian kita menghapusnya dengan .drop_duplicates()

#### mengecek missing values
![missing](https://github.com/user-attachments/assets/e7a61a91-e7ca-4b89-b47d-68e54d1f1aa9)

<br>
dari output diatas didapati bahwa tidak terdapat missing value pada dataset, tetapi harus dicek apakah terdapat nilai nol pada tiap kolom. <br>

![value_0](https://github.com/user-attachments/assets/121a2b23-05f1-4513-ae14-ac644f9b49f6)
<br>

Dapat dilihat tidak ada value yang bernilai 0 pada kolom numerik

### One Hot Encoding
Encoding dilakukan terhadap smoking_history dan one hot encoding dilakukan terhadap gender
![encode](https://github.com/user-attachments/assets/6422f87d-aa0d-44a2-8da7-958de2f04be3)




### Split Train Test

Tahap ini bertujuan untuk memisahkan data menjadi dua bagian, yaitu data pelatihan (training) dan data pengujian (testing). Data pelatihan digunakan untuk membangun dan melatih model berdasarkan data yang tersedia, sementara data pengujian dimanfaatkan untuk mengevaluasi performa model terhadap data yang belum pernah dilihat sebelumnya. Proses pembagian ini dilakukan dengan rasio 80% untuk data pelatihan dan 20% untuk data pengujian, menggunakan fungsi train_test_split dari library scikit-learn.

### Oversampling
Tahap ini bertujuan untuk menyeimbangkan kelas diabetes yang sangat tidak seimbang
![oversampling](https://github.com/user-attachments/assets/b5d144a7-3c4c-4bf6-b318-47051e8c38e0)

### Standarisasi

Tahapan ini dilakukan agar algoritma machine learning memiliki performa lebih baik dan konvergen lebih cepat ketika dimodelkan pada data dengan skala relatif sama atau mendekati distribusi normal. Proses scaling dan standarisasi membantu untuk membuat fitur data menjadi bentuk yang lebih mudah diolah oleh algoritma dengan range 0 hingga 1 dan menyeragamkan karena memiliki satuan yang berbeda pada tiap fitur.

## Modeling

Ada 3 algoritma *Machine Learning* yang digunakan untuk membuat model, yaitu sebagai berikut.

### 1. ***Logistik Regresion***

Logistic Regression adalah metode statistik untuk memprediksi probabilitas hasil biner (dua kategori) berdasarkan satu atau lebih variabel independen. Meskipun dinamakan "regression," metode ini digunakan untuk klasifikasi, bukan regresi seperti pada linear regression. Logistic regression sering dipakai dalam pembelajaran mesin dan statistik untuk memodelkan hubungan antara fitur input dan hasil biner.

Dalam implementasinya, Logistic Regression menggunakan LogisticRegression dari library sklearn.linear_model. Model dilatih dengan X_train_balanced dan y_train_balanced, lalu diuji dengan X_test dan y_test menggunakan data testing yang tidak termasuk dalam data pelatihan. Parameter yang digunakan adalah solver: liblinear untuk optimasi parameter (koefisien) pada data besar dan bersifat sparse,

### 2. ***K-Nearest Neighbors* (KNN)**

Algoritma KNN mengklasifikasikan data berdasarkan kelas mayoritas dari k tetangga terdekatnya. Kelebihannya meliputi kemudahan penggunaan dan efektifitas. Namun, kekurangannya adalah sensitivitas terhadap pemilihan nilai k dan metrik jarak, serta performa yang buruk pada data berdimensi tinggi (curse of dimensionality).

Dalam proyek ini, KNN diimplementasikan menggunakan KNeighborsClassifier dari library sklearn.neighbors. Model dilatih dengan X_train_balanced dan y_train_balanced, kemudian diuji dengan X_test dan y_test pada data testing yang terpisah. Parameter yang digunakan adalah n_neighbors, yaitu jumlah tetangga, dengan nilai n_neighbors = 21.

### 3. ***Random Forest***

Random Forest adalah algoritma yang membentuk banyak pohon keputusan (decision trees) dengan teknik bootstrapping dan pemilihan fitur acak untuk meningkatkan keragaman pohon. Kelebihannya adalah akurasi tinggi melalui pendekatan ensemble, mampu mencegah overfitting dengan jumlah pohon yang banyak, serta efektif untuk dataset besar dan berdimensi tinggi. Kekurangannya adalah kebutuhan komputasi dan memori yang besar untuk jumlah pohon yang banyak.

Dalam implementasinya, Random Forest menggunakan RandomForestClassifier dari library sklearn.ensemble. Model dilatih dengan X_train dan y_train, lalu diuji dengan X_test dan y_test pada data testing terpisah. Parameter yang digunakan meliputi n_estimators (jumlah pohon), dan random_state (mengatur seed acak). Pada proyek ini, parameter yang digunakan adalah n_estimators = 100,  dan random_state = 42.


###  Pemilihan Model

Setelah semua model dijalankan, penulis memilih algoritma Random forest sebagai model terbaik yang akan digunakan sebagai solusi untuk memprediksi penyakit diabetes karena model ini memiliki akurasi dan recall tertinggi dibandingkan model lainnya, serta kesalahan klasifikasi pada matriks confusion yang lebih kecil dibanding model lainnya. Penjelasan lebih lengkap mengenai alasan ini ada di bagian selanjutnya, yaitu **evaluation**.

## Evaluation

Pada rana medis Akurasi dan recall yang dipentingkan untuk menghindari komplikasi salah memvonis positif pasien. Karena itu model terbaik adalah Random Forest

### Sekilas Tentang Matriks Confusion, Akurasi, dan Recall

Matriks Confusion merupakan sebuah tabel untuk mengukur akurasi dari model klasifikasi. Contoh dari Matriks Confusion beserta labelnya dapat dilihat pada gambar di bawah ini. 

![image](https://github.com/user-attachments/assets/62a14ec6-a60a-48ff-b6bd-f5d41ef23c69)
 <br>

Setiap baris pada matriks confusion merepresentasikan nilai sesungguhnya, sedangkan setiap kolom pada matriks confusion merepresentasikan nilai yang diprediksi. Terdapat 4 label pada matriks confusion seperti yang terlihat di gambar, yaitu TP, TN, FP, dan FN.
1. *True Positive* (TP) merupakan jumlah data pada positif yang ditebak dengan benar.
2. *True Negative* (TN) merupakan jumlah data pada negatif yang ditebak dengan benar.
3. *False Positive* (FP) merupakan jumlah data yang ditebak dengan salah karena diprediksi positif, sedangkan aslinya adalah negatif.
4. *False Negative* (FN) merupakan jumlah data yang ditebak dengan salah karena diprediksi negatif, sedangkan aslinya adalah positif.

Selanjutnya, metrik evaluasi yang digunakan berdasarkan label-label yang diketahui dari matriks confusion ada 4, yaitu sebagai berikut.
1. Akurasi (*Accuracy*) merupakan proporsi data yang berhasil diprediksi dengan benar dari seluruh data yang diprediksi. 

2. *Precision* merupakan proporsi data positif yang berhasil diprediksi dengan benar dari seluruh data yang diprediksi positif.

3. *Recall* merupakan proporsi data positif yang berhasil diprediksi dengan benar dari seluruh data yang aslinya positif.


### Penerapan Matriks Confusion, Akurasi, dan Recall
## Model Logistic Regression 
![image](https://github.com/user-attachments/assets/7bd2a86c-2fad-41af-b388-5650b861b2d5)
Menggunakan Logistic Regression :

1. 15610 responden nondiabetes telah diklasifikasikan dengan benar
2. 1354 responden diabetes telah diklasifikasikan dengan benar
3. 1498 responden nondiabetes diklasifikasikan sebagai responden diabetes (False Positif)
4. 335 responden diabetes diklasifikasikan sebagai responden nondiabetes (False negatif)
## Model KNN
![image](https://github.com/user-attachments/assets/ea77e66e-29b5-4540-9c45-d8fa1a5b95bf)
Menggunakan K-Nearest Neighbor :

1. 15753 responden nondiabetes telah diklasifikasikan dengan benar
2. 1350 responden diabetes telah diklasifikasikan dengan benar
3. 1355 responden nondiabetes diklasifikasikan sebagai responden diabetes (False Positif)
4. 339 responden diabetes diklasifikasikan sebagai responden nondiabetes (False negatif)
## Model Random Forest
![image](https://github.com/user-attachments/assets/b75ad4c7-4e03-4a03-b353-efb662c976b4)
Menggunakan Random Forest :

1. 16754 responden nondiabetes telah diklasifikasikan dengan benar
2. 1244 responden diabetes telah diklasifikasikan dengan benar
3. 354 responden nondiabetes diklasifikasikan sebagai responden diabetes (False Positif)
4. 445 responden diabetes diklasifikasikan sebagai responden nondiabetes (False negatif)

#### Hasil Evaluasi
Metrik evaluasi yang aka digunakan adalah akurasi dan recall. Berdasarkan classification report dan confusion matrix diatas. Model yang mempunyai akurasi paling bagus adalah Random Forest, namun pada kelas diabetes model ini mempunyai recall 0.74. Sedangkan pada rana kesehatan mengidentifikasi recall seringkali lebih penting karena melewatkan kasus positif diabetes bisa fatal. Penyakit yang seharusnya dapat ditangani dini bisa menyebabkan kematian. Oleh karena itu penulis memutuskan bahwa model yang terbaik adalah KNN dengan akurasi (0.9099) dan recall pada kelas diabetes (0.80). 


![feature_import](https://github.com/user-attachments/assets/f9a80039-1194-44ae-a468-7e3ffd6c9b6c)

Fitur paling penting menurut random forest adalah HbA1c_level yaitu tingkat gula dalam darah 2-3 bulan terakhir

## Kesimpulan
1. Berdasarkan data yang diperoleh, menunjukan bahwa 2 faktor yang sangat berpengaruh seseorang terkena penyakit diabetes ,yaitu tekanan darah HbA1c_level, tingkat gula darah saat ini. Disimpulkan bahwa seseorang jika ingin mencegah diabetes harus menjaga gula darahnya rendah baik itu dengan olahragaa maupun mengurangi konsumsi gula.

2. Seluruh pasien diabetes memiliki kesamaan dalam beberapa faktor, yaitu
   * memiliki kadar glukosa lebih dari rata-rata batas normal.
   * memiliki kadar HbA1c_level lebih dari rata-rata batas normal.
   * umur rentang 30 tahun sampai 80 tahun.
   
3. Setelah menguji data menggunakan 3 diperoleh model KNN merupakan model terbaik dibandingkan model lainnya berdasarkan skor akurasi dan recall
## Referensi
[1] World Health Organization. (2021). Diabetes Fact Sheet. https://www.who.int/news-room/fact-sheets/detail/diabetes

[2] Kementerian Kesehatan Republik Indonesia. (2018). Riset Kesehatan Dasar (Riskesdas) 2018. Jakarta: Badan Penelitian dan Pengembangan Kesehatan.

[3] Kavakiotis, I., et al. (2017). Machine Learning and Data Mining Methods in Diabetes Research. Computational and Structural Biotechnology Journal, 15, 104-116.

[4] Abdullah, A., Peeters, A., de Courten, M., & Stoelwinder, J. (2010). The magnitude of association between overweight and obesity and the risk of diabetes: a meta-analysis of prospective cohort studies. Diabetes research and clinical practice, 89(3), 309-319.

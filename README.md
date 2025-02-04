# House-Pricing

# Laporan Proyek Machine Learning - Gatot Santoso

## Project Overview

Proyek ini bertujuan untuk memprediksi nilai median rumah di distrik-distrik California berdasarkan data sensus. Proyek ini penting karena memberikan wawasan berharga bagi agen real estate, pembuat kebijakan, dan pembeli rumah dalam memahami faktor-faktor yang memengaruhi harga properti.

Sebagai referensi, prediksi harga rumah sering menjadi subjek penelitian, seperti yang dijelaskan dalam [California Housing Market Analysis](https://scholar.google.com/). Proyek ini menggunakan dataset "California Housing Prices" yang tersedia di [Kaggle](https://www.kaggle.com/datasets/camnugent/california-housing-prices).

## Business Understanding

### Problem Statements

1. Bagaimana faktor-faktor geografis dan demografis memengaruhi nilai median rumah di California?
2. Bagaimana model prediktif dapat membantu memperkirakan harga rumah dengan akurasi tinggi?

### Goals

1. Mengidentifikasi faktor utama yang memengaruhi harga rumah.
2. Mengembangkan model prediksi untuk memperkirakan nilai median rumah dengan metrik evaluasi yang optimal.

### Solution Statements

Untuk mencapai tujuan tersebut, dua pendekatan digunakan:
1. **Linear Regression**: Model regresi sederhana untuk memahami hubungan linier antara fitur dan target.
2. **Random Forest Regressor**: Model ensemble untuk menangkap hubungan non-linear dan meningkatkan akurasi prediksi.

## Data Understanding

Dataset ini mencakup 20.640 sampel dengan beberapa fitur seperti berikut:

- `longitude` dan `latitude`: Lokasi geografis distrik.
- `housing_median_age`: Usia median rumah di distrik.
- `total_rooms` dan `total_bedrooms`: Jumlah total kamar dan kamar tidur.
- `population`: Populasi di distrik.
- `households`: Jumlah rumah tangga.
- `median_income`: Pendapatan median penduduk.
- `ocean_proximity`: Kategori lokasi geografis.
- `median_house_value`: Target prediksi.

Dataset ini diunduh dari [link ini](https://raw.githubusercontent.com/ageron/handson-ml/master/datasets/housing/housing.csv). Analisis awal menunjukkan beberapa nilai yang hilang di kolom `total_bedrooms`, yang diatasi dengan imputasi menggunakan median.

Berikut adalah info dataset dan jumlah nilai yang hilang

<img width="328" alt="Screenshot 2025-01-11 at 00 50 05" src="https://github.com/user-attachments/assets/5351e465-db11-4d57-bf96-4e152c20a3e0" />

Visualisasi distribusi target ditunjukkan dari plot di bawah ini

<img width="367" alt="Screenshot 2025-01-11 at 00 53 45" src="https://github.com/user-attachments/assets/b020b1b7-e989-4869-b365-0eb4c37eba7a" />

Matriks korelasi

<img width="482" alt="Screenshot 2025-01-11 at 00 54 24" src="https://github.com/user-attachments/assets/77623ae7-20f5-4582-95d8-cd3f5d5189aa" />


## Data Preparation

1. **Handling Missing Values**: Nilai yang hilang pada kolom `total_bedrooms` diimputasi dengan median.

<img width="294" alt="Screenshot 2025-01-15 at 16 55 10" src="https://github.com/user-attachments/assets/32b74208-e51c-4132-b2a5-a7b6da1c63f0" />

2. **Encoding Categorical Variables**: Kolom `ocean_proximity` diubah menjadi variabel dummy menggunakan one-hot encoding.
   
<img width="459" alt="Screenshot 2025-01-15 at 16 55 52" src="https://github.com/user-attachments/assets/cf93d879-f77f-4e78-a0fc-47a5a2be254c" />

3. **Feature Scaling**: Fitur numerik dinormalisasi untuk memastikan skala yang konsisten.

<img width="457" alt="Screenshot 2025-01-15 at 16 45 18" src="https://github.com/user-attachments/assets/3ba6284f-ab3a-4b5f-9b76-74ba9da74b6c" />

4. **Pembagian Data**: Pada tahap ini data di split menjadi data training dan data test, Dengan perbandingan data training 80% dan data test 20%.
   
```
# Memisahkan fitur dan target setelah scaling
X = scaled_data.drop('median_house_value', axis=1)
y = scaled_data['median_house_value']
```

```
# Membagi dataset menjadi data latih dan data uji
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)
```

<img width="181" alt="Screenshot 2025-01-15 at 18 23 42" src="https://github.com/user-attachments/assets/babbd3ba-f884-4b93-8329-57777cf8a95a" />


Proses ini memastikan data siap untuk digunakan dalam model prediksi.

## Modeling

Dua model digunakan:

1. Linear Regression

Linear regression adalah metode statistik yang digunakan untuk memodelkan hubungan linier antara satu atau lebih variabel independen (fitur) dengan variabel dependen (target). Model ini mencoba menemukan garis terbaik (best-fit line) yang meminimalkan jarak kuadrat antara nilai prediksi dan nilai aktual, dikenal sebagai metode Ordinary Least Squares (OLS).

Pada project ini:

Pendekatan: Linear Regression diasumsikan bahwa hubungan antara fitur-fitur seperti median_income, total_rooms, dan population dengan median_house_value bersifat linier.

Keunggulan:
Mudah diimplementasikan dan diinterpretasikan.
Memberikan wawasan tentang kontribusi relatif setiap fitur melalui koefisien regresi.

Keterbatasan:
Tidak mampu menangkap hubungan non-linear yang kompleks antar fitur.
Rentan terhadap outlier, yang dapat memengaruhi garis regresi.
Hasil Evaluasi: Model ini memberikan hasil yang cukup baik dengan R^2 di kisaran 0.64, menunjukkan bahwa sekitar 64% variabilitas dalam target dapat dijelaskan oleh fitur. Namun, kinerjanya terbatas karena hubungan kompleks antar fitur tidak dapat ditangkap sepenuhnya.

```
# Membuat model Linear Regression
model = LinearRegression()
model.fit(X_train, y_train)

# Membuat model Linear Regression
model = LinearRegression()
model.fit(X_train, y_train)

# Prediksi pada data uji
y_pred = model.predict(X_test)
```

2. Random Forest Regressor

Random Forest Regressor adalah implementasi khusus dari Random Forest yang digunakan untuk masalah regresi, di mana target variabelnya adalah nilai kontinu. Pada kasus ini, setiap pohon menghasilkan prediksi numerik, dan Random Forest Regressor menggabungkan hasil prediksi dengan cara menghitung rata-rata dari semua pohon.

Pada Kasus di Atas:

Pendekatan: Random Forest menangkap hubungan kompleks dan non-linear antara fitur-fitur seperti median_income, ocean_proximity, dan population dengan target median_house_value. Setiap pohon mempelajari pola dari subset data yang berbeda, mengurangi overfitting dan meningkatkan generalisasi.

Keunggulan:
Mampu menangkap hubungan non-linear yang kompleks.
Tahan terhadap outlier dan kurang rentan terhadap overfitting dibandingkan Decision Tree tunggal.
Memberikan fitur penting untuk analisis lebih lanjut (feature importance).

Keterbatasan:
Membutuhkan sumber daya komputasi yang lebih besar dibandingkan Linear Regression.
Hasil lebih sulit diinterpretasikan dibandingkan model yang lebih sederhana seperti Linear Regression.

Hasil Evaluasi: Random Forest memberikan R^2 sekitar 0.81, menunjukkan bahwa 81% variabilitas target dapat dijelaskan oleh fitur. Metrik MAE dan MSE juga lebih rendah dibandingkan Linear Regression, mengindikasikan prediksi yang lebih akurat.
  
```
# Inisialisasi model Random Forest
rf_model = RandomForestRegressor(random_state=42)
rf_model.fit(X_train, y_train)

# Prediksi pada data uji
y_pred_rf = rf_model.predict(X_test)
```

Kelebihan dan kekurangan:
- Linear Regression: Mudah diinterpretasi namun kurang fleksibel dalam menangkap hubungan non-linear.
- Random Forest Regressor: Lebih akurat namun membutuhkan sumber daya komputasi lebih besar.

## Evaluation

Model dievaluasi menggunakan metrik berikut:

1. **Mean Absolute Error (MAE)**:
   Memberikan rata-rata kesalahan prediksi dalam satuan asli.

2. **Mean Squared Error (MSE)**:
   Memberikan penalti lebih besar untuk kesalahan prediksi yang besar.

3. **R-squared (\(R^2\))**:
   Mengukur proporsi variabilitas target yang dapat dijelaskan oleh model.

Hasil evaluasi menunjukkan bahwa Random Forest Regressor memberikan hasil terbaik dan berikut adalah tabel perbandingan nilai aktual dengan linear regression dan random forest regressor.

<img width="488" alt="Screenshot 2025-01-17 at 14 09 07" src="https://github.com/user-attachments/assets/d2a8ab51-dab9-416e-b772-cde49c55ca5d" />

Berikut plot hasil harga prediksi dan nilai aktual.

<img width="418" alt="Screenshot 2025-01-17 at 14 09 40" src="https://github.com/user-attachments/assets/e3ae115f-1df0-409b-bf00-86b406149639" />


## Kesimpulan

Pemodelan Random Forest Regressor adalah pilihan terbaik untuk prediksi harga rumah dalam analisis ini. Model ini lebih akurat, stabil, dan mampu menangkap hubungan kompleks antar fitur dibandingkan dengan Regression Tree. Dengan evaluasi yang lebih baik dan hasil yang lebih andal, Random Forest dapat menjadi alat yang efektif untuk memahami faktor-faktor yang memengaruhi harga rumah di distrik-distrik California.

**---Ini adalah bagian akhir laporan---**


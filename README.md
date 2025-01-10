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

## Data Preparation

1. **Handling Missing Values**: Nilai yang hilang pada kolom `total_bedrooms` diimputasi dengan median.
2. **Encoding Categorical Variables**: Kolom `ocean_proximity` diubah menjadi variabel dummy menggunakan one-hot encoding.
3. **Feature Scaling**: Fitur numerik dinormalisasi untuk memastikan skala yang konsisten.

Proses ini memastikan data siap untuk digunakan dalam model prediksi.

## Modeling

Dua model digunakan:

1. **Linear Regression**:
   - Menggunakan semua fitur numerik dan variabel dummy.
   - Hasil evaluasi: R-squared sebesar 0.64 menunjukkan hubungan linier moderat.

2. **Random Forest Regressor**:
   - Model ensemble dengan parameter default.
   - Hasil evaluasi: R-squared sebesar 0.81 menunjukkan kinerja yang lebih baik dibandingkan regresi linier.

Kelebihan dan kekurangan:
- Linear Regression: Mudah diinterpretasi namun kurang fleksibel dalam menangkap hubungan non-linear.
- Random Forest: Lebih akurat namun membutuhkan sumber daya komputasi lebih besar.

## Evaluation

Model dievaluasi menggunakan metrik berikut:

1. **Mean Absolute Error (MAE)**:
   - Formula: \( \text{MAE} = \frac{1}{n} \sum_{i=1}^{n} |y_i - \hat{y}_i| \)
   - Memberikan rata-rata kesalahan prediksi dalam satuan asli.

2. **Mean Squared Error (MSE)**:
   - Formula: \( \text{MSE} = \frac{1}{n} \sum_{i=1}^{n} (y_i - \hat{y}_i)^2 \)
   - Memberikan penalti lebih besar untuk kesalahan prediksi yang besar.

3. **R-squared (\(R^2\))**:
   - Formula: \( R^2 = 1 - \frac{\text{SS}_\text{res}}{\text{SS}_\text{tot}} \)
   - Mengukur proporsi variabilitas target yang dapat dijelaskan oleh model.

Hasil evaluasi menunjukkan bahwa Random Forest Regressor memberikan hasil terbaik dengan MAE sebesar 22.100, MSE sebesar 65.000, dan \(R^2\) sebesar 0.81.

**---Ini adalah bagian akhir laporan---**


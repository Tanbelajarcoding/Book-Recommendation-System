# Laporan Proyek Machine Learning - Sistem Rekomendasi Buku
### Oleh Sulthan Muhammad Rafif Ilham

# 🌍 Project Overview

## 1. Latar Belakang

## 2. Mengapa dan Bagaimana Masalah Ini Harus Diselesaikan

## 3. Referensi

# 📈 Business Understanding

## 1. Problem Statements (Pernyataan Masalah)

## 2. Goals (Tujuan)

## 3. Solution Approach (Pendekatan Solusi)

# 🧠 Data Understanding

## Dataset Overview

## Feature Description

## Data Exploration Findings

### User Data Analysis

### Book Data Analysis

### Matrix Density

## 🔍 Ringkasan EDA

## 🚩 Permasalahan dan Insight Data

# ⚙️ Data Preparation

## 1. Menggabungkan Kolom Nama dan Kategori Destinasi Wisata

## 2. Standardisasi Format Kategori Destinasi

## 3. Mengatasi Missing Values dan Duplikasi Data

## 4. Penyiapan Data Final untuk Analisis

## 5. Persiapan Data untuk Model Content Based Filtering

### 1. Persiapan data

### 2. Ekstraksi Informasi Destinasi Wisata

### 3. Vektorisasi Fitur Kategori dengan TF-IDF

### 4. Ringkasan Hyperparameter TF-IDF Vectorizer (`TfidfVectorizer`)

## 6. Persiapan Data untuk Model Collaborative Filtering

### 1. Persiapan data

### 2. Pembagian Data Latih dan Validasi (Train-Validation Split) dan Normalisasi Rating

# 🧮 Modeling

## Solusi 1: Content-Based Filtering (CBF)

### 1. Perhitungan Kemiripan Antar Destinasi dengan Cosine Similarity

### 2. Implementasi Fungsi Rekomendasi Destinasi Wisata

### 3. Ringkasan Hyperparameter Model Content Based Filtering Perhitungan Cosine Similarity (`cosine_similarity`)

### 4. Kelebihan dan Kekurangan Content-Based Filtering

## Solusi 2: Collaborative Filtering (CF) dengan Embedding Deep Learning

### 1. Membangun Model Deep Learning untuk Collaborative Filtering

### 2. Kompilasi dan Pelatihan Model

### 3. Inferensi dan Contoh Penggunaan untuk Top-N Rekomendasi

### 4. Ringkasan Hyperparameter Model Collaborative Filtering

   #### 1. **Embedding-related Hyperparameters**

   #### 2. **Model Training Hyperparameters**

   #### 3. **EarlyStopping**

   #### 4. **ReduceLROnPlateau**

### 5. Kelebihan dan Kekurangan Collaborative Filtering (dengan Deep Learning)

# 💯 Evaluation

## Metrik Evaluasi yang Digunakan

## Evaluasi Model Content-Based Filtering (CBF)

## Evaluasi Model Collaborative Filtering (CF)

### 1. Evaluasi Performa Selama Pelatihan (RMSE Plot)

### 2. Perhitungan RMSE dan MAE pada Data Validasi

### 3. Evaluasi Kualitas Rekomendasi Top-N (Precision@K, Recall@K, F1-Score@K)

# 📋 Kesimpulan


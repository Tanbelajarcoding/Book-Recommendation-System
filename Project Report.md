# Laporan Proyek Machine Learning - Sistem Rekomendasi Buku
### Oleh Sulthan Muhammad Rafif Ilham

# 🌍 Project Overview

Bagian ini memberikan gambaran umum mengenai proyek sistem rekomendasi buku. Ini mencakup latar belakang masalah, justifikasi pentingnya proyek, serta tinjauan terhadap penelitian terkait yang menjadi dasar bagi pengembangan.

## 1. Latar Belakang
Minat baca di Indonesia merupakan salah satu tantangan yang signifikan. Menurut sebuah studi, Indonesia menempati peringkat 60 dari 61 negara dalam hal minat baca, yang salah satu faktor penyebabnya adalah kesulitan pembaca dalam menemukan buku yang sesuai di tengah banyaknya pilihan yang beredar (Sukmawati, et al., 2023). Fenomena *information overload* ini juga digarisbawahi oleh Zayyad (2021), yang menyatakan bahwa tersebarnya informasi mengenai beragam jenis buku seringkali menyulitkan seseorang untuk mencari buku berdasarkan kriteria yang disukai.

Untuk mengatasi permasalahan tersebut, pemanfaatan teknologi **sistem rekomendasi** menjadi sangat relevan. Sistem rekomendasi adalah alat penting yang telah banyak digunakan di berbagai industri untuk meningkatkan pengalaman pengguna (Hutabarat, 2022) dan mengubah pendekatan bisnis agar dapat menjangkau calon pelanggan secara lebih efektif (Putri, et al., 2020). Sistem ini tidak hanya merekomendasikan item spesifik, tetapi seringkali menyajikan sejumlah item teratas yang paling mungkin cocok dengan preferensi pengguna, atau yang dikenal sebagai "top-N recommendation" (Hutabarat, 2022).

Penelitian sebelumnya telah banyak mengeksplorasi berbagai metode untuk sistem rekomendasi buku:
* **Zayyad (2021)** berhasil mengimplementasikan metode **Content-Based Filtering (CBF)** dengan algoritma TF-IDF dan Cosine Similarity untuk memberikan rekomendasi buku dan mencapai nilai presisi sebesar 85%.
* **Sukmawati, et al. (2023)** menggunakan pendekatan **Collaborative Filtering (CF)** pada data rating buku dari Kaggle untuk memudahkan pengguna menemukan buku fiksi yang sesuai dengan selera mereka.
* **Hutabarat (2022)** juga menerapkan teknik **Collaborative Filtering** namun dengan algoritma K-Nearest Neighbors (KNN) dan berhasil memberikan rekomendasi buku dengan nilai *Mean Absolute Error* (MAE) yang rendah.
* Sementara itu, **Putri, et al. (2020)** menunjukkan bahwa metode CBF dengan TF-IDF juga efektif diterapkan di domain produk lain untuk meningkatkan *Customer Relationship Management* (CRM).

Proyek ini akan membangun dan membandingkan kedua pendekatan utama tersebut (CBF dan CF) menggunakan Book-Crossing Dataset untuk memberikan solusi yang komprehensif.

## 2. Mengapa dan Bagaimana Masalah Ini Harus Diselesaikan

Kesulitan pembaca dalam menemukan buku yang relevan dapat menimbulkan beberapa konsekuensi negatif, antara lain:
* Menurunnya minat baca karena pengalaman mencari buku yang kurang memuaskan.
* Pembaca cenderung hanya terpaku pada buku-buku populer atau *bestseller*, sehingga potensi penulis dan buku berkualitas lainnya menjadi kurang terekspos.
* Pembaca menghabiskan banyak waktu dan tenaga untuk mencari buku yang tepat.

**Penyelesaian masalah ini menjadi penting untuk:**
1.  **Meningkatkan Pengalaman Membaca**: Dengan menyajikan rekomendasi yang dipersonalisasi, sistem dapat membuat proses penemuan buku menjadi lebih mudah dan menyenangkan.
2.  **Mendorong Eksplorasi Penulis dan Genre Baru**: Sistem dapat memperkenalkan pengguna pada buku-buku yang mungkin mereka sukai tetapi belum pernah mereka temukan sebelumnya, menciptakan efek penemuan (*serendipity*).
3.  **Menyediakan Solusi yang Efektif**: Dengan mengimplementasikan dan mengevaluasi dua metode berbeda, proyek ini bertujuan untuk memberikan solusi praktis yang dapat memberikan rekomendasi yang akurat dan beragam.

## 3. Referensi
* Hutabarat, K. I. (2022). *Implementasi Algoritma K-Nearest Neighbors Pada Sistem Rekomendasi Buku Menggunakan Teknik Collaborative Filtering* (Skripsi doktoral, Universitas Medan Area).
* Putri, M. W., Muchayan, A., & Kamisutara, M. (2020). Sistem rekomendasi produk pena eksklusif menggunakan metode content-based filtering dan TF-IDF. *JOINTECS (Journal of Information Technology and Computer Science)*, 5(3), 229-236.
* Sukmawati, P. A. S., Hiryanto, L., & Mawardi, V. C. (2023). Implementasi Metode Collaborative Filtering Based Untuk Sistem Rekomendasi Buku Fiksi. *Jurnal Ilmu Komputer Dan Sistem Informasi*, 11(2).
* Zayyad, M. R. A. (2021). *Sistem Rekomendasi Buku Menggunakan Metode Content Based Filtering*.

# 📈 **Business Understanding**

Bagian ini menguraikan pemahaman bisnis terkait proyek pengembangan sistem rekomendasi buku. Ini mencakup identifikasi masalah yang ada, tujuan yang ingin dicapai, serta pendekatan solusi yang akan diimplementasikan.

## 1. Problem Statements (Pernyataan Masalah)

Industri perbukuan dan minat baca menghadapi tantangan signifikan di era digital. Salah satu masalah utamanya adalah kesulitan pembaca dalam menemukan buku yang sesuai di tengah jutaan pilihan yang ada. Tantangan ini, yang dikenal sebagai **information overload**, menyebabkan proses pencarian buku menjadi tidak efisien dan seringkali kurang memuaskan karena platform yang ada bersifat generik dan **kurangnya personalisasi**. Akibatnya, pembaca cenderung kesulitan menemukan penulis atau genre baru dan lebih memilih buku-buku yang sudah populer (*bestseller*).

Kondisi ini berdampak langsung pada ekosistem literasi dan bisnis perbukuan:
1.  **Pengalaman membaca menjadi kurang optimal**, yang dapat mempengaruhi tingkat kepuasan dan loyalitas pembaca.
2.  **Banyak buku berkualitas**, terutama dari penulis yang kurang populer, menjadi **tidak terekspos** sehingga potensi mereka tidak tergali secara maksimal.
3.  **Pembaca cenderung hanya memilih buku-buku populer**, yang membatasi keragaman bacaan dan menghambat penemuan karya-karya baru.
4.  **Menurunnya minat baca secara umum** karena pengalaman mencari buku yang dirasa sulit dan tidak memuaskan.

**Pernyataan Masalah Utama:**
1.  **Bagaimana** mengatasi *information overload* dan kurangnya personalisasi agar pembaca dapat secara efisien menemukan buku yang paling relevan dengan preferensi unik mereka?
2.  **Bagaimana** mengembangkan sistem rekomendasi yang dipersonalisasi, yang tidak hanya meningkatkan kepuasan pembaca, tetapi juga mampu mendorong penemuan buku, genre, dan penulis baru untuk mendukung ekosistem literasi yang lebih beragam?

## 2. Goals (Tujuan)

**Tujuan Utama:**
Mengembangkan sistem rekomendasi buku yang cerdas, personal, dan mampu memberikan rekomendasi yang beragam.

**Tujuan Spesifik:**
- **Mengembangkan Model Content-Based Filtering**: Tujuan ini adalah untuk membangun sistem rekomendasi yang menyarankan buku berdasarkan kemiripan konten, yaitu fitur **kategori**. Secara teknis, ini melibatkan penggunaan metode TF-IDF untuk mengubah atribut kategori menjadi representasi vektor, kemudian menggunakan Cosine Similarity untuk menghitung kemiripan antar buku. ``
- **Mengembangkan model Collaborative Filtering dengan deep learning**: Poin ini berfokus pada pembuatan model rekomendasi yang belajar dari pola rating kolektif semua pengguna. Dengan menggunakan arsitektur *deep learning* berbasis *embedding*, model dapat menangkap pola preferensi yang kompleks dan tersembunyi untuk merekomendasikan buku yang disukai oleh pengguna-pengguna dengan selera serupa. ``
- **Menyediakan rekomendasi akurat dan dipersonalisasi**: Tujuan ini menekankan pada kualitas output sistem. "Akurat" berarti rekomendasi yang diberikan sesuai dengan apa yang kemungkinan besar akan disukai pengguna, sementara "dipersonalisasi" berarti saran yang ditampilkan unik untuk setiap individu.
- **Meningkatkan pengalaman pencarian buku**: Proyek ini bertujuan untuk membuat proses pencarian buku menjadi lebih personal dan intuitif, di mana sistem secara proaktif menyajikan pilihan yang telah disesuaikan dengan profil pengguna.
- **Membantu menemukan buku baru dan beragam**: Salah satu tujuan penting adalah membantu pengguna menemukan "*hidden gem*". Sistem rekomendasi, terutama melalui pendekatan Collaborative Filtering, dapat menyarankan buku yang mungkin tidak pernah terpikirkan oleh pengguna sebelumnya namun berpotensi besar untuk disukai.

## 3. Solution Approach (Pendekatan Solusi)
Proyek ini mengimplementasikan dan membandingkan dua pendekatan utama dalam sistem rekomendasi:
1.  **Content-Based Filtering** menggunakan TF-IDF dan Cosine Similarity. ``
2.  **Collaborative Filtering** dengan model *deep learning* berdasarkan interaksi rating pengguna. ``

**Perbandingan Pendekatan:**
| Aspek | Content-Based | Collaborative |
| :--- | :--- | :--- |
| **Kekuatan** | Transparan, baik untuk preferensi spesifik | Personal, menemukan item tak terduga |
| **Kelemahan** | Terbatas pada kemiripan konten | Masalah *Cold start* |
| **Data yang Dibutuhkan**| Metadata buku (kategori) | Histori interaksi pengguna (rating) |
| **Kompleksitas** | Relatif sederhana | Lebih kompleks |

# 🧠 Data Understanding

Bagian ini memberikan pemahaman mendalam mengenai dataset yang digunakan dalam proyek sistem rekomendasi buku. Ini mencakup gambaran umum dataset, deskripsi lengkap setiap fitur, serta temuan-temuan kunci dari proses analisis data eksplorasi (EDA).

## Dataset Overview
* **Nama Dataset:** Book-Crossing Dataset ``
* **Sumber:** Kaggle ([Link Dataset](https://www.kaggle.com/datasets/ruchi798/bookcrossing-dataset)) ``

**Cakupan dan Proses Pengurangan Data:**
Proyek ini menggunakan file `Preprocessed_data.csv` yang merupakan gabungan data rating, pengguna, dan buku. Dataset asli memiliki skala yang sangat besar (lebih dari 1 juta rating), yang akan sangat membebani sumber daya komputasi. Untuk mengatasi hal ini, dilakukan proses pengurangan data yang cermat:
1.  **Sampling**: Pertama, diambil sampel acak sebanyak **100.000** baris rating dari dataset asli.
2.  **Identifikasi Buku Unik**: Dari sampel tersebut, diidentifikasi buku-buku unik berdasarkan ISBN-nya.
3.  **Filtering**: Dataset asli yang berisi 1 juta rating kemudian difilter untuk hanya menyimpan semua baris rating yang terkait dengan buku-buku yang telah teridentifikasi dari sampel.

Proses ini menghasilkan dataset kerja yang lebih fokus namun tetap kaya akan interaksi untuk buku-buku yang terpilih. Berikut adalah perbandingan skala data sebelum dan sesudah proses filtering:

| Deskripsi | Jumlah Awal | Jumlah Setelah Filter (Digunakan untuk EDA) |
| :--- | :--- | :--- |
| **Jumlah Rating** | 1.031.175 | 617.642 |
| **Jumlah User Unik**| 92.107 | 71.675 |
| **Jumlah Buku Unik**| 270.170 | 58.949 |

## Feature Description
Berikut adalah deskripsi lengkap dari 19 fitur yang terdapat dalam dataset `rating_filtered` yang digunakan untuk analisis. ``

| Kolom | Tipe Data | Deskripsi |
| :--- | :--- | :--- |
| `Unnamed: 0`| `int64` | Kolom indeks sisa dari proses pra-pemrosesan sebelumnya. |
| `user_id` | `int64` | ID unik untuk setiap pengguna. |
| `location` | `object` | Lokasi pengguna (kota, provinsi, negara). |
| `age` | `float64` | Usia pengguna (beberapa nilai merupakan hasil imputasi). |
| `isbn` | `object` | ID unik standar internasional untuk setiap buku. |
| `rating` | `int64` | Skor penilaian yang diberikan pengguna (skala 0-10). |
| `book_title`| `object` | Judul dari buku. |
| `book_author`| `object` | Nama penulis buku. |
| `year_of_publication`| `float64`| Tahun buku diterbitkan. |
| `publisher` | `object` | Nama penerbit buku. |
| `img_s` | `object` | URL gambar sampul buku ukuran kecil. |
| `img_m` | `object` | URL gambar sampul buku ukuran sedang. |
| `img_l` | `object` | URL gambar sampul buku ukuran besar. |
| `Summary` | `object` | Ringkasan atau sinopsis buku. |
| `Language` | `object` | Bahasa dari buku. |
| `Category` | `object` | Kategori atau genre dari buku. |
| `city` | `object` | Kota domisili pengguna. |
| `state` | `object` | Provinsi/negara bagian domisili pengguna. |
| `country` | `object` | Negara domisili pengguna. |

## Data Exploration Findings

### Distribusi Geografis
Analisis awal terhadap sebaran geografis pengguna dalam dataset menunjukkan bahwa **71.675 pengguna unik** berasal dari **18.350 lokasi berbeda**. Tingginya jumlah lokasi ini menandakan bahwa basis pengguna sangat beragam dan tersebar secara internasional, mencakup berbagai kota dan negara di seluruh dunia, tidak terkonsentrasi pada satu wilayah tertentu. ``

### Analisis Univariat

#### Location
![image](https://github.com/user-attachments/assets/d3d0de26-d9c0-498b-b59b-b8b9d15ffd77)

**Insight:** Grafik 10 lokasi teratas menunjukkan bahwa tidak ada satu pun lokasi yang mendominasi secara kuat. **Toronto, Kanada (1.3%)** menjadi lokasi dengan kontribusi rating tertinggi. Namun, temuan menarik adalah munculnya **'n/a, n/a, n/a' (1.1%)** sebagai lokasi kedua teratas, yang mengindikasikan adanya masalah kualitas pada data lokasi. Hal ini mengonfirmasi bahwa basis pengguna sangat tersebar secara geografis. ``

#### Age
![image](https://github.com/user-attachments/assets/2efa77ed-8c7f-4f27-9d16-0f2f1a696350)

**Insight:** Distribusi usia pengguna menunjukkan puncak frekuensi yang sangat tajam di sekitar usia **34.7 tahun**, yang merupakan nilai median. Puncak ini kemungkinan besar adalah hasil dari imputasi nilai kosong pada data asli. Di luar itu, mayoritas pengguna berada pada rentang usia dewasa muda hingga paruh baya, dengan nilai rata-rata (mean) **36.3 tahun**. ``

#### Rating
![image](https://github.com/user-attachments/assets/de4d5104-33dc-49a4-8e3c-3781368245d5)

**Insight:** Terdapat puncak frekuensi yang sangat besar pada **rating 0**, yang mengindikasikan mayoritas interaksi bersifat implisit (pengguna tidak memberikan skor). Untuk rating eksplisit (1-10), distribusinya sangat miring ke kiri dengan puncak pada **rating 8**, menandakan pengguna cenderung memberikan ulasan positif. ``

#### Book Author
![image](https://github.com/user-attachments/assets/0230aa2b-c58a-49dc-aeb6-86326d602d42)

**Insight:** Analisis 10 penulis teratas menunjukkan bahwa **Stephen King (1.5%)** adalah penulis yang paling banyak diulas, diikuti oleh penulis fiksi populer lainnya seperti **Nora Roberts (1.3%)** dan **John Grisham (0.9%)**. ``

#### Year of Publication
![image](https://github.com/user-attachments/assets/2410631d-7b2f-40af-b922-0e8441c1fcbe)

**Insight:** Dataset didominasi oleh buku-buku modern, dengan puncak publikasi terjadi pada **akhir 1990-an hingga awal 2000-an**. Distribusi yang sangat miring ke kiri ini menunjukkan bahwa sebagian besar buku yang diberi rating dalam dataset ini terbit dalam beberapa dekade terakhir. ``

#### Publisher
![image](https://github.com/user-attachments/assets/0444fc60-07b6-498d-bb99-9409b46483a6)

**Insight:** Dari hasil visualisasi, terlihat bahwa **Ballantine Books** merupakan penerbit yang paling dominan dengan **4.5%** dari total entri, diikuti oleh penerbit besar lainnya seperti **Pocket (4.1%)**. Ini menunjukkan adanya konsentrasi pada penerbit buku pasar massal. ``

#### Language
![image](https://github.com/user-attachments/assets/f1baee1d-749b-4c34-913f-406413aeb378)

**Insight:** **Bahasa Inggris (`en`)** mendominasi dataset secara absolut (64.2%). Ditemukan juga anomali data yang signifikan, di mana nilai **'9'** muncul sebagai 'bahasa' kedua teratas dengan frekuensi tinggi (34.8%). ``

#### Category
![image](https://github.com/user-attachments/assets/5637dc85-637f-4c25-9365-4cbc9debe5e5)

**Insight:** Kategori **Fiksi (`['Fiction']`)** merupakan yang paling dominan (46.1%). Seperti pada kolom bahasa, nilai anomali **'9'** juga muncul dengan frekuensi tinggi (35.2%). Selain itu, format datanya belum seragam dan masih terbungkus dalam format *string list*. ``

### Matrix Density
Dengan total **617.642 rating** dari **71.675 pengguna** dan **58.949 buku** dalam dataset yang difilter, kepadatan matriks interaksinya adalah:
$$\text{Density} = \frac{\text{Jumlah Rating}}{\text{Jumlah User} \times \text{Jumlah Buku}} = \frac{617.642}{71.675 \times 58.949} \approx 0.0146\%$$
Nilai kepadatan yang sangat rendah ini (**0.0146%**) mengonfirmasi bahwa dataset bersifat sangat **sparse** (jarang). Artinya, hanya sebagian kecil dari kemungkinan pasangan pengguna-buku yang benar-benar memiliki rating, yang menjadi tantangan utama untuk model *collaborative filtering*. ``

## 🔍 Ringkasan EDA
1.  **Kualitas Data**: Ditemukan beberapa masalah kualitas data, termasuk nilai anomali ('9'), format yang tidak konsisten pada kolom kategori, nilai yang diimputasi pada kolom usia, dan data lokasi yang tidak valid.
2.  **Demografi Pengguna**: Pengguna tersebar secara global dan mayoritas berada pada rentang usia dewasa.
3.  **Karakteristik Buku**: Dataset sangat didominasi oleh buku fiksi modern berbahasa Inggris yang diterbitkan oleh penerbit besar.
4.  **Pola Pemberian Rating**: Terdapat banyak sekali rating implisit (nilai 0). Untuk rating eksplisit, pengguna cenderung memberikan skor tinggi.
5.  **Kekosongan Data (Sparsity)**: Matriks interaksi pengguna-buku sangat jarang (*sparse*), yang dapat menimbulkan masalah *cold start*.

## 🚩 Permasalahan dan Insight Data
1.  **Skala Data & Keterbatasan Komputasi**: Ukuran dataset asli yang sangat besar mengharuskan dilakukannya proses sampling agar dapat diolah.
2.  **Kualitas Data & Anomali**: Adanya nilai anomali dan format yang tidak konsisten wajib ditangani pada tahap persiapan data untuk memastikan kualitas model.
3.  **Rating Implisit vs. Eksplisit**: Keberadaan rating 0 perlu dipisahkan dari rating eksplisit (1-10) agar tidak mengganggu proses training model yang berfokus pada prediksi skor.
4.  **Sparsity Tinggi**: Tingkat kepadatan yang sangat rendah menjadi tantangan utama yang dapat mempengaruhi kemampuan model collaborative filtering dalam generalisasi.

# ⚙️ Data Preparation

Tahap Data Preparation merupakan langkah berikutnya setelah Data Understanding. Pada tahap ini, dataset yang telah dieksplorasi akan diolah dan ditransformasi menjadi format yang sesuai dan optimal untuk tahap pemodelan. Proses ini melibatkan serangkaian teknik untuk membersihkan, menyeleksi fitur, dan menstrukturkan data guna meningkatkan kualitasnya. Tahap ini akan mencakup persiapan data yang spesifik untuk masing-masing pendekatan: vektorisasi dengan TF-IDF untuk *Content-Based Filtering* dan *encoding* serta normalisasi untuk *Collaborative Filtering*.

### 1. Pembersihan Data dan Standardisasi Format
Langkah awal adalah membersihkan data dari berbagai anomali dan format yang tidak konsisten yang ditemukan pada tahap EDA.

* **Proses yang Dilakukan:**
    1.  **Identifikasi Format**: Pengecekan awal pada kolom `Category` menggunakan `.unique()` menunjukkan format data belum seragam (contoh: `"['Social Science']"`) dan terdapat nilai anomali. ``
    2.  **Penghapusan Data Anomali**: Semua baris yang memiliki nilai **'9'** pada kolom `Category` dihapus karena dianggap sebagai data yang tidak valid. ``
    3.  **Standardisasi String**: Format kolom `Category` dibersihkan dengan menghapus semua karakter yang tidak diinginkan seperti tanda kurung (`[]`) serta tanda kutip (`' "`), dan spasi diganti dengan *underscore* (`_`). ``
    4.  **Penghapusan Rating Implisit**: Semua baris dengan **rating 0** (yang dianggap sebagai interaksi implisit) dihapus untuk memfokuskan model pada preferensi eksplisit pengguna (rating 1-10). ``
* **Alasan Dilakukan:**
    * **Validitas Data**: Menghapus data anomali dan rating implisit sangat penting untuk memastikan model dilatih pada data yang bersih, valid, dan sesuai dengan tujuan (memprediksi rating eksplisit).
    * **Konsistensi Fitur**: Menyeragamkan format `Category` krusial untuk proses *feature engineering* (seperti TF-IDF) agar setiap kategori dapat diproses sebagai token yang konsisten.

### 2. Seleksi Fitur
Setelah data dibersihkan, dilakukan pemilihan fitur yang relevan untuk tujuan pemodelan.

* **Proses yang Dilakukan:**
    * Dari 19 kolom awal, hanya 5 kolom yang dipertahankan: `user_id`, `isbn`, `rating`, `book_title`, dan `Category`. ``
    * Langkah ini menghasilkan DataFrame akhir (`df_cleaned`) dengan **149.289 baris** dan 5 kolom. ``
* **Alasan Dilakukan:**
    * Menyederhanakan dataset agar lebih fokus dan efisien untuk pemodelan.
    * Memastikan hanya fitur yang paling esensial untuk kedua pendekatan rekomendasi yang digunakan.

### 3. Verifikasi Akhir Kualitas Data
Pengecekan terakhir dilakukan untuk memastikan tidak ada lagi masalah pada data yang telah diolah.

* **Proses yang Dilakukan:**
    1.  Pemeriksaan `Missing Values` menggunakan `.isnull().sum()`. Hasilnya menunjukkan **0 nilai hilang** pada semua kolom yang telah diseleksi. ``
    2.  Pemeriksaan data duplikat menggunakan `.duplicated().sum()`. Hasilnya juga menunjukkan **0 data duplikat**. Perintah `.drop_duplicates()` tetap dijalankan sebagai langkah preventif. ``
* **Alasan Dilakukan:**
    * Langkah verifikasi ini adalah praktik terbaik untuk menjamin kualitas akhir data dan mencegah potensi error saat pelatihan model.

### 4. Penyiapan Data Final untuk Analisis
Sebuah DataFrame final disiapkan sebagai *working copy* untuk kedua pendekatan model.

* **Proses yang Dilakukan:**
    * DataFrame `df_cleaned` yang telah melalui semua proses pembersihan disimpan ke dalam variabel baru bernama `preparation`. ``
    * Data diurutkan berdasarkan `isbn` untuk memberikan struktur yang rapi dan mempermudah inspeksi. ``
* **Struktur Data Final:**
    | Kolom | Tipe Data |
    | :--- | :--- |
    | `user_id` | `int64` |
    | `isbn` | `object` |
    | `rating` | `int64` |
    | `book_title`| `object` |
    | `Category` | `object` |

### 5. Persiapan Data untuk Model Content-Based Filtering

#### 1. Persiapan Data Buku Unik
* **Proses yang Dilakukan:** Data duplikat berdasarkan kolom `isbn` dihapus dari `preparation`. Langkah ini menghasilkan DataFrame baru (`preparation_CBF`) yang berisi **25.183 baris**, di mana setiap baris mewakili satu buku unik. ``
* **Alasan Dilakukan:** Model *Content-Based Filtering* berfokus pada karakteristik intrinsik buku, sehingga hanya memerlukan satu representasi unik untuk setiap buku.

#### 2. Ekstraksi Informasi Buku
* **Proses yang Dilakukan:** Kolom `isbn`, `book_title`, dan `Category` diekstrak dari `preparation_CBF` menjadi *list* terpisah. Dari *list* ini, sebuah DataFrame baru bernama `book_data` dibuat dengan tiga kolom (`id`, `book`, `category`). ``
* **Alasan Dilakukan:** Menyederhanakan struktur data agar sesuai dengan input yang dibutuhkan untuk proses vektorisasi fitur.

#### 3. Vektorisasi Fitur Kategori dengan TF-IDF
* **Proses yang Dilakukan:** Fitur `category` yang berbasis teks diubah menjadi representasi vektor numerik menggunakan **TF-IDF**. Proses ini menghasilkan sebuah matriks fitur (`tfidf_matrix`) berukuran **(25183, 1727)**. ``
* **Alasan Dilakukan:** Mengubah data tekstual menjadi format numerik yang dapat diolah oleh algoritma untuk menghitung kemiripan.

#### 4. Ringkasan Hyperparameter TF-IDF Vectorizer (`TfidfVectorizer`)
Meskipun tidak disetel secara eksplisit, proyek ini menggunakan nilai default dari `TfidfVectorizer` yang penting untuk dipahami.

| Hyperparameter | Nilai Default | Penjelasan |
| :--- | :--- | :--- |
| `lowercase` | `True` | Mengubah semua teks menjadi huruf kecil untuk konsistensi. |
| `stop_words`| `None` | Tidak ada *stop words* yang dihapus. |
| `ngram_range`| `(1,1)` | Hanya menggunakan unigram (token tunggal) sebagai fitur. |
| `norm` | `'l2'` | Menerapkan normalisasi L2 pada setiap vektor output. |
| `use_idf` | `True` | Mengaktifkan pembobotan *Inverse Document Frequency*. |


### 6. Persiapan Data untuk Model Collaborative Filtering

#### 1. Encoding Fitur Pengguna dan Buku
* **Proses yang Dilakukan:** `user_id` dan `isbn` yang bersifat kategorikal diubah menjadi indeks integer yang berurutan (dimulai dari 0). Proses ini menciptakan dua kolom baru (`user_encoded` dan `book_encoded`) dan *dictionary* untuk pemetaan. ``
* **Alasan Dilakukan:** *Embedding layer* pada model *deep learning* memerlukan input berupa indeks integer yang padat.

#### 2. Pembagian Data Latih dan Validasi (Train-Validation Split) dan Normalisasi Rating
* **Proses yang Dilakukan:**
    1.  Seluruh dataset diacak secara acak (`random_state=42`). ``
    2.  Variabel input `x` dibentuk dari pasangan `user_encoded` dan `book_encoded`. ``
    3.  Variabel target `y` (kolom `rating`) dinormalisasi ke rentang nilai **[0, 1]** menggunakan *min-max scaling*. ``
    4.  Data dibagi menjadi **80% data latih** dan **20% data validasi**. ``
* **Hasil Pembagian Data:**
    | Deskripsi | Jumlah Sampel |
    | :--- | :--- |
    | **Total Sampel** | 149.289 |
    | **Data Latih (80%)** | 119.431 |
    | **Data Validasi (20%)** | 29.858 |
* **Alasan Dilakukan:**
    * Normalisasi rating membantu menstabilkan proses pelatihan.
    * Pembagian data adalah praktik standar untuk mengevaluasi kemampuan generalisasi model pada data yang belum pernah dilihat.

# 🧮 Modeling
Tahap pemodelan adalah inti dari proyek ini di mana teknik-teknik *machine learning* diterapkan untuk mencapai tujuan yang telah ditetapkan. Dalam proyek ini, akan dikembangkan dua solusi sistem rekomendasi buku yang menggunakan algoritma berbeda untuk memberikan saran Top-N (sejumlah N item teratas) yang relevan kepada pengguna.

Dua pendekatan utama yang diimplementasikan adalah:
1.  **Content-Based Filtering (Penyaringan Berbasis Konten):** Memanfaatkan atribut atau fitur dari buku (dalam kasus ini, kategori) untuk merekomendasikan item yang serupa.
2.  **Collaborative Filtering (Penyaringan Kolaboratif):** Menggunakan interaksi historis pengguna dengan buku (rating) dan menerapkan model *deep learning* berbasis *embedding* untuk menemukan pola kesukaan dan merekomendasikan buku berdasarkan preferensi pengguna lain yang serupa.

Berikut ini adalah penjelasan detail untuk masing-masing pendekatan:

## Solusi 1: Content-Based Filtering (CBF)
Pendekatan *Content-Based Filtering* (CBF) merekomendasikan item berdasarkan kemiripan antara fitur item yang telah disukai pengguna di masa lalu dengan fitur item lain yang tersedia. Dalam proyek ini, CBF diimplementasikan dengan memanfaatkan **kategori buku** sebagai fitur utama.

### 1. Perhitungan Kemiripan Antar Buku dengan Cosine Similarity
Setelah buku direpresentasikan sebagai vektor TF-IDF pada tahap persiapan data, langkah pertama adalah menghitung kemiripan antar semua pasangan buku.

* **Proses yang Dilakukan:**
    1.  Fungsi `cosine_similarity` dari `sklearn.metrics.pairwise` diterapkan pada `tfidf_matrix` yang telah dibuat. ``
        ```python
        # from sklearn.metrics.pairwise import cosine_similarity
        # cosine_sim = cosine_similarity(tfidf_matrix)
        ```
    2.  Hasilnya adalah matriks kemiripan (`cosine_sim`) berukuran **25.183 x 25.183**. Setiap elemen (i, j) dalam matriks ini merepresentasikan skor kemiripan antara buku ke-i dan buku ke-j. ``
    3.  Matriks kemiripan ini kemudian diubah menjadi DataFrame pandas (`cosine_sim_df`) dengan judul buku sebagai indeks dan kolom untuk memudahkan interpretasi. ``
        ```python
        # cosine_sim_df = pd.DataFrame(cosine_sim, index=book_data['book'], columns=book_data['book'])
        ```
* **Alasan Dilakukan:**
    *Cosine Similarity* adalah metrik yang efektif untuk mengukur kesamaan antara dua vektor dalam ruang multidimensi, sangat cocok untuk data tekstual yang telah divektorisasi. Matriks `cosine_sim_df` ini menjadi dasar bagi model CBF untuk menemukan buku yang paling mirip dengan buku input.

### 2. Implementasi Fungsi Rekomendasi Buku
Untuk menghasilkan rekomendasi, sebuah fungsi khusus (`book_recommendations`) dibuat. ``

* **Proses yang Dilakukan:**
    Fungsi ini menerima judul buku sebagai input dan bekerja sebagai berikut:
    1.  Mengambil baris/kolom yang sesuai dengan buku input dari matriks kemiripan.
    2.  Mengidentifikasi 5 buku lain dengan skor kemiripan tertinggi menggunakan `argpartition` untuk efisiensi.
    3.  Menghilangkan buku input dari daftar rekomendasi.
    4.  Menggabungkan hasil dengan informasi kategori buku dan mengembalikan 5 buku teratas. ``
* **Contoh Output Rekomendasi (Top-5):**
    Ketika fungsi diuji dengan input buku **"Wild Animus"** (kategori: Fiction), sistem memberikan output sebagai berikut: ``
    ```
    ✨ Rekomendasi buku Serupa untuk: Wild Animus (Kategori: Fiction)
    ============================================================
    No.  book                                     | Category
    ------------------------------------------------------------
    1    Where Do You Stop? : The Personal History... | Fiction
    2    Humboldt's Gift                          | Friendship
    3    Humboldt's Gift                          | Fiction
    4    That Camden Summer                       | Fiction
    5    That Camden Summer                       | Fiction
    ------------------------------------------------------------
    ```
    Hasil ini menunjukkan model berhasil merekomendasikan buku-buku lain yang mayoritas berkategori sama (Fiction). Adanya judul duplikat atau kategori yang sedikit berbeda ('Friendship') kemungkinan disebabkan oleh variasi data pada dataset asli.

### 3. Kelebihan dan Kekurangan Content-Based Filtering

* **Kelebihan:**
    * **Transparan:** Rekomendasi mudah dijelaskan (contoh: "direkomendasikan karena memiliki kategori yang sama").
    * **Tidak Memerlukan Data Pengguna Lain:** Dapat memberikan rekomendasi untuk buku yang belum memiliki rating.
    * **Penanganan Item Baru (*Item Cold Start*):** Selama metadata buku tersedia, sistem dapat langsung memberikan rekomendasi.
* **Kekurangan:**
    * **Terbatasnya Serendipitas:** Cenderung merekomendasikan item yang sangat mirip, sehingga mengurangi peluang pengguna menemukan genre atau penulis yang benar-benar baru.
    * ***Filter Bubble***: Pengguna mungkin terjebak dalam rekomendasi yang monoton dari kategori yang sama.
    * **Ketergantungan pada Kualitas Fitur:** Kualitas rekomendasi sangat bergantung pada kelengkapan fitur `Category`.

---

## Solusi 2: Collaborative Filtering (CF) dengan Embedding Deep Learning
Pendekatan ini fokus pada pola interaksi pengguna-buku (rating) dan diimplementasikan menggunakan model *deep learning* yang memanfaatkan teknik *embedding*.

### 1. Membangun Model Deep Learning untuk Collaborative Filtering
Sebuah model *neural network* kustom dirancang menggunakan Keras API.

* **Arsitektur Model (`RecommenderNet`):**
    Sebuah kelas `RecommenderNet` didefinisikan dengan komponen utama sebagai berikut: ``
    1.  **Embedding Layers:** `user_embedding` dan `book_embedding` memetakan setiap ID ke sebuah vektor *embedding* berdimensi 8.
    2.  **Bias Layers:** `user_bias` dan `book_bias` mempelajari bias spesifik untuk setiap pengguna dan buku.
    3.  **Metode `call` (Forward Pass):**
        * Melakukan operasi *dot product* antara vektor *embedding* pengguna dan buku untuk menangkap interaksi.
        * Menambahkan bias pengguna dan bias buku ke hasil *dot product*.
        * Melewatkan hasil akhir melalui fungsi aktivasi **sigmoid** untuk menghasilkan prediksi rating dalam rentang [0, 1].
* **Alasan Arsitektur Ini:**
    Arsitektur ini pada dasarnya mengimplementasikan teknik *Matrix Factorization*. *Embedding layers* bertugas mempelajari fitur-fitur laten dari pengguna dan buku yang dapat menjelaskan pola rating yang diamati.

### 2. Kompilasi dan Pelatihan Model
Model yang telah dirancang kemudian dikompilasi dan dilatih.

* **Proses Kompilasi dan Pelatihan:**
    1.  Model `RecommenderNet` diinisialisasi dengan jumlah pengguna dan buku unik, serta ukuran *embedding* (8). ``
    2.  *Callbacks* `EarlyStopping` (patience=10) dan `ReduceLROnPlateau` (patience=5) disiapkan untuk optimasi. ``
    3.  Model dikompilasi menggunakan *loss function* `MeanSquaredError`, *optimizer* `Adam`, dan metrik `RootMeanSquaredError`. ``
    4.  Model dilatih (`model.fit`) dengan `batch_size = 125` dan maksimum `epochs = 100`. Pelatihan berhenti pada **epoch 45** dan mengembalikan bobot terbaik dari **epoch 35**. ``

### 3. Inferensi dan Contoh Penggunaan untuk Top-N Rekomendasi
Model yang telah dilatih digunakan untuk memberikan rekomendasi yang dipersonalisasi.

* **Proses Inferensi:**
    1.  Satu `user_id` (User ID 8) dipilih sebagai contoh. ``
    2.  Daftar buku yang *belum* pernah diulas oleh pengguna tersebut dibuat. ``
    3.  Model (`model.predict`) digunakan untuk memprediksi skor rating untuk semua buku yang belum diulas tersebut. ``
    4.  10 buku dengan prediksi skor tertinggi diambil sebagai rekomendasi. ``
* **Contoh Output Rekomendasi (Top-10 untuk User ID: 8):**
    Sebagai konteks, riwayat baca pengguna (hanya "Clara Callan") ditampilkan. Kemudian, model memberikan 10 rekomendasi baru: ``
    ```
    ✨ Top 10 Book Recommendations for User:
    ------------------------------------------------------------
    No.  Book                                     | Category
    ------------------------------------------------------------
    1    The Return of the King (The Lord of The... | Fantasy_fiction,_English
    2    Calvin and Hobbes                        | Humor
    3    The Authoritative Calvin and Hobbes...   | Humor
    4    Bridge to Terabithia                     | Death
    5    More Than Complete Hitchhiker's Guide    | Dent,_Arthur_(Fict...
    6    The Sneetches and Other Stories          | Juvenile_Fiction
    7    My Sister's Keeper : A Novel (Picoult... | Fiction
    8    The Giving Tree                          | Juvenile_Fiction
    9    Harry Potter and the Chamber of Secr...  | Juvenile_Fiction
    10   The Hitchhiker's Guide to the Galaxy     | Fiction
    ```
    Output ini menunjukkan kemampuan model dalam memberikan rekomendasi yang beragam dan bersifat penemuan (*serendipity*).

### 4. Ringkasan Hyperparameter Model Collaborative Filtering

#### **1. Hyperparameter Terkait Embedding**
| Hyperparameter | Nilai | Deskripsi |
| :--- | :--- | :--- |
| `embedding_size` | `8` | Ukuran vektor embedding untuk pengguna dan buku. |
| `embeddings_initializer`| `'he_normal'` | Metode inisialisasi bobot untuk layer embedding. |
| `embeddings_regularizer`| `l2(1e-4)` | Regularisasi L2 untuk mencegah overfitting. |

#### **2. Hyperparameter Pelatihan Model**
| Hyperparameter | Nilai | Deskripsi |
| :--- | :--- | :--- |
| `loss` | `MeanSquaredError` | Fungsi kerugian untuk regresi rating. |
| `optimizer` | `Adam` | Optimizer yang digunakan. |
| `learning_rate` | `0.001` | Learning rate awal. |
| `batch_size`| `125` | Jumlah sampel per iterasi. |
| `epochs` | `100` | Jumlah maksimum iterasi pelatihan. |

### 5. Kelebihan dan Kekurangan Collaborative Filtering
* **Kelebihan:**
    * Mampu menangkap pola preferensi yang kompleks dan non-linear.
    * Memungkinkan penemuan rekomendasi yang bersifat *serendipitous*.
    * Tidak memerlukan *feature engineering* pada konten item.
* **Kekurangan:**
    * Mengalami masalah **Cold Start** untuk pengguna atau buku baru.
    * Membutuhkan data interaksi yang cukup besar untuk bisa efektif.
    * Rekomendasi yang dihasilkan kurang transparan (*less explainable*).

# 💯 Evaluation

Tahap evaluasi model bertujuan untuk menilai sejauh mana model-model sistem rekomendasi yang telah dikembangkan mampu mencapai tujuan yang ditetapkan. Pada tahap ini, kinerja kedua pendekatan model—*Content-Based Filtering* dan *Collaborative Filtering*—diukur menggunakan serangkaian metrik yang relevan untuk tugas prediksi rating dan kualitas daftar rekomendasi Top-N.

## Metrik Evaluasi yang Digunakan

Berikut adalah metrik-metrik yang digunakan untuk mengevaluasi performa model dalam proyek ini:

| Metrik | Tipe | Penggunaan |
| :--- | :--- | :--- |
| **RMSE** | Regression | Mengukur akar dari rata-rata kuadrat eror, sehingga memiliki skala yang sama dengan variabel target (rating). Memberikan bobot lebih besar pada eror yang lebih besar. Formula: $$RMSE = \sqrt{\frac{1}{N} \sum_{i=1}^{N} (y_i - \hat{y}_i)^2}$$ |
| **MAE** | Regression | Mengukur rata-rata selisih absolut antara nilai aktual dan prediksi. Memberikan gambaran langsung tentang besaran rata-rata eror. Formula: $$MAE = \frac{1}{N} \sum_{i=1}^{N} |y_i - \hat{y}_i|$$ |
| **Classification Report** | Classification | Digunakan untuk mengevaluasi model CBF sebagai tugas klasifikasi kategori. Menyajikan metrik `Precision`, `Recall`, dan `F1-Score`. |
| **Precision@K** | Ranking Metric | Dari K item teratas yang direkomendasikan, berapa proporsi yang benar-benar relevan bagi pengguna. Formula: $$\frac{\text{Jumlah item relevan dalam K rekomendasi}}{\text{K}}$$ |
| **Recall@K** | Ranking Metric | Dari semua item yang relevan bagi pengguna, berapa proporsi yang berhasil ditemukan dan direkomendasikan dalam K item teratas. Formula: $$\frac{\text{Jumlah item relevan dalam K rekomendasi}}{\text{Total item relevan untuk pengguna}}$$ |
| **F1-Score@K**| Ranking Metric | Rata-rata harmonik dari Precision@K dan Recall@K, memberikan ukuran tunggal yang menyeimbangkan kedua metrik. Formula: $$2 \cdot \frac{Precision@K \cdot Recall@K}{Precision@K + Recall@K}$$ |

\<br\>
Di mana $N$ adalah jumlah sampel, $y\_i$ adalah nilai aktual, dan $\\hat{y}\_i$ adalah nilai prediksi.

## Evaluasi Model Content-Based Filtering (CBF)

Evaluasi untuk model CBF difokuskan pada kemampuannya untuk mengenali buku berdasarkan kategorinya, dengan studi kasus pada kategori 'Fiction'.

  * **Proses Evaluasi:**
    Label *ground truth* dibuat dengan memberi nilai 1 untuk buku berkategori 'Fiction' dan 0 untuk kategori lainnya. Sistem kemudian memprediksi kategori sebuah buku dengan cara mencari buku lain yang memiliki *cosine similarity* tertinggi, lalu menggunakan kategori dari buku paling mirip tersebut sebagai hasil prediksi. \`\`

  * **Hasil dan Interpretasi:**

    ```
              precision    recall  f1-score   support

           0       1.00      1.00      1.00     11582
           1       1.00      1.00      1.00     13601

    accuracy                           1.00     25183
    macro avg       1.00      1.00      1.00     25183
    ```

weighted avg       1.00      1.00      1.00     25183
\`\`\`
Hasil evaluasi menunjukkan performa yang **sempurna** dengan nilai `precision`, \`recall\`, dan \`f1-score\` mencapai **1.00 (100%)** untuk kedua kelas. \`Accuracy\` keseluruhan juga mencapai **1.00**. Skor sempurna ini wajar terjadi karena kemiripan antar buku dalam model CBF ini hanya didasarkan pada satu fitur (kategori), sehingga buku 'Fiction' akan selalu memiliki kemiripan tertinggi dengan buku 'Fiction' lainnya. \`\`

## Evaluasi Model Collaborative Filtering (CF)

Evaluasi model CF berbasis *deep learning* dilakukan dalam beberapa aspek: pemantauan performa selama pelatihan, akurasi prediksi rating, dan kualitas daftar rekomendasi Top-N.

### 1\. Evaluasi Performa Selama Pelatihan (RMSE Plot)

Metrik *Root Mean Squared Error* (RMSE) dipantau pada setiap epoch untuk data latih dan data validasi guna memahami dinamika proses pembelajaran model.

[![image](https://github.com/user-attachments/assets/9b53df94-2977-4876-b93e-f0ede1238994)]

  * **Interpretasi Kurva RMSE:**
      * **Kurva RMSE Pelatihan (biru):** Menunjukkan penurunan nilai RMSE yang konsisten, menandakan bahwa model berhasil mempelajari pola dari data pelatihan dengan baik.
      * **Kurva RMSE Validasi (oranye):** Menurun pada beberapa epoch awal, kemudian cenderung stagnan dan sedikit meningkat. Kesenjangan (*gap*) yang melebar antara kedua kurva ini merupakan indikasi terjadinya **overfitting**. Fenomena ini memvalidasi pentingnya penggunaan *callback* `EarlyStopping` yang menghentikan pelatihan pada waktu yang tepat (epoch 45) dan mengembalikan bobot dari epoch terbaik (epoch 35). \`\`

### 2\. Perhitungan RMSE dan MAE pada Data Validasi

Performa akhir model dievaluasi pada data validasi yang belum pernah dilihat sebelumnya.

  * **Hasil dan Interpretasi:**
    Berdasarkan output yang diperoleh: \`\`

      * **RMSE: 0.1938**
      * **MAE : 0.1505**

    Nilai-nilai ini, yang diukur pada skala rating ternormalisasi [0, 1], memberikan ukuran kuantitatif dari eror prediksi model. **MAE sebesar 0.1505** mengindikasikan bahwa rata-rata selisih absolut prediksi dari nilai sebenarnya adalah sekitar 0.15. Nilai RMSE yang sedikit lebih tinggi mengonfirmasi bahwa model memiliki tingkat akurasi prediksi yang baik. \`\`

### 3\. Evaluasi Kualitas Rekomendasi Top-N (Precision@K, Recall@K, F1-Score@K)

Evaluasi ini mengukur kualitas dari daftar 10 rekomendasi teratas (K=10). Item dianggap "relevan" jika rating aktualnya **≥ 7**. \`\`

  * **Hasil dan Interpretasi:**
    Hasil perhitungan metrik evaluasi Top-10 adalah: \`\`

      * **Recall@10: 0.8020**
      * **Precision@10: 0.1444**
      * **F1-Score@10: 0.2448**

    Interpretasi hasil ini adalah sebagai berikut:

      * **Recall@10 yang tinggi (80.2%)** menunjukkan bahwa model sangat efektif dalam menemukan sebagian besar buku yang kemungkinan besar akan sangat disukai oleh pengguna.
      * **Precision@10 sebesar 14.4%** mengindikasikan bahwa dari 10 buku teratas yang direkomendasikan, rata-rata hanya sekitar 1-2 buku yang benar-benar relevan sesuai *threshold* yang ketat (rating ≥ 7).
      * **F1-Score sebesar 0.2448** merefleksikan adanya *trade-off* antara presisi yang rendah dan recall yang tinggi. Model saat ini lebih unggul dalam hal cakupan (*recall*) dibandingkan ketepatan (*precision*). \`\`

Baik, saya akan menyusun bagian **Kesimpulan** dan **Saran Pengembangan** dari laporan Anda, menyesuaikannya dengan detail dari notebook Anda dan mengikuti struktur laporan referensi yang diberikan.

# 📋 Kesimpulan

Proyek pengembangan sistem rekomendasi buku ini telah berhasil mengimplementasikan dan mengevaluasi dua pendekatan utama: *Content-Based Filtering* (CBF) dan *Collaborative Filtering* (CF) berbasis *deep learning*. Evaluasi menunjukkan bahwa kedua model memiliki karakteristik dan potensi yang berbeda dalam menyelesaikan permasalahan *information overload* dan personalisasi rekomendasi bagi pembaca.

* **Model Content-Based Filtering (CBF):**
    * Model CBF menunjukkan **akurasi sempurna (1.00)** dalam tugas evaluasi spesifiknya, yaitu mengklasifikasikan buku berdasarkan kategori 'Fiction'. Hasil ini mengonfirmasi konsistensi logika internal model dalam mencocokkan item berdasarkan kesamaan fitur kategori tunggal. ``
    * **Kelebihan utama CBF** terletak pada transparansinya (rekomendasi mudah dijelaskan), kemampuannya menangani buku baru (*item cold start*), dan kemampuannya melayani pengguna dengan preferensi kategori yang sangat spesifik.
    * Namun, **keterbatasannya** adalah ketergantungan pada kualitas fitur (dalam hal ini, hanya `Category`), serta kurangnya kemampuan untuk menghasilkan rekomendasi yang mengejutkan (*serendipity*) dan potensi terjadinya *filter bubble*.

* **Model Collaborative Filtering (CF) dengan Deep Learning:**
    * Model CF menunjukkan **performa prediksi yang baik**, dengan **RMSE sebesar 0.1938** dan **MAE sebesar 0.1505** pada data validasi. ``
    * Dalam evaluasi kualitas peringkat (dengan *threshold* rating ≥ 7), model ini mencapai **Recall@10 yang sangat tinggi (0.8020)**, yang berarti sangat efektif dalam menemukan sebagian besar buku yang benar-benar disukai pengguna. Namun, **Precision@10 (0.1444)** lebih rendah, menunjukkan adanya *trade-off* antara cakupan dan ketepatan. ``
    * **Kelebihan utama CF** adalah kemampuannya untuk personalisasi yang mendalam berdasarkan perilaku kolektif, potensi untuk *serendipity*, dan tidak bergantung pada metadata item.
    * **Kelemahan utamanya** adalah masalah *cold start* untuk pengguna dan buku baru, serta sensitivitas terhadap kekarangan data (*data sparsity*). ``

### Perbandingan dan Kesesuaian Penggunaan

Tidak ada satu model yang superior secara absolut untuk semua skenario.
* **Model Collaborative Filtering (CF)** menunjukkan potensi yang lebih besar sebagai sistem rekomendasi utama. Tingginya nilai Recall@10 sangat relevan dengan tujuan untuk membantu pembaca **menemukan beragam buku yang mungkin mereka sukai**, termasuk yang belum pernah mereka dengar sebelumnya. Kemampuan personalisasinya yang mendalam juga sejalan dengan tujuan untuk meningkatkan pengalaman membaca.
* **Model Content-Based Filtering (CBF)** tetap berharga untuk kasus penggunaan spesifik, seperti **memberikan rekomendasi yang dapat dijelaskan** ("buku ini direkomendasikan karena Anda menyukai buku fiksi lainnya"), menangani buku baru, atau sebagai sistem *fallback* ketika data interaksi pengguna tidak mencukupi.

### Saran Pengembangan Lanjutan
Berdasarkan hasil proyek ini, beberapa pengembangan dapat dilakukan di masa depan:
* **Untuk Content-Based Filtering**: Menggunakan fitur yang lebih kaya seperti **ringkasan buku (Summary)** dengan teknik NLP yang lebih canggih, atau menggabungkan fitur **penulis dan penerbit** untuk menghasilkan rekomendasi yang lebih beragam.
* **Untuk Collaborative Filtering**: Melakukan eksperimen dengan arsitektur model yang berbeda (misalnya, menambah jumlah layer atau mengubah ukuran *embedding*) untuk mencoba meningkatkan presisi. Selain itu, model dapat dikembangkan lebih lanjut untuk menangani data rating implisit yang sebelumnya difilter.
* **Model Hybrid**: Menggabungkan kekuatan kedua model (*content-based* dan *collaborative*) untuk menciptakan sistem rekomendasi *hybrid* yang dapat memberikan rekomendasi yang akurat dan juga baru (*serendipity*).
* **Skalabilitas**: Melatih model dengan keseluruhan dataset menggunakan sumber daya komputasi yang lebih besar (misalnya, GPU atau platform cloud) untuk melihat apakah performa dapat ditingkatkan.

Secara keseluruhan, proyek ini berhasil mengimplementasikan sistem rekomendasi buku dari awal hingga akhir, memberikan analisis yang mendalam, dan menjadi dasar yang kuat untuk pengembangan lebih lanjut.


# Laporan Proyek Machine Learning - Sistem Rekomendasi Buku
### Oleh Sulthan Muhammad Rafif Ilham

---

# 🌍 **Project Overview**

### **1. Latar Belakang**

Di era digital dengan informasi yang melimpah, pembaca dihadapkan pada jutaan pilihan buku yang tersedia di berbagai platform. Fenomena ini, yang dikenal sebagai *information overload*, seringkali membuat pembaca kesulitan untuk menemukan bacaan baru yang benar-benar sesuai dengan selera unik mereka. Sistem rekomendasi buku hadir sebagai solusi teknologi untuk menjembatani kesenjangan ini. Dengan menganalisis data preferensi pengguna dan karakteristik buku, sistem ini dapat menyajikan saran yang relevan dan dipersonalisasi, membantu pengguna menemukan buku yang mungkin mereka sukai namun belum pernah mereka temukan sebelumnya.

### **2. Mengapa dan Bagaimana Masalah Ini Harus Diselesaikan**

Proyek ini penting karena bertujuan untuk meningkatkan pengalaman membaca dengan mengatasi tantangan penemuan konten. Masalah ini akan diselesaikan dengan membangun model *machine learning* yang cerdas, menggunakan **Book-Crossing Dataset** yang kaya akan data interaksi pengguna dan buku. Pendekatan yang akan dieksplorasi adalah:
* **Content-Based Filtering**: Merekomendasikan buku berdasarkan kemiripan atribut intrinsik buku itu sendiri, seperti kategori.
* **Collaborative Filtering**: Merekomendasikan buku berdasarkan pola perilaku dan preferensi dari pengguna lain yang memiliki selera serupa.

### **3. Referensi**

Dataset yang digunakan dalam proyek ini adalah **Book-Crossing Dataset** yang bersumber dari platform Kaggle. Dataset ini merupakan salah satu dataset publik yang populer dan sering digunakan untuk penelitian dan pengembangan sistem rekomendasi.
* **URL Dataset:** [https://www.kaggle.com/datasets/ruchi798/bookcrossing-dataset](https://www.kaggle.com/datasets/ruchi798/bookcrossing-dataset)

---

# 📈 **Business Understanding**

### **1. Problem Statements (Pernyataan Masalah)**

Berdasarkan latar belakang, masalah utama yang ingin diselesaikan adalah:
* Bagaimana cara membangun model yang dapat merekomendasikan buku yang relevan kepada pengguna berdasarkan kategori buku yang pernah mereka sukai? (Content-Based)
* Bagaimana cara membangun model yang dapat memprediksi preferensi seorang pengguna terhadap buku yang belum pernah ia baca, berdasarkan pola rating dari pengguna lain yang seleranya mirip? (Collaborative Filtering)
* Bagaimana cara mengevaluasi dan membandingkan efektivitas dari kedua pendekatan tersebut dalam memberikan rekomendasi yang berkualitas?

### **2. Goals (Tujuan)**

Tujuan dari proyek ini adalah:
* Melakukan analisis data eksplorasi (EDA) untuk memahami karakteristik dataset Book-Crossing.
* Melakukan persiapan data yang komprehensif, termasuk pembersihan, penanganan data anomali, dan rekayasa fitur.
* Mengembangkan model **Content-Based Filtering** yang fungsional berdasarkan kategori buku.
* Mengembangkan model **Collaborative Filtering** berbasis *deep learning* (matrix factorization) untuk memprediksi rating.
* Mengevaluasi kedua model menggunakan metrik yang relevan untuk mengukur akurasi dan kualitas rekomendasinya.

### **3. Solution Approach (Pendekatan Solusi)**

Solusi yang diusulkan adalah dengan merancang, melatih, dan mengevaluasi dua jenis model rekomendasi:
1.  **Pendekatan Content-Based Filtering**: Solusi ini akan diimplementasikan dengan mengubah fitur kategori buku menjadi representasi vektor numerik menggunakan **TF-IDF**. Selanjutnya, kemiripan antar buku dihitung menggunakan metrik **Cosine Similarity** untuk menemukan buku-buku yang paling mirip.
2.  **Pendekatan Collaborative Filtering**: Solusi ini akan menggunakan arsitektur *deep learning* dengan **embedding layer** untuk pengguna dan buku. Model ini akan dilatih pada data rating eksplisit untuk mempelajari preferensi laten pengguna dan karakteristik buku, yang kemudian digunakan untuk memprediksi rating dan menghasilkan rekomendasi.

---

# 🧠 **Data Understanding**

### **Dataset Overview**
Dataset yang digunakan adalah **Book-Crossing Dataset**. Versi yang dimuat adalah `Preprocessed_data.csv`, yang merupakan gabungan dari data rating, pengguna, dan buku. Dataset awal sebelum difilter memiliki skala yang sangat besar:
* Jumlah Data Rating: 1.031.175
* Jumlah User Unik: 92.107
* Jumlah Buku Unik (ISBN): 270.170

### **Feature Description**
Berikut adalah deskripsi dari fitur-fitur utama yang digunakan setelah dataset dibersihkan dan difilter:

| Nama Fitur | Deskripsi | Tipe Data |
| :--- | :--- | :--- |
| **user\_id** | ID unik untuk setiap pengguna. | `int64` |
| **isbn** | ID unik standar internasional untuk setiap buku. | `object` (string) |
| **rating** | Skor penilaian eksplisit yang diberikan pengguna (skala 1-10). | `int64` |
| **book\_title**| Judul dari buku. | `object` (string) |
| **Category** | Kategori atau genre dari buku. | `object` (string) |
| **age** | Usia dari pengguna. | `float64` |
| **location** | Lokasi dari pengguna (kota, provinsi, negara). | `object` (string) |
| **book\_author**| Nama penulis buku. | `object` (string) |
| **publisher** | Nama penerbit buku. | `object` (string) |

### **Data Exploration Findings**

#### **User Data Analysis**
* **Geografis**: Pengguna dalam dataset ini sangat tersebar secara internasional, berasal dari 18.350 lokasi berbeda. Tidak ada wilayah yang mendominasi secara signifikan, meskipun **Toronto, Kanada** menjadi lokasi dengan rating terbanyak (1.3%).
* **Usia**: Distribusi usia pengguna menunjukkan puncak frekuensi yang sangat tinggi di sekitar **34.7 tahun**, yang kemungkinan besar adalah hasil dari imputasi nilai kosong pada data asli. Di luar itu, mayoritas pengguna berada pada rentang usia dewasa muda hingga paruh baya.

#### **Book Data Analysis**
* **Rating**: Distribusi rating didominasi oleh nilai **0**, yang menandakan rating implisit. Untuk rating eksplisit (1-10), distribusinya sangat miring ke kiri, dengan puncak frekuensi pada rating **8**, menunjukkan pengguna cenderung memberikan ulasan positif.
* **Penulis dan Penerbit**: **Stephen King** adalah penulis yang paling banyak diulas, dan **Ballantine Books** adalah penerbit yang paling dominan. Ini menunjukkan fokus dataset pada buku-buku fiksi populer dan pasar massal.
* **Bahasa dan Kategori**: Sebagian besar buku berbahasa Inggris (`en`) dengan kategori dominan adalah Fiksi (`Fiction`). Ditemukan pula data anomali pada kedua kolom ini dengan nilai '9' yang muncul dengan frekuensi tinggi.
* **Tahun Publikasi**: Dataset didominasi oleh buku-buku modern, dengan puncak publikasi terjadi pada akhir 1990-an hingga awal 2000-an.

### **Matrix Density**
Setelah pembersihan dan pengurangan data, dataset yang digunakan untuk pemodelan memiliki:
* Pengguna Unik: 71.675
* Buku Unik: 58.949
* Rating: 617.642

Kepadatan matriks interaksi dapat dihitung sebagai:
$$\text{Density} = \frac{\text{Jumlah Rating}}{\text{Jumlah User} \times \text{Jumlah Buku}} = \frac{617.642}{71.675 \times 58.949} \approx 0.0146\%$$
Nilai kepadatan yang sangat rendah ini mengonfirmasi bahwa dataset bersifat sangat *sparse*.

### 🚩 **Permasalahan dan Insight Data**
Dari EDA, beberapa permasalahan dan insight utama teridentifikasi:
1.  **Skala Data**: Dataset terlalu besar untuk diproses dengan sumber daya komputasi standar, sehingga perlu dilakukan sampling.
2.  **Rating Implisit**: Dominasi rating 0 perlu ditangani karena dapat mengganggu model yang berfokus pada rating eksplisit.
3.  **Kualitas Data**: Terdapat data anomali (nilai '9') dan format yang tidak konsisten (contoh: `['Fiction']`) pada kolom `Category` dan `Language` yang memerlukan pembersihan.

# ⚙️ Data Preparation
Setelah memahami karakteristik dan permasalahan dalam dataset, tahap selanjutnya adalah persiapan data. Proses ini krusial untuk memastikan data yang digunakan untuk melatih model berkualitas tinggi, konsisten, dan bebas dari *noise*.

### **1. Standardisasi Format Kategori dan Pembersihan Data**
Berdasarkan temuan di tahap EDA, beberapa langkah pembersihan dilakukan:
* **Menghapus Data Anomali**: Semua baris data yang memiliki nilai '9' pada kolom `Category` dihapus karena dianggap sebagai data yang tidak valid.
* **Menghapus Rating Implisit**: Rating bernilai 0 dianggap sebagai interaksi implisit (bukan penilaian eksplisit) dan dihapus dari dataset untuk memfokuskan model pada preferensi yang jelas.
* **Membersihkan Format Kategori**: Format kategori yang tidak seragam (contoh: `"['Fiction']"`) dibersihkan dengan menghapus semua karakter non-alfanumerik seperti tanda kurung dan kutip. Spasi juga diganti dengan *underscore* (`_`) untuk menciptakan nama kategori yang utuh (contoh: `Social_Science`).

### **2. Seleksi Fitur**
Dari 19 kolom yang tersedia, hanya 5 kolom yang relevan untuk tujuan pemodelan yang dipilih:
* `user_id`
* `isbn`
* `rating`
* `book_title`
* `Category`

Langkah ini menghasilkan DataFrame yang lebih ringkas dan fokus pada fitur-fitur yang akan digunakan untuk membangun kedua model rekomendasi.

### **3. Mengatasi Missing Values dan Duplikasi Data**
Dilakukan verifikasi akhir untuk memastikan kualitas data:
* **Missing Values**: Pengecekan dengan `.isnull().sum()` mengonfirmasi bahwa DataFrame akhir yang telah dibersihkan tidak lagi memiliki nilai yang hilang.
* **Duplikasi Data**: Pengecekan dengan `.duplicated().sum()` juga menunjukkan hasil 0, yang memastikan bahwa setiap baris dalam dataset adalah entri yang unik.

### **4. Penyiapan Data Final untuk Analisis**
DataFrame yang telah sepenuhnya bersih kemudian disimpan dalam variabel `preparation` dan diurutkan berdasarkan `isbn` untuk memberikan struktur yang rapi. Dataset akhir ini berisi **149.289** entri rating yang valid dan siap untuk tahap rekayasa fitur dan pemodelan.

### **5. Persiapan Data untuk Model Content-Based Filtering**

#### **1. Persiapan Data Buku Unik**
Untuk model *Content-Based Filtering*, data duplikat berdasarkan `isbn` dihapus, karena model ini hanya memerlukan metadata unik dari setiap buku, bukan semua data ratingnya. Langkah ini menghasilkan DataFrame baru berisi **25.183** data buku unik yang siap diolah lebih lanjut.

#### **2. Ekstraksi Informasi Buku**
Fitur-fitur relevan (`isbn`, `book_title`, `category`) diekstrak dari DataFrame buku unik dan diubah menjadi *list* Python. Dari *list* ini, sebuah DataFrame baru bernama `book_data` dibuat dengan struktur yang lebih sederhana untuk memfokuskan proses pada metadata yang akan divektorisasi.

#### **3. Vektorisasi Fitur Kategori dengan TF-IDF**
Untuk memungkinkan model memahami karakteristik buku, fitur `category` yang berbasis teks diubah menjadi representasi vektor numerik menggunakan teknik **TF-IDF** (*Term Frequency-Inverse Document Frequency*). Proses ini menghasilkan sebuah matriks fitur berukuran **(25183, 1727)**, di mana setiap baris mewakili satu buku dan setiap kolom mewakili satu kategori unik yang telah dipelajari dari dataset.

### **6. Persiapan Data untuk Model Collaborative Filtering**

#### **1. Encoding Fitur**
Model *deep learning* memerlukan input numerik. Oleh karena itu, dilakukan proses *encoding* untuk mengubah `user_id` dan `isbn` menjadi indeks integer yang berurutan (dimulai dari 0). Proses ini menghasilkan dua kolom baru (`user_encoded` dan `book_encoded`) yang akan menjadi input bagi *embedding layer* pada model.

#### **2. Pembagian Data Latih dan Validasi (Train-Validation Split) dan Normalisasi Rating**
* **Pengacakan Data**: Dataset diacak secara menyeluruh untuk menghilangkan bias urutan dan memastikan distribusi data yang representatif pada set latih dan validasi.
* **Normalisasi Rating**: Nilai `rating` (skala 1-10) dinormalisasi ke rentang [0, 1] menggunakan *min-max scaling*.
* **Pembagian Data**: Dataset kemudian dibagi dengan rasio **80:20**, menghasilkan **119.431** data untuk pelatihan dan **29.858** data untuk validasi.

---
# 🧮 Modeling
Setelah data dipersiapkan, tahap selanjutnya adalah pengembangan model. Proyek ini mengimplementasikan dua pendekatan solusi: **Content-Based Filtering** dan **Collaborative Filtering**.

---
## **Solusi 1: Content-Based Filtering (CBF)**
Pendekatan ini merekomendasikan buku berdasarkan kemiripan konten atau atributnya. Dalam proyek ini, fitur yang digunakan adalah **`Category`** buku.

### **1. Perhitungan Kemiripan Antar Buku dengan Cosine Similarity**
Inti dari model ini adalah menghitung tingkat kemiripan antar buku. Fungsi `cosine_similarity` diterapkan pada matriks TF-IDF yang telah dibuat pada tahap persiapan data. Langkah ini menghasilkan sebuah matriks simetris berukuran **25.183 x 25.183**, yang memuat skor kemiripan antara semua pasangan buku. Nilai pada matriks ini berkisar dari 0 hingga 1, di mana skor 1 menandakan kemiripan yang identik.

Untuk mempermudah interpretasi, matriks ini diubah menjadi DataFrame pandas dengan judul buku sebagai indeks dan kolomnya. Sampel acak dari DataFrame ini menunjukkan pola yang jelas: buku-buku dengan kategori yang sama memiliki skor *similarity* 1.0, sedangkan yang berbeda kategori memiliki skor 0.0.

### **2. Implementasi Fungsi Rekomendasi Buku**
Sebuah fungsi `book_recommendations` dirancang untuk memberikan rekomendasi berdasarkan matriks kemiripan yang telah dihitung. Fungsi ini bekerja dengan cara:
1.  Mencari buku-buku dengan skor *similarity* tertinggi terhadap buku input.
2.  Mengambil 5 rekomendasi teratas.
3.  Menghapus buku input dari daftar rekomendasi.
4.  Menampilkan hasil rekomendasi beserta kategorinya.

Saat diuji dengan buku **"Wild Animus"** (kategori: Fiction), fungsi ini berhasil merekomendasikan buku-buku lain yang mayoritas juga berkategori Fiction.

### **3. Kelebihan dan Kekurangan Content-Based Filtering**

**Kelebihan:**
* **Transparan dan Mudah Diinterpretasikan**: Rekomendasi yang diberikan mudah dijelaskan karena didasarkan pada fitur yang jelas (kategori).
* **Tidak Memerlukan Data Pengguna Lain**: Model ini dapat memberikan rekomendasi kepada pengguna baru atau untuk buku yang belum memiliki rating, selama metadata buku tersedia.
* **Tidak Ada Masalah *Cold Start***: Selama buku memiliki atribut kategori, model dapat langsung menemukan kemiripannya dengan buku lain.

**Kekurangan:**
* **Terlalu Spesifik (*Overspecialization*)**: Karena hanya menggunakan fitur kategori, model ini cenderung merekomendasikan item yang sangat mirip dan kurang mampu memberikan rekomendasi yang bersifat kejutan (*serendipity*).
* **Ketergantungan pada Kualitas Fitur**: Kualitas rekomendasi sangat bergantung pada kelengkapan dan akurasi fitur kategori. Fitur yang kurang deskriptif akan menghasilkan rekomendasi yang kurang relevan.

---
## **Solusi 2: Collaborative Filtering (CF) dengan Embedding Deep Learning**
Pendekatan ini merekomendasikan buku berdasarkan pola rating dari pengguna-pengguna yang memiliki selera serupa.

### **1. Membangun Model Deep Learning untuk Collaborative Filtering**
Model ini dibangun menggunakan kelas `RecommenderNet` yang merupakan turunan dari `tf.keras.Model`. Arsitektur ini secara efektif mengimplementasikan konsep *matrix factorization* melalui pendekatan *deep learning*.

Komponen utamanya adalah:
* **Embedding Layer**: Lapisan ini memetakan setiap ID pengguna dan ID buku ke dalam vektor berdimensi rendah (vektor *embedding*) yang menangkap preferensi laten pengguna dan karakteristik buku.
* **Dot Product**: Interaksi antara pengguna dan buku dihitung melalui *dot product* dari kedua vektor embedding mereka.
* **Bias Layer**: Lapisan bias ditambahkan untuk menangkap kecenderungan rating umum dari setiap pengguna dan buku.
* **Fungsi Aktivasi Sigmoid**: Menghasilkan output prediksi rating dalam rentang [0, 1] yang sesuai dengan data rating yang telah dinormalisasi.

### **2. Kompilasi dan Pelatihan Model**
Model dikompilasi dengan *loss function* **Mean Squared Error (MSE)** dan *optimizer* **Adam**. Metrik utama yang dipantau selama pelatihan adalah **Root Mean Squared Error (RMSE)**. Dua *callback* penting, `EarlyStopping` dan `ReduceLROnPlateau`, digunakan untuk mengoptimalkan proses pelatihan dan mencegah *overfitting*.

Proses pelatihan dijalankan selama maksimal 100 *epoch* dengan `batch_size` 125. Namun, berkat `EarlyStopping`, pelatihan berhenti secara otomatis pada **epoch 45** setelah performa pada data validasi tidak membaik, dan model menggunakan bobot terbaik dari **epoch 35**.

### **3. Inferensi dan Contoh Penggunaan untuk Top-N Rekomendasi**
Setelah dilatih, model digunakan untuk menghasilkan rekomendasi untuk **User ID 8**. Hasilnya menunjukkan dua bagian:
* **Buku yang Pernah Diulas**: Sebagai konteks, ditampilkan buku yang pernah diberi rating tinggi oleh pengguna, yaitu **"Clara Callan"**.
* **10 Rekomendasi Teratas**: Model berhasil merekomendasikan 10 buku baru yang beragam, mencakup genre populer seperti Fantasy ("The Return of the King"), Humor ("Calvin and Hobbes"), dan Fiction. Ini menunjukkan kemampuan model dalam menyarankan buku di luar kategori yang pernah diulas pengguna.

### **4. Ringkasan Hyperparameter Model Collaborative Filtering**

#### **1. Hyperparameter Terkait Embedding**
| Hyperparameter | Nilai | Deskripsi |
| :--- | :--- | :--- |
| `embedding_size` | 8 | Dimensi dari vektor embedding untuk pengguna dan buku. |
| `embeddings_initializer`| 'he_normal'| Metode inisialisasi bobot untuk layer embedding. |
| `embeddings_regularizer`| L2 (1e-4) | Teknik regularisasi untuk mencegah overfitting pada bobot embedding. |

#### **2. Hyperparameter Pelatihan Model**
| Hyperparameter | Nilai | Deskripsi |
| :--- | :--- | :--- |
| `loss` | Mean Squared Error | Fungsi kerugian yang digunakan untuk mengukur kesalahan prediksi. |
| `optimizer` | Adam | Algoritma optimisasi yang digunakan untuk memperbarui bobot model. |
| `metrics` | Root Mean Squared Error | Metrik yang dipantau selama pelatihan. |
| `batch_size`| 125 | Jumlah sampel yang diproses dalam satu iterasi. |
| `epochs` | 100 | Jumlah maksimum iterasi pelatihan. |

#### **3. Hyperparameter *Callback* `EarlyStopping`**
| Parameter | Nilai | Deskripsi |
| :--- | :--- | :--- |
| `monitor` | 'val_loss' | Metrik yang dipantau untuk menghentikan pelatihan. |
| `patience`| 10 | Jumlah epoch tanpa perbaikan sebelum pelatihan dihentikan. |

#### **4. Hyperparameter *Callback* `ReduceLROnPlateau`**
| Parameter | Nilai | Deskripsi |
| :--- | :--- | :--- |
| `monitor` | 'val_loss' | Metrik yang dipantau untuk mengurangi *learning rate*. |
| `patience`| 5 | Jumlah epoch tanpa perbaikan sebelum *learning rate* dikurangi. |
| `factor` | 0.1 | Faktor pengurangan *learning rate* (new_lr = lr * 0.1). |


### **5. Kelebihan dan Kekurangan Collaborative Filtering (dengan Deep Learning)**

**Kelebihan:**
* **Personalisasi Mendalam**: Mampu menangkap pola preferensi yang kompleks dan non-linear antar pengguna dan item, menghasilkan rekomendasi yang sangat personal.
* **Kemampuan *Serendipity***: Dapat merekomendasikan item yang tidak terduga namun relevan karena tidak bergantung pada fitur konten, melainkan pada selera komunitas.
* **Tidak Memerlukan Fitur Item**: Model ini hanya membutuhkan data interaksi (rating), sehingga tidak bergantung pada kelengkapan metadata item.

**Kekurangan:**
* **Masalah *Cold Start***: Kesulitan memberikan rekomendasi untuk pengguna baru (yang belum punya riwayat rating) atau untuk buku baru (yang belum pernah diberi rating).
* **Membutuhkan Data Besar**: Efektivitas model sangat bergantung pada ketersediaan data interaksi yang besar dan cukup padat.
* **Kurang Dapat Diinterpretasikan**: Sifat *black box* dari model *deep learning* membuat alasan di balik sebuah rekomendasi menjadi sulit untuk dijelaskan.

---
# 💯 Evaluation

Tahap evaluasi bertujuan untuk mengukur performa dari kedua model yang telah dikembangkan secara kuantitatif. Metrik yang berbeda digunakan untuk setiap model, disesuaikan dengan tujuan dan cara kerja masing-masing.

### **Metrik Evaluasi yang Digunakan**
* **Evaluasi Content-Based Filtering**:
    * **Classification Report**: Untuk mengevaluasi model CBF pada tugas klasifikasi, digunakan metrik `Precision`, `Recall`, `F1-Score`, dan `Accuracy`. Metrik ini mengukur seberapa akurat model dalam mengidentifikasi buku dengan kategori yang benar. ``
* **Evaluasi Collaborative Filtering**:
    * **RMSE (Root Mean Squared Error) & MAE (Mean Absolute Error)**: Metrik ini digunakan untuk mengukur akurasi prediksi rating. Keduanya menghitung rata-rata kesalahan antara rating yang diprediksi model dengan rating aktual. ``
    * **Precision@K, Recall@K, & F1-Score@K**: Metrik ini digunakan untuk mengukur kualitas dari daftar peringkat rekomendasi. Metrik ini menilai seberapa relevan item-item yang disajikan di posisi teratas. ``

### **Evaluasi Model Content-Based Filtering (CBF)**
Evaluasi dilakukan dengan mengukur kemampuan model dalam mengenali buku dengan kategori **'Fiction'**. Label *ground truth* dibuat dengan memberi nilai 1 untuk kategori 'Fiction' dan 0 untuk lainnya. Hasil prediksi kemudian dibandingkan dengan *ground truth* menggunakan `classification_report`. ``

**Hasil:**
```
              precision    recall  f1-score   support

           0       1.00      1.00      1.00     11582
           1       1.00      1.00      1.00     13601

    accuracy                           1.00     25183
   macro avg       1.00      1.00      1.00     25183
weighted avg       1.00      1.00      1.00     25183
```
**Interpretasi:**
Model mencapai nilai **1.00 (100%)** untuk semua metrik. Performa yang sempurna ini wajar terjadi karena model *content-based* yang dibangun hanya menggunakan satu fitur, yaitu `category`. Dengan demikian, buku yang paling mirip dengan sebuah buku fiksi hampir pasti adalah buku fiksi lainnya, sehingga model dapat mengklasifikasikannya dengan sangat akurat. ``

### **Evaluasi Model Collaborative Filtering (CF)**

#### **1. Evaluasi Performa Selama Pelatihan (RMSE Plot)**
Grafik metrik pelatihan menunjukkan bahwa kurva RMSE data latih (biru) terus menurun secara konsisten, menandakan model belajar dengan efektif. Namun, kurva RMSE data validasi (oranye) mulai stagnan dan sedikit meningkat setelah beberapa epoch. Kesenjangan yang melebar antara kedua kurva ini merupakan indikasi terjadinya **overfitting**. Fenomena ini memvalidasi pentingnya penggunaan *callback* `EarlyStopping` yang telah menghentikan pelatihan pada waktu yang tepat. ``

#### **2. Perhitungan RMSE dan MAE pada Data Validasi**
Evaluasi kuantitatif pada data validasi menghasilkan nilai berikut:
* **RMSE: 0.1938** ``
* **MAE : 0.1505** ``

Nilai-nilai ini, pada skala rating yang telah dinormalisasi [0, 1], menunjukkan tingkat kesalahan prediksi yang rendah. Nilai **MAE sebesar 0.1505** berarti secara rata-rata, prediksi rating memiliki selisih sekitar 0.15 dari rating aktual. ``

#### **3. Evaluasi Kualitas Rekomendasi Top-N (Precision@K, Recall@K, F1-Score@K)**
Evaluasi ini dilakukan dengan *threshold* relevansi yang lebih ketat, di mana buku dianggap relevan jika rating aslinya **≥ 7**. ``

**Hasil:**
* **F1-Score@10: 0.2448** ``
* **Precision@10: 0.1444** ``
* **Recall@10: 0.8020** ``

**Interpretasi:**
* Nilai **Recall@10 sebesar 80.2%** menunjukkan bahwa model masih sangat mampu menemukan sebagian besar buku yang sangat disukai pengguna. ``
* Nilai **Precision@10 sebesar 14.4%** mengindikasikan bahwa dari 10 buku yang direkomendasikan, rata-rata hanya sekitar 1-2 buku yang memenuhi kriteria rating tinggi. ``
* **F1-Score sebesar 0.2448** merefleksikan adanya *trade-off* antara presisi yang rendah dan recall yang tinggi, yang merupakan konsekuensi dari penggunaan *threshold* relevansi yang lebih ketat. ``

---

# 📋 Kesimpulan

Proyek ini telah berhasil membangun dan mengevaluasi dua jenis sistem rekomendasi buku—*Content-Based Filtering* dan *Collaborative Filtering*—menggunakan Book-Crossing Dataset. `` Melalui serangkaian tahapan yang terstruktur, proyek ini menunjukkan implementasi praktis dari teknik-teknik sistem rekomendasi. ``

Analisis data eksplorasi (EDA) mengungkapkan bahwa dataset ini sangat besar, bersifat *sparse*, dan memiliki beberapa isu kualitas data seperti rating implisit dan format kategori yang tidak konsisten. `` Tahap persiapan data berhasil mengatasi tantangan-tantangan ini melalui sampling, pembersihan, dan rekayasa fitur, menghasilkan dataset akhir yang bersih dan siap untuk pemodelan. ``

Kedua model yang dikembangkan menunjukkan performa yang sesuai dengan karakteristiknya masing-masing:
* **Model Content-Based Filtering**, yang berbasis fitur `Category`, menunjukkan performa klasifikasi yang sempurna. `` Hal ini wajar karena kesederhanaan fiturnya, namun juga menyoroti keterbatasannya dalam memberikan rekomendasi yang beragam. ``
* **Model Collaborative Filtering**, yang menggunakan arsitektur *deep learning*, menunjukkan performa yang kuat. Model ini berhasil mencapai **RMSE yang rendah (0.1938)**, menandakan akurasi prediksi rating yang baik. `` Dalam evaluasi peringkat, model ini unggul dalam hal **Recall (0.8020)**, yang berarti sangat efektif dalam menemukan hampir semua buku yang berpotensi disukai pengguna. `` Namun, **Precision-nya lebih rendah (0.1444)**, yang menunjukkan adanya ruang untuk perbaikan dalam hal ketepatan rekomendasi di posisi teratas. ``

Secara keseluruhan, proyek ini berhasil mengimplementasikan sistem rekomendasi buku dari awal hingga akhir, memberikan analisis yang mendalam, dan menjadi dasar yang kuat untuk pengembangan lebih lanjut. Model *collaborative filtering* menunjukkan potensi terbesar sebagai sistem rekomendasi utama karena kemampuannya dalam personalisasi dan menemukan preferensi laten pengguna.

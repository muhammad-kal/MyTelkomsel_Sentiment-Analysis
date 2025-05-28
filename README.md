#  Analisis Sentimen Ulasan Aplikasi MyTelkomsel 📊🤖

Proyek ini bertujuan untuk melakukan analisis sentimen terhadap ulasan pengguna aplikasi **MyTelkomsel** dari Google Play Store. Seluruh proses dilakukan menggunakan Python dalam satu notebook utama, yang mencakup beberapa tahap: scraping data ulasa, pra-pemrosesan teks, pelabelan sentimen, pelatihan model machine learning, dan inferensi untuk prediksi sentimen pada data baru.

---

## 📁 Struktur Direktori Proyek

-   `Projek_Sentimen_Analisis.ipynb`
    Notebook utama yang berisi semua langkah proyek: kode untuk scraping data serta pemuatan data hasil scraping, pra-pemrosesan data teks, pelabelan sentimen, ekstraksi fitur, pelatihan model machine learning, evaluasi model, dan inferensi sederhana.
-   `ulasan_aplikasi_telkomsel.csv`
    Dataset mentah berisi ulasan pengguna aplikasi MyTelkomsel yang telah di-scrap.
-   `README.md`

---

## ⚙️ Tools & Library Utama

- `google-play-scraper` – untuk scraping ulasan aplikasi.
- `pandas`, `nltk`, `scikit-learn` – untuk preprocessing teks dan machine learning.
- `tensorflow` – digunakan dalam model.
- `pickle` – menyimpan dan memuat model serta vektorisasi.


---

## 🔍 Proses Analisis

### 1. Pengumpulan Data (Data Scraping)
Menggunakan library `google-play-scraper`, dilakukan pengambilan data ulasan pengguna untuk aplikasi **MyTelkomsel** dari platform Google Play Store. Targetnya adalah mengumpulkan minimal 3.000 ulasan (proyek ini berhasil mengumpulkan lebih dari 16.000 ulasan). Ulasan yang terkumpul disimpan dalam format `.csv` yaitu `ulasan_aplikasi_telkomsel.csv`. Kode untuk scraping ini bisa jadi merupakan bagian dari notebook utama atau dijalankan terpisah sebelumnya untuk menghasilkan file CSV.

### 2. Pra-pemrosesan Teks & Pelabelan Sentimen
Tahap ini krusial untuk menyiapkan data teks agar dapat diolah oleh model machine learning.
-   **Pembersihan Teks**: Menghilangkan karakter yang tidak relevan seperti URL, mention, hashtag, angka, dan tanda baca berlebih. Teks juga diubah menjadi huruf kecil (*case folding*).
-   **Normalisasi Kata**: Menggunakan kamus slang sederhana untuk mengubah kata-kata tidak baku menjadi bentuk bakunya.
-   **Tokenisasi**: Memecah kalimat menjadi token atau kata-kata individual.
-   **Stopword Removal**: Menghapus kata-kata umum yang tidak memiliki makna sentimen signifikan (misalnya, "yang", "di", "dan") menggunakan daftar stopword Bahasa Indonesia dari NLTK.
-   **Pelabelan Sentimen**: Pelabelan dilakukan berdasarkan skor (rating bintang) yang diberikan pengguna:
    -   `positive`: skor 4–5
    -   `negative`: skor 1–2
    -   `neutral`: skor 3
    Proyek ini menggunakan ketiga kelas sentimen tersebut.

### 3. Ekstraksi Fitur & Pelatihan Model
-   **Ekstraksi Fitur**: Teks yang sudah bersih diubah menjadi representasi numerik menggunakan **TF-IDF (Term Frequency-Inverse Document Frequency)**. Ini membantu model memahami pentingnya kata dalam konteks ulasan.
-   **Pembagian Data**: Dataset dibagi menjadi data latih (80%) dan data uji (20%) menggunakan `train_test_split` dengan stratifikasi untuk menjaga proporsi kelas.
-   **Pelatihan Model**: Model klasifikasi dilatih menggunakan algoritma **Logistic Regression**.
-   **Evaluasi Model**: Kinerja model dievaluasi pada data uji menggunakan metrik seperti akurasi, presisi, recall, F1-score, dan *confusion matrix*. Target akurasi minimal adalah 85%.

Model machine learning yang telah dilatih dan objek TF-IDF Vectorizer kemudian disimpan (misalnya, menggunakan `joblib` atau `pickle`) untuk digunakan kembali pada tahap inferensi.

### 4. Inferensi Sentimen
Sebuah fungsi atau bagian kode disiapkan untuk melakukan prediksi sentimen pada teks ulasan baru yang belum pernah dilihat sebelumnya. Proses inferensi melibatkan:
1.  Menerima input teks baru.
2.  Melakukan pra-pemrosesan teks yang sama seperti pada data latih.
3.  Mengubah teks yang sudah diproses menjadi vektor TF-IDF menggunakan objek vectorizer yang sudah di-fit sebelumnya.
4.  Melakukan prediksi sentimen menggunakan model yang sudah dilatih.
5.  Menampilkan hasil prediksi sentimen (positif, negatif, atau netral).



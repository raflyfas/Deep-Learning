# UTS 2 Deep Learning - Year Prediction

## Data Diri

| Kategori | Detail |
| :--- | :--- |
| **Nama** | **Rafly Fasha Purnomo Putra** |
| **Kelas** | **TK-46-GAB** |
| **NIM** | **1103223050** |

## 1. Tujuan Repositori
Repositori ini berisi kode dan implementasi untuk proyek regresi Deep Learning. Tujuan utamanya adalah untuk:

* **Memprediksi Tahun (Target Regresi):** Mengembangkan model *Deep Neural Network* (DNN) untuk memprediksi nilai target berupa **Tahun** berdasarkan 90 fitur input yang tersedia dalam dataset.
* **Menerapkan Alur Kerja Deep Learning:** Menerapkan langkah-langkah lengkap dalam proyek *Deep Learning*, mulai dari pembersihan data, pra-pemrosesan, pembagian data, hingga pelatihan dan evaluasi model menggunakan **PyTorch**.

## 2. Gambaran Singkat Projek dan Model Deep Learning

### Gambaran Projek
Projek ini berfokus pada tugas **regresi** di mana variabel target adalah tahun kontinu (mulai dari 1922 hingga 2010). Dataset yang digunakan memiliki 90 fitur dan sekitar 107.000 lebih sampel setelah pembersihan data awal.

Langkah-langkah yang dilakukan meliputi:
1.  **Pembersihan Data:** Menghapus baris yang berisi nilai kosong sepenuhnya dan duplikat.
2.  **Pra-pemrosesan:** Melakukan imputasi nilai yang hilang (jika ada) dan Standardisasi fitur menggunakan `StandardScaler`.
3.  **Pelatihan Model:** Melatih model DNN dengan fungsi *loss* MSE dan dioptimalkan dengan Adam.
4.  **Evaluasi:** Menilai kinerja model pada data uji (test set) menggunakan metrik regresi.

### Model Deep Learning yang Dipakai
Model yang digunakan adalah **Deep Neural Network (DNN)** atau sering juga disebut *Multi-Layer Perceptron* (MLP).

#### Alasan Penggunaan Model:
Model DNN/MLP dipilih karena:
* **Sifat Regresi Kompleks:** Regresi tahun berdasarkan 90 fitur yang ada kemungkinan memiliki hubungan yang sangat non-linear dan kompleks. DNN unggul dalam menangkap pola dan interaksi yang kompleks dalam data berdimensi tinggi.
* **Kecepatan dan Skalabilitas:** Untuk dataset dengan jumlah sampel yang besar (~100K baris) dan banyak fitur, DNN yang diimplementasikan dengan PyTorch menawarkan efisiensi dalam pelatihan, terutama jika memanfaatkan akselerasi GPU.

## 3. Deskripsi Model dan Hasil Metrik

### Deskripsi Arsitektur Model
Model ini diimplementasikan menggunakan PyTorch (`torch.nn.Module`) dengan arsitektur *feedforward* sederhana:

| Lapisan | Jenis | Ukuran Input | Ukuran Output | Fungsi Aktivasi | Keterangan |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Input** | Linear | 90 | 128 | ReLU | Menerima 90 fitur input. |
| **Hidden 1** | Linear | 128 | 64 | ReLU | Lapisan tersembunyi pertama. |
| **Output** | Linear | 64 | 1 | None | Menghasilkan nilai regresi tunggal (Tahun). |

* **Fungsi *Loss* (Kerugian):** Mean Squared Error (MSE) (`nn.MSELoss`).
* **Optimizer:** Adam (`optim.Adam`) dengan *initial learning rate* 0.001.
* **Teknik Tambahan:** Digunakan *Early Stopping* untuk mencegah *overfitting*. Pelatihan dihentikan pada **Epoch 60** karena tidak ada peningkatan pada *validation loss*.

### Hasil Metrik (Matrix Results)
Evaluasi akhir model dilakukan pada **Test Set** (data uji) dan menghasilkan metrik berikut:

| Metrik | Nilai | Keterangan |
| :--- | :--- | :--- |
| **Mean Squared Error (MSE)** | 73.3174 | Rata-rata kuadrat dari error. |
| **Root Mean Squared Error (RMSE)** | 8.5626 | Akar kuadrat dari MSE. Menggambarkan deviasi prediksi dalam satuan Tahun. |
| **Mean Absolute Error (MAE)** | 5.8819 | Rata-rata nilai absolut dari error. Mengindikasikan bahwa rata-rata kesalahan prediksi adalah sekitar 5.88 tahun. |
| **R-squared (R²)** | 0.3841 | Proporsi varians dalam variabel dependen yang dapat diprediksi dari variabel independen. Nilai 0.3841 menunjukkan model menangkap 38.41% variabilitas target. |

## 4. Pustaka (Library) yang Diperlukan

Untuk menjalankan kode di repositori ini, Anda perlu menginstal pustaka-pustaka Python berikut:

```bash
pip install numpy pandas matplotlib scikit-learn torch
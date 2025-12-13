# UTS 1 Deep Learning - Transaction Fraud Detection

## Data Diri

| Kategori | Detail |
| :--- | :--- |
| **Nama** | **Rafly Fasha Purnomo Putra** |
| **Kelas** | **TK-46-03** |
| **NIM** | **1103223050** |

## 1. Tujuan Repositori

Repositori ini dibuat untuk menyimpan semua aset dan kode yang terkait dengan Proyek Ujian Tengah Semester (Midterm) **Transaction Fraud Detection**.

Tujuan utama proyek ini adalah untuk:
1.  Menganalisis dan memahami karakteristik data transaksi yang diberikan.
2.  Membangun, melatih, dan mengevaluasi model *Neural Network* yang mampu mengklasifikasikan transaksi sebagai **penipuan (fraud)** atau **bukan penipuan (non-fraud)**.
3.  Menghasilkan prediksi pada set data uji (`test_transaction.csv`) untuk mengidentifikasi potensi penipuan.

## 2. Gambaran Singkat Proyek

* **Pemuatan Data:** Memuat data transaksi train (`train_transaction.csv`) dan test (`test_transaction.csv`).
* **Eksplorasi Data (EDA):** Analisis statistik, visualisasi distribusi, dan penanganan missing values.
* **Preprocessing Data:** Penanganan data kategorikal, normalisasi/standarisasi data numerik, dan rekayasa fitur (feature engineering) tambahan.
* **Pelatihan Model:** Menguji beberapa algoritma klasifikasi.
* **Evaluasi:** Menilai kinerja model menggunakan metrik klasifikasi yang sesuai.

### 3. Evaluasi Model

Model utama yang digunakan dalam proyek ini adalah **Deep Neural Network (DNN)** yang dilatih menggunakan data yang telah di-*oversampling* dengan SMOTE dan diskalakan (StandardScaler).

#### Metrik Kinerja

Berikut adalah hasil metrik utama yang dicapai oleh model pada set data validasi/uji:

| Metrik Kunci | Nilai | Interpretasi |
| :--- | :--- | :--- |
| **AUC-ROC** | **0.9994** | Nilai yang sangat mendekati 1.0 menunjukkan kemampuan model yang bagus bgt dalam membedakan antara kelas positif (Fraud) dan negatif (Non-Fraud). |
| **Accuracy** | **0.99** | **99%** dari total prediksi yang dibuat oleh model adalah benar. |
| **F1-Score (Macro Avg)** | **0.99** | Menunjukkan keseimbangan yang sangat baik antara Precision dan Recall di kedua kelas. |
| Precision | **0.98 (macro avg)** | Model memiliki tingkat keakuratan prediksi yang sangat tinggi, rata-rata sebesar 98% di kedua kelas (Fraud dan Non-Fraud).
| Recall | **0.98 (macro avg)** |Model Anda memiliki tingkat cakupan deteksi yang sangat tinggi, rata-rata sebesar 98% dalam menemukan semua sampel yang relevan di kedua kelas.
| Support | **1268 samples** |

Evaluasi per Kelasnya :
| Class | Precision | Recall | F1-Score | Support |
|--------|-----------|--------|----------|---------|
| 0.0 | 1.00 | 0.98 | 0.99 | 634 |
| 1.0 | 0.98 | 1.00 | 0.99 | 634 |

## 4. Cara Navigasi

Melakukan download file dataset yang sudah tersedia di cell pertama pada notebook, setelah itu melakukan upload pada content drive di notebook.
Semua analisis dan implementasi kode utama proyek ini terkandung dalam satu file *Jupyter Notebook* utama:

| File Name | Deskripsi |
| :--- | :--- |
| `train_transaction.csv` | Dataset transaksi untuk pelatihan model|
| `test_transaction.csv` | Dataset transaksi untuk pengujian model (membutuhkan prediksi)|

Pastikan semua *library* yang diperlukan sudah terinstal :
```bash
pip install polars pandas numpy matplotlib seaborn scikit-learn torch imbalanced-learn
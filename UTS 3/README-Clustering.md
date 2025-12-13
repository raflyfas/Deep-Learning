# UTS 3 Deep Learning - Customer Segmentation: Credit Card Usage Data

## Data Diri

| Kategori | Detail |
| :--- | :--- |
| **Nama** | **Rafly Fasha Purnomo Putra** |
| **Kelas** | **TK-46-GAB** |
| **NIM** | **1103223050** |

Proyek ini melakukan segmentasi pelanggan (customer segmentation) menggunakan data penggunaan kartu kredit, bertujuan untuk mengelompokkan pelanggan ke dalam grup-grup yang memiliki pola perilaku serupa.

## 1. Tujuan Repositori

Tujuan utama dari repositori ini adalah untuk mengimplementasikan dan menganalisis hasil dari algoritma *clustering* (pengelompokan) pada data transaksi kartu kredit.

Tujuan spesifik yang ingin dicapai melalui proyek ini meliputi:
* Mengidentifikasi pola-pola perilaku unik di antara pelanggan kartu kredit.
* Mengelompokkan pelanggan ke dalam segmen yang berbeda (klaster) berdasarkan karakteristik dan kebiasaan transaksi mereka.
* Menghasilkan wawasan yang dapat digunakan untuk strategi bisnis, seperti mengidentifikasi pelanggan bernilai tinggi untuk retensi, menemukan pelanggan berisiko, dan merancang kampanye pemasaran yang lebih tertarget.

Apa yang dilakukan di sini:
* Pembersihan data, termasuk penanganan nilai yang hilang (`CREDIT_LIMIT` dan `MINIMUM_PAYMENTS` diisi dengan median) dan penanganan *outliers* (menggunakan metode IQR).
* Melakukan *Feature Engineering* (pembuatan fitur baru) seperti `TOTAL_PURCHASES`, `UTILIZATION_RATE`, dan `PURCHASE_TO_BALANCE_RATIO`.
* Penskalaan data menggunakan `RobustScaler` untuk mengurangi sensitivitas terhadap *outliers*.
* Reduksi dimensi menggunakan PCA (Principal Component Analysis) untuk visualisasi.
* Penerapan model *clustering* untuk segmentasi pelanggan.
* Interpretasi klaster dan rekomendasi bisnis.

## 2. Gambaran Singkat Proyek dan Pemilihan Model

Proyek ini adalah inisiatif *Unsupervised Machine Learning* yang berfokus pada **Segmentasi Pelanggan**. Data yang digunakan mencakup berbagai metrik penggunaan kartu kredit seperti saldo, frekuensi pembelian, penarikan tunai (*cash advance*), batas kredit, dan pembayaran.

**Model Machine Learning yang Dipakai:**
Model utama yang digunakan adalah **K-Means Clustering**. Meskipun K-Means bukan model *deep learning*, ini adalah algoritma *clustering* yang paling umum dan efektif untuk tugas segmentasi awal.

**Alasan Pemilihan K-Means:**
K-Means dipilih karena:
1.  **Sederhana dan Efisien:** Algoritma ini relatif mudah diimplementasikan dan sangat efisien untuk dataset besar seperti data pelanggan ini [Inference].
2.  **Hasil yang Jelas:** K-Means menghasilkan klaster yang jelas dan terpusat (berbentuk sferis) di sekitar *centroid*, yang memudahkan interpretasi untuk kebutuhan bisnis [Inference].

## 3. Deskripsi Model dan Hasil Metrik

### Model dan Metode yang Digunakan
| Komponen | Model / Metode | Keterangan |
| :--- | :--- | :--- |
| **Preprocessing** | `RobustScaler` | Digunakan untuk menskalakan data, meminimalkan dampak *outliers* pada proses *clustering*. |
| **Reduksi Dimensi** | PCA (Principal Component Analysis) | Digunakan untuk mengurangi dimensi data menjadi 2 Komponen Utama (PC1 dan PC2) untuk visualisasi. Kedua komponen ini berhasil menjelaskan **86.15%** dari total varian data. |
| **Clustering** | `KMeans` | Algoritma *clustering* utama yang diterapkan setelah menentukan jumlah klaster optimal. |
| **Model Alternatif** | `DBSCAN`, `AgglomerativeClustering` | Diimpor dan dapat digunakan sebagai model alternatif. |

### Metrik Evaluasi
Metrik yang digunakan untuk mengevaluasi kualitas klaster dan menentukan jumlah klaster optimal (*k*) adalah **Silhouette Score** dan **Davies Bouldin Score**.
| Model | Silhouette Score | Davies-Bouldin Index |
| :--- | :--- | :--- |
| K-Means | 0.963 | 0.504|
| Hierarchical | 0.969 | 0.313 |

Untuk DBScan menemukan banyak sekali noise points, sebanyak **7981**. Maka model DBScan tidak cocok digunakan dalam kasus ini.

Walaupun hasil Silhouette Score dan DBI dari Hierarchical lebih baik dibanding K-Means, saya tetap memilih model K-Means dalam kasus ini. 
K-Means dipilih bukan karena performa metrik inferior, melainkan karena superioritas dalam hal:

1. Interpretabilitas klinis untuk stakeholder bisnis

2. Efisiensi komputasi untuk deployment skala besar

3. Validasi ekstensif dalam literatur customer segmentation

4. Stability dan reproducibility yang lebih tinggi 

### Hasil Segmentasi (Optimal K = 2)
Setelah penentuan optimal, K-Means diterapkan dengan **2 klaster**, menghasilkan segmen-segmen pelanggan sebagai berikut:

| Klaster | Jumlah Pelanggan | Tipe Pelanggan | Rata-rata Key Metrics | Deskripsi Singkat |
| :--- | :--- | :--- | :--- | :--- |
| **Klaster 0** | 8935 (99.8%) | **Cash Advance Users** | Balance: ~$1,393; Cash Advances: ~$674; Credit Utilization: 31.5%. | Pelanggan yang sangat bergantung pada penarikan tunai (*cash advance*), yang mungkin mengindikasikan tekanan finansial. |
| **Klaster 1** | 15 (0.2%) | **High Spenders / Good Payer** | Balance: ~$0; Purchases: ~$1,078; Credit Utilization: 0.0%. | Pelanggan dengan frekuensi pembelian tinggi yang mampu mempertahankan saldo rendah, kemungkinan besar membayar lunas tagihan secara teratur. |

## 4. Library yang Diperlukan (Dependencies)

Untuk menjalankan *notebook* dan mereplikasi analisis ini, Anda perlu menginstal library Python berikut:

```bash
pip install pandas numpy matplotlib seaborn scikit-learn scipy
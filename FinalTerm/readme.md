# Tugas 2: Generative Question Answering dengan T5-Base

Repositori ini berisi implementasi **Task 2** untuk tugas Deep Learning NLP. Proyek ini berfokus pada teknik *fine-tuning* model **Sequence-to-Sequence (Seq2Seq)** menggunakan arsitektur Transformer untuk melakukan *Generative Question Answering*.

## Identitas Mahasiswa

| Informasi | Detail |
| :--- | :--- |
| **Nama** | [Rafly Fasha Purnomo Putra] |
| **NIM** | [1103223050] |
| **Kelas** | [TK4603] |
| **Kelompok** | [Kelompok 6] |

---

## Gambaran Umum Proyek

Tujuan dari repositori ini adalah untuk mendemonstrasikan kemampuan **Generative Transformers** dalam pemrosesan bahasa alami (NLP). Berbeda dengan model *Extractive QA* (seperti BERT) yang hanya memprediksi indeks awal dan akhir jawaban dalam teks, proyek ini menggunakan **T5 (Text-to-Text Transfer Transformer)** untuk menghasilkan teks jawaban secara langsung (generatif).

### Tujuan Utama
1.  Melakukan preprocessing data SQuAD agar sesuai dengan format input T5.
2.  Melakukan *fine-tuning* pada model *pre-trained* `t5-base`.
3.  Mengevaluasi kemampuan model dalam menjawab pertanyaan berdasarkan konteks yang diberikan.

---

## Deskripsi Model & Hasil Evaluasi

### 1. Arsitektur Model: T5-Base
Kami menggunakan model **T5 (Text-to-Text Transfer Transformer)** dari Google.
* **Tipe Arsitektur:** Encoder-Decoder (Seq2Seq).
* **Mekanisme:** T5 memperlakukan setiap masalah NLP sebagai masalah "teks-ke-teks".
* **Format Input:** `question: <teks pertanyaan> context: <paragraf konteks>`
* **Format Output:** `<teks jawaban>`

### 2. Dataset: SQuAD v1.1
Model dilatih menggunakan **Stanford Question Answering Dataset (SQuAD)**.
* **Konten:** Pasangan pertanyaan dan paragraf konteks dari artikel Wikipedia.
* **Tugas:** Model harus menemukan informasi relevan dalam paragraf dan menyusun jawaban teks.

### 3. Matriks & Hasil Evaluasi
Performa model diukur berdasarkan *Training Loss* dan metrik standar QA:
* **Training Loss:** Model dilatih selama beberapa epoch. Penurunan *loss* (menuju angka kisaran 0.24 - 0.25) menunjukkan model berhasil mempelajari pola pemetaan antara pertanyaan+konteks menjadi jawaban.

---

## Struktur Repositori & Navigasi

File utama dalam proyek ini adalah:

```text
├── notebook_lengkap_aman.ipynb   # Notebook utama berisi seluruh kode (pipeline)
├── README.md                     # Dokumentasi proyek (file ini)
└── requirements.txt              # (Opsional) Daftar library yang dibutuhkan
```
---

**## Panduan Navigasi notebook_lengkap_aman.ipynb**
Notebook disusun secara berurutan sebagai berikut:

| Proses | Deskripsi |
| :--- | :--- |
| **Instalasi & Setup:** | [Menginstall library transformers, datasets, dan evaluate
] |
| **Load Dataset** | [Memuat data SQuAD dari Hugging Face Hub] |
| **Preprocessing** | [Tokenisasi dan format ulang input dengan prefix khusus T5 ("question: ... context: ...")] |
| **Training (Fine-Tuning)** | [Melatih model t5-base menggunakan Seq2SeqTrainer] |
| **Inference (Testing)** | [Bagian pengujian manual di mana Anda bisa memasukkan konteks dan pertanyaan sendiri (contoh: pertanyaan tentang "Monas") untuk melihat jawaban model] |
---
## Cara Menjalankan
1. Clone repositori ini atau unduh file .ipynb.

2. Buka file notebook menggunakan Google Colab (disarankan) atau Jupyter Lab.

3. Pastikan Runtime Type diatur ke GPU (misalnya T4 GPU) agar proses training berjalan cepat.

4. Jalankan setiap sel kode secara berurutan dari atas ke bawah. Notebook sudah menyertakan perintah instalasi library yang diperlukan.
---
## Sitasi & Referensi
* **Model:** [Hugging Face T5-Base](https://huggingface.co/t5-base)
* **Dataset:** [SQuAD on Hugging Face](https://huggingface.co/datasets/squad)
* **Paper:** Raffel, C., et al. (2020). *Exploring the Limits of Transfer Learning with a Unified Text-to-Text Transformer*.

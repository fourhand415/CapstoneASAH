# 🛒 Customer Segmentation for Personalized Retail Marketing (A25-CS256)

[![Python](https://img.shields.io/badge/Python-3.9%2B-blue?logo=python&logoColor=white)](https://www.python.org/)
[![Streamlit](https://img.shields.io/badge/Dashboard-Streamlit-FF4B4B?logo=streamlit&logoColor=white)](https://dashboard-asah.streamlit.app/)
[![Scikit-Learn](https://img.shields.io/badge/Machine%20Learning-Scikit--Learn-orange?logo=scikit-learn&logoColor=white)](https://scikit-learn.org/)
---

## 🔗 Tautan & Sumber Daya
Berikut adalah seluruh sumber daya yang digunakan dalam proyek ini:

- **🌐 Live Dashboard:** [https://dashboard-asah.streamlit.app/](https://dashboard-asah.streamlit.app/)
  *(Aplikasi web untuk melihat hasil analisis secara interaktif)*
- **📂 Sumber Daya Pendukung (G-Drive):** [Aset & File Tambahan](https://drive.google.com/drive/folders/1GhXmFzP0nDhblYxRAIvsIk5rKELX6jLc?hl=id)
  *(Berisi file presentasi, aset gambar, dan dokumen lengkap proyek)*
- **💾 Sumber Dataset:** [Online Retail II UCI (Kaggle)](https://www.kaggle.com/datasets/mashlyn/online-retail-ii-uci)

---
# Core Team
| No | Nama | ID Anggota |
|----|--------------|----------------|
| 1  | Richie Leonard Tjias   |   M004D5Y1701  |
| 2  | Muhammad Farhan Lucky Putra | M004D5Y1259 |
| 3  |  Muhammad Rafi Insani    | M004D5Y1341 |

---
## 🧠 Arsitektur & Alur Kerja Proyek

Proyek ini terdiri dari dua komponen utama yang saling terhubung: **Analisis (Notebook)** dan **Visualisasi (Dashboard)**.

### 1. 📘 The "Brain": Analisis Data (`Final_Project_ASAH.ipynb`)
File notebook (`.ipynb`) dalam repositori ini berfungsi sebagai "otak" dari proyek. Di sinilah semua proses pengolahan data mentah terjadi.
* **Input:** Data mentah transaksi penjualan.
* **Proses:** Pembersihan data, perhitungan skor RFM, pelatihan algoritma K-Means, dan perhitungan matriks kesamaan produk (*Cosine Similarity*).
* **Output:** Menghasilkan file model (`.pkl`) yang berisi pola perilaku pelanggan dan aturan rekomendasi produk.

### 2. 📊 The "Face": Dashboard Aplikasi (`dashboard.py` di Repo ASAH)
Dashboard adalah antarmuka pengguna (*User Interface*) yang dibangun menggunakan **Streamlit**. Dashboard tidak melakukan pelatihan ulang model, melainkan **membaca file `.pkl`** yang dihasilkan oleh Notebook.
* **Fungsi:** Menampilkan grafik segmentasi pelanggan, metrik bisnis, dan formulir interaktif untuk mencari rekomendasi produk bagi pelanggan tertentu.

---

## 🛠️ Metodologi Analisis (Detail IPYNB)

Berikut adalah tahapan teknis yang dilakukan di dalam `Final_Project_ASAH.ipynb`:

### A. Data Cleaning & Preprocessing
* Menghapus transaksi yang dibatalkan (Invoice diawali huruf 'C').
* Membuang data tanpa `Customer ID` (anonim) karena tidak bisa disegmentasi.
* Menghapus kode stok non-produk (seperti 'POST', 'BANK CHARGES', 'D').
* Membersihkan duplikasi data dan harga yang tidak valid (<= 0).

### B. RFM Analysis (Feature Engineering)
Kami mengubah data transaksi menjadi metrik perilaku pelanggan:
* **Recency (R):** Jumlah hari sejak pembelian terakhir pelanggan.
* **Frequency (F):** Seberapa sering pelanggan berbelanja.
* **Monetary (M):** Total uang yang dihabiskan pelanggan.

### C. K-Means Clustering (Segmentation)
* **Normalisasi:** Menggunakan `MinMaxScaler` agar skala data seragam.
* **Elbow Method:** Digunakan untuk menentukan jumlah klaster optimal (ditemukan $k=4$).
* **Hasil Segmen:**
    1.  **Champions:** Pelanggan terbaik (Baru beli, sering beli, belanja banyak).
    2.  **Loyal Potential:** Pelanggan setia dengan potensi *upselling*.
    3.  **At Risk:** Pelanggan yang sudah lama tidak kembali.
    4.  **Lost/Hibernating:** Pelanggan yang sudah berhenti berbelanja.

### D. Recommendation System (Hybrid)
1.  **Collaborative Filtering:** Jika pelanggan punya riwayat belanja, sistem mencari produk yang mirip dengan pembelian terakhir mereka menggunakan **Cosine Similarity**.
2.  **Cluster-Based:** Jika pelanggan baru atau datanya sedikit, sistem merekomendasikan produk terlaris ("Top Sellers") dari segmen/klaster tempat mereka berada.

---

## 🚀 Panduan Instalasi & Penggunaan

Ikuti panduan di bawah ini untuk menjalankan analisis atau dashboard di komputer lokal Anda.

### 1️⃣ Menjalankan Analisis (Repo Ini)
Lakukan ini jika Anda ingin mempelajari kode analisis atau memperbarui model data.

1.  **Clone Repositori CapstoneASAH**
    ```bash
    git clone [https://github.com/fourhand415/CapstoneASAH.git](https://github.com/fourhand415/CapstoneASAH.git)
    cd CapstoneASAH
    ```
2.  **Install Library**
    ```bash
    pip install -r requirements.txt
    ```
3.  **Jalankan Notebook**
    Buka `Final_Project_ASAH.ipynb` di Jupyter Notebook atau VS Code, lalu jalankan semua sel (*Run All*). Ini akan menghasilkan file `.pkl` baru.

---

### 2️⃣ Menjalankan Dashboard (Lokal)
Lakukan ini jika Anda ingin melihat tampilan aplikasi Streamlit di laptop Anda.

1.  **Clone Repositori Dashboard (ASAH)**
    *Dashboard berada di repositori terpisah agar lebih ringan untuk deployment.*
    ```bash
    git clone [https://github.com/fourhand415/ASAH.git](https://github.com/fourhand415/ASAH.git)
    cd ASAH
    ```
2.  **Install Dependencies**
    ```bash
    pip install -r requirements.txt
    ```
3.  **Jalankan Aplikasi**
    ```bash
    streamlit run dashboard.py
    ```
    Aplikasi akan terbuka otomatis di browser Anda (biasanya di `http://localhost:8501`).

---

## 📂 Struktur File

```text
CapstoneASAH/
│
├── Final_Project_ASAH.ipynb  # [OTAK] Notebook utama analisis & modeling
├── requirements.txt          # Daftar library Python yang dibutuhkan
├── README.md                 # Dokumentasi proyek ini
│
# Output Model (Dihasilkan oleh Notebook, dipakai oleh Dashboard):
├── rfm.pkl                   # Dataframe RFM hasil olahan
├── topN_cluster.pkl          # Daftar produk terlaris per klaster
├── user_item_matrix.pkl      # Matriks interaksi User vs Item
└── item_similarity_df.pkl    # Matriks kemiripan antar produk

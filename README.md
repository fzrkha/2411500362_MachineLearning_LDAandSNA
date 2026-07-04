# 📊 Analisis Topik & Jaringan Sosial: Pidato Presiden Prabowo di Twitter/X

> **Dibuat oleh:** Fansoli Ibnu Mustafa (2411500362)  
> **Dosen Pengampu:** Dr. Indra, S.Kom., M.T.I.

Halo! 👋 Selamat datang di repositori ini. Pada proyek ini, saya mengeksplorasi dan menganalisis *dataset* Twitter (sebanyak 520 *tweet*) yang berisi tanggapan publik mengenai pidato Presiden Prabowo. Tujuan dari analisis ini adalah untuk menemukan topik utama yang sedang hangat diperbincangkan, serta memvisualisasikan bagaimana bentuk struktur interaksi antar pengguna di platform Twitter/X.

Proyek ini dibagi menjadi tiga tahapan utama: **Pra-pemrosesan (Preprocessing)**, **Pemodelan Topik (LDA)**, dan **Analisis Jaringan Sosial (SNA)**.

---

### 🛠️ Tahapan Analisis dalam Proyek Ini

#### 1. 🧹 Preprocessing Data (Pra-pemrosesan)
Data mentah dari media sosial umumnya sangat tidak terstruktur. Oleh karena itu, pada tahap ini dilakukan pembersihan agar teks lebih optimal saat diproses oleh algoritma:
* **Pembersihan Dasar:** Menghapus tautan (URL), *mention* (@), *hashtag* (#), dan tanda baca. Karakter emoji juga dikonversi menjadi teks agar maknanya tidak hilang.
* **Normalisasi Bahasa:** Mengubah kata tidak baku (slang) menjadi kata baku yang sesuai. Selain itu, kata negasi (seperti "tidak") digabungkan dengan kata setelahnya (misalnya: "tidak_berdaya") untuk mempertahankan konteks kalimat.
* **Penggabungan Kata (N-grams):** Menggabungkan frasa penting menjadi satu kesatuan token menggunakan garis bawah (*underscore*), seperti `presiden_prabowo`, `makan_bergizi_gratis`, dan `kabinet_merah_putih`.
* **Stopwords & Stemming:** Menghapus kata hubung yang tidak memiliki makna signifikan dan mengembalikan setiap kata ke bentuk dasarnya menggunakan *library* **Sastrawi**.
* **💾 Output:** Hasil dari tahap ini diekstrak menjadi file `hasil-preprocessing_pidato-prabowo.csv`.

#### 2. 🤖 Topic Modeling (Pemodelan LDA)
Setelah teks dibersihkan, algoritma *Latent Dirichlet Allocation* (LDA) digunakan untuk mengelompokkan *tweet* ke dalam **5 Topik Utama**. 
* Model ini bekerja dengan mencari pola kata yang memiliki probabilitas tinggi untuk muncul bersamaan.
* Setiap *tweet* kemudian diklasifikasikan dan diberikan label berdasarkan topik yang paling dominan (misalnya: topik terkait bursa saham/IHSG, program pemerintah, dsb).
* **💾 Output:** Data yang telah dilengkapi dengan label topik ini disimpan dalam file `hasil-modeling-lda_pidato-prabowo.csv`.

#### 3. 🕸️ Social Network Analysis (SNA) & Otomatisasi Gephi
Ini adalah bagian yang paling menarik! Saya memetakan siapa membalas siapa untuk melihat pusat interaksi dalam jaringan.
* **Smart Imputation untuk Akun Target:** Seringkali pengguna membalas akun besar (seperti portal berita atau tokoh publik) yang datanya tidak ikut terambil dalam *dataset*. Agar akun tersebut tetap memiliki atribut topik dalam visualisasi, saya menerapkan logika perhitungan **Modus**. Topik untuk akun target diisi berdasarkan topik mayoritas dari *tweet* yang membalas mereka.
* **Otomatisasi Atribut Gephi:** Penentuan ukuran simpul (*Nodes*) diotomatisasi sepenuhnya di Python berdasarkan metrik **In-Degree** (seberapa sering akun tersebut dibalas). Atribut warna khusus untuk masing-masing topik juga langsung diinjeksi ke dalam kode. 
* **💾 Output:** Format akhir diekspor menjadi file `SNA_Pidato-Prabowo.gexf`. File ini sudah terkonfigurasi secara matematis dan visual, sehingga Anda hanya perlu memuatnya ke dalam *software* **Gephi**, menjalankan *layout* **ForceAtlas 2**, dan jaringan akan langsung terbentuk dengan rapi (Total: 248 Nodes & 165 Edges).

---

### 💻 Tools & Libraries yang Digunakan
Untuk menjalankan atau memodifikasi kode dalam repositori ini, pastikan *library* berikut telah terinstal pada *environment* Python Anda:

```python
pip install gensim nltk scikit-learn emoji pandas Sastrawi networkx

# Customer Segmentation Using K-Means Clustering

Segmentasi 500 data pelanggan sintetis menggunakan K-Means berdasarkan frekuensi pembelian dan total pendapatan. Hasil clustering dibagi menjadi tiga kelompok: Low Value, Mid Value, dan High Value (VIP).

Seluruh kode ada di satu file: `customer-segmentation-kmeans.py`.

## Dataset

Data dibuat sendiri menggunakan NumPy, bukan berasal dari transaksi pelanggan sungguhan. Dataset awal berisi 500 baris dengan lima kolom:

| Kolom | Keterangan |
|---|---|
| `age` | Usia pelanggan |
| `gender` | Jenis kelamin (`M` atau `F`) |
| `country` | Negara (`USA`, `Canada`, atau `UK`) |
| `purchase_frequency` | Frekuensi pembelian |
| `total_revenue` | Total pendapatan pelanggan |

Untuk menguji proses pembersihan data, dibuat 25 nilai kosong pada `age`, 25 nilai kosong pada `total_revenue`, serta 10 baris dengan nilai ekstrem pada `purchase_frequency` dan `total_revenue`.

## Metode

1. **EDA:** melihat distribusi usia, gender, dan negara, korelasi fitur numerik, serta outlier melalui boxplot.
2. **Missing value:** mengisi nilai kosong pada `age` dan `total_revenue` menggunakan median. Median yang digunakan masing-masing 42 dan 5.380.
3. **Outlier:** menggunakan metode IQR pada `purchase_frequency` dan `total_revenue`. Setelah penyaringan, jumlah data berkurang dari 500 menjadi 490 baris.
4. **Standardisasi:** mengubah skala `purchase_frequency` dan `total_revenue` menggunakan `StandardScaler`.
5. **Elbow Method:** mencoba jumlah cluster dari K = 1 sampai K = 10. K = 3 dipilih dalam proyek ini.
6. **K-Means:** menjalankan model dengan `n_clusters=3`, `random_state=42`, dan `n_init=10`.
7. **Interpretasi:** membandingkan rata-rata frekuensi pembelian dan total pendapatan untuk memberi nama pada masing-masing cluster.

## Hasil

Dari 500 data awal, 490 data digunakan dalam clustering setelah proses pembersihan. Model membentuk tiga cluster dengan hasil profil berikut:

| Segmen | Jumlah pelanggan | Rata-rata frekuensi pembelian | Rata-rata total pendapatan |
|---|---:|---:|---:|
| Low Value | 164 | 10,77 | 1.947,07 |
| Mid Value | 158 | 4,85 | 6.620,77 |
| High Value (VIP) | 168 | 14,55 | 6.860,68 |

Temuan dari hasil segmentasi:

- **Low Value** memiliki rata-rata total pendapatan paling rendah, yaitu 1.947,07. Namun, frekuensi pembeliannya (10,77) bukan yang paling rendah.
- **Mid Value** memiliki rata-rata total pendapatan 6.620,77, tetapi frekuensi pembeliannya justru paling rendah, yaitu 4,85.
- **High Value (VIP)** memiliki rata-rata frekuensi pembelian tertinggi (14,55) dan rata-rata total pendapatan tertinggi (6.860,68).
- Jumlah pelanggan pada ketiga segmen relatif berimbang, berkisar antara 158 sampai 168 pelanggan.

Hasil tersebut menunjukkan bahwa label segmen tidak sepenuhnya menggambarkan urutan frekuensi pembelian. Penamaan Low, Mid, dan High pada kode dibuat berdasarkan urutan rata-rata `total_revenue`, bukan berdasarkan gabungan kedua fitur.

## Keterbatasan

- Dataset dibuat secara acak untuk latihan, sehingga pola yang ditemukan belum tentu mewakili perilaku pelanggan nyata.
- `age`, `gender`, dan `country` hanya digunakan pada eksplorasi data. Ketiga kolom tersebut tidak ikut menentukan cluster.
- Label Low Value, Mid Value, dan VIP ditentukan hanya dari rata-rata `total_revenue`. Karena itu, segmen Mid Value memiliki frekuensi pembelian lebih rendah daripada Low Value.
- Pemilihan K = 3 didasarkan pada pembacaan visual Elbow Method dan belum dibandingkan dengan metrik validasi cluster seperti silhouette score.
- Pada file sumber, bagian Elbow Method memanggil `KMeans` dan `X_scaled` sebelum keduanya didefinisikan. Urutan kode perlu dirapikan agar dapat dijalankan dari awal sampai akhir tanpa error.

## Cara menjalankan

1. Install library yang digunakan:

   ```bash
   pip install pandas numpy matplotlib seaborn scikit-learn
   ```

2. Buka file `customer-segmentation-kmeans.py` di Google Colab atau Jupyter Notebook.
3. Pastikan bagian import `KMeans`, pemilihan fitur, dan standardisasi dijalankan sebelum bagian Elbow Method.
4. Jalankan kode secara berurutan.

## Struktur repo

```text
customer-segmentation-kmeans/
├── customer-segmentation-kmeans.py
└── README.md
```

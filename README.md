# Laporan Proyek Machine Learning - Nur Adilah

## Project Overview

Sistem rekomendasi telah menjadi komponen penting dalam industri e-commerce modern. Dengan volume produk yang sangat besar, pelanggan seringkali kesulitan menemukan produk yang sesuai dengan preferensi atau kebutuhannya. Dalam era digital saat ini, sistem rekomendasi menjadi salah satu fitur krusial dalam meningkatkan kualitas layanan di industri e-commerce. Berdasarkan laporan dari McKinsey, sistem rekomendasi dapat meningkatkan penjualan hingga 20% dan keterlibatan pelanggan secara signifikan [1]. Tidak hanya itu, laporan dari Forbes juga menyatakan bahwa pelanggan cenderung lebih loyal pada platform yang mampu memberikan rekomendasi produk yang relevan  [2]. 
Supermarket sebagai bagian dari sektor ritel juga mengalami transformasi digital. Banyak dari mereka mulai menyediakan layanan pembelian online, dan kebutuhan untuk menyajikan produk yang sesuai preferensi pelanggan menjadi penting agar tetap kompetitif. Oleh karena itu, sistem rekomendasi dibutuhkan untuk memberikan pengalaman belanja yang lebih personal dan efisien.

Dalam proyek ini, dibangun sistem rekomendasi berbasis data penjualan supermarket yang bertujuan untuk menyajikan rekomendasi produk secara otomatis kepada pelanggan. Sistem ini memanfaatkan dua pendekatan: 
- **Content-Based Filtering**: Rekomendasi berdasarkan karakteristik produk, seperti jenis produk dan harga.
- **Collaborative Filtering**: Rekomendasi berdasarkan pola pembelian pelanggan lain yang serupa.

Pemilihan kedua pendekatan ini memungkinkan sistem untuk menggabungkan pemahaman atas karakteristik produk dengan preferensi kolektif dari pelanggan, sehingga menghasilkan rekomendasi yang lebih akurat dan relevan.

Dataset yang digunakan adalah Supermarket Sales Dataset dari Kaggle, yang mencakup informasi transaksi penjualan di toko ritel dengan berbagai fitur seperti: jenis produk (Product Line), cabang toko (Branch), harga (Unit Price), rating produk, total transaksi, tanggal dan waktu pembelian, serta informasi lainnya yang relevan untuk analisis sistem rekomendasi.

Referensi:

- [1] McKinsey & Company. (2013). Big Data, Analytics, and the Future of Marketing & Sales.
- [2] Bernard Marr. (2019). How Netflix, Amazon, and Spotify Use AI To Keep You Hooked. Forbes.

# Business Understanding

### Problem Statement  
Dalam konteks e-commerce supermarket, pelanggan menghadapi kesulitan dalam menemukan produk yang sesuai dengan kebutuhannya karena banyaknya variasi produk yang tersedia. Selain itu, kurangnya  sistem rekomendasi yang memanfaatkan riwayat pembelian dan preferensi pelanggan menyebabkan rendahnya tingkat personalisasi, yang pada akhirnya berdampak pada menurunnya kepuasan serta loyalitas pelanggan terhadap platform.

### Goals
Berdasarkan pernyataan masalah di atas, tujuan dari proyek ini adalah:
1. Membangun sistem rekomendasi berbasis produk yang dapat membantu pelanggan menemukan produk yang relevan dengan preferensinya.
2. Meningkatkan pengalaman belanja pelanggan melalui rekomendasi yang bersifat personal dan kontekstual.
3. Mengevaluasi dan membandingkan dua pendekatan sistem rekomendasi **Content-Based Filtering** dan **Collaborative Filtering** untuk menentukan metode yang paling efektif dalam konteks data penjualan supermarket.

### Solution Approach
Untuk mencapai tujuan tersebut, pendekatan solusi yang digunakan terdiri dari:

1. Content-Based Filtering

Pendekatan ini menganalisis karakteristik dari produk yang telah dibeli oleh pelanggan, seperti jenis produk (Product Line), harga (Unit Price), dan rating produk. Sistem kemudian merekomendasikan produk-produk yang memiliki kesamaan fitur dengan produk-produk yang sebelumnya diminati oleh pelanggan tersebut.

2. Collaborative Filtering

Pendekatan ini berfokus pada perilaku dan interaksi antar pelanggan. Model akan mempelajari pola pembelian dari pelanggan lain yang memiliki kesamaan preferensi, dan merekomendasikan produk yang disukai oleh pelanggan serupa.

Untuk Collaborative Filtering, digunakan pendekatan matrix factorization, khususnya dengan mempertimbangkan implicit feedback. Salah satu algoritma yang digunakan adalah Alternating Least Squares (ALS), yang terbukti efektif dalam mengolah data interaksi pelanggan dalam sistem rekomendasi skala besar.

# Data Understanding
Pada proyek ini, dataset yang digunakan dalam proyek ini adalah Supermarket Sales Dataset yang tersedia secara publik di Kaggle. Dataset ini dapat diakses melalui tautan berikut: [Supermarket-Sales-Dataset](https://www.kaggle.com/datasets/faresashraf1001/supermarket-sales)

### Variabel-variabel pada tudent Performance Dataset adalah sebagai berikut:
- 'InvoiceID': ID Transaksi, menunjukkan transaksi unik, akan digunakan untuk Collaborative Filtering.
- 'Branch' & 'City': Cabang toko yang masing-masing berada di kota yang berbeda.
- 'Customer type': Ada dua jenis pelanggan yaitu `Member` dan `Normal`.
- 'Gender': Jenis kelamin pelanggan antara laki-laki (`Male`) dan perempuan (`Female`).
- 'Product Line': Kategori produk yang dibeli, misalnya Health and beauty, Electronic accesories, Home and lifestyle, dll. Menunjukkan jenis produk yang dibeli, penting untuk Content-based Filtering.
- 'Unit Price': Harga satuan produk.
- 'Quantity': Jumlah item yang dibeli
- 'Total': Total transaksi (Unit price x Quantity).
- 'Date' & 'Time': waktu transaksi.
- 'Payment': Metode pembayaran, yang terdapat tiga metode digunakan: `Cash`, `Credit card`, dan `Ewallet`.
- 'Rating': Penilaian pelanggan terhadap transaksi. Dapat digunakan sebagai implicit feedback atau relevansi produk.
  
### Exploratory Data Analysis
Exploratory data analysis atau sering disingkat EDA merupakan proses investigasi awal pada data untuk menganalisis karakteristik, menemukan pola, anomali, dan memeriksa asumsi pada data. Teknik ini biasanya menggunakan bantuan statistik dan representasi grafis atau visualisasi.

Berikut ini adalah EDA yang dilakukan:

```python 
supermarket.info()
```
output:
<pre>
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 1000 entries, 0 to 999
Data columns (total 17 columns):
 #   Column                   Non-Null Count  Dtype  
---  ------                   --------------  -----  
 0   Invoice ID               1000 non-null   object 
 1   Branch                   1000 non-null   object 
 2   City                     1000 non-null   object 
 3   Customer type            1000 non-null   object 
 4   Gender                   1000 non-null   object 
 5   Product line             1000 non-null   object 
 6   Unit price               1000 non-null   float64
 7   Quantity                 1000 non-null   int64  
 8   Tax 5%                   1000 non-null   float64
 9   Sales                    1000 non-null   float64
 10  Date                     1000 non-null   object 
 11  Time                     1000 non-null   object 
 12  Payment                  1000 non-null   object 
 13  cogs                     1000 non-null   float64
 14  gross margin percentage  1000 non-null   float64
 15  gross income             1000 non-null   float64
 16  Rating                   1000 non-null   float64
dtypes: float64(7), int64(1), object(9)
memory usage: 132.9+ KB
</pre>

Dapat dilihat dartaset ini memiliki 1000 baris dan memiliki 17 kolom. Sebagian besar kolom bertipe 'object', terutama kolom kategori seperti 'Branch', 'City', 'Customer type', 'Gender', dan 'Product line', kemudian terdapat Kolom 'Date' dan 'Time' masih bertipe 'object', sehingga perlu di ubah menjadi tipe data 'datetime'agar bisa diolah lebih lanjut dalam analisis waktu (misalnya pola pembelian berdasarkan hari), Kolom numerik seperti 'Unit Price', 'Quantity', 'Sales', dan 'Rating' sudah bertipe data numerik dan siap dianalisis. Kemudian Tidak terlihat adanya nilai null pada setiap kolom, jadi tidak perlu melakukan penanganan missing value.

```python 
supermarket.describe()
```
output:
| Statistic | Unit Price | Quantity | Tax 5%   | Sales    | COGS     | Gross Margin % | Gross Income | Rating   |
|-----------|------------|----------|----------|----------|----------|----------------|--------------|----------|
| Count     | 1000.000   | 1000.000 | 1000.000 | 1000.000 | 1000.000 | 1000.000       | 1000.000     | 1000.000 |
| Mean      | 55.672     | 5.510    | 15.379   | 322.967  | 307.587  | 4.7619         | 15.379       | 6.973    |
| Std       | 26.495     | 2.923    | 11.709   | 245.885  | 234.177  | ~0.0000        | 11.709       | 1.719    |
| Min       | 10.080     | 1.000    | 0.509    | 10.679   | 10.170   | 4.7619         | 0.509        | 4.000    |
| 25%       | 32.875     | 3.000    | 5.925    | 124.422  | 118.498  | 4.7619         | 5.925        | 5.500    |
| 50%       | 55.230     | 5.000    | 12.088   | 253.848  | 241.760  | 4.7619         | 12.088       | 7.000    |
| 75%       | 77.935     | 8.000    | 22.445   | 471.350  | 448.905  | 4.7619         | 22.445       | 8.500    |
| Max       | 99.960     | 10.000   | 49.650   | 1042.650 | 993.000  | 4.7619         | 49.650       | 10.000   |









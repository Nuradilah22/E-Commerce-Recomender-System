# Laporan Proyek Machine Learning - Nur Adilah

## Project Overview

Sistem rekomendasi telah menjadi komponen penting dalam industri e-commerce modern. Dengan volume produk yang sangat besar, pelanggan seringkali kesulitan menemukan produk yang sesuai dengan preferensi atau kebutuhannya. Dalam era digital saat ini, sistem rekomendasi menjadi salah satu fitur krusial dalam meningkatkan kualitas layanan di industri e-commerce. Berdasarkan laporan dari McKinsey, sistem rekomendasi dapat meningkatkan penjualan hingga 20% dan keterlibatan pelanggan secara signifikan [1]. Tidak hanya itu, laporan dari Forbes juga menyatakan bahwa pelanggan cenderung lebih loyal pada platform yang mampu memberikan rekomendasi produk yang relevan [2].
Supermarket sebagai bagian dari sektor ritel juga mengalami transformasi digital. Banyak dari mereka mulai menyediakan layanan pembelian online, dan kebutuhan untuk menyajikan produk yang sesuai preferensi pelanggan menjadi penting agar tetap kompetitif. Tanpa panduan, pelanggan dapat kewalahan dengan banyaknya pilihan, sementara supermarket kehilangan peluang untuk menawarkan produk yang paling relevan bagi setiap individu. Oleh karena itu, pembangunan sistem rekomendasi berbasis data penjualan menjadi krusial untuk memberikan pengalaman belanja yang lebih personal, efisien, dan pada akhirnya meningkatkan kinerja bisnis.

Dalam proyek ini, dibangun sistem rekomendasi berbasis data penjualan supermarket yang bertujuan untuk menyajikan rekomendasi produk secara otomatis kepada pelanggan. Proyek ini penting untuk diselesaikan karena secara langsung mengatasi tantangan menemukan produk relevan di tengah keragaman pilihan dan memberikan supermarket alat untuk meningkatkan interaksi serta penjualan melalui personalisasi. Sistem ini mengeksplorasi dan memanfaatkan dua pendekatan populer:

- **Content-Based Filtering**: Merekomendasikan produk berdasarkan kesamaan karakteristik internal produk itu sendiri, seperti jenis produk, harga, dan rating.
- **Collaborative Filtering**: Merekomendasikan produk berdasarkan pola perilaku atau interaksi (pembelian) dari pelanggan lain yang serupa.

Pemilihan kedua pendekatan ini memungkinkan sistem untuk menggabungkan pemahaman atas karakteristik produk dengan preferensi kolektif dari pelanggan, sehingga menghasilkan rekomendasi yang diharapkan lebih akurat dan relevan.

Dataset yang digunakan adalah Supermarket Sales Dataset dari Kaggle, yang mencakup informasi transaksi penjualan di toko ritel dengan berbagai fitur penting untuk analisis dan pemodelan rekomendasi, seperti: ID Transaksi (Invoice ID), jenis produk (Product Line), cabang toko (Branch), harga satuan (Unit Price), jumlah dibeli (Quantity), rating produk, dan total transaksi.

Referensi:

- [1] McKinsey & Company. (2013). Big Data, Analytics, and the Future of Marketing & Sales.
- [2] Bernard Marr. (2019). How Netflix, Amazon, and Spotify Use AI To Keep You Hooked. Forbes.

# Business Understanding

### Problem Statement  
Dalam konteks e-commerce supermarket, pelanggan sering menghadapi kesulitan dalam menemukan produk yang sesuai dengan kebutuhannya karena banyaknya variasi produk yang tersedia (information overload). Ketidakhadiran sistem rekomendasi yang mampu memanfaatkan riwayat pembelian dan preferensi pelanggan mengakibatkan rendahnya tingkat personalisasi dalam pengalaman belanja. Hal ini berdampak langsung pada penurunan kepuasan pengguna, engagement, serta loyalitas pelanggan terhadap platform. **Bagi supermarket, kurangnya personalisasi ini juga dapat mengurangi efisiensi penjualan, menghambat upaya cross-selling dan upselling, serta menyulitkan identifikasi tren dan preferensi pelanggan secara individual.**

### Goals
Berdasarkan pernyataan masalah di atas, tujuan dari proyek ini adalah:
1. Membangun dua model sistem rekomendasi: Content-Based Filtering dan Collaborative Filtering, memanfaatkan data penjualan supermarket untuk menghasilkan daftar rekomendasi produk (top-N) yang relevan bagi pelanggan.
2. Mengevaluasi kinerja kedua model rekomendasi yang dibangun menggunakan metrik yang sesuai untuk mengukur efektivitasnya dalam memberikan rekomendasi yang akurat.
3. Melakukan perbandingan hasil evaluasi antara kedua pendekatan untuk mengidentifikasi kelebihan dan kekurangan masing-masing dalam konteks data ini, sebagai dasar potensi pengembangan di masa depan.

### Solution Approach
Untuk mencapai tujuan tersebut, pendekatan solusi yang diimplementasikan terdiri dari:

1. Content-Based Filtering

Pendekatan ini akan memanfaatkan informasi deskriptif dari produk itu sendiri. Analisis dilakukan terhadap karakteristik dari produk yang telah dibeli atau dilihat oleh pelanggan, seperti jenis produk (Product Line), harga (Unit Price), dan rating produk. Sistem kemudian akan merekomendasikan produk-produk lain yang dinilai memiliki kesamaan fitur yang tinggi dengan produk-produk yang sebelumnya diminati oleh pelanggan tersebut.

2. Collaborative Filtering

Pendekatan ini berfokus pada analisis pola perilaku dan interaksi antar pelanggan. Model akan mempelajari riwayat pembelian dari sekumpulan besar pelanggan untuk menemukan pengguna yang memiliki selera atau pola pembelian yang serupa. Berdasarkan identifikasi tersebut, sistem akan merekomendasikan produk yang disukai atau dibeli oleh pelanggan serupa, namun belum pernah dibeli oleh pelanggan target.

Untuk Collaborative Filtering, digunakan pendekatan **matrix factorization** dengan mempertimbangkan **implicit feedback** (berdasarkan kuantitas pembelian). Salah satu algoritma yang dipilih adalah **Alternating Least Squares (ALS)**, yang terbukti efektif dalam mengolah data interaksi pelanggan (user-item interaction matrix) yang biasanya bersifat sparse.

# Data Understanding
Pada proyek ini, dataset yang digunakan dalam proyek ini adalah Supermarket Sales Dataset yang tersedia secara publik di Kaggle. Dataset ini dapat diakses melalui tautan berikut: [Supermarket-Sales-Dataset](https://www.kaggle.com/datasets/faresashraf1001/supermarket-sales)

### Variabel-variabel pada tudent Performance Dataset adalah sebagai berikut:
- `InvoiceID` : ID Transaksi, menunjukkan transaksi unik, akan digunakan untuk Collaborative Filtering.
- `Branch` & `City` : Cabang toko yang masing-masing berada di kota yang berbeda.
- `Customer type` : Ada dua jenis pelanggan yaitu `Member` dan `Normal`.
- `Gender` : Jenis kelamin pelanggan antara laki-laki (`Male`) dan perempuan (`Female`).
- `Product Line` : Kategori produk yang dibeli, misalnya Health and beauty, Electronic accesories, Home and lifestyle, dll. Menunjukkan jenis produk yang dibeli, penting untuk Content-based Filtering.
- `Unit Price` : Harga satuan produk.
- `Quantity` : Jumlah item yang dibeli
- `Total` : Total transaksi (Unit price x Quantity).
- `Date` & `Time` : waktu transaksi.
- `Payment` : Metode pembayaran, yang terdapat tiga metode digunakan: `Cash`, `Credit card`, dan `Ewallet`.
- `Rating` : Penilaian pelanggan terhadap transaksi. Dapat digunakan sebagai implicit feedback atau relevansi produk.
  
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

### Visualisasi Data
- Visualisasi distribusi kategori produk
  
  ![download](https://github.com/user-attachments/assets/7d039313-709d-436d-af80-b99fea584226)

  Dari hasil visualisasi distribusi kategori produk (Product Line) menampilkan sebaran volume penjualan di berbagai jenis produk yang tersedia di supermarket, terlihat bahwa keenam kategori produk – Electronic accessories, Fashion accessories, Food and beverages, Health and beauty, Home and lifestyle, dan Sports and travel – memiliki jumlah transaksi yang relatif seimbang, tanpa adanya satu kategori yang mendominasi pasar secara signifikan. Perbedaan jumlah transaksi antar kategori memang ada, namun tidak menunjukkan perbedaan yang mencolok, mengindikasikan bahwa pelanggan memiliki preferensi yang bervariasi dan tidak terfokus pada satu atau dua jenis produk tertentu saja di supermarket ini.

- Visualisasi distribusi kategori Unit price
  
  ![download](https://github.com/user-attachments/assets/0850fa76-f814-40d4-a4ff-74f5bf092b00)

  Dari hasil visualisasi distribusi harga per unit produk (Unit Price), disertai dengan kurva KDE (Kernel Density Estimate), menunjukkan bahwa harga produk di supermarket ini cukup bervariasi, tersebar dari nilai terendah (sekitar 10) hingga nilai tertinggi (sekitar 100). Kurva distribusi cenderung terlihat relatif datar di sebagian besar rentang harga, dengan sedikit peningkatan kepadatan di beberapa area, mengindikasikan bahwa tidak ada satu rentang harga tunggal yang paling mendominasi jumlah produk yang dijual, melainkan terdapat produk di berbagai tingkatan harga dari yang terjangkau hingga yang lebih mahal.

- Visualisasi distribusi kategori Rating
  
  ![download](https://github.com/user-attachments/assets/46c2b89a-3822-49d5-a95c-db0e16ab3ac4)

  Dari hasil visualisasi distribusi rating produk, dilengkapi dengan kurva KDE, memperlihatkan bahwa penilaian pelanggan cenderung terfokus pada skala rating yang lebih tinggi, dengan konsentrasi nilai paling sering berada di kisaran 7 hingga 9. Meskipun terdapat sebaran rating di seluruh rentang nilai (4-10), kepadatan distribusi terlihat lebih signifikan pada angka-angka yang lebih tinggi, mengindikasikan bahwa mayoritas pelanggan memiliki tingkat kepuasan yang cukup baik terhadap produk atau layanan di supermarket ini, meskipun tetap ada variasi dalam penilaian yang mencakup rating lebih rendah.

# Data Preparation
Tahap Data Preparation (Persiapan Data) dilakukan untuk membersihkan, mengubah, dan memformat data agar siap digunakan dalam proses pemodelan sistem rekomendasi.

Kode dibawah ini melakukan konveri tipe data 

```python
# Konversi tipe data 'Date' dan 'Time'
supermarket['Date'] = pd.to_datetime(supermarket['Date'])
supermarket['Time'] = pd.to_datetime(supermarket['Time'], format='%I:%M:%S %p').dt.time

print("Datasetail setelah konversi tipe data:")
print(supermarket.info())
```
Output:

<pre>
Datasetail setelah konversi tipe data:
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
 10  Date                     1000 non-null   datetime64[ns]
 11  Time                     1000 non-null   object        
 12  Payment                  1000 non-null   object        
 13  cogs                     1000 non-null   float64       
 14  gross margin percentage  1000 non-null   float64       
 15  gross income             1000 non-null   float64       
 16  Rating                   1000 non-null   float64       
dtypes: datetime64[ns](1), float64(7), int64(1), object(8)
memory usage: 132.9+ KB
</pre>

Kolom 'Date' dan 'Time' pada dataset awalnya bertipe object. Untuk memungkinkan analisis berbasis waktu dan memastikan format data yang sesuai, kedua kolom ini dikonversi ke tipe data yang tepat. Setelah konversi, dilakukan pengecekan tipe data kembali untuk memastikan perubahan berhasil.

Selanjutnya, dilakukan pembersihan teks (text cleaning) pada kolom-kolom kategorikal dalam dataset. Tujuannya adalah untuk menghilangkan karakter non-alfanumerik dan menyeragamkan penulisan teks (misalnya, penggunaan huruf kapital) untuk menghindari inkonsistensi data. Sebuah fungsi kustom, clean_text, didefinisikan untuk menjalankan proses ini. Fungsi clean_text ini kemudian diterapkan pada setiap kolom dalam DataFrame yang terdeteksi memiliki tipe data object, memastikan bahwa teks pada kolom-kolom seperti 'Product line', 'Branch', dan lainnya menjadi bersih dan seragam.

```python
# Membersihkan teks dari karakter non-alfanumerik dan mengubahnya ke huruf kecil
# Tujuan: agar tidak ada inkonsistensi seperti 'Male' vs 'male', 'Health & beauty' vs 'health & beauty', dll.
def clean_text(text):
    if isinstance(text, str):
        return re.sub(r'[^a-zA-Z0-9 ]', '', text.lower().strip())
    return ''
```
```python
# Terapkan pembersihan teks ke seluruh kolom kategorikal
for col in supermarket.select_dtypes(include='object').columns:
    supermarket[col] = supermarket[col].apply(clean_text)
```





























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
Dalam upaya meningkatkan kualitas layanan dan pengalaman pelanggan di supermarket, proyek ini dilatarbelakangi oleh tiga permasalahan utama berikut:
1. Bagaimana memberikan rekomendasi produk yang relevan kepada pelanggan berdasarkan pola transaksi dan preferensi sebelumnya?
Pelanggan seringkali kesulitan menemukan produk yang sesuai dengan kebutuhan mereka. Tanpa pemahaman atas preferensi sebelumnya, rekomendasi produk menjadi tidak personal dan kurang efektif.
2. Bagaimana meningkatkan tingkat penjualan dan kepuasan pelanggan melalui personalisasi produk?
Personalisasi merupakan kunci dalam menciptakan pengalaman belanja yang lebih memuaskan. Dengan menyajikan produk yang tepat kepada pelanggan yang tepat, supermarket dapat meningkatkan engagement dan mendorong peningkatan penjualan.
3. Bagaimana mengatasi keterbatasan data pelanggan dan produk agar rekomendasi tetap akurat?
Keterbatasan data, seperti tidak adanya rating eksplisit atau informasi preferensi pelanggan, menjadi tantangan tersendiri dalam membangun sistem rekomendasi yang andal. Oleh karena itu, dibutuhkan pendekatan yang dapat bekerja secara efektif meskipun data yang tersedia terbatas.

### Goals
Berdasarkan pernyataan masalah di atas, tujuan dari proyek ini adalah:
1. Membangun sistem rekomendasi produk yang dapat menyarankan produk serupa atau produk yang sering dibeli bersama berdasarkan data transaksi dan fitur produk.
2. Meningkatkan pengalaman belanja pelanggan dengan memberikan rekomendasi yang personal dan relevan, sehingga mendorong loyalitas dan retensi.
3. Menggunakan metode yang efektif untuk menghasilkan rekomendasi dengan data yang tersedia, tanpa mengandalkan informasi eksplisit seperti rating atau feedback pelanggan.

### Solution Approach
Untuk mencapai tujuan tersebut, proyek ini menggunakan dua pendekatan utama dalam sistem rekomendasi:

1. Content-Based Filtering
    Pendekatan ini akan memanfaatkan informasi deskriptif dari produk itu sendiri. Mengandalkan fitur produk seperti Product Line, Unit Price, dan Rating untuk merekomendasikan produk yang mirip dengan produk yang pernah dibeli atau disukai pelanggan sebelumnya. Pendekatan ini sangat berguna untuk memberikan rekomendasi personal bahkan saat data interaksi pengguna terbatas.

2. Collaborative Filtering
   Pendekatan ini menggunakan Collaborative Filtering berbasis Item (Item-Based) untuk menganalisis pola pembelian pelanggan dan mengukur kemiripan antar produk menggunakan Cosine Similarity. Model ini merekomendasikan produk kepada user berdasarkan produk lain yang sering dibeli bersamaan atau disukai oleh user yang sama, sehingga mampu menemukan relasi antar produk dari perilaku kolaboratif pelanggan.

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

Kode dibawah ini mencetak nilai unique Product line dan Customer type

```python
print("\nUnique Product Lines:", supermarket['Product line'].nunique())
print("Unique Customer Types:", supermarket['Customer type'].unique())
```

### Visualisasi Data
- Visualisasi distribusi Product line (produk terjual terbanyak)
  
  ![download](https://github.com/user-attachments/assets/7d039313-709d-436d-af80-b99fea584226)

  Dari hasil visualisasi distribusi kategori produk (Product Line) menampilkan sebaran volume penjualan di berbagai jenis produk yang tersedia di supermarket, terlihat bahwa keenam kategori produk – Electronic accessories, Fashion accessories, Food and beverages, Health and beauty, Home and lifestyle, dan Sports and travel – memiliki jumlah transaksi yang relatif seimbang, tanpa adanya satu kategori yang mendominasi pasar secara signifikan. Perbedaan jumlah transaksi antar kategori memang ada, namun tidak menunjukkan perbedaan yang mencolok, mengindikasikan bahwa pelanggan memiliki preferensi yang bervariasi dan tidak terfokus pada satu atau dua jenis produk tertentu saja di supermarket ini.

- Visualisasi distribusi Customer Type dan Gender
  
  ![download](https://github.com/user-attachments/assets/f7b977e4-30c7-4bdd-80b7-6dba61a9c1e8)

  Dari hasil visualisasi distribusi Customer Type dan Gender, dapat dilihat proporsi jumlah pelanggan antara tipe Member dan Normal, serta perbandingan jumlah pelanggan berdasarkan jenis kelamin, yang memberikan gambaran umum tentang komposisi dasar pelanggan dalam dataset.

- Visualisasi distribusi Unit price per Product line dan Rating per Product line

  ![download](https://github.com/user-attachments/assets/d159ee5b-6624-46c3-9aa8-0c214a34d57a)

  Dari hasil visualisasi distribusi Unit price per Product line dan Rating per Product line, menampilkan harga satuan ("Unit price") dan rating untuk setiap kategori "Product line". Dari plot ini, kita bisa mendapatkan insight mengenai kisaran harga typical dan variasi rating dalam setiap jenis produk, serta mengidentifikasi jika ada jenis produk yang secara konsisten memiliki harga atau rating yang lebih tinggi atau lebih rendah dibandingkan yang lain.

- Visualisasi distribusi Quantity dan Total transakasi (gross income)

  ![download](https://github.com/user-attachments/assets/a2b75fab-4aee-4a69-b133-234e7d0a209a)

  Dari hasil visualisasi distribusi Quantity dan Total transakasi (gross income), menampilkan distribusi jumlah produk yang terjual ("Quantity") dan total pendapatan dari transaksi ("gross income"), di mana distribusi kuantitas menunjukkan seberapa sering sejumlah unit produk tertentu terjual, sementara distribusi pendapatan kotor dengan estimasi kurva kepadatan (KDE) menggambarkan pola umum dari nilai total transaksi yang terjadi.

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

### CBF Data Preparation

Untuk data preparation CBF dilakukan pembuatan DataFrame baru bernama df_product yang hanya berisi informasi unik tentang setiap jenis produk dari dataset asli supermarket. Dengan memilih kolom "Product line", "Rating", dan "Unit price", kode ini mengambil fitur-fitur kunci yang menggambarkan karakteristik produk. Kemudian, metode drop_duplicates() digunakan untuk menghapus baris-baris duplikat, sehingga setiap kombinasi unik dari product line, rating, dan unit price hanya muncul sekali. Terakhir, reset_index(drop=True) mengatur ulang indeks DataFrame yang baru dibuat agar berurutan dari 0, dan menghapus kolom indeks lama yang mungkin tersisa setelah menghapus duplikat. 

```python
# Membuat DataFrame produk unik dengan fitur yang digunakan
df_product = supermarket[['Product line', 'Rating', 'Unit price']].drop_duplicates().reset_index(drop=True)
```

Kemudian, menggabungkan kolom "Product line", "Rating", dan "Unit price" dari DataFrame df_product menjadi satu kolom teks bernama features. Penggabungan ini penting untuk menyiapkan data fitur produk dalam format teks yang dapat diolah oleh algoritma TF-IDF, yang akan digunakan untuk menghitung kemiripan antar produk berdasarkan deskripsinya dalam Content-Based Filtering.

Penggabungan data dilakukan pada kode dibawah ini:

```python
# Mengabungkan fitur menjadi string untuk TF-IDF
df_product['features'] = df_product['Product line']  + ' ' + df_product['Rating'].astype(str) + ' ' + df_product['Unit price'].astype(str)
```
### CF Data Preparation

Untuk data preparation CF pertama dilakukan pembuatan kolom 'CustomerID' baru dalam DataFrame supermarket dengan menggabungkan 'Customer type' dan 'Gender'. Hal ini dilakukan untuk mendapatkan identitas unik bagi setiap "user" dalam dataset, karena tidak ada ID pengguna asli, yang mana identifikasi unik ini diperlukan untuk membangun matriks interaksi user-item. Selanjutnya melakukan mapping ID user ('CustomerID') dan ID produk ('Product line') yang unik ke dalam indeks integer berurutan. Pemetaan ini krusial karena algoritma CF bekerja dengan matriks yang menggunakan indeks numerik. Terakhir, matriks sparse interaksi user-produk dibangun menggunakan format COO, di mana baris merepresentasikan user, kolom merepresentasikan produk, dan nilainya adalah kuantitas produk yang dibeli user tersebut. Matriks sparse ini menjadi input utama yang efisien untuk melatih model Collaborative Filtering seperti ALS.

Pembuatan kolom baru dilakukan pada kode dibawah ini:

```python
supermarket['CustomerID'] = supermarket['Customer type'] + '_' + supermarket['Gender']
```
Kemudian dilakukan mapping antara ID pelanggan unik ('CustomerID') dan ID produk unik ('Product line') ke dalam bentuk indeks integer berurutan.

```python
user_ids = supermarket['CustomerID'].unique()
product_ids = supermarket['Product line'].unique()

user_to_idx = {user: idx for idx, user in enumerate(user_ids)}
product_to_idx = {prod: idx for idx, prod in enumerate(product_ids)}
```

Kemudian Kode dibawah ini untuk membuat sparse matrix user-product berdasarkan Quantity (bisa juga Total)

```python
rows = supermarket['CustomerID'].map(user_to_idx)
cols = supermarket['Product line'].map(product_to_idx)
data = supermarket['Quantity']

sparse_user_product = coo_matrix((data, (rows, cols)), shape=(len(user_ids), len(product_ids)))
```
# Modeling
Modeling pada tahap awal menghasilkan dua model rekomendasi: satu model Content-Based Filtering berdasarkan kemiripan fitur produk yang diukur dengan cosine similarity dari representasi TF-IDF, dan satu model Collaborative Filtering yang dilatih menggunakan algoritma Alternating Least Squares (ALS) pada matriks sparse interaksi user-produk.

## 1. Content-Based Filtering (CBF)
Pendekatan Content-Based Filtering dilakukan dengan memanfaatkan informasi deskriptif dari produk, seperti "Product line", "Rating", dan "Unit price". Informasi ini digabungkan ke dalam satu kolom features, kemudian dilakukan proses vektorisasi menggunakan TF-IDF (Term Frequency-Inverse Document Frequency). TF-IDF merupakan teknik yang mengukur seberapa penting suatu term (dalam hal ini, elemen dari fitur gabungan) dalam sebuah dokumen (setiap baris produk di df_product['features']) relatif terhadap seluruh kumpulan dokumen. Term-term yang sering muncul di satu produk tetapi jarang muncul di produk lain akan memiliki bobot lebih tinggi, sehingga membantu membedakan karakteristik unik dari setiap produk. Vektor hasil TF-IDF ini kemudian digunakan untuk menghitung kemiripan antar produk, yang menjadi dasar rekomendasi.

Kemudian tahap yang dilakukan yaitu:

- Menerapkan TfidfVectorizer

  ```python
  tfidf = TfidfVectorizer()
  tfidf_matrix = tfidf.fit_transform(df_product['features'])
  ```
- Menunjukkan seberapa mirip setiap produk satu sama lain berdasarkan fitur-fitur yang digunakan

  ```python
  cosine_sim = cosine_similarity(tfidf_matrix, tfidf_matrix)
  ```
- Menggunakan fungsi pencarian (atau fungsi rekomendasi)  untuk menghasilkan rekomendasi produk serupa menggunakan skor kemiripan konten yang sudah dihitung sebelumnya.

  ```python
  def recommend_product_based(product_index, top_n=5):
  similiar_scores = list(enumerate(cosine_sim[product_index]))
  similiar_scores = sorted(similiar_scores, key=lambda x: x[1], reverse=True)
  similiar_scores = similiar_scores[1:top_n+1]
  product_indices = [i[0] for i in similiar_scores]
  return df_product.iloc[product_indices]
  ```
Setelah kode diatas dijalankan, output yang dihasilkan dari `recommend_product_based(5)` adalah daftar produk-produk yang paling mirip (serupa) dengan produk yang memiliki indeks ke-5 dalam DataFrame `df_product`. Output tersebut ditampilkan dalam bentuk DataFrame yang menampilkan detail dari produk-produk yang direkomendasikan, seperti "Product line", "Rating", "Unit price", dan kolom "features" gabungan.

| ID Produk | Product Line           | Rating | Unit Price | Features                           |
|-----------|------------------------|--------|------------|------------------------------------|
| 55        | Electronic accessories | 8.2    | 85.98      | Electronic accessories 8.2 85.98   |
| 291       | Electronic accessories | 6.0    | 27.85      | Electronic accessories 6.0 27.85   |
| 172       | Electronic accessories | 6.3    | 20.85      | Electronic accessories 6.3 20.85   |
| 680       | Electronic accessories | 6.5    | 39.48      | Electronic accessories 6.5 39.48   |
| 877       | Electronic accessories | 6.1    | 39.75      | Electronic accessories 6.1 39.75   |

Ketika merekomendasikan berdasarkan produk dengan indeks ke-5, model Content-Based Filtering merekomendasikan 5 produk lain yang semuanya termasuk dalam kategori 'Electronic accessories'. Ini menunjukkan bahwa produk acuan (indeks 5) kemungkinan adalah produk 'Electronic accessories', dan model berhasil menemukan produk serupa dalam kategori yang sama.

Kelebihan dan kekurangan model
- Kelebihan: mampu merekomendasikan item baru yang belum pernah dilihat atau dinilai oleh siapa pun, selama item tersebut memiliki deskripsi fitur yang memadai. Kemudian, Mampu merekomendasikan item baru dan kepada user baru dan rekomendasi relatif transparan (berbasis kemiripan fitur).
- Kekurangan: Kualitas rekomendasi sangat bergantung pada seberapa kaya, akurat, dan representatif fitur-fitur deskriptif item. Jika fitur item kurang mendeskripsikan item dengan baik, rekomendasi bisa jadi buruk. Kemudian Cenderung mengalami over-specialization, hanya merekomendasikan item yang sangat mirip dan juga sulit merekomendasikan item dari kategori yang sama sekali berbeda dari riwayat user.

## 2. Collaborative Filtering (CF)
Pendekatan ini menggunakan Collaborative Filtering berbasis Item (Item-Based) untuk menganalisis pola pembelian pelanggan dan mengukur kemiripan antar produk menggunakan Cosine Similarity. Model ini merekomendasikan produk kepada user berdasarkan produk lain yang sering dibeli bersamaan atau disukai oleh user yang sama, sehingga mampu menemukan relasi antar produk dari perilaku kolaboratif pelanggan.

Tahapan yang dilakukan yaitu:
- Tahapan persiapan dan pembangunan model Collaborative Filtering berbasis Item (Item-Based) menggunakan Cosine Similarity.

  ```python
  cf_pivot = supermarket.pivot_table(index='CustomerID', columns='Product line', values='Quantity', aggfunc='sum').fillna(0)

  cf_similarity = cosine_similarity(cf_pivot.T)
  cf_similarity_df = pd.DataFrame(cf_similarity, index=cf_pivot.columns, columns=cf_pivot.columns)
  ```
  Kode ini dilakukan untuk mempersiapkan data interaksi user-produk dan menghitung kemiripan antar produk menggunakan Cosine Similarity sebagai langkah awal dalam membangun model Collaborative Filtering berbasis Item.

- Menggunakan fungsi untuk menghasilkan rekomendasi pada model Collaborative Filtering berbasis Item yang telah dibangun sebelumnya.

  ```python
  def recommend_cf(product_line, top_n=5):
    if product_line not in cf_similarity_df.columns:
        return []
    similar_items = cf_similarity_df[product_line].sort_values(ascending=False)[1:top_n+1]
    return similar_items
  ```
  
  Setelah kode diatas dijalankan, output yang dihasilkan dari `recommend_cf("Electronic accessories", top_n=5)`, output yang dihasilkan adalah daftar 5 produk yang paling mirip dengan "Electronic accessories" berdasarkan pola pembelian kolaboratif user, beserta skor kemiripan Cosine-nya. Output ini mengindikasikan produk-produk yang sering dibeli bersamaan atau oleh user yang sama dengan "Electronic accessories".

# Evaluasi
  Pada tahap evaluasi, digunakan beberapa metrik evaluasi

- Evaluasi Content-Based Filtering. Metrik evaluasi yang digunakan untuk menilai performa model Content-Based Filtering (CBF) adalah Precision@K. Metrik ini mengukur seberapa relevan rekomendasi produk teratas yang diberikan oleh model CBF. Dalam implementasi ini, relevansi didefinisikan berdasarkan kesamaan kategori produk ('Product line') antara produk yang direkomendasikan dengan produk yang dijadikan input referensi. Untuk setiap produk yang dijadikan rekomendasi, model menghasilkan rekomendasi produk teratas berdasarkan kemiripan konten (Cosine Similarity dari fitur TF-IDF). Precision@K kemudian dihitung dengan membandingkan berapa banyak dari produk item rekomendasi tersebut yang memiliki kategori produk yang sama persis dengan kategori produk refensi.
  
  Formula yang digunakan untuk menghitung Precision@K:
  
  ![image](https://github.com/user-attachments/assets/bab59c1e-1007-49aa-bd58-53769a09ef73)

  Kode di bawah ini akan membuat fungsi untuk menghitung precision: 

  ```python
  # Membuat fungsi untuk menghitung presisi model

  def precision_at_k_cbf(product_index, k=5):
      target_product = df_product.iloc[product_index]
      target_category = target_product['Product line']

    recommended_items_df = recommend_product_based(product_index, top_n=k)

    # Hitung berapa banyak rekomendasi yang memiliki kategori yang sama
    relevant_recommended_count = recommended_items_df['Product line'].eq(target_category).sum()

    # Hitung Precision@K
    precision = relevant_recommended_count / k if k > 0 else 0

    return precision
  ```
  Kemudian menghitung precision:
  
  ```python
  precisions = [precision_at_k_cbf(i, k=5) for i in df_product.index]
  average_precision_cbf = np.mean(precisions)
  
  print(f'\nPrecision Content-Based Filtering (based on category): {average_precision_cbf:.2f}')
  ```
  Kemudian output yang dihasilkan:
  <pre>Precision Content-Based Filtering (based on category): 0.84</pre>

   Evaluasi model Content-Based Filtering (CBF) menggunakan **Precision\@5** menunjukkan hasil rata-rata sebesar **0.84**, dengan definisi relevansi berdasarkan kesamaan kategori produk (*Product line*). Artinya, rata-rata 84% dari 5 rekomendasi teratas memiliki kategori yang sama dengan produk acuan. Ini menunjukkan bahwa model CBF sangat efektif dalam mengenali dan merekomendasikan produk serupa berdasarkan fitur kontennya, terutama kategori produk yang digunakan sebagai fitur utama.
   
2. Evaluasi Collaborative Filtering (CF) menggunakan beberapa metrik yang umum untuk mengevaluasi sistem rekomendasi dalam skenario Top-K recommendation. Metrik-metrik ini fokus pada seberapa baik model merekomendasikan item yang relevan kepada pengguna. Metrik yang digunakan adalah Precision@K: Mengukur proporsi item yang relevan di antara $K$$K$ item teratas yang direkomendasikan, kemudian Recall@K: Mengukur proporsi item relevan yang berhasil direkomendasikan di antara semua item relevan yang ada. Untuk kedua metrik, nilai dihitung pada Top-5 rekomendasi dan kemudian menghitung rata-rata di seluruh produk unik yang dijadikan acuan untuk mendapatkan Average Precision@5 dan Average Recall@5. Relevansi didefinisikan berdasarkan kemiripan kolaboratif antar item (sering dibeli bersamaan atau disukai oleh user yang sama).

Formula yang digunakan untuk menghitung Precision@K dan Recall@5:

![image](https://github.com/user-attachments/assets/bab59c1e-1007-49aa-bd58-53769a09ef73)
![image](https://github.com/user-attachments/assets/edf0e55a-ebd9-4d1c-823c-867f5dd71f1b)

Kode di bawah ini akan membuat fungsi untuk menghitung precision dan recall:

```python
def evaluate_cf_topk(k=5):
    total_precision = 0
    total_recall = 0
    total_items = 0

    for product in cf_similarity_df.index:
        recommended = recommend_cf(product, top_n=k).index.tolist()
        relevant_items = [p for p in cf_similarity_df.columns if p != product]

        if len(relevant_items) == 0:
          continue

        retrieved_relevant = [p for p in recommended if p in relevant_items]

        precision = len(retrieved_relevant) / k if k > 0 else 0
        recall = len(retrieved_relevant) / len(relevant_items)

        total_precision += precision
        total_recall += recall
        total_items += 1

    avg_precision = total_precision / total_items if total_items > 0 else 0
    avg_recall = total_recall / total_items if total_items > 0 else 0

    return avg_precision, avg_recall, k
  ```
  Kemudian menghitung precision dan recall:

  ```python
  avg_precision, avg_recall, k_val = evaluate_cf_topk(k=5)
  
  print(f"\nEvaluasi Collaborative Filtering (Top-{k_val})")
  print(f"Precision@{k_val}: {avg_precision:.2f}")
  print(f"Recall@{k_val}: {avg_recall:.2f}")
  ```
  Kemudian output yang dihasilkan:
  <pre>
    Evaluasi Collaborative Filtering (Top-5)
    Precision@5: 1.00
    Recall@5: 1.00
  </pre>

Evaluasi model Collaborative Filtering (CF) menggunakan metrik Average Precision@5 dan Average Recall@5 menunjukkan hasil sempurna, yaitu 1.00. Ini berarti model selalu merekomendasikan item yang dianggap relevan—dalam hal ini, semua item lain selain item acuan. Hasil ini menandakan bahwa model mampu menangkap kemiripan item secara kolaboratif. Namun, karena definisi relevansi yang digunakan cukup luas, hasil evaluasi perlu diinterpretasikan dengan hati-hati.

# Kesimpulan
Proyek ini berhasil membangun dan mengevaluasi dua jenis sistem rekomendasi untuk supermarket. Dengan menggunakan Content-Based Filtering (CBF) Model ini merekomendasikan produk berdasarkan kemiripan fitur produk seperti kategori, rating, dan harga. Evaluasi menunjukkan bahwa model ini dapat merekomendasikan produk dengan kategori yang sama. Kemudian dengan menggunakan Collaborative Filtering (CF) Model ini merekomendasikan produk berdasarkan pola transaksi pelanggan (barang apa yang dibeli bersama). Evaluasi menggunakan metrik Precision@k dan Recall@k menunjukkan kemampuan model ini untuk merekomendasikan item yang serupa dengan item yang telah dibeli sebelumnya, meskipun dengan nilai presisi dan recall yang bervariasi. Kedua model ini menunjukkan potensi untuk memberikan rekomendasi produk, namun efektivitasnya dalam skenario nyata perlu diuji lebih lanjut dengan data yang lebih kompleks dan mempertimbangkan faktor lain seperti waktu transaksi dan demografi pelanggan.

Model yang dibangun dalam proyek ini berhasil menjawab seluruh problem statement dan mencapai tujuan yang telah dirumuskan pada tahap Business Understanding.

1. dua model rekomendasi: Collaborative Filtering (CF) yang memanfaatkan pola pembelian bersama, dan Content-Based Filtering (CBF) yang merekomendasikan produk serupa berdasarkan fitur. Meski sudah relevan, personalisasi masih terbatas karena kurangnya data seperti riwayat pembelian individual atau rating eksplisit.
2. Sistem rekomendasi ini bertujuan mempersonalisasi pengalaman belanja dengan menyajikan produk yang lebih relevan, yang secara teori dapat meningkatkan penjualan dan kepuasan pelanggan. Namun, tanpa A/B testing atau uji langsung di lingkungan nyata, dampak model terhadap penjualan dan kepuasan hanya bisa dinilai secara teoritis.
3. Proyek ini mengatasi keterbatasan data dengan dua pendekatan:
  - CBF memanfaatkan fitur produk (seperti kategori, rating, harga) untuk merekomendasikan item serupa, cocok saat data transaksi individu terbatas.
  - CF menggunakan pola transaksi agregat (quantity) untuk membentuk matriks user-item, meski tanpa ID pelanggan unik, agar bisa menangkap pola pembelian kelompok.
    Namun, tanpa data seperti rating eksplisit, info demografis, atau riwayat pembelian yang lebih detail, personalisasi dan akurasi masih terbatas. Langkah awal ini sudah tepat, tapi hasil bisa ditingkatkan dengan data yang lebih kaya.


















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












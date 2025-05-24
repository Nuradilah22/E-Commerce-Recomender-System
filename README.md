# Laporan Proyek Machine Learning - Nur Adilah

## Project Overview

Sistem rekomendasi telah menjadi komponen penting dalam industri e-commerce modern. Dengan volume produk yang sangat besar, pelanggan seringkali kesulitan menemukan produk yang sesuai dengan preferensi atau kebutuhannya. Dalam era digital saat ini, sistem rekomendasi menjadi salah satu fitur krusial dalam meningkatkan kualitas layanan di industri e-commerce. Berdasarkan laporan dari McKinsey, sistem rekomendasi dapat meningkatkan penjualan hingga 20% dan keterlibatan pelanggan secara signifikan [1]. Tidak hanya itu, laporan dari Forbes juga menyatakan bahwa pelanggan cenderung lebih loyal pada platform yang mampu memberikan rekomendasi produk yang relevan  [2]. 
Supermarket sebagai bagian dari sektor ritel juga mengalami transformasi digital. Banyak dari mereka mulai menyediakan layanan pembelian online, dan kebutuhan untuk menyajikan produk yang sesuai preferensi pelanggan menjadi penting agar tetap kompetitif. Oleh karena itu, sistem rekomendasi dibutuhkan untuk memberikan pengalaman belanja yang lebih personal dan efisien.

Dalam proyek ini, dibangun sistem rekomendasi berbasis data penjualan supermarket yang bertujuan untuk menyajikan rekomendasi produk secara otomatis kepada pelanggan. Sistem ini memanfaatkan dua pendekatan: 
- **Content-Based Filtering**: Rekomendasi berdasarkan karakteristik produk, seperti jenis produk dan harga.
- **Collaborative Filtering**: Rekomendasi berdasarkan pola pembelian pelanggan lain yang serupa.

Dengan menggunakan dataset publik dari Kaggle yang berisi informasi transaksi penjualan produk di supermarket, sistem ini dirancang untuk memberikan pengalaman belanja yang lebih personal, serta membantu pelanggan menemukan produk baru yang relevan.

Referensi:

- [1] McKinsey & Company. (2013). Big Data, Analytics, and the Future of Marketing & Sales.
- [2] Bernard Marr. (2019). How Netflix, Amazon, and Spotify Use AI To Keep You Hooked. Forbes.

# Business Understanding

### Problem Statement  
Dalam konteks e-commerce supermarket, terdapat beberapa tantangan yang dihadapi, antara lain:
1. Pelanggan kesulitan menemukan produk yang sesuai kebutuhannya karena banyaknya varian produk yang tersedia.
2. Kurangnya personalisasi dalam penawaran produk, yang dapat mengurangi minat dan loyalitas pelanggan.
3. Minimnya sistem rekomendasi yang mampu memanfaatkan riwayat pembelian pelanggan secara efisien.

### Goals
Berdasarkan pernyataan masalah di atas, tujuan dari proyek ini adalah:
1. Mengembangkan sistem rekomendasi berbasis produk untuk membantu pelanggan menemukan produk yang relevan.
2. Meningkatkan pengalaman belanja pelanggan dengan menyediakan rekomendasi yang dipersonalisasi.
3. Membandingkan dua pendekatan sistem rekomendasi (content-based dan collaborative filtering) untuk melihat pendekatan mana yang lebih sesuai dalam konteks data supermarket.

### Solution Approach
Untuk mencapai tujuan tersebut, pendekatan solusi yang digunakan terdiri dari:
- Solution 1: Content-Based Filtering

Sistem rekomendasi ini bekerja dengan menganalisis karakteristik dari produk yang dibeli pelanggan, seperti: jenis produk (_Product Line_), Harga (_Price_), dan Rating produk. Dengan pendekatan ini, pelanggan akan direkomendasikan produk-produk yang mirip dengan yang pernah mereka beli.

- Solution 2: Collaborative Filtering

Pendekatan ini menganalisis interaksi antar pelanggan. Model akan mempelajari kesamaan pola pembelian antar pelanggan dan merekomendasikan produk yang disukai oleh pelanggan lain dengan profil pembelian yang mirip.

Untuk metode ini akan digunakan teknik:
- Matrix Factorization (dengan pendekatan implicit feedback)
- Alternating Least Squares (ALS) atau pendekatan serupa












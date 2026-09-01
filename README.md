# Analisis Faktor yang Berkaitan dengan Rating Rendah pada Olist E-Commerce

## Gambaran Proyek
Customer review yang menjadi salah satu indikator penting untuk melihat pengalaman berbelanja pelanggan dalam sebuah platform e-commerce. Project ini menggunakan dataset **Olist Brazilian E-Commerce Public Dataset** untuk mengeksplorasi pengalaman pelanggan dan mencari faktor yang berkaitan dengan rendahnya rating.

Analisis dimulai dengan melihat distribusi rating dari 1 sampai 5.

<img width="589" height="455" alt="Rating Score" src="https://github.com/user-attachments/assets/1559148a-7763-43be-9796-defa172ac7dd" />

Dari distribusi rating terlihat bahwa sebagian besar pelanggan memberikan rating tinggi, terutama rating 5. Namun, terdapat hal yang menarik yaitu jumlah rating 1 lebih tinggi dibandingkan rating 2 dan 3.

Hal ini menunjukkan bahwa meskipun sebagian besar pelanggan memberikan rating tinggi, tetap terdapat cukup banyak pelanggan yang memberikan **rating terendah**, yang menjadi indikasi adanya pengalaman berbelanja yang kurang memuaskan.

Lalu, apa yang menyebabkan sebagian pelanggan memberikan rating 1?

Sebelum mencari tahu faktor yang berkaitan dengan rating 1, kita lihat terlebih dahulu bagaimana persebarannya sepanjang periode pengamatan.

<img width="1014" height="584" alt="line persebaran rating" src="https://github.com/user-attachments/assets/8b94e6f8-2afa-4379-ba32-5350b7fd9e33" />

Dan hasilnya menunjukkan bahwa rating 1 secara konsisten berada di posisi ketiga dan jumlahnya lebih tinggi dibandingkan rating 2 dan 3 sepanjang sebagian besar periode pengamatan.
Temuan awal ini menjadi dasar untuk melakukan analisis lebih lanjut terhadap faktor-faktor yang mungkin berkaitan dengan munculnya rating 1.

## Fokus Permasalahan
Beberapa faktor yang kemudian dianalisis meliputi:
* Durasi Pengiriman, apakah pesanan dengan waktu pengiriman yang lebih lama cenderung mendapatkan rating 1?
* Keterlambatan pengiriman, apakah order yang melewati estimasi pengiriman lebih sering mendapatkan rating 1?
* Harga produk dan biaya pengiriman, apakah karakteristik harga dan biaya pengiriman berkaitan dengan rendahnya rating?
* Wilayah seller dan customer, apakah lokasi seller dan customer memiliki pola tertentu pada order rating 1?
* Rute pengiriman, rute seller ke customer mana yang memiliki konsentrasi masalah rating 1 dan keterlambatan paling tinggi?

## Tujuan Analisis
Proyek ini bertujuan untuk menemukan faktor yang berkaitan dengan munculnya rating 1 dari segi pengiriman, wilayah pengiriman, harga dan biaya pengiriman. Diharapkan hasil analisis dapat memberikan gambaran tentang fenomena rating 1 yang cenderung dominan pada review score pelanggan olist.

## Persiapan Data
Dataset : [Olist Brazilian E-Commerce Public Dataset](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce) 

Periode : September 2016 -  Agustus 2018

Dataset yang digunakan : `olist_orders_dataset`,`olist_order_items_dataset`,`olist_customers_dataset`,`olist_sellers_dataset`,`olist_order_reviews_dataset`.

Sebelum analisis dilakukan, data terlebih dahulu dipersiapkan dengan memeriksa missing value dan duplikat, mengubah format tanggal, menggabungkan beberapa dataset Olist berdasarkan ID yang sesuai, serta membuat variabel baru seperti durasi dan keterlambatan pengiriman untuk kebutuhan analisis.

## Tahapan Analisis
### 1. Durasi Pengiriman dan Rating
Pertama, analisis dilakukan untuk melihat apakah durasi pengiriman berkaitan dengan rating pelanggan.
<img width="855" height="547" alt="Durasi pengiriman terhadap rating" src="https://github.com/user-attachments/assets/2b205faf-d9a0-46e7-b262-0b4fc38a3fb2" />
Dari hasil analisis terlihat bahwa order dengan durasi pengiriman yang lebih lama cenderung mendapatkan rating yang lebih rendah (grafik batang 1 tertinggi). Hal ini menunjukkan bahwa waktu pengiriman menjadi salah satu aspek yang berkaitan dengan pengalaman pelanggan.

### 2. Keterlambatan Pengiriman dan Rating
Selanjutnya, analisis dilakukan dengan membandingkan tanggal pengiriman aktual dengan tanggal estimasi pengiriman. Order kemudian dikategorikan menjadi pengiriman _tepat waktu_, _lebih awal_ dan _terlambat_.
<img width="989" height="590" alt="Status pengiriman terhadap rating" src="https://github.com/user-attachments/assets/fb38ecf1-4e0c-4aa0-bd3c-04ffdcfb0b8c" />
Rating 1 lebih banyaj ditemukan pada order yang mengalami keterlambatan pengiriman dibandingkan order yang dikirim sesuai estimasi. Hal ini menunjukkan bahwa **keterlambatan pengiriman merupakan salah satu faktor yang berkaitan dengan rendahnya rating pelanggan**.

### 3. Harga Produk (Price) dan Biaya Pengiriman (Freight Value)
Lalu bagaimana dengan harga dan ongkos kirim pesanan, apakah terdapat pengaruh yang menunjukkan hubungan rendahnya rating pelanggan?
a. Harga Produk (Price)


b. Biaya Pengiriman (Freight Value)


Perbedaan harga produk dan biaya pengiriman antar kelompok rating tidak menunjukkan pola yang cukup kuat untuk menjadikannya sebagai faktor utama dalam menjelaskan rating 1.
Oleh karena itu, kedua variabel tersebut digunakan sebagai faktor pendukung dalam analisis, bukan sebagai fokus utama penyebab rating rendah.

### 4. Analisis Rute Seller -> Customer
Setelah menemukan bahwa keterlambatan pengiriman berkaitan dengan rating 1, analisis kemudian difokuskan pada order yang memenuhi dua kondisi yaitu mendapatkan rating 1 dan mengalami keterlambatan pengiriman dari estimasi. 
Order tersebut kemudian dikelompokkan berdasarkan kombinasi **Seller State ke Customer State**. 
a. Jumlah rating 1 terlambat
Analisis ini digunakan untuk mengetahui rute mana yang memiliki jumlah kasus rating 1 terlambat paling banyak. Hal ini menunjukkan bahwa kedua rute tersebut memiliki konsentrasi kasus bermasalah yang besar secara absolut dan layak mendapatkan perhatian lebih lanjut.

SP -> RJ dan SP -> SP memiliki jumlah rating 1 terlambat paling tinggi.
b. Persentase rating 1 terlambat
Selain jumlah kasus, persentase juga digunakan untuk melihat proporsi order bermasalah terhadap seluruh order pada masing-masing rute. Pendekatan ini penting karena rute dengan jumlah kasus besar belum tentu memiliki tingkat masalah yang paling tinggi.

Kemunculan state seller SP pada berbagai rute dengan peprsebtase rating 1 terlambat yang paling tinggi menunjukkan bahwa rute yang berasal dari SP perlu ditinjau lebih lanjut. Tapi bukan berarti SP ini merupakan penyebab rating 1.

### 5. Dampak Bisnis
Kemudian dilakukan analisis untuk menghitung nilai transaksi atau **GMV (Gross Merchandise Value)** yang terkait dengan order rating 1 dan mengalami keterlambatan.
GMV dihitung berdasarkan nilai `price` dari order yang termasuk dalam kelompok tersebut.

Analisis ini digunakan untuk menjawab seberapa besar nilai transaksi yang terkait dengan order yang mengalami masalah rating 1 dan keterlambatan?

SP -> RJ dan SP -> SP termasuk rute dengan GMV terkait order bermasalah terbesar. Sebelumnya juga rute ini memiliki jumlah rating terlambat yang tinggi. Dengan demikian masalah pada rute tersebut tidak hanya terlihat dari jumlah kasus, tetapi juga melibatkan nilai transaksi yang cukup besar.

## Insight
Berdasarkan seluruh analisis, beberapa temuan utama yaitu:
1. Order dengan durasi pengiriman yang lebih panjang dan keterlambatan pengiriman lebih sering dikaitkan dengan rating rendah (rating 1).
2. Begitupun dengan order yang melewati batas estimasi tanggal diterima (terlambat) menunjukkan hubungan signifikan dengan rendahnya review score dari pelanggan.
3. Harga produk dan biaya pengiriman tidak menunjukkan pola yang cukup kuat untuk menjelaskan munculnya rating 1.
4. Wilayah seller ke customer SP -> RJ dan SP -> SP memiliki jumlah rating 1 dengan status keterlambatan pengiriman dari estimasi paling tinggi. Dengan seller state SP yang muncul pada banyak rute memiliki tingkat rating 1 tertinggi menjadikan rute tersebut memerlukan investigasi lebih lanjut.

## Kesimpulan
Analisis menunjukkan bahwa kinerja pengiriman merupakan aspek yang paling relevan dalam kaitannya dengan rating rendah pelanggan, terutama ketika pesanan mengalami keterlambatan.

Masalah tersebut tidak tersebar secara merata pada seluruh rute. Beberapa rute, khususnya rute yang berasal dari São Paulo (SP), menunjukkan konsentrasi kasus rating 1 terlambat yang cukup tinggi.

SP → RJ menjadi salah satu rute yang paling menonjol karena memiliki jumlah kasus rating 1 terlambat yang tinggi serta nilai transaksi dan biaya pengiriman yang signifikan.

Namun, hasil analisis ini tidak menunjukkan bahwa satu wilayah atau satu variabel merupakan penyebab tunggal rating 1. Temuan tersebut lebih tepat digunakan sebagai dasar untuk menentukan area yang perlu diteliti dan dievaluasi lebih lanjut.


## Rekomendasi
Karena keterlambatan berkaitan dengan rating rendah, peningkatan akurasi estimasi waktu pengiriman dapat membantu mengurangi kesenjangan antara ekspektasi pelanggan dan waktu penerimaan aktual. 
Selanjutnya rute pengiriman wilayah seller ke customer seperti SP -> RJ perlu mendapatkan perhatian karena memiliki jumlah kasus rating 1 terlambat yang tinggi sekaligus nilai transaksi yang besar.

## Tentang Project
Project ini dibuat sebagai bagian dari portofolio pembelajaran Data Analyst menggunakan Python.
**Kemampuan yang digunakan:**
* Data Cleaning
* Data Transformation
* Data Filtering
* Grouping dan Aggregation
* Merge
* Datetime Analysis
* Exploratory Data Analysis (EDA)
* Data Visualization
* Business Insight
* Business Recommendation

**Tools:**
* Python
* Pandas, Matplotlib, NumPy
* Google Colab, Drive




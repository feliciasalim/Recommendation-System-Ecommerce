# Laporan Proyek Machine Learning - Felicia Salim

## Project Overview

Di tengah-tengah perkembangan industri e-commerce, jumlah produk yang tersedia secara online terus meningkat dari tahun ke tahun. Ini menyebabkan kelebihan informasi yang dapat membingungkan pengguna[1]. Konsumen kini dihadapkan pada banyak sekali pilihan produk, dari berbagai merek, kategori, maupun harga. Untuk membantu pengguna menemukan produk yang relevan dengan preferensinya, sistem rekomendasi menjadi solusi penting yang mampu meningkatkan pengalaman belanja secara personal[2].

Bobadilla et al. menyatakan dalam ACM Computing Surveys bahwa metode collaborative filtering secara konsisten menunjukkan performa yang baik dalam mendeteksi preferensi pengguna melalui pola interaksi[3]. Di sisi lain, content-based filtering memungkinkan sistem merekomendasikan produk serupa berdasarkan deskripsi atau fitur item. Penggabungan kedua pendekatan ini menjadi sebuah solusi untuk sistem rekomendasi yang mampu menghasilkan rekomendasi lebih relevan dalam konteks e-commerce.

**Pentingnya Proyek**

Di tengah banyaknya pilihan produk yang tersedia, sistem rekomendasi dapat membantu pengguna menyaring informasi dan menemukan item yang sesuai dengan preferensi atau kebutuhan mereka secara efisien. Oleh karena itu, proyek ini penting untuk dilakukan. Tidak hanya itu, dengan proyek ini kita dapat membantu pengguna menghindari kebingungan akibat banyaknya produk, mempercepat proses pencarian produk yang relevan, dan memberikan rekomendasi yang lebih tepat (yang pengguna inginkan).

**Referensi**

[1] Adomavicius, G., & Tuzhilin, A. (2005). Toward the next generation of recommender systems: A survey of the state-of-the-art and possible extensions. In IEEE Transactions on Knowledge and Data Engineering (Vol. 17, Issue 6). https://doi.org/10.1109/TKDE.2005.99

[2] Chen, L., Chen, G., & Wang, F. (2015). Recommender systems based on user reviews: the state of the art. User Modeling and User-Adapted Interaction, 25(2). https://doi.org/10.1007/s11257-015-9155-5

[3] Bobadilla, J., Ortega, F., Hernando, A., & Gutiérrez, A. (2013). Recommender systems survey. ACM Computing Surveys (CSUR), 49(2), 1–35. https://doi.org/10.1145/2554850

## Business Understanding

### Problem Statements
- Terlalu banyaknya jumlah produk di platform e-commerce menyebabkan pengguna cukup bingung mana produk yang mau dibeli. Hal ini membuat proses pencarian menjadi lebih rumit dan memakan waktu karena pengguna harus menelusuri banyak pilihan, membandingkan fitur, harga, dan ulasan, sehingga seringkali mereka merasa kewalahan dan akhirnya tidak mendapatkan produk yang paling tepat.
- Informasi produk yang sangat banyak dapat menimbulkan information overload (saat pencarian produk), sehingga menyulitkan pengguna dalam menyaring produk yang relevan secara efisien. Terkadang juga pada saat pencarian produk, sering muncul produk yang tidak sesuai dengan apa yang dicari. Pengguna menjadi kesulitan untuk memproses berbagai informasi yang tersedia sehingga dapat mengurangi kepuasan mereka dalam berbelanja. 

### Goals
- Mempermudah pengguna dalam menemukan produk yang cocok dengan keinginan mereka (dari data ulasan, pembelian, dan data produk) melalui sistem rekomendasi yang lebih tepat dan relevan di platform e-commerce secara cepat. Dengan demikian, pengguna tidak perlu lagi untuk membuang waktu menelusuri banyak pilihan seperti melihat ulasan karena produk yang direkomendasi oleh sistem pasti ada pengguna yang pernah memberi ulasan tinggi.
- Mengatasi kesulitan pengguna dalam mengelola banyaknya informasi produk dengan menampilkan hasil sistem rekomendasi pilihan produk yang mirip dengan preferensi personal sehingga mengeliminasi produk-produk yang berpotensi tidak menarik bagi pengguna. Alhasil, perngguna akan lebih leluasa untuk memilih produk selanjutnya yang akan dibeli.

### Solution Statements
- Mengimplementasikan pendekatan content-based filtering dengan memanfaatkan informasi produk seperti nama produk, deskripsi, atau kategori, untuk merekomendasikan produk yang mirip dengan apa yang pernah dibeli atau dicari oleh pengguna. Sistem ini menganalisis fitur konten dari item (misalnya genre film atau kategori produk) dan mencocokkannya dengan preferensi pengguna. Content-based filtering digunakan karena dapat memberikan rekomendasi yang dipersonalisasi, sehingga bisa memberikan apa yang pengguna mau.
- Mengimplementasikan pendekatan collaborative filtering dengan menganalisis perilaku pengguna lain yang memiliki pola interaksi serupa. Dengan kata lain, sistem ini menyimpulkan bahwa jika pengguna A dan pengguna B menyukai item yang sama, maka item lain yang disukai B kemungkinan juga akan disukai A.

## Data Understanding
Dataset yang digunakan dalam proyek ini diambil dari [Kaggle E-Commerce Dataset](https://www.kaggle.com/datasets/shivrajguvi/e-commerce-dataset-for-practice) dan merupakan simulasi transaksi pengguna yang mencakup informasi pengguna, produk, transaksi, dan perilaku pengguna. Dataset ini terdiri 100.000 baris dan 21 fitur/kolom yaitu:
- UserID: Identifikasi unik untuk setiap pengguna.
- UserName: Nama pengguna yang disimulasikan.
- Age: Usia pengguna (antara 18 hingga 70 tahun).
- Gender: Jenis kelamin pengguna (Male, Female, atau Non-Binary).
- Country: Negara asal pengguna (USA, Canada, UK, Australia, India, Germany).
- SignUpDate: Tanggal pengguna mendaftar di platform.
- ProductID: Identifikasi unik untuk setiap produk.
- ProductName: Nama produk yang dibeli (misalnya: Laptop, Smartphone, Headphones, dsb.).
- Category: Kategori produk (Electronics, Apparel, Books, Accessories).
- Price: Harga produk ($)
- PurchaseDate: Tanggal transaksi dilakukan.
- Quantity: Jumlah unit produk yang dibeli dalam satu transaksi.
- TotalAmount: Total nominal yang dibelanjakan oleh pengguna (Price * Quantity).
- HasDiscountApplied: Menunjukkan apakah diskon diterapkan dalam transaksi (True/False).
- DiscountRate: Besarnya diskon yang diberikan (antara 0 hingga 0.5).
- ReviewScore: Skor ulasan yang diberikan pengguna untuk produk (1 hingga 5).
- ReviewText: Ulasan dalam bentuk teks singkat (Excellent, Good, Average, Poor).

### Exploratory Data Analysis
Tujuan dari EDA adalah untuk memperoleh wawasan awal yang mendalam mengenai data dan menentukan langkah selanjutnya dalam analisis atau pemodelan. Beberapa tahapan EDA yang akan dilakukan adalah pemahaman terhadap struktur data, analisis setiap fitur, pengecekan data duplikat dan nilai null, analisis univariate serta analisis outlier data.

```
df.info()
```
Output:
```
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 100000 entries, 0 to 99999
Data columns (total 21 columns):
 #   Column              Non-Null Count   Dtype  
---  ------              --------------   -----  
 0   UserID              100000 non-null  int64  
 1   UserName            100000 non-null  object 
 2   Age                 100000 non-null  int64  
 3   Gender              100000 non-null  object 
 4   Country             100000 non-null  object 
 5   SignUpDate          100000 non-null  object 
 6   ProductID           100000 non-null  int64  
 7   ProductName         100000 non-null  object 
 8   Category            100000 non-null  object 
 9   Price               100000 non-null  float64
 10  PurchaseDate        100000 non-null  object 
 11  Quantity            100000 non-null  int64  
 12  TotalAmount         100000 non-null  float64
 13  HasDiscountApplied  100000 non-null  bool   
 14  DiscountRate        100000 non-null  float64
 15  ReviewScore         100000 non-null  float64
 16  ReviewText          100000 non-null  object 
 17  LastLogin           100000 non-null  object 
 18  SessionDuration     100000 non-null  float64
 19  DeviceType          100000 non-null  object 
 20  ReferralSource      100000 non-null  object 
dtypes: bool(1), float64(5), int64(4), object(11)
memory usage: 15.4+ MB
```
Terdapat 21 fitur pada dataset ecommerce yang digunakan. Fitur tersebut terdiri dari 12 fitur dengan tipe string, 4 fitur dengan tipe integer, dan 5 fitur dengan tipe float. Dataset terdiri dari 100.000 row.

### Eksplor Parameter Statistik

```
df.describe(include="all")
```
Output:
| Column Name    | Count      | Unique   | Top Value     | Freq   | Mean      | Std Dev   | Min   | 25%       | 50%       | 75%       | Max      |
|----------------|------------|----------|---------------|--------|-----------|-----------|--------|-----------|-----------|-----------|-----------|
| UserID         | 100000     | –        | –             | –      | 50000.50  | 28867.66  | 1      | 25000.75  | 50000.50  | 75000.25  | 100000   |
| UserName       | 100000     | 100000   | User_99984    | 1      | –         | –         | –      | –         | –         | –         | –        |
| Age            | 100000     | –        | –             | –      | 43.46     | 14.98     | 18     | 31        | 43        | 56        | 69       |
| Gender         | 100000     | 3        | Non-Binary    | 33538  | –         | –         | –      | –         | –         | –         | –        |
| Country        | 100000     | 6        | USA           | 16844  | –         | –         | –      | –         | –         | –         | –        |
| SignUpDate     | 100000     | 1096     | 2022-01-17    | 125    | –         | –         | –      | –         | –         | –         | –        |
| ProductID      | 100000     | –        | –             | –      | 5508.12   | 2606.54   | 1000   | 3228      | 5520      | 7776      | 9998     |
| ProductName    | 100000     | 7        | T-shirt       | 14401  | –         | –         | –      | –         | –         | –         | –        |
| Category       | 100000     | 4        | Apparel       | 25201  | –         | –         | –      | –         | –         | –         | –        |
| Price          | 100000     | –        | –             | –      | 505.63    | 286.14    | 10     | 257.14    | 505.95    | 753.73    | 999.98   |
| PurchaseDate        | 100000     | 366      | 2021-07-16                | 316    | –        | –         | –      | –       | –       | –       | –        |
| Quantity            | 100000     | –        | –                         | –      | 2.50     | 1.12      | 1      | 1       | 2       | 4       | 4        |
| TotalAmount         | 100000     | –        | –                         | –      | 1260.85  | 964.10    | 10.02  | 494.68  | 966.08  | 1850.33 | 3999.72  |
| HasDiscountApplied  | 100000     | 2        | False                     | 50221  | –        | –         | –      | –       | –       | –       | –        |
| DiscountRate        | 100000     | –        | –                         | –      | 0.25     | 0.14      | 0      | 0.13    | 0.25    | 0.37    | 0.50     |
| ReviewScore         | 100000     | –        | –                         | –      | 4.01     | 1.00      | -0.60  | 3.30    | 4.00    | 4.70    | 8.60     |
| ReviewText          | 100000     | 4        | Excellent                 | 25035  | –        | –         | –      | –       | –       | –       | –        |
| LastLogin           | 100000     | 100000   | 2024-09-11 04:04:28.072330| 1      | –        | –         | –      | –       | –       | –       | –        |
| SessionDuration     | 100000     | –        | –                         | –      | 62.41    | 33.18     | 5      | 33.72   | 62.42   | 91.04   | 120.00   |
| DeviceType          | 100000     | 3        | Mobile                    | 33568  | –        | –         | –      | –       | –       | –       | –        |
| ReferralSource      | 100000     | 4        | Email Marketing           | 25154  | –        | –         | –      | –       | –       | –       | –        |

**Insight:**

- Terdapat 3 jenis kelamin pada dataset yang kemungkinan karena mengikuti gaya hidup barat (non-binary).
- Mayoritas pelanggan dari ecommerce berasal dari USA dengan 16844 pelanggan.
- Barang yang paling sering dibeli adalah T-Shirt dan kategori yang paling menjual adalah Apparel.
- Orang-orang sering melakukan pembelian barang dari ecommerce melalui mobile atau ponsel.
- Referal aplikasi ecommerce kebanyakan didapatkan dari marketing email yang ditujukan pada pelanggan, sehingga menandakan bahwa teknik marketing ini cukup bagus.
- Pada kolom ReviewScore, terdapat data yang abnormal yaitu reviewnya bernilai negatif. Range dari nilai review juga salah karena range harusnya dari 1-5, sehingga nilai rating yang lebih dari 5 itu salah. Maka, ini harus ditangani pada tahap preprocessing nanti.

### Pengecekan Data Nil dan Data Duplikat

```
df.isna().sum()
```
Output:


| Column Name           | Missing Values |
|------------------------|----------------|
| UserID                | 0              |
| UserName              | 0              |
| Age                   | 0              |
| Gender                | 0              |
| Country               | 0              |
| SignUpDate            | 0              |
| ProductID             | 0              |
| ProductName           | 0              |
| Category              | 0              |
| Price                 | 0              |
| PurchaseDate          | 0              |
| Quantity              | 0              |
| TotalAmount           | 0              |
| HasDiscountApplied    | 0              |
| DiscountRate          | 0              |
| ReviewScore           | 0              |
| ReviewText            | 0              |
| LastLogin             | 0              |
| SessionDuration       | 0              |
| DeviceType            | 0              |
| ReferralSource        | 0              |

Tidak ada data null

```
df.duplicated().sum()
```
Output:
```
np.int64(0)
```

### Analisis Fitur Country
```
df['Country'].value_counts()
```
Output:
| Country   | Count |
|-----------|-------|
| USA       | 16,844 |
| Canada    | 16,767 |
| UK        | 16,699 |
| Germany   | 16,582 |
| Australia | 16,570 |
| India     | 16,538 |

Pengguna berasal dari enam negara utama yaitu: USA, Canada, UK, Germany, Australia, dan India. Jumlah pengguna juga seimbang dengan sekitar +/- 16.500 pengguna per negara. Hal ini menandakan bahwa produk memiliki jangkauan global yang merata. Mayoritas pengguna berasal dari USA sebanyak 16844 pengguna.

### Analisis Fitur ProductName
```
df['ProductName'].value_counts()
```
Output: 
| Product Name | Count  |
|--------------|--------|
| T-shirt      | 14,401 |
| Headphones   | 14,396 |
| Book         | 14,360 |
| Watch        | 14,287 |
| Shoes        | 14,261 |
| Laptop       | 14,169 |
| Smartphone   | 14,126 |

```
plt.figure(figsize=(8, 5))
sns.countplot(x=df['ProductName'])
plt.title('Product Name')
```
Output: 

![image](https://github.com/user-attachments/assets/abfd34d4-16a0-43ea-9615-c753ad677f92)

Produk yang paling banyak dibeli adalah T-shirt dengan 14.401 pembelian dan diikuti sangat dekat oleh Headphones, Book, Watch, Shoes, Laptop, dan Smartphone. Namun, produk yang dibeli cukup seimbang untuk semua tipe produk. Ini menandakan bahwa pelanggan menunjukkan minat yang seimbang terhadap berbagai jenis barang.

### Analisis Fitur Category
```
df['Category'].value_counts()
```
Output:
| Category     | Count  |
|--------------|--------|
| Apparel      | 25,201 |
| Accessories  | 25,015 |
| Electronics  | 24,936 |
| Books        | 24,848 |

```
plt.figure(figsize=(8, 5))
sns.countplot(x=df['Category'])
plt.title('Category')
```
Output:

![image](https://github.com/user-attachments/assets/24526519-d9dc-414a-987f-ab269c484aad)

Kategori produk yang paling banyak diminati adalah Apparel yang kemudian diikuti dengan Accessories, Electronics, dan Books. Semua kategori juga seimbang yang menunjukkan bahwa konsumen memiliki preferensi yang cukup merata terhadap berbagai kategori.

### Analisis Fitur ReferralSource
```
df['ReferralSource'].value_counts()
```
Output:
| Referral Source  | Count  |
|------------------|--------|
| Email Marketing  | 25,154 |
| Ad Campaign      | 25,087 |
| Organic Search   | 25,021 |
| Social Media     | 24,738 |

```
plt.figure(figsize=(8, 5))
sns.countplot(x=df['ReferralSource'])
plt.title('Referral Source')
```
Output:

![image](https://github.com/user-attachments/assets/36e95a1f-d73a-4550-bd87-9d9d8d844106)

Dapat dilihat bahwa ada 4 metode referal yang digunakan oleh platform ecommerce dari dataset ini, dengan metode paling tinggi Email Marketing, diikuti oleh Ad Campaign, Organic Search dan Sosial Media.

### Analisis Fitur ReviewText
```
df['ReviewText'].value_counts()
```
Output:
| Review Text | Count  |
|-------------|--------|
| Excellent   | 25,035 |
| Good        | 25,029 |
| Poor        | 24,978 |
| Average     | 24,958 |

```
plt.figure(figsize=(8, 5))
sns.countplot(x=df['ReviewText'])
plt.title('Review Text')
```
Output:

![image](https://github.com/user-attachments/assets/2f93366b-8f3e-4573-b742-997217594849)

Terdapat 4 tipe review yang ada pada dataset ecommerce yaitu Excellent, Good, Poor, dan Average. Mayoritas review bernilai Excellent yang berarti banyak yang puas dengan transaksi pembelian mereka.

### Analisis Fitur ReviewScore dengan ReviewText
```
# Melihat kaitan ReviewText dan ReviewScore (Apakah ReviewText buruk berarti ReviewScore Rendah? Dan sebaliknya?)
# Jika iya, maka harusnya tidak ada hasil untuk kode di bawah
df[(df['ReviewText'] == 'Poor') & (df['ReviewScore'] > 7)].head(5)
```
Output:
| UserID | UserName   | Age | Gender     | Country | SignUpDate | ProductID | ProductName | Category    | Price  | PurchaseDate | Quantity | TotalAmount | HasDiscountApplied | DiscountRate | ReviewScore | ReviewText | LastLogin                  | SessionDuration | DeviceType | ReferralSource |
|--------|------------|-----|------------|---------|------------|-----------|-------------|-------------|--------|---------------|----------|--------------|---------------------|---------------|--------------|-------------|----------------------------|------------------|-------------|----------------|
| 563    | User_563   | 45  | Non-Binary | Canada  | 2022-03-16 | 8122      | Headphones  | Apparel     | 735.88 | 2021-03-17    | 2        | 1471.76      | True                | 0.02          | 8.0          | Poor        | 2024-01-08 04:04:27.593931 | 10.26            | Tablet      | Organic Search  |
| 683    | User_683   | 40  | Non-Binary | Canada  | 2020-06-06 | 3709      | Laptop      | Electronics | 375.39 | 2021-01-28    | 3        | 1126.17      | False               | 0.49          | 7.1          | Poor        | 2024-03-30 04:04:27.594409 | 109.28           | Desktop     | Ad Campaign     |
| 2191   | User_2191  | 42  | Female     | Canada  | 2021-05-29 | 5305      | T-shirt     | Electronics | 279.25 | 2021-07-01    | 1        | 279.25       | False               | 0.42          | 7.7          | Poor        | 2024-02-21 04:04:27.601014 | 15.18            | Tablet      | Organic Search  |
| 10362  | User_10362 | 35  | Female     | UK      | 2021-12-02 | 8707      | Headphones  | Accessories | 432.28 | 2021-05-13    | 4        | 1729.12      | False               | 0.50          | 7.2          | Poor        | 2024-02-02 04:04:27.634616 | 106.94           | Desktop     | Social Media    |
| 10568  | User_10568 | 68  | Male       | Germany | 2022-09-04 | 7051      | Smartphone  | Accessories | 223.15 | 2021-01-15    | 3        | 669.45       | True                | 0.08          | 7.3          | Poor        | 2024-01-22 04:04:27.635456 | 8.25             | Tablet      | Organic Search  |

Setelah tabel di atas dianalisis, dapat disimpulkan bahwa ReviewScore dan ReviewText tidak memiliki kaitan yang berbanding lurus. Sehingga, kita kemungkinan hanya akan menggunakan ReviewScore untuk pembangunan model nantinya.

### Analisis ReviewScore (Cek Data Abnormal)
```
#Melihat ReviewScore yang tidak berada di range 1-5
df[(df['ReviewScore'] > 5) | (df['ReviewScore'] < 1)]
```
Output:
| UserID | UserName   | Age | Gender     | Country   | SignUpDate | ProductID | ProductName | Category    | Price  | PurchaseDate | Quantity | TotalAmount | HasDiscountApplied | DiscountRate | ReviewScore | ReviewText | LastLogin                  | SessionDuration | DeviceType | ReferralSource |
|--------|------------|-----|------------|-----------|------------|-----------|-------------|-------------|--------|---------------|----------|--------------|---------------------|---------------|--------------|-------------|----------------------------|------------------|-------------|----------------|
| 1      | User_1     | 39  | Male       | UK        | 2021-02-01 | 8190      | Shoes       | Books       | 532.37 | 2021-02-25    | 1        | 532.37       | False               | 0.02          | 5.1          | Excellent   | 2024-05-03 04:04:27.591583 | 45.02            | Mobile      | Social Media    |
| 2      | User_2     | 25  | Female     | Canada    | 2020-12-04 | 9527      | T-shirt     | Accessories | 848.83 | 2021-09-22    | 1        | 848.83       | True                | 0.29          | 5.1          | Excellent   | 2024-08-31 04:04:27.591606 | 13.83            | Mobile      | Social Media    |
| 5      | User_5     | 23  | Female     | Canada    | 2021-11-06 | 1389      | Shoes       | Books       | 331.82 | 2021-01-12    | 1        | 331.82       | False               | 0.02          | 5.1          | Average     | 2024-07-02 04:04:27.591619 | 14.99            | Tablet      | Email Marketing |
| 10     | User_10    | 47  | Non-Binary | UK        | 2020-01-31 | 4719      | Book        | Electronics | 250.35 | 2021-01-19    | 1        | 250.35       | True                | 0.25          | 5.2          | Good        | 2024-08-06 04:04:27.591640 | 71.17            | Tablet      | Organic Search  |
| 11     | User_11    | 63  | Female     | Australia | 2022-05-01 | 4576      | Smartphone  | Apparel     | 567.15 | 2021-12-07    | 2        | 1134.30      | False               | 0.11          | 6.2          | Poor        | 2024-09-03 04:04:27.591644 | 37.03            | Mobile      | Social Media    |
|...|...|...|...|...|...|...|...|...|...|...|...|...|...|...|...|...|...|...|...|...|
| 99971   | User_99971   | 49  | Female     | India   | 2020-10-28 | 9331      | Watch       | Apparel     | 981.05 | 2021-06-25    | 4        | 3924.20      | True                | 0.35          | 5.1          | Good        | 2024-10-07 04:04:28.072272 | 88.88            | Desktop     | Organic Search  |
| 99974   | User_99974   | 44  | Non-Binary | UK      | 2020-01-07 | 3694      | Book        | Books       | 863.19 | 2021-09-05    | 4        | 3452.76      | False               | 0.49          | 5.9          | Excellent   | 2024-08-16 04:04:28.072288 | 34.85            | Desktop     | Organic Search  |
| 99980   | User_99980   | 19  | Female     | Germany | 2022-07-19 | 4452      | Book        | Books       | 139.32 | 2021-03-03    | 2        | 278.64       | False               | 0.16          | 6.1          | Average     | 2024-04-20 04:04:28.072314 | 34.54            | Mobile      | Ad Campaign     |
| 99991   | User_99991   | 51  | Male       | USA     | 2022-08-20 | 4917      | Laptop      | Accessories | 45.94  | 2021-10-01    | 2        | 91.88        | False               | 0.15          | 6.3          | Good        | 2024-06-16 04:04:28.072357 | 74.74            | Tablet      | Email Marketing |
| 99997   | User_99997   | 53  | Non-Binary | Canada  | 2020-07-28 | 6555      | T-shirt     | Electronics | 672.12 | 2021-10-29    | 3        | 2016.36      | True                | 0.42          | 5.4          | Excellent   | 2024-04-16 04:04:28.072381 | 60.98            | Tablet      | Social Media    |

Terdapat 14898 data yang tidak berada dalam range 1-5 dan kita harus drop data tersebut dikarenakan tidak bisa diperbaiki menggunakan IQR atau metode lain. Sangat disayangkan namun tidak masalah karena jumlah data masih banyak jika terdapat 15.000 data yang di drop.

### Analisis ProductName dengan Category
```
#Melihat apakah ProductName sesuai dengan Category (Cth: T-shirt = Apparel, Smartphone = Electronics)
df[(df['ProductName'] == 'Smartphone') & (df['Category'] != 'Electronics')].head(5)
```
Output:
| UserID | UserName | Age | Gender     | Country   | SignUpDate | ProductID | ProductName | Category    | Price  | PurchaseDate | Quantity | TotalAmount | HasDiscountApplied | DiscountRate | ReviewScore | ReviewText | LastLogin               | SessionDuration | DeviceType | ReferralSource   |
|--------|----------|-----|------------|-----------|------------|-----------|-------------|-------------|--------|--------------|----------|-------------|--------------------|--------------|-------------|------------|------------------------|-----------------|------------|------------------|
| 5      | User_6   | 54  | Male       | USA       | 2021-04-04 | 1524      | Smartphone  | Apparel     | 939.70 | 2021-08-05   | 1        | 939.70      | False              | 0.21         | 4.6         | Poor       | 2024-09-26 04:04:27.591623 | 37.30          | Mobile     | Social Media     |
| 10     | User_11  | 63  | Female     | Australia | 2022-05-01 | 4576      | Smartphone  | Apparel     | 567.15 | 2021-12-07   | 2        | 1134.30     | False              | 0.11         | 6.2         | Poor       | 2024-09-03 04:04:27.591644 | 37.03          | Mobile     | Social Media     |
| 12     | User_13  | 31  | Non-Binary | Canada    | 2020-12-29 | 7529      | Smartphone  | Apparel     | 190.95 | 2021-06-04   | 3        | 572.85      | True               | 0.11         | 2.5         | Poor       | 2024-06-11 04:04:27.591656 | 23.75          | Tablet     | Email Marketing  |
| 13     | User_14  | 68  | Male       | Canada    | 2020-03-01 | 2204      | Smartphone  | Accessories | 88.11  | 2021-09-06   | 4        | 352.44      | True               | 0.11         | 3.1         | Excellent  | 2024-03-24 04:04:27.591660 | 19.92          | Desktop    | Social Media     |
| 18     | User_19  | 38  | Male       | Canada    | 2022-05-25 | 6620      | Smartphone  | Accessories | 191.30 | 2021-12-24   | 4        | 765.20      | True               | 0.45         | 4.4         | Excellent  | 2024-08-22 04:04:27.591679 | 55.56          | Desktop    | Organic Search   |

Terdapat data yang abnormal dimana Smartphone menjadi kategori Apparel, padahal seharusnya masuk ke kategori Electronics. Hal yang sama terjadi pada banyak data. Oleh karena itu kita akan mengubah kolom Category sesuai dengan nama produk.

### Visualisasi Boxplot ReviewScore & Age (Cek Outlier)
```
plt.figure(figsize=(15, 5))

plt.subplot(1, 3, 2)
sns.boxplot(x=df['ReviewScore'])
plt.title('Review Score')

plt.subplot(1, 3, 3)
sns.boxplot(x=df['Age'])
plt.title('Age')
```
Output:

![image](https://github.com/user-attachments/assets/fd4aabbd-c8f9-4220-bdac-c3a18ba14746)

Terdapat banyak outlier pada fitur ReviewScore, yang menandakan data abnormal seperti adanya banyak review negatif pada data. Untuk fitur age, tidak ada outlier dan semuanya normal.

## Data Preparation
Pada bagian ini Anda menerapkan dan menyebutkan teknik data preparation yang dilakukan. Teknik yang digunakan pada notebook dan laporan harus berurutan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan proses data preparation yang dilakukan
- Menjelaskan alasan mengapa diperlukan tahapan data preparation tersebut.

## Modeling
Tahapan ini membahas mengenai model sisten rekomendasi yang Anda buat untuk menyelesaikan permasalahan. Sajikan top-N recommendation sebagai output.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menyajikan dua solusi rekomendasi dengan algoritma yang berbeda.
- Menjelaskan kelebihan dan kekurangan dari solusi/pendekatan yang dipilih.

## Evaluation
Pada bagian ini Anda perlu menyebutkan metrik evaluasi yang digunakan. Kemudian, jelaskan hasil proyek berdasarkan metrik evaluasi tersebut.

Ingatlah, metrik evaluasi yang digunakan harus sesuai dengan konteks data, problem statement, dan solusi yang diinginkan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan formula metrik dan bagaimana metrik tersebut bekerja.



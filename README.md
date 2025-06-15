# Laporan Proyek Machine Learning - Rafii Ahmad Fahreza

## Domain Proyek

Dalam beberapa tahun terakhir, terutama pasca pandemi COVID-19, dunia kerja mengalami perubahan signifikan dengan meningkatnya adopsi sistem kerja *remote* dan *hybrid*[1][2]. Pergeseran ini tidak hanya mengubah cara bekerja, tetapi juga menimbulkan tantangan baru dalam hal penentuan struktur penggajian[3]. Ketika batasan geografis menjadi semakin kabur, muncul pertanyaan tentang seberapa besar pengaruh lokasi, pengalaman, dan jenis pekerjaan terhadap besaran gaji[4][5]. Apakah pekerja *remote* di negara berkembang harus dibayar lebih rendah daripada mereka yang tinggal di pusat ekonomi global, meskipun memiliki keterampilan serupa? Bagaimana perusahaan dapat menetapkan gaji yang adil dan kompetitif dalam konteks kerja lintas batas ini? Proyek ini bertujuan untuk membangun model prediktif yang dapat memperkirakan besaran gaji tahunan berdasarkan berbagai karakteristik pekerjaan seperti jabatan, industri, lokasi, pengalaman kerja, dan fleksibilitas kerja. Pendekatan ini tidak hanya penting untuk membantu perusahaan dalam pengambilan keputusan berbasis data, tetapi juga memberi wawasan kepada para pekerja dalam memahami nilai pasar mereka di era kerja jarak jauh.

[1] Bulut, S., & Maimaiti, R. (2021). Remote working in the period of the COVİD-19. https://doi.org/10.30564/JPR.V3I1.2898 <br>
[2] A. Wontorczyk and B. Roznowski, “Remote, Hybrid, and On-Site Work during the SARS-CoV-2 Pandemic and the Consequences for Stress and Work Engagement,” International Journal of Environmental Research and Public Health, Feb. 2022, doi: 10.3390/ijerph19042400. <br>
[3] Best, S. (2021). The future of work: Remote work in the emerging new normal. Business Management Review. https://doi.org/10.24052/BMR/V121NU01/ART-27<br>
[4] Deneva, A., Hristova, V., Pavlov, D., Blazheva, V., Kostov, I., Angelova, D., & Petrova, M. (2022). The Geographical Location as a Limitation for Starting Entrepreneurial Initiatives and Career Development. European Journal of Sustainable Development. https://doi.org/10.14207/ejsd.2022.v11n3p124<br>
[5] J. Morales-Arilla and C. Daboin, “Is remote work in high demand? Evidence from job postings during COVID-19,” Jun. 2021. doi: 10.1145/3460112.3471984.<br>

## Business Understanding

### Problem Statements

Transformasi sistem kerja menuju model *remote*, *hybrid*, dan *onsite* memunculkan tantangan baru dalam pengelolaan struktur gaji. Tanpa standar yang jelas, perusahaan sering kali menetapkan gaji berdasarkan asumsi atau pendekatan tradisional yang kurang relevan dalam konteks kerja jarak jauh. Akibatnya, muncul ketimpangan dalam kompensasi berdasarkan lokasi, jabatan, atau tingkat pengalaman yang tidak sepenuhnya mencerminkan nilai sebenarnya dari peran tersebut.

### Goals

Proyek ini bertujuan untuk membangun model prediktif yang dapat memperkirakan gaji tahunan berdasarkan fitur-fitur pekerjaan seperti jabatan, industri, lokasi, jenis pekerjaan, fleksibilitas kerja, dan pengalaman kerja. Model ini diharapkan dapat memberikan wawasan objektif bagi perusahaan dalam menyusun struktur penggajian yang adil serta membantu individu dalam memahami ekspektasi gaji berdasarkan profil profesional mereka.

### Solution Statements

Untuk mencapai tujuan tersebut, proyek ini akan:
1.  Mengembangkan dua model prediksi menggunakan algoritma yang berbeda, yaitu Random Forest Regressor dan Gradient Boosting (XGBoost).
2.  Memilih model terbaik berdasarkan metrik regresi seperti MAE, RMSE, dan R² Score.

## Data Understanding

Dataset yang digunakan dalam proyek ini berjudul “Work From Anywhere Salary Data”, yang terdiri dari 500 data terstruktur mengenai individu yang bekerja secara *remote*, *hybrid*, maupun *onsite*. Data ini mencakup berbagai jabatan, industri, tingkat pengalaman, lokasi kerja, serta informasi mengenai penggajian. Dataset ini bersifat sintetis namun merepresentasikan pola dan tren yang lazim di dunia kerja global saat ini.

Sumber Data: [https://raw.githubusercontent.com/rfahreza/Predictive-Analytic/main/Work_From_Anywhere_Salary_Data.csv](https://raw.githubusercontent.com/rfahreza/Predictive-Analytic/main/Work_From_Anywhere_Salary_Data.csv)

### Variabel-variabel pada dataset adalah sebagai berikut:

* **Company**: Nama organisasi tempat individu bekerja.
* **Job Title**: Jabatan individu (misalnya: Software Engineer, Product Manager).
* **Industry**: Sektor industri (misalnya: Teknologi, Finansial, Kesehatan).
* **Location**: Lokasi geografis kerja (kota dan/atau negara).
* **Employment Type**: Jenis pekerjaan (Full-time, Part-time, Contract, Internship).
* **Experience Level**: Tingkat senioritas (Entry, Mid, Senior, Lead).
* **Remote Flexibility**: Tipe kerja: Remote, Hybrid, atau Onsite.
* **Salary (Annual)**: Gaji tahunan kotor sebelum pajak.
* **Currency**: Mata uang pembayaran gaji (misalnya: USD, EUR, INR).
* **Years of Experience**: Total tahun pengalaman profesional individu.
* **Job Satisfaction Score (1–10)**: Skor kepuasan kerja individu dari 1 (sangat tidak puas) hingga 10 (sangat puas).
* **Tech Stack**: Teknologi yang digunakan (misalnya: Python, JavaScript, SQL, dsb.).
* **Perks**: Tunjangan tambahan yang diberikan (misalnya: asuransi, WFH allowance).
* **Last Promotion (Years Ago)**: Jumlah tahun sejak terakhir kali individu dipromosikan.

## Data Preparation

### Memeriksa Missing Value

Tidak terdapat *missing value* pada *dataset* ini. Pemeriksaan *missing value* ini penting untuk menjaga kualitas data dan akurasi model prediktif.

### Memeriksa Data Duplikat

Tidak terdapat data yang duplikat pada *dataset* ini. Pemeriksaan data duplikat dilakukan untuk menjaga kualitas data, menghemat ruang penyimpanan, mempercepat proses, dan agar tidak terjadi bias dalam analisis.

### Transformasi (Konversi Mata Uang dan Encoding)

* **Konversi Mata Uang:** Kolom `Salary (Annual)` dan `Currency` diubah menjadi satu kolom `Salary (USD)` untuk menyeragamkan satuan gaji, menggunakan nilai tukar yang telah ditentukan. Kolom `Salary (Annual)` dan `Currency` kemudian dihapus.
* **Encoding Fitur Kategorikal:** Kolom `Company`, `Job Title`, `Location`, `Industry`, `Experience Level`, `Remote Flexibility`, dan `Employment Type` diubah menjadi bentuk numerik menggunakan `LabelEncoder`.
* **Penghapusan Kolom:** Kolom `Tech Stack` dan `Perks` dihapus karena tidak digunakan untuk prediksi.

### Memeriksa Data Outlier

Setelah transformasi data, tidak ditemukan adanya *outlier* pada *dataset*. Hal ini dikonfirmasi melalui deteksi IQR dan visualisasi *boxplot* untuk fitur-fitur numerik yang relevan.

### Data Cleansing

Tidak ada proses pembersihan data yang dilakukan karena dataset sudah terbukti bersih dari *missing value*, duplikat, dan *outlier*.

### Univariate Analysis (EDA)

* **Secara keseluruhan**, distribusi fitur pada data ini cukup merata di tiap kolom.
* **Years of Experience**: Distribusi pengalaman tersebar cukup merata dari 0 hingga sekitar 15 tahun, namun sedikit lebih rendah pada tahun-tahun awal (0-2 tahun) dan sekitar 5-7 tahun.
* **Job Satisfaction Score (1-10)**: Skor kepuasan kerja relatif merata di seluruh rentang 1 hingga 10, menunjukkan beragam tingkat kepuasan tanpa satu skor yang mendominasi.
* **Last Promotion (Years Ago)**: Mayoritas promosi terjadi dalam 0-1 tahun terakhir, menunjukkan pola promosi yang relatif sering atau baru saja terjadi di antara para pekerja dalam dataset.
* **Salary (USD)**: Mayoritas gaji terkonsentrasi pada rentang yang lebih rendah (di bawah \$50.000), dengan distribusi yang sangat miring ke kanan. Hal ini berbeda dari visualisasi awal `Salary (Annual)` dan dimungkinkan setelah disamakannya mata uang yang digunakan serta dipengaruhi konversi dari AUD dan INR yang cukup rendah, mengingat pekerja yang menggunakan mata uang tersebut cukup banyak.
* **Variabel Kategorikal/Diskrit (Company, Job Title, Industry, Location, Employment Type, Experience Level)**: Menunjukkan distribusi yang relatif seragam atau merata di antara kategori-kategori mereka.

### Multivariative Analysis (EDA)

* **Gaji vs Perusahaan (Company)**: Tidak ada korelasi linear yang jelas atau pola signifikan yang terlihat. Gaji menunjukkan variasi yang sangat luas (dari rendah hingga tinggi) di setiap kategori perusahaan. Ini mengindikasikan bahwa gaji tidak ditentukan secara langsung oleh perusahaan, dan ada rentang gaji yang lebar dalam setiap perusahaan.
* **Gaji vs Posisi Pekerjaan (Job Title)**: Mirip dengan perusahaan, tidak ada korelasi linear yang jelas. Gaji sangat bervariasi di setiap kategori posisi pekerjaan. Ini menunjukkan bahwa gaji tidak secara langsung tergantung pada jenis posisi pekerjaan yang spesifik dalam konteks linear.
* **Gaji vs Industri (Industry)**: Tidak ada pola linear atau korelasi yang menonjol. Setiap kategori industri menunjukkan rentang gaji yang luas dari nilai rendah hingga tinggi. Ini berarti industri saja tidak secara langsung menunjukkan hubungan linear yang kuat dengan tingkat gaji.
* **Gaji vs Tipe Pekerjaan (Employment Type)**: Tidak ada korelasi linear yang jelas. Gaji memiliki variasi yang luas di setiap tipe pekerjaan. Ini mengindikasikan bahwa tipe pekerjaan tertentu tidak secara langsung berkorelasi secara linear dengan tingkat gaji.
* **Gaji vs Pengalaman Kerja (Tahun)**: Tidak ada korelasi linear positif yang kuat. Meskipun ada individu dengan pengalaman tinggi yang memiliki gaji tinggi, ada juga individu dengan pengalaman rendah yang memiliki gaji tinggi, dan sebaliknya. Titik-titik tersebar cukup acak, menunjukkan bahwa pengalaman kerja saja tidak selalu berkorelasi secara linear dengan gaji yang lebih tinggi.
* **Gaji vs Skor Kepuasan Kerja**: Tidak ada pola linear atau korelasi yang jelas. Gaji menunjukkan rentang yang sangat luas untuk setiap skor kepuasan kerja. Artinya, gaji tidak berkorelasi secara linear dengan tingkat kepuasan kerja.
* **Gaji vs Terakhir Promosi (Tahun Lalu)**: Tidak ada korelasi linear yang jelas. Gaji bervariasi secara luas terlepas dari berapa tahun yang lalu seseorang terakhir dipromosikan. Seseorang yang baru dipromosikan bisa memiliki gaji rendah atau tinggi, sama seperti yang sudah lama tidak dipromosikan.
* **Kesimpulan Umum Multivariat**: Sebagian besar fitur individual yang diplot terhadap gaji (Perusahaan, Posisi Pekerjaan, Industri, Tipe Pekerjaan, Skor Kepuasan Kerja, Pengalaman Kerja, Terakhir Promosi) menunjukkan variasi gaji yang sangat luas dalam setiap kategorinya dan tidak ada korelasi linear yang kuat. Ini menyiratkan bahwa gaji kemungkinan besar dipengaruhi oleh kombinasi banyak faktor yang kompleks, dan tidak ada satu fitur pun dari yang ditampilkan yang secara tunggal memiliki hubungan linear langsung yang dominan dengan gaji.

## Modeling

Untuk menyelesaikan permasalahan prediksi gaji tahunan (`Salary (USD)`), dua algoritma regresi dipilih: Random Forest Regressor dan XGBoost Regressor. Keduanya dipilih karena mampu menangani data dengan banyak variabel kategorikal (terutama yang telah diubah menjadi numerik menggunakan LabelEncoder) dan *non-linear relationship* antara fitur dan target.

### Data Splitting

Data dibagi menjadi *fitur* (`X`) dan *target* (`y`). Fitur `X` mencakup semua kolom kecuali `Salary (USD)`, sedangkan `y` adalah kolom `Salary (USD)`. Dataset kemudian dibagi menjadi data *training* dan *testing* dengan proporsi 70:30 (70% untuk *training*, 30% untuk *testing*).

* Jumlah data total: 500
* Jumlah data training: 350
* Jumlah data testing: 150

### Random Forest

Random Forest cocok digunakan karena *dataset* ini memiliki banyak fitur kategorikal yang sudah diubah ke bentuk numerik menggunakan Label Encoding. Model ini tidak sensitif terhadap urutan angka hasil *encoding*, sehingga tetap dapat menghasilkan prediksi yang baik. Selain itu, jumlah kategori pada setiap fitur tidak terlalu banyak (umumnya <10), sehingga kompleksitas model tetap terjaga.

**Training Model:**
Model Random Forest Regressor diinisialisasi dengan `random_state=42` dan dilatih menggunakan data *training* (`X_train`, `y_train`).

### XGBoost

XGBoost juga sesuai karena mampu menangani data kategorikal yang sudah di-*label encoding* dengan baik. Model ini kuat terhadap data tabular seperti yang digunakan dalam proyek ini, dan memiliki kemampuan generalisasi yang baik, terutama jika dilakukan *tuning hyperparameter*. Jumlah kategori yang relatif sedikit juga membuat proses *training* lebih efisien.

**Training Model:**
Model XGBoost Regressor diinisialisasi dengan `random_state=42` dan dilatih menggunakan data *training* (`X_train`, `y_train`).

## Evaluation

### Metrik Evaluasi

Karena permasalahan ini adalah regresi (prediksi nilai kontinu `Salary (USD)`), metrik evaluasi yang digunakan adalah:

* **Mean Absolute Error (MAE)**
    Mengukur rata-rata selisih absolut antara nilai prediksi dan nilai aktual. Semakin kecil MAE, semakin baik model dalam memprediksi nilai.
    Formula: $MAE = \frac{1}{n} \sum_{i=1}^{n} |y_i - \hat{y}_i|$

* **Mean Squared Error (MSE)**
    Mengukur rata-rata selisih kuadrat antara nilai prediksi dan aktual. MSE memberikan penalti lebih besar untuk *error* yang besar (karena dikuadratkan).
    Formula: $MSE = \frac{1}{n} \sum_{i=1}^{n} (y_i - \hat{y}_i)^2$

* **Root Mean Squared Error (RMSE)**
    Akar dari MSE. Metrik ini juga mempertimbangkan *error* besar tetapi memiliki satuan yang sama dengan target (USD), sehingga mudah ditafsirkan.
    Formula: $RMSE = \sqrt{\frac{1}{n} \sum_{i=1}^{n} (y_i - \hat{y}_i)^2}$

* **R-Squared (R² Score)**
    Mengukur seberapa baik model menjelaskan variasi data. Nilai R² berkisar antara negatif tak hingga sampai 1. Nilai mendekati 1 berarti model menjelaskan variansi dengan baik, sedangkan nilai negatif menunjukkan model lebih buruk dari *baseline* (rata-rata target saja).
    Formula: $R^2 = 1 - \frac{\sum_{i=1}^{n} (y_i - \hat{y}_i)^2}{\sum_{i=1}^{n} (y_i - \bar{y})^2}$

### Perbandingan Model

| Model         | MAE          | RMSE         | R²         |
| :------------ | :----------- | :----------- | :--------- |
| Random Forest | 61872.94     | 83568.78     | -0.129     |
| XGBoost       | 67888.92     | 83568.78     | -0.412     |


**Hasil Proyek Berdasarkan Metrik Evaluasi:**

1.  **Random Forest** lebih unggul dari XGBoost dalam memprediksi gaji (`Salary (USD)`), ditunjukkan dari nilai:
    * **MAE lebih kecil**: \$61.872 (Random Forest) vs \$67.888 (XGBoost). Ini berarti rata-rata kesalahan prediksi Random Forest lebih kecil sekitar \$6.000.
    * **R² Score lebih tinggi**: -0.129 (Random Forest) vs -0.412 (XGBoost). Meskipun keduanya masih memiliki skor negatif (artinya performanya lebih buruk dari rata-rata), Random Forest masih lebih "dekat" menuju model yang baik.

2.  **RMSE** sama pada kedua model (\~ \$83.568), menunjukkan bahwa keduanya menghasilkan penyebaran *error* yang cukup besar terhadap nilai aktual.

3.  **Nilai R² negatif** pada kedua model mengindikasikan bahwa model belum mampu menjelaskan variansi dari target `Salary (USD)` dengan baik. Ini bisa disebabkan oleh beberapa faktor, seperti *dataset* yang terlalu kecil, banyaknya fitur kategorikal yang belum cukup diolah, data mungkin memiliki multikolinearitas atau *noise* tinggi, atau skala antar fitur yang berbeda memengaruhi performa model.

**Insight:**

Random Forest lebih cocok untuk *dataset* ini dibandingkan XGBoost, walaupun keduanya masih perlu ditingkatkan performanya. Peningkatan bisa dilakukan melalui *feature selection*, *feature engineering*, standardisasi/normalisasi fitur numerik, atau *hyperparameter tuning* pada model.

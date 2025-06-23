# Laporan Proyek Machine Learning - Nama Anda

## Domain Proyek

Proyek ini berada pada domain climate science, khususnya pengamatan terhadap perubahan suhu permukaan sebagai salah satu indikator utama perubahan iklim. Indonesia sebagai negara kepulauan di daerah tropis sangat rentan terhadap efek perubahan iklim, sehingga penting untuk menganalisis tren suhu dalam jangka panjang.

Perubahan iklim merupakan tantangan global yang semakin mendesak. Planet kita saat ini berada dalam kisaran ~1 °C dari suhu permukaan tertingginya dalam satu juta tahun terakhir. Salah satu indikator paling penting dalam mengamati pemanasan global dan perubahan iklim adalah global mean surface temperature (GMST) [1].

Perubahan suhu permukaan tidak hanya berdampak pada sistem iklim global, tetapi juga memengaruhi variabel iklim lain seperti kecepatan angin permukaan (wind speed/WS), albedo (AL), dan dinamika vegetasi (NDVI). Kombinasi dari perubahan ini berkontribusi pada peningkatan suhu regional dan global [1].

Laporan terbaru dari Organisasi Meteorologi Dunia (WMO) menyatakan bahwa periode 2015–2024 kemungkinan besar menjadi dekade terpanas yang pernah tercatat, dengan suhu global rata-rata pada Januari–September 2024 mencapai 1.54 °C di atas tingkat pra-industri [2]. Tren ini memperkuat indikasi bahwa perubahan iklim telah memasuki fase yang lebih cepat dan lebih intensif, didorong oleh konsentrasi gas rumah kaca yang terus meningkat.

Selain itu, data dari National Centers for Environmental Information (NCEI) menunjukkan bahwa suhu permukaan global pada Februari 2025 adalah 1.26 °C di atas rata-rata abad ke-20, menjadikannya Februari terpanas ketiga dalam catatan sejarah [3]. Dengan probabilitas bahwa tahun 2025 menjadi tahun terpanas dalam sejarah mencapai 4%, penting untuk melakukan analisis regional secara lebih mendalam, terutama di wilayah tropis seperti Indonesia.

**Referensi**:
[1] M. Valipour, S. M. Bateni, dan C. Jun, “Global surface temperature: a new insight,” Climate, vol. 9, no. 5, p. 81, 2021.

[2] World Meteorological Organization (WMO), “2024 is on track to be hottest year on record as warming temporarily hits 1.5°C,” WMO Newsroom, Press Release, 11 November 2024. [Online]. Tersedia: https://wmo.int/news/media-centre/2024-track-be-hottest-year-record-warming-temporarily-hits-15degc

[3] National Centers for Environmental Information (NCEI), “Assessing the Global Climate in February 2025,” NOAA NCEI, 2025. [Online]. Tersedia: https://www.ncei.noaa.gov/news/global-climate-202502

## Business Understanding

### Problem Statements
Perubahan suhu permukaan global telah menunjukkan tren peningkatan yang signifikan dalam beberapa dekade terakhir, didorong oleh pemanasan global akibat akumulasi gas rumah kaca di atmosfer. Indonesia, sebagai negara kepulauan di wilayah tropis, menghadapi risiko tinggi terhadap dampak perubahan iklim seperti kenaikan permukaan air laut, gelombang panas, kekeringan, dan gangguan terhadap sektor pertanian serta ekosistem alami. Meskipun tren pemanasan global telah banyak dianalisis secara global, kajian mendalam terkait tren suhu permukaan di Indonesia dalam jangka panjang masih terbatas.

Perubahan suhu permukaan yang terus meningkat dapat memengaruhi berbagai sektor di Indonesia, seperti:
- Kesehatan masyarakat (peningkatan penyakit tropis, heatstroke)
- Ketahanan pangan (produktivitas pertanian terganggu)
- Bencana alam (kekeringan, banjir akibat pola cuaca ekstrem)

### Goals
Membangun model prediksi suhu permukaan menggunakan metode time series forecasting yang nantinya dapat digunakan oleh pembuat kebijakan, peneliti, dan organisasi lingkungan untuk menyusun strategi mitigasi dan adaptasi perubahan iklim secara berbasis data historis.

### Solution statements
- Melakukan visualisasi tren jangka panjang suhu permukaan.
- Melakukan analisis musiman bulanan.
- Menggunakan teknik pemodelan evaluasi machine learning time series ARIMA untuk model statistik deret waktu klasik dan Prophet untuk pendekatan fleksibel yang mempertimbangkan tren dan musiman secara eksplisit.
- Evaluasi performa model menggunakan RMSE, MAE, MAPE, dan SMAPE.

**note:** 

Data historis dari 1940–2024 panjang dan cocok untuk model klasik time-series seperti ARIMA karena model ini bekerja sangat baik ketika data memiliki pola tren yang konsisten dan tidak terlalu kompleks.

Sedangkan Prophet dipilih karena model ini sangat andal dalam mengelola data deret waktu dengan pola musiman yang berulang, tren non-linear, dan titik perubahan tren (changepoints).

## Data Understanding
Dataset ini berisi rincian suhu permukaan rata-rata bulanan (1940-2024). Perubahan iklim saat ini terutama disebabkan oleh emisi gas rumah kaca yang dihasilkan manusia. Pemanasan ini dapat mendorong perubahan besar pada permukaan laut, es laut dan keseimbangan gletser, pola curah hujan, dan suhu ekstrem. Hal ini berpotensi menimbulkan dampak yang sangat buruk bagi kesehatan manusia, sistem pertanian, stabilitas masyarakat, dan spesies lainnya.

Data yang digunakan merupakan data public yang tersedia di Kaggle dengan sumber data awal dari worldbank data.

Unduh data: https://www.kaggle.com/datasets/samithsachidanandan/average-monthly-surface-temperature-1940-2024/code

### Variabel-variabel pada Dataset adalah sebagai berikut:
Entity : Nama nergara (object)
Code : Kode negara (object)
Year : Tahun (int64)
Day: Tanggal (object)
Average surface temperature : Suhu permukaan rata-rata harian (float64)
Average surface temperature.1 : Rata-rata suhu permukaan bulanan (float64)

### Data before Preprocessing

Dataset ini memiliki:
- 198900 total baris
- 0 total baris null
- 0 total baris duplikat
- 4381 total baris outlier
- data dari tahun 1940 - 2024
- data dari 195 negara
- statistik kolom Average surface temperature dan Average surface temperature.1:
    	Average surface temperature	Average surface temperature.1
count	198900.000000	            198900.000000
mean	18.072073	                18.072073
std	    10.246142	                8.710114
min	    -36.240032              	-21.529121
25% 	12.304079               	10.569263
50%    	22.055794	                21.856285
75%	    25.317015	                25.142885
max	    39.889374	                29.794220


### Data After Prepocessing
Dataset untuk data khusus negara Indonesia memiliki:
- 1020 total baris
- 0 total baris null
- 0 total baris duplikat
- 0 total baris outlier
- tidak ada waktu bulan yang terlewat
- data dari tahun 1940 - 2024
- data hanya dari Indonesia saja
- statistik kolom Average surface temperature dan Average surface temperature.1:
	    Average surface temperature	Average surface temperature.1
count	1020.000000	                1020.000000
mean	24.607071	                24.607071
std	    0.635861	                0.575478
min 	23.137548               	23.644049
25% 	24.112764               	24.157072
50% 	24.560066	                24.535385
75%	    25.069886	                25.052223
max	    26.479654	                26.005700

### Exploratory Data Analysis
1. Visualisasi histogram dan KDE (Kernel Density Estimation) terhadap dua kolom suhu 'Average surface temperature' dan 'Average surface temperature.1' serta menampilkan statistik skewness, kurtosis, dan standar deviasinya.
**Hasil insight:** *Skewness kedua variabel adalah 0.3 dan 0.36, dimana berarti kedua distribusi dalam rentang normal*
2. Dilakukan visualisasi plot deret waktu (line plot) untuk kedua kolom suhu terhadap waktu (Day) untuk melihat perubahan tren suhu dari waktu ke waktu, apakah meningkat, menurun, atau musiman.
**Hasil insight:** *Terlihat tren kenaikan suhu rata-rata permukaan yang signifikan dari waktu ke waktu, khususnya mulai dari tahun 1980-an ke atas. Suhu permukaan yang awalnya berkisar di antara 24 C kini sering melewati 25.5 C bahkan mendekati 26.5 C.*
3. Agregasi suhu berdasarkan bulan untuk menganalisis pola musiman. 
**Hasil Insight:** *Indonesia memiliki variasi musiman suhu yang tidak ekstrim karena termasuk negara tropis. Suhu di Indonesia berfluktuasi secara musiman, tetapi tetap dalam rentang sempit (~0.6°C per tahun), khas iklim tropis.Rata-rata suhu permukaan tertinggi berada pada bulan Mei dan Oktober, sedangkan rata-rata suhu permukaan terendah berada pada bulan Juli*

## Data Preparation
### Data Cleaning
1. Pemfilteran berdasarkan negara: Dataset awal mencakup banyak negara. Data difilter untuk hanya mencakup Indonesia.
2. Konversi tipe data:
    - Kolom Day dikonversi menjadi datetime untuk memungkinkan manipulasi waktu.
3. Membuat kolom baru month yang berisi periode bulanan (Period[M]) dari kolom Day yang bertipe datetime64 untuk mengelompokkan data per bulan dan mendeteksi apakah ad abulan yang hilang. hasil: tidak ada bulan yang hilang
4. Memeriksa karakteristik data 'Average surface temperature' dan 'Average surface temperature.1' menggunakan describe() untuk mengetahui karakteristik data numerik
5. Menampilkan seluruh nilai unik kolom data untuk memastikan bahwa data hanya untuk negara Indonesia
6. Pengecekan outlier pada data filter negara Indonesia

### Preparation pre-modelling
1. Konversi Format Waktu
Mengubah kolom month dari format Period ke Timestamp agar cocok dengan library time series.
2. Pilih dan Rename Kolom untuk Time Series
```
monthly_ts = data[['month', 'Average surface temperature.1']].copy()
monthly_ts.columns = ['ds', 'y']
```
ds = timestamp (time component)
y = target value (nilai suhu rata-rata)

Format ini khusus digunakan oleh Prophet, tapi juga disesuaikan untuk digunakan konsisten di semua model.
3. Set Index Waktu
```
monthly_ts_arima = monthly_ts.set_index('ds')
```
Untuk ARIMA, time series harus di-index dengan datetime.
4. Data Splitting
Dataset di-split menjadi 80% data latih (train) dan 20% data uji (test) secara time-based (bukan acak), sesuai karakteristik time series.

## Modeling
Dalam tahap ini, dilakukan proses pembangunan dan evaluasi model prediksi temperatur rata-rata bulanan menggunakan tiga pendekatan time series forecasting: ARIMA, AutoARIMA, dan Prophet. Masing-masing dipilih karena keunggulannya dalam menangani struktur waktu yang berbeda.

1. ARIMA (AutoRegressive Integrated Moving Average)
ARIMA adalah model statistik yang menggabungkan tiga komponen utama:
- AutoRegressive (AR): Memprediksi nilai masa depan berdasarkan nilai-nilai sebelumnya
- Integrated (I): Melakukan differencing untuk membuat data menjadi stasioner
- Moving Average (MA): Menggunakan error prediksi sebelumnya untuk memperbaiki prediksi

**Cara Kerja:** Model ARIMA mengkombinasikan ketiga proses di atas untuk memodelkan dan meramalkan nilai masa depan secara linear berdasarkan data historis.

**Parameter:**
```
    order=(1,1,1) → terdiri dari:
    p=1 (autoregressive): Model menggunakan 1 lag dari nilai sebelumnya
    d=1 (differencing): Dilakukan 1 kali differencing untuk mencapai stasioneritas
    q=1 (moving average): Menggunakan 1 lag dari error term sebelumnya
```

**Kelebihan:**
- Cocok untuk data time series non-musiman dan linear trend.
- Model yang matematis solid dan interpretable.
- Efisien pada data suhu yang tidak banyak dipengaruhi oleh musiman - ekstrem seperti Indonesia.

2. AutoARIMA
AutoARIMA adalah versi otomatis dari ARIMA yang menggunakan algoritma stepwise search untuk menemukan parameter optimal (p, d, q) secara otomatis. Model ini menggunakan kriteria informasi seperti AIC (Akaike Information Criterion) untuk memilih kombinasi parameter terbaik.

**Proses kerja AutoARIMA:**
- Melakukan tes stasioneritas untuk menentukan parameter d
- Menggunakan grid search atau stepwise search untuk menemukan p dan q optimal
- Mengevaluasi setiap kombinasi menggunakan kriteria informasi
- Memilih model dengan skor terbaik

**Parameter:**
```
    seasonal=True: Mengizinkan deteksi musiman.
    stepwise=True: Menyederhanakan pencarian parameter secara efisien.
    suppress_warnings=True: Mengabaikan warning saat fitting.
```

**Kelebihan:**
- Tidak perlu trial-error dalam memilih parameter.
- Cepat dan efisien, cocok untuk prototyping dan deployment.
- Memberikan model yang optimal secara statistik

3. Prophet (by Facebook/Meta)
Prophet menggunakan pendekatan dekomposisi additive yang memecah time series menjadi beberapa komponen:
Formula matematika Prophet:
```
y(t) = g(t) + s(t) + h(t) + εt
```
Dimana:

g(t): Trend component (menggunakan piecewise linear atau logistic growth)

s(t): Seasonal component (Fourier series untuk pola musiman)

h(t): Holiday component (efek hari libur)

εt: Error term

**Cara Kerja:** Prophet menggunakan Bayesian approach dengan Stan untuk fitting model, yang memungkinkan uncertainty quantification dan handling missing values.

**Parameter (default pada model awal):**
```
    yearly_seasonality=True   : Mengaktifkan pola musiman tahunan
    weekly_seasonality=False  : Menonaktifkan pola musiman mingguan
    daily_seasonality=False   : Menonaktifkan pola musiman harian
```

**Kelebihan:**
- Sangat baik untuk data dengan tren dan musiman yang jelas.
- Dapat menangani changepoints (perubahan trend) secara otomatis
- Mudah diinterpretasi dengan visualisasi komponen yang terpisah
- Cocok untuk data suhu yang memiliki pola musiman tahunan

## Evaluation
### Metrik Evaluasi
- RMSE (Root Mean Square Error): Mengukur rata-rata kesalahan prediksi dalam satuan yang sama dengan target (derajat Celsius).
Tujuan: Semakin kecil RMSE, semakin baik performa model.
- MAE (Mean Absolute Error): Menunjukkan rata-rata deviasi absolut antara prediksi dan data aktual.
Tujuan: Nilai lebih kecil menunjukkan model lebih akurat.
- MAPE (Mean Absolute Percentage Error): Memahami seberapa besar kesalahan dalam bentuk persentase.
- SMAPE (Symmetric MAPE): Alternatif yang memperlakukan overprediksi dan underprediksi secara seimbang.

### Hasil Evaluasi
Model Comparison:
           Model   RMSE    MAE   MAPE  SMAPE
0  ARIMA (1,1,1)  0.423  0.361  1.409  1.423
1      AutoARIMA  0.423  0.361  1.409  1.423
2        Prophet  0.195  0.148  0.580  0.582

Prophet memiliki skor terbaik di semua metrik evaluasi:
    - RMSE & MAE jauh lebih rendah dari ARIMA dan AutoARIMA.
    - MAPE & SMAPE juga lebih rendah, menunjukkan performa sangat baik dalam hal presisi relatif (persentase kesalahan kecil).

ARIMA dan AutoARIMA menunjukkan hasil yang identik:
    Hal ini terjadi karena AutoARIMA memilih parameter yang menghasilkan model sama dengan ARIMA manual, yaitu (0,1,0), yang cukup sederhana.

### Hyperparameter Tuning
Mengoptimalkan performa model Prophet dengan mencari kombinasi hyperparameter terbaik yang meminimalkan error.

1. Manual Grid Search
Membuat grid dari 5 hyperparameter utama:
- changepoint_prior_scale: Mengontrol fleksibilitas tren. Semakin kecil nilainya, semakin "halus" tren (tidak terlalu berubah-ubah).
- seasonality_prior_scale: Mengontrol seberapa kuat model mengakomodasi pola musiman.
- holidays_prior_scale: Untuk efek hari libur (tidak digunakan langsung jika tidak ada libur, tapi tetap tersedia).
- seasonality_mode: 'additive' atau 'multiplicative'. Mode ini mengontrol bagaimana pola musiman ditambahkan ke tren.
- changepoint_range: Proporsi awal data tempat Prophet boleh menempatkan changepoint (perubahan tren).

Hasil: Best MAPE (on test set): 0.6180%

Best parameters:
changepoint_prior_scale: 0.001
seasonality_prior_scale: 0.01
holidays_prior_scale: 0.01
seasonality_mode: multiplicative
changepoint_range: 0.9

2. Cross-Validation (CV)
Untuk menghindari overfitting dan memastikan robustness dari parameter yang dipilih.

Hasil: Cross-validation MAPE: 0.5811%

3. Final Model Evaluation
Setelah tuning dan validasi selesai, model final dilatih dengan keseluruhan data train menggunakan parameter terbaik, lalu dievaluasi pada test set.

Hasil:
Metric	Value
RMSE	0.2035
MAE	    0.1580
MAPE	0.6180%
SMAPE	0.6205%

4. Perbandingan hasil:
Original MAPE: 0.58%
Tuned MAPE: 0.6180%
Note: Original model was already quite optimal!

### Final Model
Model terbaik: Prophet tanpa tuning

Prophet mengungguli dua model lainnya dalam semua metrik evaluasi.
Hyperparameter tuning Prophet menghasilkan MAPE 0.6180%, sedikit lebih tinggi dari model awal (0.580%).

### Evaluasi terhadap Goals

| Goal                                                                | Status     | Penjelasan                                                                                    |
| ------------------------------------------------------------------- | ---------- | --------------------------------------------------------------------------------------------- |
| Visualisasi tren jangka panjang suhu permukaan                      | ✅ Tercapai | Dihasilkan melalui analisis time series dan dekomposisi musiman dari data suhu bulanan.       |
| Analisis musiman bulanan                                            | ✅ Tercapai | Model Prophet secara eksplisit menangkap dan memvisualisasikan pola musiman tahunan.          |
| Penggunaan metode ARIMA & Prophet untuk membandingkan pendekatan    | ✅ Tercapai | Ketiga model diimplementasikan dan dibandingkan secara objektif menggunakan metrik yang sama. |
| Evaluasi performa model secara kuantitatif (RMSE, MAE, MAPE, SMAPE) | ✅ Tercapai | Semua metrik dihitung dan menunjukkan Prophet sebagai model paling unggul.                    |

Model prediksi suhu permukaan yang dikembangkan telah secara langsung menjawab problem statement utama, yaitu kebutuhan akan pemahaman tren suhu jangka panjang di Indonesia. Melalui pendekatan time series forecasting, khususnya dengan model Prophet, telah dihasilkan prediksi suhu bulanan yang sangat akurat, dengan hasil MAPE sangat rendah (0.58%),, yang menunjukkan kemampuan model dalam menangkap dinamika suhu secara realistis dan menjadikannya pilihan paling tepat untuk forecasting suhu tropis dengan pola musiman ringan seperti Indonesia.

Dengan tren suhu yang meningkat dari tahun ke tahun, seperti terlihat dalam data historis maupun hasil forecasting, risiko terhadap sektor-sektor kritis di Indonesia—seperti pertanian, kesehatan, dan lingkungan—dapat dianalisis lebih dini dan lebih berbasis data.
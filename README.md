# Heart-Disease-Attack-Analysis

## 1. Pemahaman Bisnis
Tujuan utama dari analisis ini adalah untuk membangun model yang dapat mengidentifikasi individu yang berisiko mengalami penyakit jantung atau serangan jantung. Ini merupakan langkah penting dalam upaya pencegahan dan intervensi dini dalam bidang kesehatan.

## 2. Dataset
Dataset yang digunakan bersumber dari URL dan diberi nama heart_disease_health_indicators_BRFSS2015 (1).csv. Dataset ini memiliki 253.680 entri dan 22 kolom fitur yang semuanya bertipe float64. Fitur-fitur dalam dataset ini mencakup berbagai indikator kesehatan seperti tekanan darah tinggi (HighBP), kolesterol tinggi (HighChol), pemeriksaan kolesterol (CholCheck), Indeks Massa Tubuh (BMI), status perokok (Smoker), riwayat stroke (Stroke), diabetes (Diabetes), aktivitas fisik (PhysActivity), konsumsi buah (Fruits) dan sayuran (Veggies), konsumsi alkohol berat (HvyAlcoholConsump), kepemilikan asuransi kesehatan (AnyHealthcare), tidak adanya biaya dokter (NoDocbcCost), kesehatan umum (GenHlth), kesehatan mental (MentHlth), kesehatan fisik (PhysHlth), kesulitan berjalan (DiffWalk), jenis kelamin (Sex), usia (Age), pendidikan (Education), dan pendapatan (Income). Variabel target adalah HeartDiseaseorAttack, yang menunjukkan apakah seseorang pernah mengalami penyakit jantung atau serangan jantung.

Distribusi variabel target menunjukkan bahwa sebagian besar data adalah kasus 'tidak terpapar' (0.0), yaitu 229.787 entri, dibandingkan dengan kasus 'terpapar' (1.0) sebanyak 23.893 entri. Ini mengindikasikan adanya ketidakseimbangan kelas dalam dataset.

## 3. Eksplorasi Data (EDA)
3.1 Informasi Dataset: Semua kolom dalam dataset tidak memiliki nilai null (non-null count adalah 253.680 untuk semua kolom), yang menunjukkan bahwa tidak ada missing value yang perlu ditangani.

3.2 Statistik Deskriptif: Ringkasan statistik deskriptif menunjukkan rentang nilai untuk setiap fitur, seperti BMI dari 12 hingga 98, usia dari 1 hingga 13 (kemungkinan kategori usia), dan pendapatan dari 1 hingga 8 (kemungkinan kategori pendapatan).

3.3 Korelasi: Analisis korelasi antar fitur (heart_data.corr()) digunakan untuk memahami hubungan antara variabel-variabel. Misalnya, ada korelasi sekitar 0.209 antara HeartDiseaseorAttack dan HighBP. Visualisasi korelasi menggunakan heatmap membantu mengidentifikasi fitur-fitur yang paling berpengaruh terhadap risiko penyakit jantung.

3.4 Distribusi Data: Histogram dari setiap kolom menunjukkan distribusi data untuk setiap fitur, yang dapat membantu dalam mengidentifikasi anomali atau pola dalam data.

## 4. Pemodelan
Analisis ini menggunakan model regresi linier untuk memprediksi HeartDiseaseorAttack. Langkah-langkah utama dalam pemodelan meliputi:

4.1 Pembagian Data: Data dibagi menjadi variabel independen (X) dan variabel dependen (y), di mana HeartDiseaseorAttack adalah variabel dependen. Kemudian, data dibagi lagi menjadi set pelatihan (X_train, y_train) dan set pengujian (X_test, y_test) dengan rasio 80:20, dan stratifikasi diterapkan pada variabel y untuk menjaga distribusi kelas yang sama antara set pelatihan dan pengujian.

4.2 Pembentukan Model: Model regresi linier berganda dibuat menggunakan statsmodels.api.OLS. Konstanta ditambahkan ke matriks variabel independen (X) untuk model regresi.

4.3 Pelatihan Model: Model dilatih menggunakan data pelatihan (X_train_with_const dan y_train).

4.4 Prediksi: Model digunakan untuk membuat prediksi pada set pengujian (X_test_with_const).

## 5. Evaluasi
Evaluasi model dilakukan dengan menggunakan metrik berikut:
a. RMSE (Root Mean Squared Error): Nilai RMSE yang diperoleh adalah 0.2691.
b. R-squared: Nilai R-squared yang diperoleh adalah 0.1509.

Nilai R-squared yang rendah (0.1509) menunjukkan bahwa model regresi linier hanya dapat menjelaskan sekitar 15.09% varians dalam variabel dependen (HeartDiseaseorAttack). Ini menunjukkan bahwa model regresi linier sederhana mungkin tidak cukup kuat untuk memprediksi risiko penyakit jantung secara akurat dengan dataset ini, dan mungkin ada banyak faktor lain yang tidak terangkum dalam fitur yang digunakan, atau model yang lebih kompleks mungkin diperlukan.

Analisis koefisien menunjukkan variabel-variabel yang paling berpengaruh terhadap HeartDiseaseorAttack (dengan p-value < 0.05). Variabel-variabel tersebut dan koefisiennya adalah:

a. Stroke: 0.1879
b.Sex: 0.0531
c.DiffWalk: 0.0498
d. GenHlth: 0.0330
e. HighBP: 0.0335
f. HighChol: 0.0386
g. Diabetes: 0.0239
h. Smoker: 0.0230
i. Age: 0.0110
j. NoDocbcCost: 0.0077
k. AnyHealthcare: 0.0080
l. Fruits: 0.0038
m.Veggies: 0.0035
n. PhysActivity: 0.0032
o. PhysHlth: 0.0010
p. HvyAlcoholConsump: -0.0192
q. Income: -0.0035
r. BMI: -0.0012
s. MentHlth: -0.0002
t. CholCheck: 0.0145
u. const: -0.1454

Variabel Education memiliki p-value 0.103, yang berarti tidak signifikan secara statistik pada tingkat kepercayaan 0.05 (atau 95%).

## 6. Library yang Digunakan
Berikut adalah library Python yang diimpor untuk analisis ini:
a. mlxtend.plotting: Untuk plot daerah keputusan.
b. pandas: Untuk manipulasi dan analisis data.
c. numpy: Untuk operasi numerik.
d. matplotlib.pyplot: Untuk visualisasi data.
e. seaborn: Untuk visualisasi statistik data.
f. warnings: Untuk mengelola peringatan.
g. sklearn.model_selection.train_test_split: Untuk membagi data menjadi set pelatihan dan pengujian.
h.sklearn.metrics.accuracy_score, confusion_matrix, classification_report: Untuk evaluasi model klasifikasi.
i. sklearn.preprocessing.StandardScaler: Untuk penskalaan fitur.
j. sklearn.metrics.mean_squared_error, r2_score: Untuk evaluasi model regresi.
k. statsmodels.api: Untuk model regresi statistik.
l. sklearn.linear_model.LogisticRegression: Untuk model regresi logistik.
m. sklearn.linear_model.LinearRegression: Untuk model regresi linier.

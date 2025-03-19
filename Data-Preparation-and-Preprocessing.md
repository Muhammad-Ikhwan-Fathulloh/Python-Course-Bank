# Data Preparation and Preprocessing

## 1. Introduction
Data preparation dan preprocessing adalah langkah penting dalam machine learning dan data analysis. Proses ini bertujuan untuk memastikan bahwa data yang digunakan dalam model machine learning sudah bersih, relevan, dan terstruktur dengan baik. Langkah-langkah utama yang dilakukan meliputi:
- **Data Collection**: Mengumpulkan data dari berbagai sumber seperti database, API, atau file CSV.
- **Data Cleaning**: Menghilangkan duplikasi, menangani missing values, dan memperbaiki inkonsistensi data.
- **Data Preprocessing**: Melakukan transformasi data seperti encoding, normalisasi, dan scaling.
- **Feature Engineering**: Membuat fitur baru atau mengubah fitur yang ada agar lebih bermakna bagi model.
- **Handling Missing Values**: Menangani data yang hilang dengan metode tertentu seperti imputasi atau penghapusan.
- **Handling Outliers**: Mendeteksi dan menangani nilai ekstrem yang dapat mempengaruhi performa model.
- **Data Versioning**: Menyimpan versi dataset agar dapat ditelusuri perubahannya dan mempermudah reproduksi eksperimen.

## 2. Loading Dataset
Langkah pertama adalah memuat dataset ke dalam Pandas DataFrame.
```python
import pandas as pd

# Load dataset dari GitHub
url = "https://raw.githubusercontent.com/Muhammad-Ikhwan-Fathulloh/Dataset/main/anemia-dataset.csv"
df = pd.read_csv(url)

# Menampilkan 5 baris pertama
df.head()
```
Kode di atas membaca file CSV dari GitHub dan menampilkannya dalam bentuk DataFrame. Fungsi `df.head()` digunakan untuk melihat 5 baris pertama dari dataset agar dapat memahami struktur data.

## 3. Exploratory Data Analysis (EDA)
EDA bertujuan untuk memahami karakteristik dataset sebelum melakukan preprocessing lebih lanjut.
```python
# Melihat informasi dataset
df.info()

# Melihat statistik deskriptif
df.describe()

# Melihat jumlah nilai unik pada setiap kolom
df.nunique()
```
- `df.info()` memberikan gambaran umum tentang dataset, termasuk jumlah kolom, tipe data, dan jumlah missing values.
- `df.describe()` menampilkan statistik deskriptif seperti mean, median, dan standar deviasi.
- `df.nunique()` menunjukkan jumlah nilai unik dalam setiap kolom, berguna untuk mengetahui apakah suatu fitur bersifat kategorikal atau numerik.

## 4. Handling Missing Values
Missing values dapat menyebabkan bias dalam analisis data dan model machine learning.
```python
# Cek missing values
df.isnull().sum()

# Jika ada missing values, bisa dihandle dengan:
# - Menghapus data: df.dropna(inplace=True)
# - Mengisi dengan mean/median/mode: df.fillna(df.mean(), inplace=True)
```
Jika terdapat missing values, ada beberapa metode yang dapat digunakan:
1. **Menghapus baris** yang mengandung missing values (`df.dropna(inplace=True)`).
2. **Mengisi missing values** dengan nilai rata-rata (mean), median, atau modus (`df.fillna(df.mean(), inplace=True)`).

## 5. Encoding Categorical Variables
Karena model machine learning hanya bisa bekerja dengan data numerik, maka kolom kategorikal harus dikonversi.
```python
# Mengubah kolom Gender menjadi numerik (0: female, 1: male)
df['Gender'] = df['Gender'].map({'female': 0, 'male': 1})
```
Proses encoding ini mengubah nilai kategorikal menjadi angka, sehingga bisa digunakan dalam analisis lebih lanjut.

## 6. Handling Outliers
Outlier dapat mengganggu performa model karena nilai ekstrem yang tidak mencerminkan pola sebenarnya.
```python
import matplotlib.pyplot as plt
import seaborn as sns

# Boxplot untuk melihat outlier
plt.figure(figsize=(10, 6))
sns.boxplot(data=df[['Hemoglobin', 'MCH', 'MCHC', 'MCV']])
plt.show()
```
Dengan menggunakan boxplot, kita bisa mengidentifikasi keberadaan outlier.
```python
# Menggunakan IQR untuk menghapus outlier
Q1 = df[['Hemoglobin', 'MCH', 'MCHC', 'MCV']].quantile(0.25)
Q3 = df[['Hemoglobin', 'MCH', 'MCHC', 'MCV']].quantile(0.75)
IQR = Q3 - Q1

# Menyaring outlier
df = df[~((df[['Hemoglobin', 'MCH', 'MCHC', 'MCV']] < (Q1 - 1.5 * IQR)) | (df[['Hemoglobin', 'MCH', 'MCHC', 'MCV']] > (Q3 + 1.5 * IQR))).any(axis=1)]
```
Interquartile Range (IQR) digunakan untuk mengidentifikasi dan menghapus nilai ekstrem.

## 7. Feature Scaling
Scaling diperlukan agar fitur memiliki skala yang sama, terutama dalam model berbasis jarak seperti KNN dan SVM.
```python
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()
df[['Hemoglobin', 'MCH', 'MCHC', 'MCV']] = scaler.fit_transform(df[['Hemoglobin', 'MCH', 'MCHC', 'MCV']])
```
StandardScaler mengubah data menjadi distribusi dengan mean 0 dan standar deviasi 1.

## 8. Data Versioning
Data versioning penting untuk melacak perubahan dataset dan memastikan reprodusibilitas eksperimen.
```python
# Menyimpan versi dataset yang telah diproses
df.to_csv("processed_anemia_dataset.csv", index=False)
```
Dataset yang telah diproses disimpan dalam format CSV agar bisa digunakan kembali.

## 9. Conclusion
Proses data preparation dan preprocessing sangat penting untuk memastikan data bersih, relevan, dan siap digunakan dalam analisis atau model machine learning. Langkah-langkah yang dilakukan meliputi:
- **Cleaning** data dari missing values dan outliers.
- **Encoding** variabel kategori agar bisa digunakan dalam model.
- **Feature Scaling** untuk normalisasi data agar memiliki skala yang sama.
- **Data Versioning** untuk menyimpan hasil preprocessing sehingga mudah direproduksi.

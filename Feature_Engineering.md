# Materi: Feature Engineering dalam Machine Learning dengan Studi Kasus

---

## 1. Apa itu Feature Engineering?
**Feature Engineering** adalah proses mengubah data mentah menjadi fitur-fitur (variabel) yang lebih bermakna dan representatif untuk digunakan dalam model machine learning. Ini melibatkan pemilihan, transformasi, dan pembuatan fitur baru dari data yang ada agar model dapat belajar dengan lebih efektif.

- **Fitur (Feature)**: Variabel atau atribut yang digunakan sebagai input untuk model machine learning.
- **Tujuan**: Meningkatkan performa model dengan menyediakan data yang lebih relevan dan informatif.

---

## 2. Mengapa Feature Engineering begitu penting?

### a. Hubungannya dengan Performa Model
- **Kualitas Fitur > Algoritma**: Fitur yang baik lebih berpengaruh pada performa model daripada pemilihan algoritma.
- **Data yang Tidak Relevan**: Fitur yang tidak relevan atau redundan dapat mengurangi akurasi model.
- **Data yang Tidak Terstruktur**: Data mentah seringkali tidak siap digunakan dan perlu diproses terlebih dahulu.

### b. Manfaat Feature Engineering
1. **Meningkatkan Akurasi Model**: Fitur yang baik membantu model memahami pola data dengan lebih baik.
2. **Mengurangi Overfitting**: Menghilangkan fitur yang tidak relevan atau redundan dapat mencegah model dari overfitting.
3. **Mempercepat Proses Training**: Data yang sudah diproses membutuhkan waktu komputasi yang lebih sedikit.
4. **Memudahkan Interpretasi Model**: Fitur yang bermakna membuat model lebih mudah dipahami.

---

## 3. Studi Kasus: Prediksi Harga Rumah

### Dataset: [House Prices Dataset](https://www.kaggle.com/c/house-prices-advanced-regression-techniques/data)
Dataset ini berisi informasi tentang rumah-rumah yang dijual, termasuk fitur-fitur seperti luas tanah, jumlah kamar, lokasi, dan harga jual.

### Langkah 1: Analisis Awal Dataset
1. **Load Dataset**:
   ```python
   import pandas as pd
   df = pd.read_csv('house_prices.csv')
   print(df.head())
   ```
2. **Statistik Deskriptif**:
   ```python
   print(df.describe())
   ```
3. **Cek Missing Values**:
   ```python
   print(df.isnull().sum())
   ```

### Langkah 2: Handling Missing Values
- **Isi Missing Values**:
  ```python
  df['LotFrontage'].fillna(df['LotFrontage'].median(), inplace=True)
  df['GarageYrBlt'].fillna(df['GarageYrBlt'].median(), inplace=True)
  ```
- **Hapus Kolom dengan Banyak Missing Values**:
  ```python
  df.drop(columns=['PoolQC', 'MiscFeature', 'Alley'], inplace=True)
  ```

### Langkah 3: Encoding Kategorikal Data
- **Label Encoding**:
  ```python
  from sklearn.preprocessing import LabelEncoder
  le = LabelEncoder()
  df['MSZoning'] = le.fit_transform(df['MSZoning'])
  ```
- **One-Hot Encoding**:
  ```python
  df = pd.get_dummies(df, columns=['SaleCondition'])
  ```

### Langkah 4: Feature Scaling
- **Standardisasi**:
  ```python
  from sklearn.preprocessing import StandardScaler
  scaler = StandardScaler()
  df[['LotArea', 'GrLivArea']] = scaler.fit_transform(df[['LotArea', 'GrLivArea']])
  ```

### Langkah 5: Feature Creation
- **Buat Fitur Baru**:
  ```python
  df['TotalSF'] = df['TotalBsmtSF'] + df['1stFlrSF'] + df['2ndFlrSF']
  df['Age'] = df['YrSold'] - df['YearBuilt']
  ```

### Langkah 6: Feature Selection
- **Hapus Fitur yang Tidak Relevan**:
  ```python
  df.drop(columns=['Id', 'YrSold', 'YearBuilt'], inplace=True)
  ```

---

## 4. Teknik-teknik Feature Engineering dalam Machine Learning

### a. **Handling Missing Values**
- **Hapus Data**: Jika missing values sedikit, hapus baris atau kolom yang mengandungnya.
- **Imputasi**: Isi missing values dengan nilai tertentu (mean, median, mode, atau prediksi).
  ```python
  df['column'].fillna(df['column'].mean(), inplace=True)
  ```

### b. **Encoding Kategorikal Data**
- **Label Encoding**: Mengubah kategori menjadi angka (0, 1, 2, ...).
  ```python
  from sklearn.preprocessing import LabelEncoder
  le = LabelEncoder()
  df['category'] = le.fit_transform(df['category'])
  ```
- **One-Hot Encoding**: Mengubah kategori menjadi vektor biner.
  ```python
  df = pd.get_dummies(df, columns=['category'])
  ```

### c. **Scaling dan Normalisasi**
- **Scaling**: Mengubah nilai fitur ke dalam rentang tertentu (misalnya, 0-1).
  ```python
  from sklearn.preprocessing import MinMaxScaler
  scaler = MinMaxScaler()
  df['feature'] = scaler.fit_transform(df[['feature']])
  ```
- **Standardisasi**: Mengubah nilai fitur agar memiliki mean = 0 dan std = 1.
  ```python
  from sklearn.preprocessing import StandardScaler
  scaler = StandardScaler()
  df['feature'] = scaler.fit_transform(df[['feature']])
  ```

### d. **Feature Transformation**
- **Log Transform**: Mengurangi skewness pada data.
  ```python
  import numpy as np
  df['feature'] = np.log(df['feature'])
  ```
- **Polynomial Features**: Menambahkan fitur polinomial untuk menangkap hubungan non-linear.
  ```python
  from sklearn.preprocessing import PolynomialFeatures
  poly = PolynomialFeatures(degree=2)
  df_poly = poly.fit_transform(df[['feature1', 'feature2']])
  ```

### e. **Feature Creation**
- **Membuat Fitur Baru**: Gabungkan atau manipulasi fitur yang ada untuk membuat fitur baru.
  - Contoh: Dari fitur `tanggal_lahir`, buat fitur `usia`.
  ```python
  df['usia'] = 2023 - df['tanggal_lahir']
  ```

### f. **Feature Selection**
- **Hapus Fitur yang Tidak Relevan**: Gunakan teknik seperti korelasi atau feature importance.
  ```python
  from sklearn.feature_selection import SelectKBest, f_classif
  selector = SelectKBest(score_func=f_classif, k=10)
  X_new = selector.fit_transform(X, y)
  ```

### g. **Binning**
- **Mengelompokkan Nilai Kontinu**: Ubah nilai kontinu menjadi kategori.
  ```python
  df['age_group'] = pd.cut(df['age'], bins=[0, 18, 35, 60, 100], labels=['child', 'young', 'adult', 'senior'])
  ```

---

## 5. Contoh Praktis Feature Engineering

### Dataset: Titanic Survival Prediction
1. **Handling Missing Values**:
   - Isi missing values pada kolom `Age` dengan median.
2. **Encoding**:
   - Ubah kolom `Sex` (male/female) menjadi 0/1 menggunakan Label Encoding.
3. **Feature Creation**:
   - Buat fitur `FamilySize` dari kolom `SibSp` dan `Parch`.
4. **Feature Selection**:
   - Hapus kolom yang tidak relevan seperti `PassengerId` dan `Name`.

---

## 6. Kesimpulan
- **Feature Engineering** adalah langkah kritis dalam pipeline machine learning.
- Dengan teknik yang tepat, Anda dapat meningkatkan performa model secara signifikan.
- Proses ini membutuhkan pemahaman mendalam tentang data dan kreativitas dalam menciptakan fitur baru.

Dengan menguasai feature engineering, Anda dapat membangun model machine learning yang lebih akurat dan efisien. Selamat mencoba! 🚀

---

## Referensi
1. [House Prices Dataset - Kaggle](https://www.kaggle.com/c/house-prices-advanced-regression-techniques/data)
2. [Scikit-learn Documentation](https://scikit-learn.org/stable/)
3. [Feature Engineering for Machine Learning - Towards Data Science](https://towardsdatascience.com/feature-engineering-for-machine-learning-3a5e293a5114)
4. [Handling Missing Values - DataCamp](https://www.datacamp.com/community/tutorials/feature-engineering-kaggle)

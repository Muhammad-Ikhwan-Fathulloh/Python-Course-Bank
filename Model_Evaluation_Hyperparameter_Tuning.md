# Materi: Metrik Evaluasi, Cross Validation, dan Hyperparameter Tuning dalam Machine Learning

---

## 1. Apa itu Metrik Evaluasi?
**Metrik Evaluasi** adalah alat atau ukuran yang digunakan untuk menilai performa model machine learning. Metrik ini membantu kita memahami seberapa baik model bekerja dalam memprediksi atau mengklasifikasikan data.

---

## 2. Kenapa Perlu Metrik Evaluasi?
- **Mengukur Performa Model**: Mengetahui seberapa akurat model dalam memprediksi data.
- **Membandingkan Model**: Membantu memilih model terbaik dari beberapa alternatif.
- **Identifikasi Masalah**: Menemukan kelemahan model, seperti overfitting atau underfitting.
- **Komunikasi Hasil**: Menyajikan hasil evaluasi secara objektif dan mudah dipahami.

---

## 3. Contoh Metrik Evaluasi

### a. **Metrik untuk Klasifikasi**
1. **Akurasi (Accuracy)**:
   - Proporsi prediksi yang benar dari total prediksi.
   - Rumus: 
     \[
     \text{Akurasi} = \frac{\text{True Positif (TP)} + \text{True Negatif (TN)}}{\text{TP} + \text{TN} + \text{False Positif (FP)} + \text{False Negatif (FN)}}
     \]
   - Contoh: Jika model memprediksi 90 dari 100 sampel dengan benar, akurasinya adalah 90%.

2. **Presisi (Precision)**:
   - Proporsi prediksi positif yang benar dari total prediksi positif.
   - Rumus:
     \[
     \text{Presisi} = \frac{\text{TP}}{\text{TP} + \text{FP}}
     \]
   - Contoh: Jika model memprediksi 80 sampel sebagai positif dan 70 benar, presisinya adalah 87.5%.

3. **Recall (Sensitivity)**:
   - Proporsi sampel positif yang berhasil diprediksi dengan benar.
   - Rumus:
     \[
     \text{Recall} = \frac{\text{TP}}{\text{TP} + \text{FN}}
     \]
   - Contoh: Jika ada 100 sampel positif dan model memprediksi 80 dengan benar, recall-nya adalah 80%.

4. **F1-Score**:
   - Rata-rata harmonik dari presisi dan recall.
   - Rumus:
     \[
     \text{F1-Score} = 2 \times \frac{\text{Presisi} \times \text{Recall}}{\text{Presisi} + \text{Recall}}
     \]
   - Contoh: Jika presisi = 0.8 dan recall = 0.7, F1-Score = 0.74.

5. **ROC-AUC**:
   - Area di bawah kurva ROC (Receiver Operating Characteristic).
   - Mengukur kemampuan model dalam membedakan kelas positif dan negatif.
   - Nilai berkisar antara 0.5 (random) hingga 1.0 (sempurna).

### b. **Metrik untuk Regresi**
1. **MSE (Mean Squared Error)**:
   - Rata-rata kuadrat selisih antara nilai prediksi dan aktual.
   - Rumus:
     \[
     \text{MSE} = \frac{1}{n} \sum_{i=1}^{n} (y_i - \hat{y}_i)^2
     \]
   - Contoh: Jika MSE = 10, rata-rata selisih kuadrat adalah 10.

2. **RMSE (Root Mean Squared Error)**:
   - Akar kuadrat dari MSE.
   - Rumus:
     \[
     \text{RMSE} = \sqrt{\text{MSE}}
     \]
   - Contoh: Jika MSE = 100, RMSE = 10.

3. **MAE (Mean Absolute Error)**:
   - Rata-rata selisih absolut antara nilai prediksi dan aktual.
   - Rumus:
     \[
     \text{MAE} = \frac{1}{n} \sum_{i=1}^{n} |y_i - \hat{y}_i|
     \]
   - Contoh: Jika MAE = 5, rata-rata selisih absolut adalah 5.

4. **R² (R-squared)**:
   - Proporsi variansi dalam data yang dijelaskan oleh model.
   - Rumus:
     \[
     R^2 = 1 - \frac{\sum_{i=1}^{n} (y_i - \hat{y}_i)^2}{\sum_{i=1}^{n} (y_i - \bar{y})^2}
     \]
   - Contoh: Jika R² = 0.85, model menjelaskan 85% variansi data.

---

## 4. Matriks Konfusi & Laporan Klasifikasi

### a. **Matriks Konfusi**
- Tabel yang menampilkan jumlah prediksi benar dan salah untuk setiap kelas.
- Contoh:
  ```
              Prediksi Negatif   Prediksi Positif
  Aktual Negatif       TN               FP
  Aktual Positif       FN               TP
  ```

### b. **Laporan Klasifikasi**
- Ringkasan metrik klasifikasi seperti presisi, recall, F1-score, dan akurasi.
- Contoh di Python:
  ```python
  from sklearn.metrics import classification_report
  print(classification_report(y_true, y_pred))
  ```

---

## 5. Cross Validation

### a. **K-fold Cross Validation**
- Membagi dataset menjadi `k` subset, melatih model pada `k-1` subset, dan menguji pada subset yang tersisa.
- Contoh:
  ```python
  from sklearn.model_selection import cross_val_score
  scores = cross_val_score(model, X, y, cv=5)
  print(scores.mean())
  ```

### b. **Stratified K-fold**
- Variasi K-fold yang menjaga proporsi kelas di setiap subset.
- Berguna untuk dataset tidak seimbang.

### c. **LOOCV (Leave-One-Out Cross Validation)**
- Setiap sampel digunakan sebagai data uji satu per satu, sementara sisanya digunakan untuk training.
- Contoh:
  ```python
  from sklearn.model_selection import LeaveOneOut
  loo = LeaveOneOut()
  scores = cross_val_score(model, X, y, cv=loo)
  ```

---

## 6. Tradeoff Bias-Varians
- **Bias**: Kesalahan karena asumsi model yang terlalu sederhana (underfitting).
- **Varians**: Kesalahan karena model terlalu kompleks (overfitting).
- **Tujuan**: Menyeimbangkan bias dan varians untuk mendapatkan model yang generalisasi dengan baik.

---

## 7. Hyperparameter Tuning

### a. **Apa itu Hyperparameter Tuning?**
- Proses mengoptimalkan parameter yang tidak dipelajari oleh model (contoh: learning rate, jumlah pohon di Random Forest).

### b. **Kenapa Perlu Hyperparameter Tuning?**
- Meningkatkan performa model.
- Menghindari overfitting atau underfitting.

### c. **Contoh Teknik Hyperparameter Tuning**
1. **Grid Search**:
   - Mencoba semua kombinasi hyperparameter yang mungkin.
   - Contoh:
     ```python
     from sklearn.model_selection import GridSearchCV
     param_grid = {'n_estimators': [10, 50, 100], 'max_depth': [None, 10, 20]}
     grid_search = GridSearchCV(estimator=model, param_grid=param_grid, cv=5)
     grid_search.fit(X, y)
     print(grid_search.best_params_)
     ```

2. **Random Search**:
   - Mencoba kombinasi hyperparameter secara acak.
   - Contoh:
     ```python
     from sklearn.model_selection import RandomizedSearchCV
     param_dist = {'n_estimators': [10, 50, 100], 'max_depth': [None, 10, 20]}
     random_search = RandomizedSearchCV(estimator=model, param_distributions=param_dist, n_iter=10, cv=5)
     random_search.fit(X, y)
     print(random_search.best_params_)
     ```

3. **Optimasi Bayesian**:
   - Menggunakan probabilitas untuk menemukan kombinasi hyperparameter terbaik.
   - Contoh dengan **Optuna**:
     ```python
     import optuna
     def objective(trial):
         n_estimators = trial.suggest_int('n_estimators', 10, 100)
         max_depth = trial.suggest_int('max_depth', 1, 20)
         model = RandomForestClassifier(n_estimators=n_estimators, max_depth=max_depth)
         return cross_val_score(model, X, y, cv=5).mean()
     study = optuna.create_study(direction='maximize')
     study.optimize(objective, n_trials=50)
     print(study.best_params)
     ```

4. **Automated Tools**:
   - **GridSearchCV** dan **RandomizedSearchCV** dari Scikit-learn.
   - **Optuna** untuk optimasi Bayesian.

---

## 8. Kesimpulan
- **Metrik Evaluasi** membantu mengukur performa model.
- **Cross Validation** memastikan evaluasi yang robust.
- **Hyperparameter Tuning** meningkatkan performa model dengan menemukan kombinasi hyperparameter terbaik.

Dengan memahami konsep-konsep ini, Anda dapat membangun dan mengevaluasi model machine learning dengan lebih efektif. Selamat mencoba! 🚀

---

## Referensi
1. [Scikit-learn Documentation](https://scikit-learn.org/stable/)
2. [Optuna Documentation](https://optuna.org/)
3. [Understanding Bias-Variance Tradeoff - Towards Data Science](https://towardsdatascience.com/understanding-the-bias-variance-tradeoff-165e6942b229)
4. [Hyperparameter Tuning with Grid Search and Random Search - Analytics Vidhya](https://www.analyticsvidhya.com/blog/2021/05/tuning-the-hyperparameters-and-cross-validation/)

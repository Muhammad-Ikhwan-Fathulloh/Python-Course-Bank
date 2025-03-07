# Materi: Time Series Analysis dan Forecasting

---

## 1. Time Series Characteristics

### a. **Trend**
- Pola jangka panjang yang menunjukkan peningkatan atau penurunan data seiring waktu.
- Contoh: Pertumbuhan penduduk, inflasi.

### b. **Seasonality**
- Pola berulang yang terjadi pada interval waktu tertentu (misalnya, harian, bulanan, tahunan).
- Contoh: Penjualan meningkat selama liburan.

### c. **Cyclicality**
- Fluktuasi yang tidak teratur dan tidak memiliki periode tetap.
- Contoh: Siklus ekonomi (boom dan resesi).

### d. **Noise**
- Variasi acak yang tidak dapat dijelaskan oleh trend, seasonality, atau cyclicality.
- Contoh: Fluktuasi harian yang tidak terduga.

---

## 2. Decomposition Methods

### a. **Additive Decomposition**
- Model: \( y(t) = \text{Trend}(t) + \text{Seasonality}(t) + \text{Noise}(t) \)
- Cocok untuk data dengan seasonality yang konstan.

### b. **Multiplicative Decomposition**
- Model: \( y(t) = \text{Trend}(t) \times \text{Seasonality}(t) \times \text{Noise}(t) \)
- Cocok untuk data dengan seasonality yang bervariasi.

### c. **Contoh di Python**
```python
from statsmodels.tsa.seasonal import seasonal_decompose
result = seasonal_decompose(series, model='additive')
result.plot()
```

---

## 3. Stationarity

### a. **Apa itu Stationarity?**
- Time series dikatakan stasioner jika properti statistiknya (mean, variance) tidak berubah seiring waktu.

### b. **ADF Test (Augmented Dickey-Fuller)**
- Uji untuk menentukan apakah time series stasioner.
- Hipotesis:
  - \( H_0 \): Time series tidak stasioner.
  - \( H_1 \): Time series stasioner.
- Contoh:
  ```python
  from statsmodels.tsa.stattools import adfuller
  result = adfuller(series)
  print(f'ADF Statistic: {result[0]}')
  print(f'p-value: {result[1]}')
  ```

### c. **KPSS Test (Kwiatkowski-Phillips-Schmidt-Shin)**
- Uji untuk menentukan apakah time series stasioner di sekitar trend.
- Hipotesis:
  - \( H_0 \): Time series stasioner.
  - \( H_1 \): Time series tidak stasioner.

### d. **Differencing**
- Teknik untuk membuat time series stasioner dengan menghitung selisih antara observasi.
- Contoh:
  ```python
  series_diff = series.diff().dropna()
  ```

---

## 4. Forecasting Models

### a. **ARIMA (AutoRegressive Integrated Moving Average)**
- Model untuk time series stasioner.
- Parameter:
  - \( p \): Order dari komponen autoregressive (AR).
  - \( d \): Order dari differencing (I).
  - \( q \): Order dari komponen moving average (MA).
- Contoh:
  ```python
  from statsmodels.tsa.arima.model import ARIMA
  model = ARIMA(series, order=(1, 1, 1))
  model_fit = model.fit()
  predictions = model_fit.forecast(steps=10)
  ```

### b. **SARIMA (Seasonal ARIMA)**
- Ekstensi ARIMA untuk menangani seasonality.
- Parameter tambahan:
  - \( P, D, Q \): Komponen musiman.
  - \( m \): Periode musiman.
- Contoh:
  ```python
  from statsmodels.tsa.statespace.sarimax import SARIMAX
  model = SARIMAX(series, order=(1, 1, 1), seasonal_order=(1, 1, 1, 12))
  model_fit = model.fit()
  predictions = model_fit.forecast(steps=10)
  ```

### c. **Exponential Smoothing (Holt-Winters)**
- Model untuk time series dengan trend dan seasonality.
- Jenis:
  - **Single Exponential Smoothing**: Hanya level.
  - **Double Exponential Smoothing**: Level dan trend.
  - **Triple Exponential Smoothing (Holt-Winters)**: Level, trend, dan seasonality.
- Contoh:
  ```python
  from statsmodels.tsa.holtwinters import ExponentialSmoothing
  model = ExponentialSmoothing(series, trend='add', seasonal='add', seasonal_periods=12)
  model_fit = model.fit()
  predictions = model_fit.forecast(steps=10)
  ```

### d. **Deep Learning Approaches**
1. **LSTMs (Long Short-Term Memory)**:
   - Jenis RNN yang cocok untuk data sekuensial.
   - Contoh:
     ```python
     from tensorflow.keras.models import Sequential
     from tensorflow.keras.layers import LSTM, Dense
     model = Sequential()
     model.add(LSTM(50, activation='relu', input_shape=(n_steps, n_features)))
     model.add(Dense(1))
     model.compile(optimizer='adam', loss='mse')
     model.fit(X_train, y_train, epochs=200, verbose=0)
     ```

2. **Prophet**:
   - Library open-source oleh Facebook untuk forecasting time series.
   - Contoh:
     ```python
     from prophet import Prophet
     model = Prophet()
     model.fit(df)
     future = model.make_future_dataframe(periods=365)
     forecast = model.predict(future)
     ```

---

## 5. Evaluation Metrics

### a. **MAPE (Mean Absolute Percentage Error)**
- Mengukur rata-rata persentase error.
- Rumus:
  \[
  \text{MAPE} = \frac{100\%}{n} \sum_{i=1}^{n} \left| \frac{y_i - \hat{y}_i}{y_i} \right|
  \]

### b. **sMAPE (Symmetric Mean Absolute Percentage Error)**
- Versi simetris dari MAPE.
- Rumus:
  \[
  \text{sMAPE} = \frac{100\%}{n} \sum_{i=1}^{n} \frac{|y_i - \hat{y}_i|}{(|y_i| + |\hat{y}_i|)/2}
  \]

### c. **MASE (Mean Absolute Scaled Error)**
- Mengukur error relatif terhadap baseline (misalnya, naive forecast).
- Rumus:
  \[
  \text{MASE} = \frac{\text{MAE}}{\frac{1}{n-1} \sum_{i=2}^{n} |y_i - y_{i-1}|}
  \]

---

## 6. Case Study: Forecasting Stock Prices atau Energy Consumption

### a. **Forecasting Stock Prices**
1. **Load Data**:
   ```python
   import yfinance as yf
   data = yf.download('AAPL', start='2020-01-01', end='2023-01-01')
   series = data['Close']
   ```

2. **Decompose Time Series**:
   ```python
   result = seasonal_decompose(series, model='multiplicative')
   result.plot()
   ```

3. **Check Stationarity**:
   ```python
   result = adfuller(series)
   print(f'ADF Statistic: {result[0]}')
   print(f'p-value: {result[1]}')
   ```

4. **Build ARIMA Model**:
   ```python
   model = ARIMA(series, order=(1, 1, 1))
   model_fit = model.fit()
   predictions = model_fit.forecast(steps=30)
   ```

5. **Evaluate Model**:
   ```python
   from sklearn.metrics import mean_absolute_error
   mae = mean_absolute_error(actual, predictions)
   print(f'MAE: {mae}')
   ```

### b. **Forecasting Energy Consumption**
1. **Load Data**:
   ```python
   import pandas as pd
   data = pd.read_csv('energy_consumption.csv', parse_dates=['Date'], index_col='Date')
   series = data['Consumption']
   ```

2. **Build Prophet Model**:
   ```python
   model = Prophet()
   model.fit(data)
   future = model.make_future_dataframe(periods=365)
   forecast = model.predict(future)
   ```

3. **Visualize Forecast**:
   ```python
   model.plot(forecast)
   ```

---

## 7. Kesimpulan
- **Time Series Analysis** memungkinkan kita memahami pola data dan membuat prediksi yang akurat.
- Dengan teknik seperti ARIMA, SARIMA, dan LSTM, kita dapat membangun model forecasting yang efektif.
- Evaluasi menggunakan metrik seperti MAPE dan MASE membantu mengukur performa model.

Selamat mencoba case study dan eksplorasi lebih lanjut! 🚀

---

## Referensi
1. [Statsmodels Documentation](https://www.statsmodels.org/)
2. [Prophet Documentation](https://facebook.github.io/prophet/)
3. [Time Series Forecasting - Towards Data Science](https://towardsdatascience.com/time-series-forecasting-methods-6d4c6d2a6c8e)
4. [YFinance Documentation](https://pypi.org/project/yfinance/)
5. [Deep Learning for Time Series - TensorFlow](https://www.tensorflow.org/tutorials/structured_data/time_series)

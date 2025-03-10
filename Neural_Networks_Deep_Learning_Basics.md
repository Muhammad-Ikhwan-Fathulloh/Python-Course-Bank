# Materi: Neural Network Architecture, Training, dan Frameworks

---

## 1. Neural Network Architecture

### a. **Struktur Dasar Neural Network**
1. **Input Layer**:
   - Lapisan pertama yang menerima data input.
   - Jumlah neuron sesuai dengan jumlah fitur dalam dataset.
2. **Hidden Layers**:
   - Lapisan antara input dan output.
   - Jumlah lapisan dan neuron dapat bervariasi.
3. **Output Layer**:
   - Lapisan terakhir yang menghasilkan prediksi.
   - Jumlah neuron sesuai dengan jumlah kelas (klasifikasi) atau nilai tunggal (regresi).

### b. **Fungsi Aktivasi**
- **ReLU (Rectified Linear Unit)**:
  - \( f(x) = \max(0, x) \)
  - Digunakan di hidden layers untuk mengatasi masalah vanishing gradient.
- **Sigmoid**:
  - \( f(x) = \frac{1}{1 + e^{-x}} \)
  - Digunakan di output layer untuk klasifikasi biner.
- **Softmax**:
  - \( f(x_i) = \frac{e^{x_i}}{\sum_{j} e^{x_j}} \)
  - Digunakan di output layer untuk klasifikasi multi-kelas.

---

## 2. Forward & Backward Propagation

### a. **Forward Propagation**
- Proses menghitung prediksi dari input hingga output.
- Langkah:
  1. Hitung weighted sum di setiap neuron.
  2. Terapkan fungsi aktivasi.
  3. Lanjutkan ke lapisan berikutnya hingga output layer.

### b. **Backward Propagation**
- Proses menghitung gradien error dan memperbarui bobot.
- Langkah:
  1. Hitung error di output layer.
  2. Propagasi error ke belakang menggunakan aturan rantai.
  3. Perbarui bobot menggunakan gradien.

---

## 3. Loss Functions

### a. **Cross-Entropy (Klasifikasi)**
- Mengukur perbedaan antara prediksi dan label aktual.
- Rumus:
  \[
  \text{Cross-Entropy} = -\sum_{i} y_i \log(\hat{y}_i)
  \]
- Contoh: Digunakan untuk klasifikasi biner atau multi-kelas.

### b. **MSE (Mean Squared Error) (Regresi)**
- Mengukur rata-rata kuadrat selisih antara prediksi dan nilai aktual.
- Rumus:
  \[
  \text{MSE} = \frac{1}{n} \sum_{i=1}^{n} (y_i - \hat{y}_i)^2
  \]
- Contoh: Digunakan untuk masalah regresi.

---

## 4. Optimizers

### a. **SGD (Stochastic Gradient Descent)**
- Memperbarui bobot menggunakan gradien dari satu sampel atau mini-batch.
- Rumus:
  \[
  w = w - \eta \nabla_w \text{Loss}
  \]
  - \( \eta \): Learning rate.

### b. **Adam (Adaptive Moment Estimation)**
- Kombinasi momentum dan adaptive learning rate.
- Lebih cepat dan stabil dibanding SGD.

### c. **Learning Rate Schedules**
- Menyesuaikan learning rate selama training.
- Contoh: Step decay, exponential decay.

---

## 5. Regularization

### a. **Dropout**
- Menonaktifkan neuron secara acak selama training untuk mencegah overfitting.
- Contoh:
  ```python
  from tensorflow.keras.layers import Dropout
  model.add(Dropout(0.5))
  ```

### b. **Batch Normalization**
- Menormalkan output dari lapisan sebelumnya untuk mempercepat training.
- Contoh:
  ```python
  from tensorflow.keras.layers import BatchNormalization
  model.add(BatchNormalization())
  ```

### c. **Early Stopping**
- Menghentikan training jika performa model tidak membaik pada validation set.
- Contoh:
  ```python
  from tensorflow.keras.callbacks import EarlyStopping
  early_stopping = EarlyStopping(monitor='val_loss', patience=5)
  model.fit(X_train, y_train, validation_data=(X_val, y_val), callbacks=[early_stopping])
  ```

---

## 6. Common Architectures

### a. **CNNs (Convolutional Neural Networks)**
- Digunakan untuk data gambar.
- Lapisan utama:
  - **Convolutional Layer**: Mengekstrak fitur dari gambar.
  - **Pooling Layer**: Mengurangi dimensi gambar.
  - **Fully Connected Layer**: Menghasilkan prediksi.

### b. **RNNs/LSTMs (Recurrent Neural Networks/Long Short-Term Memory)**
- Digunakan untuk data sekuensial (teks, time series).
- **RNN**: Memproses data sekuensial dengan mempertahankan state.
- **LSTM**: Variasi RNN yang mengatasi masalah vanishing gradient.

---

## 7. Frameworks

### a. **TensorFlow**
- Library open-source untuk machine learning.
- Contoh:
  ```python
  import tensorflow as tf
  model = tf.keras.Sequential([
      tf.keras.layers.Dense(128, activation='relu'),
      tf.keras.layers.Dense(10, activation='softmax')
  ])
  model.compile(optimizer='adam', loss='sparse_categorical_crossentropy', metrics=['accuracy'])
  model.fit(X_train, y_train, epochs=10)
  ```

### b. **PyTorch**
- Library open-source yang fleksibel untuk deep learning.
- Contoh:
  ```python
  import torch
  import torch.nn as nn
  import torch.optim as optim
  model = nn.Sequential(
      nn.Linear(784, 128),
      nn.ReLU(),
      nn.Linear(128, 10),
      nn.Softmax(dim=1)
  )
  criterion = nn.CrossEntropyLoss()
  optimizer = optim.Adam(model.parameters(), lr=0.001)
  for epoch in range(10):
      outputs = model(X_train)
      loss = criterion(outputs, y_train)
      optimizer.zero_grad()
      loss.backward()
      optimizer.step()
  ```

---

## 8. Mini-Project: Building a Simple NN for MNIST Digit Classification

### Langkah 1: Load Dataset
- MNIST adalah dataset digit tulisan tangan (0-9).
  ```python
  from tensorflow.keras.datasets import mnist
  (X_train, y_train), (X_test, y_test) = mnist.load_data()
  ```

### Langkah 2: Preprocessing
- Normalisasi dan reshape data.
  ```python
  X_train = X_train.reshape(-1, 28*28) / 255.0
  X_test = X_test.reshape(-1, 28*28) / 255.0
  ```

### Langkah 3: Bangun Model
- Gunakan TensorFlow/Keras untuk membuat model sederhana.
  ```python
  model = tf.keras.Sequential([
      tf.keras.layers.Dense(128, activation='relu', input_shape=(784,)),
      tf.keras.layers.Dense(10, activation='softmax')
  ])
  ```

### Langkah 4: Compile dan Train Model
- Compile model dengan optimizer dan loss function.
  ```python
  model.compile(optimizer='adam', loss='sparse_categorical_crossentropy', metrics=['accuracy'])
  model.fit(X_train, y_train, epochs=10, validation_data=(X_test, y_test))
  ```

### Langkah 5: Evaluasi Model
- Evaluasi performa model pada test set.
  ```python
  test_loss, test_acc = model.evaluate(X_test, y_test)
  print(f"Test Accuracy: {test_acc}")
  ```

---

## 9. Kesimpulan
- **Neural Network** adalah model yang powerful untuk berbagai tugas machine learning.
- Dengan memahami arsitektur, training, dan teknik regularisasi, Anda dapat membangun model yang efektif.
- **TensorFlow** dan **PyTorch** adalah framework populer untuk implementasi neural network.

Selamat mencoba mini-project dan eksplorasi lebih lanjut! 🚀

---

## Referensi
1. [TensorFlow Documentation](https://www.tensorflow.org/)
2. [PyTorch Documentation](https://pytorch.org/)
3. [MNIST](https://github.com/Muhammad-Ikhwan-Fathulloh/Generative-Adversarial-Network-GAN/tree/main/MNIST)
4. [Deep Learning Specialization - Coursera](https://www.coursera.org/specializations/deep-learning)
5. [MNIST Dataset - TensorFlow](https://www.tensorflow.org/datasets/catalog/mnist)

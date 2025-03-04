# **Introduction to Python, Jupyter Lab, & Google Colab**

Python adalah bahasa pemrograman tingkat tinggi yang populer karena sintaksnya yang mudah dipahami dan fleksibilitasnya. Python digunakan untuk berbagai tujuan, seperti pengembangan web, analisis data, kecerdasan buatan, dan banyak lagi. Dalam materi ini, kita akan mempelajari dasar-dasar Python dan bagaimana menggunakan **Jupyter Lab** dan **Google Colab** sebagai lingkungan pengembangan.

---

## **1. Print Function**
Fungsi `print()` digunakan untuk menampilkan teks atau output ke konsol.

**Contoh:**
```python
print("Hello, World!")
```
**Output:**
```
Hello, World!
```

Anda juga dapat mencetak beberapa nilai sekaligus:
```python
print("Nama:", "Ali", "Usia:", 25)
```
**Output:**
```
Nama: Ali Usia: 25
```

---

## **2. Data Type in Python**
Python memiliki beberapa tipe data bawaan, di antaranya:

| Tipe Data | Contoh                  |
|-----------|-------------------------|
| `int`     | `10`, `-5`              |
| `float`   | `3.14`, `-0.001`        |
| `str`     | `"Hello"`, `'Python'`   |
| `bool`    | `True`, `False`         |
| `list`    | `[1, 2, 3]`             |
| `tuple`   | `(1, 2, 3)`             |
| `dict`    | `{"nama": "Ali", "usia": 25}` |

**Contoh:**
```python
angka = 10
teks = "Python"
benar = True
print(type(angka))  # Output: <class 'int'>
print(type(teks))   # Output: <class 'str'>
print(type(benar))  # Output: <class 'bool'>
```

---

## **3. Comments**
Komentar digunakan untuk menjelaskan kode dan tidak akan dieksekusi oleh Python.

- **Single-line comment:** Menggunakan `#`.
  ```python
  # Ini adalah komentar
  print("Hello")  # Ini juga komentar
  ```

- **Multi-line comment:** Menggunakan `"""` atau `'''`.
  ```python
  """
  Ini adalah komentar
  multi-line.
  """
  print("World")
  ```

---

## **4. Keywords**
Keywords adalah kata-kata yang sudah dipesan oleh Python dan memiliki makna khusus. Contoh: `if`, `else`, `for`, `while`, `def`, `class`, dll.

**Contoh:**
```python
import keyword
print(keyword.kwlist)  # Menampilkan daftar semua keyword di Python
```

---

## **5. Variables**
Variabel digunakan untuk menyimpan data. Nama variabel harus dimulai dengan huruf atau underscore (`_`) dan tidak boleh menggunakan keyword.

**Contoh:**
```python
nama = "Ali"
usia = 25
tinggi = 175.5
print(nama, usia, tinggi)
```
**Output:**
```
Ali 25 175.5
```

---

## **6. Type Conversion**
Anda dapat mengubah tipe data menggunakan fungsi seperti `int()`, `float()`, `str()`, dll.

**Contoh:**
```python
angka = "10"
angka_int = int(angka)  # Konversi string ke integer
print(angka_int + 5)    # Output: 15
```

---

## **7. User Input**
Fungsi `input()` digunakan untuk mengambil input dari pengguna.

**Contoh:**
```python
nama = input("Masukkan nama Anda: ")
print("Halo,", nama)
```
**Output (jika input "Ali"):**
```
Halo, Ali
```

---

## **8. Literals**
Literals adalah nilai konstan yang ditulis langsung dalam kode. Contoh: `5`, `3.14`, `"Hello"`, `True`.

**Contoh:**
```python
angka = 42          # Integer literal
teks = "Python"     # String literal
benar = True        # Boolean literal
```

---

## **9. Operators**
Python mendukung berbagai operator:

| Jenis Operator | Contoh                  |
|----------------|-------------------------|
| Aritmatika     | `+`, `-`, `*`, `/`, `%` |
| Perbandingan   | `==`, `!=`, `>`, `<`    |
| Logika         | `and`, `or`, `not`      |
| Assignment     | `=`, `+=`, `-=`, `*=`   |

**Contoh:**
```python
a = 10
b = 3
print(a + b)   # Output: 13
print(a > b)   # Output: True
print(a == b)  # Output: False
```

---

## **10. If-else Statements**
Digunakan untuk pengambilan keputusan berdasarkan kondisi.

**Contoh:**
```python
usia = 18
if usia >= 18:
    print("Anda dewasa.")
else:
    print("Anda masih anak-anak.")
```
**Output:**
```
Anda dewasa.
```

---

## **11. While Loop**
Digunakan untuk mengulang blok kode selama kondisi terpenuhi.

**Contoh:**
```python
angka = 1
while angka <= 5:
    print(angka)
    angka += 1
```
**Output:**
```
1
2
3
4
5
```

---

## **12. For Loop**
Digunakan untuk mengulang blok kode sejumlah iterasi tertentu.

**Contoh:**
```python
for i in range(5):
    print(i)
```
**Output:**
```
0
1
2
3
4
```

---

## **13. Break, Continue, Pass**
- **Break:** Menghentikan loop.
- **Continue:** Melanjutkan ke iterasi berikutnya.
- **Pass:** Placeholder untuk kode yang belum diimplementasikan.

**Contoh:**
```python
for i in range(10):
    if i == 5:
        break  # Loop berhenti saat i = 5
    print(i)
```
**Output:**
```
0
1
2
3
4
```

---

## **14. Jupyter Lab**
Jupyter Lab adalah lingkungan pengembangan interaktif untuk menulis dan menjalankan kode Python. Anda dapat menulis kode dalam sel (cell) dan menjalankannya secara terpisah.

**Cara Menggunakan:**
1. Install Jupyter Lab:
   ```bash
   pip install jupyterlab
   ```
2. Jalankan Jupyter Lab:
   ```bash
   jupyter lab
   ```
3. Buat notebook baru dan mulai menulis kode Python.

---

## **15. Google Colab**
Google Colab adalah lingkungan pengembangan berbasis cloud yang menyediakan akses ke notebook Jupyter secara gratis. Colab juga menyediakan akses ke GPU dan TPU untuk komputasi yang lebih cepat.

**Cara Menggunakan:**
1. Buka [Google Colab](https://colab.research.google.com/).
2. Buat notebook baru dengan mengklik **File > New Notebook**.
3. Mulai menulis dan menjalankan kode Python.

**Keunggulan Google Colab:**
- Tidak perlu instalasi, cukup akses melalui browser.
- Terintegrasi dengan Google Drive untuk menyimpan notebook.
- Mendukung akses ke GPU dan TPU secara gratis.

**Contoh Penggunaan:**
```python
# Contoh kode di Google Colab
print("Hello, Google Colab!")
```
**Output:**
```
Hello, Google Colab!
```

Link Google Colab = https://colab.research.google.com/drive/1ntzv9_0ip6IecSiAjSvvQPwUfO05T1qA?usp=sharing

# **Python for Data & SQL Integration**

Python adalah bahasa pemrograman yang sangat populer untuk analisis data dan integrasi dengan database. Dalam materi ini, kita akan mempelajari bagaimana menggunakan Python untuk bekerja dengan data, termasuk integrasi dengan database PostgreSQL menggunakan Aiven. Kita juga akan membahas konsep-konsep penting seperti fungsi bawaan, modul Python, dan struktur data seperti list, tuple, set, dan dictionary.

---

## **1. Built-in Functions**
Python menyediakan banyak fungsi bawaan yang dapat digunakan untuk memanipulasi data. Beberapa fungsi bawaan yang sering digunakan:

- `len()`: Menghitung panjang objek (string, list, dll).
- `type()`: Mengetahui tipe data suatu objek.
- `int()`, `float()`, `str()`: Mengubah tipe data.
- `sum()`, `min()`, `max()`: Menghitung jumlah, nilai minimum, dan nilai maksimum.
- `sorted()`: Mengurutkan data.

**Contoh:**
```python
data = [10, 20, 30, 40, 50]
print(len(data))       # Output: 5
print(sum(data))       # Output: 150
print(min(data))       # Output: 10
print(sorted(data))    # Output: [10, 20, 30, 40, 50]
```

---

## **2. Python Modules (Libraries)**
Modul adalah file Python yang berisi fungsi dan variabel yang dapat digunakan di program lain. Beberapa modul populer untuk analisis data dan integrasi SQL:

- **`psycopg2`:** Untuk koneksi ke database PostgreSQL.
- **`pandas`:** Untuk manipulasi dan analisis data.
- **`numpy`:** Untuk komputasi numerik.
- **`matplotlib`:** Untuk visualisasi data.

**Contoh:**
```python
import psycopg2
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
```

---

## **3. Strings in Python**
String adalah tipe data yang digunakan untuk menyimpan teks. Python menyediakan banyak metode untuk memanipulasi string.

**Contoh:**
```python
teks = "Hello, Python"
print(teks.upper())       # Output: HELLO, PYTHON
print(teks.lower())       # Output: hello, python
print(teks.replace("Python", "World"))  # Output: Hello, World
print(teks.split(","))    # Output: ['Hello', ' Python']
```

---

## **4. List**
List adalah struktur data yang dapat menyimpan banyak nilai dalam satu variabel. List bersifat mutable (dapat diubah).

**Contoh:**
```python
buah = ["Apel", "Mangga", "Jeruk"]
buah.append("Pisang")  # Menambahkan elemen
print(buah)           # Output: ['Apel', 'Mangga', 'Jeruk', 'Pisang']
buah.remove("Mangga") # Menghapus elemen
print(buah)           # Output: ['Apel', 'Jeruk', 'Pisang']
```

---

## **5. Tuple**
Tuple mirip dengan list, tetapi bersifat immutable (tidak dapat diubah).

**Contoh:**
```python
koordinat = (10, 20)
print(koordinat[0])  # Output: 10
# koordinat[0] = 5  # Akan error karena tuple tidak bisa diubah
```

---

## **6. Set**
Set adalah kumpulan data unik yang tidak memiliki urutan.

**Contoh:**
```python
angka = {1, 2, 3, 3, 4}
print(angka)  # Output: {1, 2, 3, 4} (duplikat dihapus)
angka.add(5)  # Menambahkan elemen
print(angka)  # Output: {1, 2, 3, 4, 5}
```

---

## **7. Dictionary**
Dictionary adalah struktur data yang menyimpan pasangan key-value.

**Contoh:**
```python
mahasiswa = {"nama": "Ali", "usia": 25, "kota": "Jakarta"}
print(mahasiswa["nama"])  # Output: Ali
mahasiswa["usia"] = 26    # Mengubah nilai
print(mahasiswa)          # Output: {'nama': 'Ali', 'usia': 26, 'kota': 'Jakarta'}
```

---

## **8. Integrasi Python dengan PostgreSQL**
Kita akan menggunakan modul `psycopg2` untuk terhubung ke database PostgreSQL di Aiven.

### **Koneksi ke Database**
```python
import psycopg2

# Detail koneksi
conn_details = {
    "host": "test.aivencloud.com",
    "port": 5432,
    "database": "defaultdb",
    "user": "admin",
    "password": "**********",
    "sslmode": "require"
}

# Membuat koneksi
conn = psycopg2.connect(**conn_details)
cursor = conn.cursor()
print("Koneksi berhasil!")
```

### **Membuat Tabel**
```python
create_table_query = """
CREATE TABLE IF NOT EXISTS pelanggan (
    id SERIAL PRIMARY KEY,
    nama VARCHAR(100),
    email VARCHAR(100),
    kota VARCHAR(50)
);
"""
cursor.execute(create_table_query)
conn.commit()
print("Tabel berhasil dibuat!")
```

### **Memasukkan Data**
```python
insert_query = """
INSERT INTO pelanggan (nama, email, kota) 
VALUES (%s, %s, %s);
"""
data = ("Ali", "ali@example.com", "Jakarta")
cursor.execute(insert_query, data)
conn.commit()
print("Data berhasil dimasukkan!")
```

### **Mengambil Data**
```python
select_query = "SELECT * FROM pelanggan;"
cursor.execute(select_query)
rows = cursor.fetchall()
for row in rows:
    print(row)
```

### **Menutup Koneksi**
```python
cursor.close()
conn.close()
print("Koneksi ditutup.")
```

---

## **9. Analisis Data dengan Pandas**
Pandas adalah library Python yang sangat berguna untuk analisis data. Kita dapat menggunakan Pandas untuk membaca data dari database dan melakukan analisis.

**Contoh:**
```python
import pandas as pd

# Membaca data dari database ke DataFrame
query = "SELECT * FROM pelanggan;"
df = pd.read_sql(query, conn)
print(df)

# Analisis sederhana
print(df.describe())  # Statistik deskriptif
print(df["kota"].value_counts())  # Menghitung jumlah pelanggan per kota
```

---

## **10. Visualisasi Data dengan Matplotlib**
Matplotlib digunakan untuk membuat visualisasi data.

**Contoh:**
```python
import matplotlib.pyplot as plt

# Menghitung jumlah pelanggan per kota
kota_counts = df["kota"].value_counts()

# Membuat bar plot
kota_counts.plot(kind="bar")
plt.title("Jumlah Pelanggan per Kota")
plt.xlabel("Kota")
plt.ylabel("Jumlah Pelanggan")
plt.show()
```

---

## **11. Studi Kasus: Analisis Data Pelanggan**
Mari kita gabungkan semua konsep yang telah dipelajari untuk menganalisis data pelanggan dari database.

### **Langkah-langkah:**
1. Terhubung ke database PostgreSQL.
2. Ambil data pelanggan menggunakan Pandas.
3. Lakukan analisis sederhana (misalnya, jumlah pelanggan per kota).
4. Visualisasikan hasil analisis menggunakan Matplotlib.

**Contoh Kode:**
```python
# Langkah 1: Koneksi ke database
conn = psycopg2.connect(**conn_details)

# Langkah 2: Ambil data pelanggan
query = "SELECT * FROM pelanggan;"
df = pd.read_sql(query, conn)

# Langkah 3: Analisis data
print("Jumlah pelanggan per kota:")
print(df["kota"].value_counts())

# Langkah 4: Visualisasi data
kota_counts = df["kota"].value_counts()
kota_counts.plot(kind="bar", color="skyblue")
plt.title("Jumlah Pelanggan per Kota")
plt.xlabel("Kota")
plt.ylabel("Jumlah Pelanggan")
plt.show()

# Tutup koneksi
conn.close()
```

# **Python for Data & SQL Integration with Google Colab**

Dalam materi ini, kita akan mempelajari bagaimana menggunakan **Google Colab** untuk bekerja dengan data dan mengintegrasikannya dengan database PostgreSQL menggunakan Aiven. Kita akan menggabungkan konsep-konsep SQL dan Python untuk analisis data, termasuk penggunaan library seperti `pandas`, `psycopg2`, dan `matplotlib`.

---

## **1. Persiapan Google Colab**
Google Colab adalah lingkungan pengembangan berbasis cloud yang memungkinkan Anda menjalankan kode Python secara interaktif. Berikut langkah-langkah untuk memulai:

1. Buka [Google Colab](https://colab.research.google.com/).
2. Buat notebook baru dengan mengklik **File > New Notebook**.
3. Mulai menulis dan menjalankan kode Python.

---

## **2. Install Library yang Diperlukan**
Sebelum memulai, kita perlu menginstall library yang diperlukan seperti `psycopg2` (untuk koneksi ke PostgreSQL) dan `pandas` (untuk analisis data).

**Kode di Google Colab:**
```python
!pip install psycopg2-binary pandas matplotlib
```

---

## **3. Koneksi ke Database PostgreSQL**
Kita akan menggunakan detail koneksi dari Aiven untuk terhubung ke database PostgreSQL.

### **Detail Koneksi:**
- **Host:** `test.aivencloud.com`
- **Port:** `5432`
- **Database:** `defaultdb`
- **User:** `admin`
- **Password:** `**********`
- **SSL Mode:** `require`

### **Kode untuk Koneksi:**
```python
import psycopg2

# Detail koneksi
conn_details = {
    "host": "pg-bc25cc-utb-1779.f.aivencloud.com",
    "port": 14992,
    "database": "defaultdb",
    "user": "avnadmin",
    "password": "**********",
    "sslmode": "require"
}

# Membuat koneksi
try:
    conn = psycopg2.connect(**conn_details)
    cursor = conn.cursor()
    print("Koneksi ke database berhasil!")
except Exception as e:
    print(f"Error: {e}")
```

---

## **4. Membuat Tabel dan Memasukkan Data**
Kita akan menggunakan struktur tabel dari materi SQL sebelumnya dan memasukkan data ke dalamnya.

### **Struktur Tabel:**
- **pelanggan** (id, nama, email, kota)
- **produk** (id, nama, harga, stok, kategori_id)
- **kategori** (id, nama_kategori)
- **transaksi** (id, pelanggan_id, produk_id, jumlah, total_harga, tanggal)

### **Kode untuk Membuat Tabel:**
```python
# Membuat tabel pelanggan
create_pelanggan_table = """
CREATE TABLE IF NOT EXISTS pelanggan (
    id SERIAL PRIMARY KEY,
    nama VARCHAR(100),
    email VARCHAR(100),
    kota VARCHAR(50)
);
"""
cursor.execute(create_pelanggan_table)
conn.commit()
print("Tabel pelanggan berhasil dibuat!")
```

### **Kode untuk Memasukkan Data:**
```python
# Memasukkan data ke tabel pelanggan
insert_pelanggan = """
INSERT INTO pelanggan (nama, email, kota) 
VALUES (%s, %s, %s);
"""
data_pelanggan = [
    ("Ali", "ali@example.com", "Jakarta"),
    ("Budi", "budi@example.com", "Bandung"),
    ("Citra", "citra@example.com", "Surabaya")
]
cursor.executemany(insert_pelanggan, data_pelanggan)
conn.commit()
print("Data pelanggan berhasil dimasukkan!")
```

---

## **5. Mengambil Data dari Database**
Kita akan mengambil data dari tabel `pelanggan` dan menampilkannya menggunakan Pandas.

### **Kode untuk Mengambil Data:**
```python
import pandas as pd

# Query untuk mengambil data pelanggan
query = "SELECT * FROM pelanggan;"
df_pelanggan = pd.read_sql(query, conn)

# Menampilkan data
print(df_pelanggan)
```

**Output:**
```
   id   nama           email      kota
0   1    Ali   ali@example.com   Jakarta
1   2   Budi  budi@example.com   Bandung
2   3  Citra  citra@example.com  Surabaya
```

---

## **6. Analisis Data dengan Pandas**
Kita akan melakukan analisis sederhana seperti menghitung jumlah pelanggan per kota.

### **Kode untuk Analisis:**
```python
# Menghitung jumlah pelanggan per kota
pelanggan_per_kota = df_pelanggan["kota"].value_counts()
print("Jumlah pelanggan per kota:")
print(pelanggan_per_kota)
```

**Output:**
```
Jakarta     1
Bandung     1
Surabaya    1
Name: kota, dtype: int64
```

---

## **7. Visualisasi Data dengan Matplotlib**
Kita akan menggunakan Matplotlib untuk membuat visualisasi data.

### **Kode untuk Visualisasi:**
```python
import matplotlib.pyplot as plt

# Membuat bar plot
pelanggan_per_kota.plot(kind="bar", color="skyblue")
plt.title("Jumlah Pelanggan per Kota")
plt.xlabel("Kota")
plt.ylabel("Jumlah Pelanggan")
plt.show()
```

---

## **8. Studi Kasus: Analisis Transaksi**
Mari kita lanjutkan dengan analisis data transaksi dari tabel `transaksi`.

### **Kode untuk Membuat Tabel Transaksi:**
```python
# Membuat tabel transaksi
create_transaksi_table = """
CREATE TABLE IF NOT EXISTS transaksi (
    id SERIAL PRIMARY KEY,
    pelanggan_id INT REFERENCES pelanggan(id),
    produk_id INT REFERENCES produk(id),
    jumlah INT,
    total_harga DECIMAL(10,2),
    tanggal TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
"""
cursor.execute(create_transaksi_table)
conn.commit()
print("Tabel transaksi berhasil dibuat!")
```

### **Kode untuk Memasukkan Data Transaksi:**
```python
# Memasukkan data transaksi
insert_transaksi = """
INSERT INTO transaksi (pelanggan_id, produk_id, jumlah, total_harga) 
VALUES (%s, %s, %s, %s);
"""
data_transaksi = [
    (1, 1, 2, 14000000),  # Ali membeli 2 laptop
    (2, 2, 3, 450000),    # Budi membeli 3 baju
    (3, 3, 5, 125000)     # Citra membeli 5 snack
]
cursor.executemany(insert_transaksi, data_transaksi)
conn.commit()
print("Data transaksi berhasil dimasukkan!")
```

### **Kode untuk Analisis Transaksi:**
```python
# Query untuk mengambil data transaksi
query_transaksi = """
SELECT t.id, p.nama AS pelanggan, pr.nama AS produk, t.jumlah, t.total_harga, t.tanggal
FROM transaksi t
JOIN pelanggan p ON t.pelanggan_id = p.id
JOIN produk pr ON t.produk_id = pr.id;
"""
df_transaksi = pd.read_sql(query_transaksi, conn)

# Menampilkan data transaksi
print(df_transaksi)
```

**Output:**
```
   id pelanggan  produk  jumlah  total_harga                   tanggal
0   1       Ali  Laptop       2   14000000.0  2023-10-01 12:00:00.000
1   2      Budi    Baju       3     450000.0  2023-10-01 12:05:00.000
2   3     Citra   Snack       5     125000.0  2023-10-01 12:10:00.000
```

---

## **9. Menutup Koneksi**
Setelah selesai, jangan lupa untuk menutup koneksi ke database.

### **Kode untuk Menutup Koneksi:**
```python
cursor.close()
conn.close()
print("Koneksi ke database ditutup.")
```

---

## **10. Kesimpulan**
Dengan menggunakan **Google Colab**, Anda dapat dengan mudah mengintegrasikan Python dan SQL untuk analisis data. Anda juga dapat memanfaatkan library seperti `pandas` dan `matplotlib` untuk manipulasi dan visualisasi data. Selamat mencoba! 🚀

---

**Referensi:**
- [Google Colab Documentation](https://colab.research.google.com/notebooks/intro.ipynb)
- [Psycopg2 Documentation](https://www.psycopg.org/docs/)
- [Pandas Documentation](https://pandas.pydata.org/docs/)
- [Matplotlib Documentation](https://matplotlib.org/stable/contents.html)

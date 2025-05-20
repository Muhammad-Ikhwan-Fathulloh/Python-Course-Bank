# Fundamental Programming with Python - Google Colab Friendly

Panduan ini terdiri dari 7 bab yang dapat dijalankan langsung di Google Colab. Cocok untuk pemula yang ingin belajar dasar-dasar Python dengan contoh langsung.

---

## Bab 1: Pengenalan Python

### Apa itu Python?

Python adalah bahasa pemrograman tingkat tinggi yang mendukung berbagai paradigma seperti object-oriented, imperatif, dan fungsional. Python terkenal karena sintaksnya yang sederhana dan mudah dibaca, serta komunitasnya yang besar.

### Kelebihan Python:

* Mendukung multi-paradigma
* Bahasa yang diinterpretasi
* Tipe data dinamis
* Multi-platform
* Sintaks yang mudah dipahami
* Banyak library dan framework
* Gratis dan open source

### Hello World

Contoh paling dasar untuk mencetak ke layar:

```python
print("Hello World")
```

### Latihan:

Tampilkan bentuk kotak dengan karakter `*`

```python
print("**********")
print("*        *")
print("**********")
```

---

## Bab 2: Variabel, Tipe Data, dan Operator

### Variabel

Variabel digunakan untuk menyimpan nilai:

```python
nama = "Ikhwan"
umur = 20
tinggi = 170.5
print(type(nama), type(umur), type(tinggi))
```

### Tipe Data

Python memiliki berbagai tipe data dasar:

* `int`: bilangan bulat
* `float`: bilangan desimal
* `str`: string/teks
* `bool`: True atau False

```python
nilai = 80
print(type(nilai))
nilai = "delapan puluh"
print(type(nilai))
```

### Konversi Tipe Data

```python
a = 10
b = 3
hasil = float(a) / float(b)
print(hasil)
```

### Operator

#### Aritmatika:

```python
x = 5
y = 2
print("Penjumlahan:", x + y)
print("Pengurangan:", x - y)
print("Perkalian:", x * y)
print("Pembagian:", x / y)
```

#### Pembanding & Logika:

```python
print(x == y)
print(x != y)
print(x > y)
print(x < y)
print(x >= y)
print(x <= y)
print(x == 5 and y == 2)
```

#### Ternary:

```python
status = "Dewasa" if umur >= 17 else "Anak"
print(status)
```

---

## Bab 3: Percabangan dan Perulangan

### If, Elif, Else

```python
nilai = 75
if nilai >= 80:
    print("A")
elif nilai >= 70:
    print("B")
else:
    print("C")
```

### For Loop

```python
for i in range(5):
    print("Perulangan ke-", i)
```

### While Loop

```python
hitung = 0
while hitung < 3:
    print("Loop ke-", hitung)
    hitung += 1
```

### Latihan:

Buat program tebak angka:

```python
angka_rahasia = 7
tebak = int(input("Tebak angka 1-10: "))
while tebak != angka_rahasia:
    if tebak < angka_rahasia:
        print("Terlalu kecil!")
    else:
        print("Terlalu besar!")
    tebak = int(input("Tebak lagi: "))
print("Selamat, benar!")
```

---

## Bab 4: Fungsi

### Fungsi Tanpa Parameter

```python
def halo():
    print("Halo Dunia")
halo()
```

### Fungsi Dengan Parameter dan Return

```python
def luas_persegi(sisi):
    return sisi * sisi
print("Luas:", luas_persegi(4))
```

### Rekursif: Faktorial

```python
def faktorial(n):
    if n == 1:
        return 1
    return n * faktorial(n - 1)
print(faktorial(5))
```

### Variabel Global vs Lokal

```python
nama = "Budi"
def tampil():
    nama = "Agus"
    print("Dalam fungsi:", nama)

tampil()
print("Di luar fungsi:", nama)
```

---

## Bab 5: List

### Membuat dan Mengakses List

```python
buah = ["apel", "jeruk", "mangga"]
print(buah[1])
```

### Menambahkan, Menghapus, Mengganti Item

```python
buah.append("pisang")
buah[0] = "semangka"
del buah[1]
print(buah)
```

### List Multidimensi

```python
minuman = [["teh", "kopi"], ["jus", "soda"]]
print(minuman[1][0])
```

### Operasi List

```python
buah1 = ["apel", "mangga"]
buah2 = ["jeruk", "pisang"]
semua_buah = buah1 + buah2
print(semua_buah)
```

---

## Bab 6: Tuple & Set

### Tuple

```python
hari = ("senin", "selasa", "rabu")
print(hari[0])
```

### Set

```python
hobi = {"makan", "tidur", "coding"}
hobi.add("jalan")
hobi.discard("makan")
print(hobi)
```

### Operasi Set

```python
A = {1, 2, 3}
B = {3, 4, 5}
print("Gabungan:", A | B)
print("Irisan:", A & B)
print("Selisih:", A - B)
print("Simetri:", A ^ B)
```

---

## Bab 7: Dictionary

### Membuat Dictionary

```python
user = {
    "nama": "Ikhwan",
    "umur": 20,
    "hobi": ["ngoding", "ngopi"]
}
print(user["nama"])
```

### Update dan Tambah Data

```python
user["email"] = "ikhwan@email.com"
user.update({"umur": 21})
print(user)
```

### Loop Dictionary

```python
for key, val in user.items():
    print(f"{key}: {val}")
```

### Panjang Dictionary

```python
print("Total data:", len(user))
```

---

## Penutup

Materi ini adalah pondasi utama untuk menguasai Python. Lanjutkan eksplorasi ke:

* Manipulasi File
* Pandas & Numpy
* Flask/Django
* Data Visualization
* Machine Learning

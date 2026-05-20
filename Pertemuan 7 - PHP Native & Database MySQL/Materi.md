# Pertemuan 7: PHP Native & Database MySQL

## Pengenalan PHP 

- PHP singkatan dari PHP : Hypertext Preprocessor
- PHP banyak digunakan sebagai bahasa pemrograman yang dikhususkan untuk web development
- PHP sangat mudah digunakan dan banyak sekali diadopsi oleh programmer web
- Bahkan hampir mayoritas kebanyakan web di dunia dibuat menggunakan PHP
- PHP pertama kali dibuat oleh Rasmus Lerdorf pada tahun 1995

## Penulisan Kode PHP

Kode PHP ditulis di antara tag `<?php ... ?>`. Sebagai contoh:
```
<?php
echo "Hello World!";
?>
```

## Variabel & Tipe Data

### Variabel

Variabel pada kode PHP ditandai dengan tanda `$`. Contoh deklarasi variabel pada PHP:
```
$nama = "Budi";
echo $nama;
```

### Tipe Data

Tipe data pada variabel PHP dapat berupa teks (string), angka (integer), benar/salah (boolean), dll.
Contohnya:

```
$umur = 25; // integer
$nama = "Ayu"; // string
$aktif = true; // boolean
```

## Kondisi 

### IF, ELSE, dan ELSEIF

Bentuk umum dari `if` adalah sebagai berikut:
```
if (kondisi) {
    // kode yang dijalankan jika kondisi benar
} else {
    // kode yang dijalankan jika kondisi salah
}
```

`if` tidak harus selalu berpasangan dengan `else`. Kita bisa menggunakan `if` saja tanpa harus mencantumkan `else`. Sebagai contoh:
```
$umur = 17;

if ($umur >= 18) {
    return ('Kamu Belum Cukup Umur');
}

echo "Kamu punya akses!"
```

Jika memiliki beberapa kondisi, kita bisa menggunakan `elseif`. Sebagai contoh:
```
$nilai = 75;

if ($nilai >= 90) {
    echo "Nilai A";
} elseif ($nilai >= 80) {
    echo "Nilai B";
} elseif ($nilai >= 70) {
    echo "Nilai C";
} else {
    echo "Nilai D";
}
```

### SWITCH, CASE

`switch case` juga termasuk dalam struktur kondisi di PHP, akan tetapi lebih cocok dipakai saat kita punya banyak pilihan yang pasti nilainya.

Jika `if...else` cocok untuk kondisi beragam dan fleksibel, `switch case` cocok untuk kondisi yang nilainya tetap seperti angka atau string tertentu.

Contoh `switch case`:
```
$nilai = "B";

switch ($nilai) {
    case "A":
        echo "Sangat Baik";
        break;
    case "B":
        echo "Baik";
        break;
    case "C":
        echo "Cukup";
        break;
    default:
        echo "Nilai tidak dikenali";
}
```

## Perulangan (Loop)

Perulangan digunakan untuk menjalankan kode yang sama berulang kali, tanpa harus menulis ulang kodenya.

### Jenis-Jenis Perulangan

#### `for` Loop

Digunakan kalau kita tahu berapa kali ingin mengulang. Contoh:
```
<?php
for ($i = 1; $i <= 5; $i++) {
    echo "Ini perulangan ke-$i <br>";
}
?>
```

#### `while` Loop

Digunakan ketika kita tidak tahu pasti berapa kali harus mengulang, tapi tahu kondisinya. Contoh:
```
<?php
$i = 1;
while ($i <= 5) {
    echo "Angka: $i <br>";
    $i++;
}
?>
```

#### `do ... while` Loop

Mirip while, tapi kode dijalankan dulu minimal 1 kali, baru dicek kondisinya.
```
<?php
$i = 1;
do {
    echo "Nilai: $i <br>";
    $i++;
} while ($i <= 5);
?>
```

#### `foreach` 

Digunakan untuk mengulang isi dari array.
```
<?php
$buah = ["apel", "jeruk", "mangga"];

foreach ($buah as $item) {
    echo "Buah: $item <br>";
}
?>
```

## Function

Function adalah blok kode yang bisa dipanggil berkali-kali. Daripada menulis ulang suatu kode, kita bisa menuliskan kode yang ingin kita gunakan berulang kali di dalam function, kemudian kita cukup memanggil function itu aja. 

Berikut adalah bentuk dasar dari function:
```
function nama_fungsi() {
    // kode yang akan dijalankan
}

// Untuk memanggil function
nama_fungsi();
```

Contoh function sederhana:
```
function jumlah($a, $b) {
    return $a + $b;
}

$hasil = jumlah(5, 3);
echo $hasil;  // Output: 8
```

## MySQL

MySQL adalah tempat menyimpan data (seperti nama pengguna, email, dll).
Kalau kita analogikan, PHP itu adalah koki sedangkan MySQL itu lemari makanan. PHP akan "mengambil" dan "menyimpan" data dari/ke MySQL.

### Database

Database adalah sebuah tempat besar yang digunakan untuk menyimpan semua data. Dalam satu aplikasi biasanya punya satu database. Cara membuat database di MySQL:
```
CREATE DATABASE belajar_php;
```

### Tabel

Tabel memiliki struktur seperti lembar Excel: terdiri dari kolom dan baris. Tiap tabel dapat digunakan untuk menyimpan data tertentu (misalnya: tabel users  untuk simpan data pengguna). Cara membuat tabel di MySQL:
```
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nama VARCHAR(100),
    email VARCHAR(100),
    password VARCHAR(100)
);
```

### Kolom dan Tipe Data
Setiap kolom pasti mempunyai jenis data, contohnya:

- VARCHAR(100) = teks maksimal 100 karakter
- INT = angka bulat
- DATE = tanggal

### Foreign Key

Foreign key adalah kolom di satu tabel yang menghubungkan ke kolom PRIMARY KEY di tabel lain.
Analogi sederhananya seperti ini:

- Tabel users = daftar orang
- Tabel orders = daftar pesanan
- Di tabel `orders`, kita simpan user_id sebagai foreign key → agar tahu siapa yang mempunyai pesanan itu.

Contoh sederhana:

a. Membuat Tabel `users`
```
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nama VARCHAR(100)
);
```

b. Membuat Tabel `orders` Dengan Foreign Key `user_id`
```
CREATE TABLE orders (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nama_produk VARCHAR(100),
    user_id INT,
    FOREIGN KEY (user_id) REFERENCES users(id)
);
```

c. Menambahkan Data ke Dalam Tabel
- Menambahkan data pengguna
```
INSERT INTO users (nama, email, password)
VALUES ('April', 'april@gmail.com', '12345');
-- Misalnya id-nya 1
```
- Menambahkan data pesanan
```
INSERT INTO orders (nama_produk, user_id) VALUES ('Laptop', 1);
-- Bisa, karena user dengan id 1 ada
```

#### Catatan

a. Pastikan kolom foreign key dan kolom yang dirujuk punya tipe data yang sama (INT, VARCHAR, dll).

b.  Kalau kita mau menghapus user, tapi dia punya order, kita bisa atur foreign key-nya supaya:
- Ikut terhapus (ON DELETE CASCADE)
- Dicegah untuk dihapus (default)

Contoh:
```
FOREIGN KEY (user_id) REFERENCES users(id) ON DELETE CASCADE
```

### Koneksi PHP ke MySQL

a. Aktifkan Web-Server Kalian (XAMPP, Laragon, dll)

b. Buat Database dan Tabel di MySQL
- Buka browser dan pergi ke alamat `http://localhost/phpmyadmin`
- Klik 'Database' → beri nama misalnya `belajar_php` → klik 'Create'.

c. Buat tabel bernama `users` dengan kolom sebagai berikut:
- id (INT, AUTO_INCREMENT, PRIMARY)
- nama (VARCHAR 100)
- email (VARCHAR 100)

d. Buat file `koneksi.php`

```
<?php
$host = "localhost";
$user = "root";
$pass = "";
$db   = "belajar_php";

// Membuat koneksi
$conn = mysqli_connect($host, $user, $pass, $db);

// Cek koneksi
if (!$conn) {
    die("Koneksi gagal: " . mysqli_connect_error());
}
?>
```

### Menyimpan Data ke Dalam Database

Buat file baru bernama `store.php` dengan isi sebagai berikut:
```
<?php
include 'koneksi.php';

$nama = "Test";
$email = "testing@gmail.com";

$sql = "INSERT INTO users (nama, email) VALUES ('$nama', '$email')";

if (mysqli_query($conn, $sql)) {
    echo "Data berhasil ditambahkan!";
} else {
    echo "Error: " . mysqli_error($conn);
}
?>
```

### Menampilkan Data yang Ada di Dalam Database

Buat file baru bernama `show.php` dengan isi sebagai berikut:
```
<?php
include 'koneksi.php';

$sql = "SELECT * FROM users";
$result = mysqli_query($conn, $sql);

while ($row = mysqli_fetch_assoc($result)) {
    echo "ID: " . $row['id'] . "<br>";
    echo "Nama: " . $row['nama'] . "<br>";
    echo "Email: " . $row['email'] . "<hr>";
}
?>
```

## Contoh: Membuat Daftar Tamu Sederhana
### Fitur yang Akan Dibuat
1. Form input buku tamu: nama & pesan
2. Validasi sederhana: wajib isi nama dan pesan
3. Simpan ke database (MySQL)
4. Tampilkan semua pesan yang sudah masuk

### Struktur Folder
```
buku_tamu/
├── index.php        ← Form + tampil data
├── simpan.php       ← Proses simpan ke database
├── db.php           ← Koneksi ke MySQL
```

### 1. Membuat Database di MYSQL

Buka phpMyAdmin -> SQL. Kemudian paste query berikut:
```
CREATE DATABASE buku_tamu;

USE buku_tamu;

CREATE TABLE tamu (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nama VARCHAR(100),
    pesan TEXT,
    waktu DATETIME DEFAULT CURRENT_TIMESTAMP
);
```

### 2. Koneksi ke Database

Buat file bernama `db.php`, kemudian isi file tersebut sebagai berikut:
```
<?php
$host = "localhost";
$user = "root";
$pass = "";
$db   = "buku_tamu";

$conn = mysqli_connect($host, $user, $pass, $db);

if (!$conn) {
    die("Koneksi gagal: " . mysqli_connect_error());
}
?>
```

### 3. Membuat Frontend

Buat file dengan nama `index.php`, kemudian isi file tersebut dengan kode sebagai berikut:
```
<?php include 'db.php'; ?>
<!DOCTYPE html>
<html>
<head>
    <title>Buku Tamu Online</title>
</head>
<body>
    <h2>Isi Buku Tamu</h2>
    <form method="POST" action="simpan.php">
        Nama: <br>
        <input type="text" name="nama" required><br><br>
        Pesan: <br>
        <textarea name="pesan" required></textarea><br><br>
        <button type="submit">Kirim</button>
    </form>

    <hr>
    <h2>Daftar Tamu</h2>
    <?php
    $hasil = mysqli_query($conn, "SELECT * FROM tamu ORDER BY waktu DESC");
    while ($row = mysqli_fetch_assoc($hasil)) {
        echo "<p><strong>{$row['nama']}</strong> ({$row['waktu']}):<br>";
        echo nl2br(htmlspecialchars($row['pesan'])) . "</p><hr>";
    }
    ?>
</body>
</html>
```

### 4. Membuat Proses Menyimpan Data ke Database

Buat file bernama `simpan.php`, isi file tersebut dengan kode sebagai berikut:
```
<?php
include 'db.php';

$nama     = $_POST['nama'];
$pesan    = $_POST['pesan'];

$sql = "INSERT INTO users (nama, pesan) VALUES ('$nama', '$pesan')";

if (mysqli_query($conn, $sql)) {
    echo "Pendaftaran berhasil!";
} else {
    echo "Error: " . mysqli_error($conn);
}
?>
```

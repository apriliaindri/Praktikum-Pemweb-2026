# Pertemuan 8: OOP & Form Validation

## Apa itu OOP?
OOP (Pemrograman Berorientasi Objek) adalah paradigma pemrograman yang menggunakan "objek" untuk menyusun program. Objek adalah representasi nyata dari sesuatu (bisa orang, barang, data, dll), dan objek ini dibuat dari kelas (class).

Dalam OOP, kamu fokus membagi program ke dalam bagian-bagian kecil (objek) yang saling berinteraksi, bukan sekadar baris-baris kode prosedural.

## Class & Object
Class adalah cetakan (template) atau blueprint yang mendefinisikan struktur dan perilaku suatu objek. Class berisi atribut (data) dan metode (fungsi) yang berkaitan dengan objek.

Sedangkan Object adalah hasil nyata dari blueprint yang mampu menjalankan metode yang didefinisikan di dalam Class.

Contoh Class & Object:
```
class Mobil {
    public $warna;

    public function jalan() {
        echo "Mobil sedang berjalan";
    }
}

$mobilSaya = new Mobil(); // membuat object dari class
$mobilSaya->warna = "Merah";
$mobilSaya->jalan();
```

## Konsep Dasar OOP

Ada 4 konsep dasar pada OOP, yaitu:

### 1. Encapsulation
Encapsulation adalah sebuah konsep yang digunakan untuk menyembunyikan data dari akses langsung luar class sehingga hanya bagian-bagian tertentu saja yang dapat di akses di luar class.

Terdapat 3 jenis access modifier dalam PHP yaitu: 
- `public` -> Dapat di akses dari mana saja, baik dari dalam class maupun luar class.
- `private` -> Hanya dapat di akses dari dalam class itu sendiri.
- `protected` -> Hanya dapat di akses dari dalam class itu sendiri dan turunannya.

Contoh:
```
class User {
    private $password;

    public function setPassword($pwd) {
        $this->password = $pwd;
    }

    public function getPassword() {
        return $this->password;
    }
}
```

### 2. Inheritance (Pewarisan)
Inheritance adalah sebuah konsep dimana class baru (subclass) bisa mewarisi properti dan method dari class lain.

Contoh:
```
class Hewan {
    public function suara() {
        echo "Hewan bersuara";
    }
}

class Kucing extends Hewan {
    public function suara() {
        echo "Meong";
    }
}
```

### 3. Polymorphism
Polymorphism adalah sebuah konsep dimana method memiliki kemampuan yang sama tetapi perilakunya berbeda tergantung objeknya.

Contoh:
```
$hewan1 = new Hewan();
$kucing1 = new Kucing();

$hewan1->suara();  // Hewan bersuara
$kucing1->suara(); // Meong
```

### 4. Abstraction
Abstraksi adalah proses menyembunyikan detail kompleks dan hanya menampilkan fungsi penting dari suatu objek. Dengan kata lain, kita membuat kerangka (struktur) umum dari class, tanpa harus mengungkapkan bagaimana cara kerjanya secara detail.

Terdapat beberapa catatan pada abstract class:
- Tidak bisa dibuat objek secara langsung.
- Digunakan sebagai class dasar untuk diturunkan ke class lain.
- Bisa punya method yang sudah didefinisikan maupun method abstrak (yang harus diisi oleh class turunannya).

Contoh:
```
abstract class Hewan {
    abstract public function bersuara();

    public function tidur() {
        echo "Hewan sedang tidur";
    }
}

class Kucing extends Hewan {
    public function bersuara() {
        echo "Meong";
    }
}


// $hewan = new Hewan(); // Ini akan error
$kucing = new Kucing();
$kucing->bersuara(); // Output: Meong
```

## Implementasi OOP pada CRUD
Dalam aplikasi yang berhubungan dengan database (seperti MySQL), kamu sering bekerja dengan data yang punya bentuk tetap (misalnya data pengguna, produk, dll). Nah, setiap jenis data itu bisa direpresentasikan sebagai sebuah class.

Contoh:
- Class User untuk tabel users
- Class Produk untuk tabel produk

Dengan OOP, kamu bisa membuat method-method di dalam class yang menangani CRUD secara rapi dan terstruktur. Ayo kita contohkan dengan membuat contoh CRUD data mahasiswa.

### Struktur Folder
```
project/
│
├─ db.php           ← Koneksi ke database
├─ Mahasiswa.php    ← Class Mahasiswa (OOP)
├─ index.php        ← Menampilkan data (READ)
├─ tambah.php       ← Menambah data (CREATE)
├─ edit.php         ← Edit data (UPDATE)
├─ hapus.php        ← Hapus data (DELETE)
```

### Membuat Database
```
CREATE DATABASE belajar_oop;

USE belajar_oop;

CREATE TABLE mahasiswa (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nama VARCHAR(100),
    nim VARCHAR(20)
);
```

### `db.php` — Koneksi ke Database
```
<?php
$host = "localhost";
$user = "root";
$pass = "";
$db   = "belajar_oop";

$conn = new mysqli($host, $user, $pass, $db);

// Cek koneksi
if ($conn->connect_error) {
    die("Koneksi gagal: " . $conn->connect_error);
}
?>
```

### `Mahasiswa.php` — Class Mahasiswa (OOP)
```
<?php
require_once 'db.php';

class Mahasiswa {
    private $conn;

    public function __construct($db) {
        $this->conn = $db;
    }

    public function getAll() {
        $result = $this->conn->query("SELECT * FROM mahasiswa");
        return $result;
    }

    public function getById($id) {
        $stmt = $this->conn->prepare("SELECT * FROM mahasiswa WHERE id = ?");
        $stmt->bind_param("i", $id);
        $stmt->execute();
        return $stmt->get_result()->fetch_assoc();
    }

    public function tambah($nama, $nim) {
        $stmt = $this->conn->prepare("INSERT INTO mahasiswa (nama, nim) VALUES (?, ?)");
        $stmt->bind_param("ss", $nama, $nim);
        return $stmt->execute();
    }

    public function update($id, $nama, $nim) {
        $stmt = $this->conn->prepare("UPDATE mahasiswa SET nama = ?, nim = ? WHERE id = ?");
        $stmt->bind_param("ssi", $nama, $nim, $id);
        return $stmt->execute();
    }

    public function hapus($id) {
        $stmt = $this->conn->prepare("DELETE FROM mahasiswa WHERE id = ?");
        $stmt->bind_param("i", $id);
        return $stmt->execute();
    }
}
?>
```

### `index.php` — Menampilkan Data (READ)
```
<?php
require_once 'Mahasiswa.php';
$mahasiswa = new Mahasiswa($conn);
$data = $mahasiswa->getAll();
?>

<h2>Data Mahasiswa</h2>
<a href="tambah.php">+ Tambah Mahasiswa</a>
<table border="1" cellpadding="5">
    <tr>
        <th>No</th><th>Nama</th><th>NIM</th><th>Aksi</th>
    </tr>
    <?php $no = 1; while ($row = $data->fetch_assoc()) : ?>
    <tr>
        <td><?= $no++ ?></td>
        <td><?= $row['nama'] ?></td>
        <td><?= $row['nim'] ?></td>
        <td>
            <a href="edit.php?id=<?= $row['id'] ?>">Edit</a> |
            <a href="hapus.php?id=<?= $row['id'] ?>" onclick="return confirm('Yakin?')">Hapus</a>
        </td>
    </tr>
    <?php endwhile; ?>
</table>
```

### `tambah.php` — Menambah Data (CREATE)
```
<?php
require_once 'Mahasiswa.php';
$mahasiswa = new Mahasiswa($conn);

if ($_POST) {
    $mahasiswa->tambah($_POST['nama'], $_POST['nim']);
    header("Location: index.php");
}
?>

<h2>Tambah Mahasiswa</h2>
<form method="post">
    Nama: <input type="text" name="nama"><br>
    NIM: <input type="text" name="nim"><br>
    <button type="submit">Simpan</button>
</form>
```

### `edit.php` — Update Data (UPDATE)
```
<?php
require_once 'Mahasiswa.php';
$mahasiswa = new Mahasiswa($conn);
$data = $mahasiswa->getById($_GET['id']);

if ($_POST) {
    $mahasiswa->update($_GET['id'], $_POST['nama'], $_POST['nim']);
    header("Location: index.php");
}
?>

<h2>Edit Mahasiswa</h2>
<form method="post">
    Nama: <input type="text" name="nama" value="<?= $data['nama'] ?>"><br>
    NIM: <input type="text" name="nim" value="<?= $data['nim'] ?>"><br>
    <button type="submit">Update</button>
</form>
```

### `hapus.php` — Menghapus Data (DELETE)
```
<?php
require_once 'Mahasiswa.php';
$mahasiswa = new Mahasiswa($conn);
$mahasiswa->hapus($_GET['id']);
header("Location: index.php");
?>
```


## Apa itu Form Validation?
Form Validation adalah proses memeriksa isi formulir (form) sebelum datanya diproses atau disimpan. Tujuannya adalah untuk memastikan data yang dimasukkan oleh pengguna sudah benar dan sesuai aturan.

Contohnya:
- Nama tidak boleh kosong
- Email harus berisi alamat email yang valid (misalnya: nama@email.com)
- Password minimal 6 karakter

## Kenapa Form Validation Penting?
- Melindungi website dari data yang salah atau berbahaya
- Membantu pengguna mengisi form dengan benar
- Menghindari error di bagian proses berikutnya (misalnya saat simpan ke database)

## Jenis Validasi
1. Client-side validation
Dicek langsung di browser (biasanya pakai JavaScript atau HTML5)

2. Server-side validation
Dicek di server setelah form dikirim (pakai PHP dalam kasus kamu)

## Contoh Implementasi Form Validation
Sekarang kita buat contoh form yang akan melakukan validasi:
- Nama (tidak boleh kosong)
- Email (tidak boleh kosong dan format harus valid)
- Password (minimal 6 karakter)
- Umur (harus angka dan minimal 18 tahun)

### Membuat Database
```
CREATE DATABASE belajar_php;

USE belajar_php;

CREATE TABLE users (
  id INT AUTO_INCREMENT PRIMARY KEY,
  nama VARCHAR(100),
  email VARCHAR(100),
  password VARCHAR(255), -- kita akan hash password
  umur INT
);
```

### Buat File `koneksi.php`
```
<?php
$host = "localhost";
$user = "root";       // sesuaikan jika bukan root
$pass = "";           // sesuaikan jika pakai password
$db   = "belajar_php";

$conn = new mysqli($host, $user, $pass, $db);

if ($conn->connect_error) {
    die("Koneksi gagal: " . $conn->connect_error);
}
?>
```

### `proses.php` Untuk Menyimpan Data ke Dalam Database
```
<?php
require 'koneksi.php'; // koneksi ke database

function bersihkan_input($data) {
    return htmlspecialchars(trim($data));
}

function validasi_form($data) {
    $errors = [];

    if (empty($data['nama'])) {
        $errors[] = "Nama tidak boleh kosong";
    }

    if (empty($data['email'])) {
        $errors[] = "Email tidak boleh kosong";
    } elseif (!filter_var($data['email'], FILTER_VALIDATE_EMAIL)) {
        $errors[] = "Format email tidak valid";
    }

    if (empty($data['password'])) {
        $errors[] = "Password tidak boleh kosong";
    } elseif (strlen($data['password']) < 6) {
        $errors[] = "Password minimal 6 karakter";
    }

    if (empty($data['umur'])) {
        $errors[] = "Umur tidak boleh kosong";
    } elseif (!is_numeric($data['umur'])) {
        $errors[] = "Umur harus berupa angka";
    } elseif ($data['umur'] < 18) {
        $errors[] = "Umur minimal harus 18 tahun";
    }

    return $errors;
}

// Ambil & bersihkan data input
$data = [
    'nama'     => bersihkan_input($_POST['nama']),
    'email'    => bersihkan_input($_POST['email']),
    'password' => $_POST['password'], // password tidak di-escape karena akan di-hash
    'umur'     => bersihkan_input($_POST['umur']),
];

$errors = validasi_form($data);

if (count($errors) > 0) {
    foreach ($errors as $error) {
        echo $error . "<br>";
    }
} else {
    // Hash password
    $hashed_password = password_hash($data['password'], PASSWORD_DEFAULT);

    // Simpan ke database
    $stmt = $conn->prepare("INSERT INTO users (nama, email, password, umur) VALUES (?, ?, ?, ?)");
    $stmt->bind_param("sssi", $data['nama'], $data['email'], $hashed_password, $data['umur']);

    if ($stmt->execute()) {
        echo "Data berhasil disimpan ke database!";
    } else {
        echo "Gagal menyimpan data: " . $stmt->error;
    }

    $stmt->close();
    $conn->close();
}
?>
```

### `index.php` Untuk Membuat Form
```
<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <title>Form Pendaftaran</title>
</head>
<body>
    <h2>Form Pendaftaran</h2>
    <form method="POST" action="proses.php">
        <label for="nama">Nama:</label><br>
        <input type="text" name="nama" id="nama" required><br><br>

        <label for="email">Email:</label><br>
        <input type="text" name="email" id="email" required><br><br>

        <label for="password">Password:</label><br>
        <input type="password" name="password" id="password" required><br><br>

        <label for="umur">Umur:</label><br>
        <input type="text" name="umur" id="umur" required><br><br>

        <input type="submit" value="Kirim">
    </form>
</body>
</html>

```

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
Encapsulation merupakan konsep OOP yang digunakan untuk melindungi data agar tidak dapat diakses atau diubah secara langsung dari luar class. Akses terhadap data dilakukan melalui method yang telah disediakan sehingga keamanan data dapat terjaga.

Terdapat 3 jenis access modifier dalam PHP yaitu: 
- `public` -> Dapat di akses dari mana saja, baik dari dalam class maupun luar class.
- `private` -> Hanya dapat di akses dari dalam class itu sendiri.
- `protected` -> Hanya dapat di akses dari dalam class itu sendiri dan turunannya.

Contoh Penerapan: 
Pada sistem login, password merupakan data yang bersifat sensitif sehingga tidak boleh diakses secara langsung. Oleh karena itu, password disimpan sebagai atribut private dan hanya dapat diubah atau ditampilkan melalui method tertentu.

Contoh Code:
```
class User {
    public $username = "admin";
    private $password = "12345";
    protected $email = "admin@gmail.com";

    public function tampilkanData() {
        echo "Username: " . $this->username . "";
        echo "Password: " . $this->password . "";
        echo "Email: " . $this->email . "";
    }
}

class Admin extends User {
    public function tampilkanEmail() {
        return $this->email;
    }
}

$user = new User();

// Public (bisa diakses dari luar class)
echo $user->username . "";

// Private (akan error jika diaktifkan)
// echo $user->password;

// Protected (akan error jika diaktifkan)
// echo $user->email;

$admin = new Admin();

// Protected dapat diakses melalui class turunan
echo $admin->tampilkanEmail();
```

### 2. Inheritance (Pewarisan)
Inheritance merupakan konsep OOP yang memungkinkan sebuah class mewarisi atribut dan method dari class lain. Class yang memberikan warisan disebut parent class (class induk), sedangkan class yang menerima warisan disebut child class (class turunan).

Konsep ini bertujuan untuk mengurangi penulisan kode yang berulang serta mempermudah pengembangan program karena class turunan dapat menggunakan kembali atribut dan method yang sudah dimiliki oleh class induk.

Contoh Penerapan: 
Dalam kehidupan sehari-hari, kucing merupakan salah satu jenis hewan. Oleh karena itu, kucing dapat mewarisi karakteristik dasar yang dimiliki oleh hewan, seperti kemampuan makan dan tidur.

Contoh Code:
```
class Hewan {
    public $nama = "Hewan";

    public function makan() {
        echo "Hewan sedang makan";
    }
}

class Kucing extends Hewan {

}

$kucing = new Kucing();

echo $kucing->nama . "";
$kucing->makan();
```

### 3. Polymorphism
Polymorphism adalah sebuah konsep dimana method memiliki kemampuan yang sama tetapi perilakunya berbeda tergantung objeknya.

Contoh Penerapan: 
Kucing dan anjing sama-sama merupakan hewan yang dapat mengeluarkan suara. Namun, suara yang dihasilkan masing-masing hewan berbeda. Dalam OOP, kondisi ini dapat direpresentasikan menggunakan method yang sama tetapi menghasilkan output yang berbeda pada setiap class.

Contoh Code:
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

class Anjing extends Hewan {
    public function suara() {
        echo "Guk Guk";
    }
}

$hewan = new Hewan();
$kucing = new Kucing();
$anjing = new Anjing();

$hewan->suara();
echo "<br>";

$kucing->suara();
echo "";

$anjing->suara();
```

### 4. Abstraction
Abstraksi adalah proses menyembunyikan detail kompleks dan hanya menampilkan fungsi penting dari suatu objek. Dengan kata lain, kita membuat kerangka (struktur) umum dari class, tanpa harus mengungkapkan bagaimana cara kerjanya secara detail.

Terdapat beberapa catatan pada abstract class:
- Tidak bisa dibuat objek secara langsung.
- Digunakan sebagai class dasar untuk diturunkan ke class lain.
- Bisa punya method yang sudah didefinisikan maupun method abstrak (yang harus diisi oleh class turunannya).

Contoh Penerapan: 
Setiap hewan memiliki kemampuan untuk bersuara, tetapi suara yang dihasilkan setiap hewan berbeda. Oleh karena itu, dibuat class Hewan sebagai kerangka umum yang mewajibkan setiap class turunan untuk mendefinisikan cara bersuaranya masing-masing.

Contoh Code:
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

$kucing = new Kucing();

$kucing->bersuara();
echo "";
$kucing->tidur();
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
Form Validation adalah proses pengecekan data yang diinputkan pengguna pada sebuah formulir sebelum data tersebut diproses atau disimpan. Tujuannya adalah untuk memastikan data yang dimasukkan sudah sesuai dengan aturan yang ditentukan sehingga dapat mengurangi kesalahan dan menjaga kualitas data.

Contohnya:
- Nama tidak boleh kosong
- Email harus berisi alamat email yang valid (misalnya: nama@email.com)
- Password harus memiliki minimal 6 karakter
- Nomor telepon hanya boleh berisi angka

## Kenapa Form Validation Penting?
- Memastikan data yang dimasukkan pengguna sesuai dengan format dan aturan yang ditentukan
- Membantu pengguna mengisi formulir dengan benar melalui pesan kesalahan yang informatif
- Mengurangi risiko masuknya data yang tidak valid atau berpotensi membahayakan sistem
- Mencegah terjadinya kesalahan pada proses selanjutnya, seperti penyimpanan data ke database atau pengolahan data oleh aplikasi

## Jenis Validasi
1. Client-side validation
Client-side validation adalah validasi yang dilakukan langsung di browser sebelum data dikirim ke server. Validasi ini biasanya menggunakan HTML5 atau JavaScript sehingga pengguna dapat langsung mengetahui jika terdapat kesalahan pada input yang diberikan.

3. Server-side validation
Server-side validation adalah validasi yang dilakukan di server setelah formulir dikirim oleh pengguna. Pada praktikum ini, validasi dilakukan menggunakan PHP untuk memastikan data yang diterima benar dan aman untuk diproses lebih lanjut.

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
        <input type="email" name="email" id="email" required><br><br>

        <label for="password">Password:</label><br>
        <input type="password" name="password" id="password" required><br><br>

        <label for="umur">Umur:</label><br>
        <input type="text" name="umur" id="umur" required><br><br>

        <input type="submit" value="Kirim">
    </form>
</body>
</html>

```

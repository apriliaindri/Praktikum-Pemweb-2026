# Cookies and Sessions

## Apa itu Cookie di PHP?

Cookie adalah data kecil yang disimpan di browser pengguna dan akan dikirim kembali ke server pada setiap request berikutnya. Cookie sering digunakan untuk menyimpan preferensi pengguna, status login, atau informasi lain yang perlu diingat oleh aplikasi web selama pengguna mengakses website.

### Set Cookie di PHP

Untuk menbuat cookie, gunakan fungsi `setcookie()`. Fungsi ini harus dipanggil sebelum ada output yang dikirim ke browser, seperti `echo`, HTML, atau spasi diluar tag PHP.

```php
<?php
// Set cookie dengan nama 'user' dan value 'audin' selama 1 jam
setcookie("user", "audin", time() + 3600, "/"); // 3600 detik = 1 jam
?>
```

Syntax

`setcookie(name, value, expire, path, domain, secure, httponly);`

Paramater `name` digunakan untuk menentukan nama cookie dan merupakan satu-satunya parameter yang wajib diisi. Parameter lainnya bersifat opsional dan dapat digunakan untuk mengatur nilai cookie, waktu kadaluwarsa, lokasi cookie dapat diakses, serta pengaturan keamanan tambahan.

### Set dan Retrieve Cookies

Berikut contoh cara membuat cookie menggunakan `setcookie()` serta mengakses nilai cookie menggunakan `$_COOKIE`.

```
 <?php
$cookie_name = "user";
$cookie_value = "audin";
setcookie($cookie_name, $cookie_value, time() + (86400 * 30), "/"); // berlaku selama 30 hari
?>
<html>
<body>

<?php
if(!isset($_COOKIE[$cookie_name])) {
  echo "Nama Cookie '" . $cookie_name . "' Not Set!";
} else {
  echo "Cookie '" . $cookie_name . "' is set!<br>";
  echo "Value : " . $_COOKIE[$cookie_name];
}
?>

</body>
</html>
```
> Catatan: Cookie yang baru dibuat biasanya baru dapat diakses pada request berikutnya. Jika cookie belum terbaca saat pertama kali menjalankan program, coba refresh halaman terlebih dahulu.

### Modify Cookie Value

Untuk mengubah nilai cookie, cukup buat kembali cookie dengan nama yang sama menggunakan fungsi `setcookie()`. Nilai cookie yang lama akan digantikan dengan nilai yang baru.

```
 <?php
$cookie_name = "user";
$cookie_value = "bani";
setcookie($cookie_name, $cookie_value, time() + (86400 * 30), "/");
?>
<html>
<body>

<?php
if(!isset($_COOKIE[$cookie_name])) {
  echo "Nama Cookie '" . $cookie_name . "' Not Set!";
} else {
  echo "Cookie '" . $cookie_name . "' is set!<br>";
  echo "Value : " . $_COOKIE[$cookie_name];
}
?>

</body>
</html>
```
> Catatan: Perubahan nilai cookie biasanya baru dapat terlihat pada request berikutnya. Jika nilai cookie belum berubah saat pertama kali dijalankan, coba refresh halaman terlebih dahulu.

### Delete Cookie

Untuk menghapus cookie, cukup buat kembali cookie yang sama dengan expiration date yang sudah terlewat.

```
 <?php
// set expiration date ke masa lalu
setcookie("user", "", time() - 3600);
?>
<html>
<body>

<?php
echo "Cookie 'user' is deleted.";
?>

</body>
</html>
```
> Catatan: Penghapusan cookie biasanya akan terlihat setelah browser menerima cookie dengan expiration date yang sudah terlewat. Jika cookie masih terlihat, coba refresh halaman terlebih dahulu.

## Apa itu Session di PHP?

Session di PHP adalah cara untuk menyimpan informasi pengguna selama mengakses beberapa halaman dalam sebuah aplikasi web. Berbeda dengan cookie, data session disimpan di server, sedangkan browser hanya menyimpan ID session yang digunakan untuk mengenali pengguna.

### Memulai Session

Untuk memulai sebuah session, gunakan fungsi `session_start()`. Fungsi ini harus dipanggil di awal script script sebelum ada output yang dikirim ke browser, seperti `echo`, HTML, atau spasi di luar tag PHP.

```php
<?php
// Memulai session
session_start();
?>
```

### Set Variabel Session

Setelah session dimulai menggunakan `session_start()`, kita dapat menyimpan data ke dalam variabel session melalui superglobal `$_SESSION`.
Pada contoh berikut, nilai `'John Doe'` disimpan ke dalam variabel session dengan nama `user`.


```php
<?php
session_start();

// Set variabel session
$_SESSION['user'] = 'John Doe';
?>

```

### Mengakses Variabel Session

Data yang disimpan di dalam session dapat diakses kembali melalui superglobal `$_SESSION`, sama seperti mengakses elemen pada array.

```php
<?php
session_start();

// Mengakses variabel session
if (isset($_SESSION['user'])) {
    echo "Halo, " . $_SESSION['user'];
} else {
    echo "Variabel session tidak ditemukan!";
}
?>

```
Pada contoh di atas, program akan memeriksa apakah variabel session `user` sudah tersedia. Jika ada, program akan menampilkan nilai yang tersimpan. Jika tidak, akan ditampilkan pesan bahwa variabel session tidak ditemukan.

### Menghancurkan Session

Session dapat dihapus menggunakan `session_destroy()`. Jika hanya ingin menghapus variabel session secara tertentu, gunakan fungsi `unset()`.

```php
<?php
session_start();

// Menghapus variabel session tertentu
unset($_SESSION['user']);

// Menghancurkan seluruh session
session_destroy();
?>

```
Pada contoh di atas, `unset($_SESSION['user'])` digunakan untuk menghapus variabel session `user` saja. Sedangkan `session_destroy()` digunakan untuk menghapus seluruh data session yang sedang aktif.

## Demo Praktikum

Download [Bahan Praktikum](https://github.com/PEMWEB-2025/PEMWEB-2025/raw/refs/heads/main/static/berkas/sessionDanCookie.zip) berikut lalu extract ke folder yang ingin kalian gunakan

## Demo Praktikum Menggunakan Postgresql

Untuk memulai, jalankan perintah berikut:

```
docker-compose up
```

Kemudian masuk ke pgAdmin menggunakan email dan password berikut:

```
EMAIL       : admin@example.com
PASSWORD    : adminpassword
```

Selanjutnya sambungkan database menggunakan detail berikut :

```
host        = host.docker.internal
port        = 5432
dbname      = pemweb
user        = myuser
password    = mypassword!
```

Setelah berhasil terhubung, buat tabel baru pada schema `public` dengan nama `users` menggunakan query berikut:

```sql
CREATE TABLE IF NOT EXISTS users (
    id SERIAL PRIMARY KEY,
    username VARCHAR(50) UNIQUE NOT NULL,
    password TEXT NOT NULL,
    role VARCHAR(20) DEFAULT 'user',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

jika sudah jalankan php menggunakan `php -S localhost:8000` atau gunakan server development lain seperti XAMPP, Laragon, dan sebagainya.

## Demo Praktikum Tidak menggunakan DB

Jalankan saja seperti biasa, dengan keterbatasan tidak bisa register, dan hanya bisa login dengan route `loginnodb.php`, berikut username dan password yang bisa digunakan :

```
    'username' => 'admin',
    'password' => 'admin123',
    'role' => 'admin'

    'username' => 'user',
    'password' => 'user123',
    'role' => 'user'
```

## Penjelasan dan Praktek

### 1. Pembuatan Session Baru

pada file `login_process.php`, terdapat pembuatan session baru dan set value value berdasarkan hasil query.

```
    $_SESSION['user_id'] = $user['id'];
    $_SESSION['username'] = $user['username'];
    $_SESSION['role'] = $user['role'];
```

### 2. Menggunakan Variable Pada Session

pada file `dashboard.php`, diambil variable-variable session yang sudah di-set pada login proses tadi untuk digunakan.

```
    $username = $_SESSION['username'];
    $role = $_SESSION['role'];
    $isAdmin = $role === 'admin';
```

### 3. Di Mana Cookie Tersimpan?

1. `Press F12` atau `inspect element` pada browser,
2. setelah itu pilih menu `storage` lalu `cookies`
3. di sana seharusnya terdapat cookies bernama `PHPSESSID` setelah melakukan login
4. Cookie ini digunakan sebagai pengenal pada session

### 4. Di Mana Session Tersimpan?

Pada route `dashboard.php` terdapat informasi dimana letak session disimpan sementara, informasi diperoleh dari :

```
ini_get('session.save_path');
```

Akses folder yang ditampilkan oleh kode tersebut, kemudian buka salah satu file session yang tersedia.

Perhatikan isi file tersebut. Apakah terdapat data seperti `username`, `role`, atau informasi lain yang sebelumnya disimpan ke dalam variabel `$_SESSION`?

# Cookies and Sessions

## Apa itu Cookie di PHP?

Cookie adalah potongan data kecil yang disimpan di browser user dan dikirim kembali ke server pada setiap request berikutnya. Cookie sering digunakan untuk menyimpan preferensi user, token otentikasi, dan track informasi across sessions.

### Set Cookie di PHP

Untuk set cookie, gunakan fungsi setcookie(). Fungsi ini harus dipanggil sebelum ada output yang dikirim ke browser.

```php
<?php
// Set cookie dengan nama 'user' dan value 'addin' selama 1 jam
setcookie("user", "addin", time() + 3600, "/"); // 3600 detik = 1 jam
?>
```

Syntax

`setcookie(name, value, expire, path, domain, secure, httponly);`

Hanya parameter name yang wajib. Parameter yang lain bersifat optional.

### Set dan Retrieve Cookies

Berikut contoh cara membuat cookie menggunakan `setcookie()` sekaligus retrieve cookies menggunakan `isset($_COOKIE[])`

```
 <?php
$cookie_name = "user";
$cookie_value = "addin";
setcookie($cookie_name, $cookie_value, time() + (86400 * 30), "/"); // 86400 = 1 hari
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

### Modify Cookie Value

Untuk meng-update cookie cukup set kembali cookie dengan name yang sama

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

### Delete Cookie

Untuk menghapus cookie cukup sederhana, update/modify cookie namun dengan expiration date yang sudah terlewat

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

## Apa itu Session di PHP?

Session di PHP adalah cara untuk menyimpan informasi selama pada saat user mengakses beberapa halaman. Berbeda dengan cookie, data session disimpan di server, dan hanya ID session yang disimpan di browser user.

### Memulai Session

Untuk memulai sebuah session, gunakan fungsi `session_start()`. Fungsi ini harus dipanggil di awal script, sebelum ada output.

```php
<?php
// Memulai session
session_start();
?>
```

### Set Variabel Session

Setelah memulai session, session bisa menyimpan data user pada superglobal `$_SESSION`.

```php
<?php
session_start();

// Set variabel session
$_SESSION['user'] = 'John Doe';
?>

```

### Mengakses Variabel Session

Data session bisa diakses seperti array.

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

### Menghancurkan Session

Session dapat dihancurkan menggunakan `session_destroy()`. Untuk menghapus variabel session secara spesifik, gunakan `unset()`.

```php
<?php
session_start();

// Menghapus variabel session tertentu
unset($_SESSION['user']);

// Menghancurkan seluruh session
session_destroy();
?>

```

## Demo Praktikum

Download [Bahan Praktikum](https://github.com/PEMWEB-2025/PEMWEB-2025/raw/refs/heads/main/static/berkas/sessionDanCookie.zip) berikut lalu extract ke folder yang ingin kalian gunakan

## Demo Praktikum Menggunakan Postgresql

untuk memulai, run
`docker-compose up`, lalu masuk ke pgadmin dengan email dan password seperti berikut :

```
EMAIL       : admin@example.com
PASSWORD    : adminpassword
```

Lalu sambungkan database dengan detail berikut :

```
host        = host.docker.internal
port        = 5432
dbname      = pemweb
user        = myuser
password    = mypassword!
```

jika sudah buat tabel baru pada skema public bernama users seperti sql berikut :

```sql
CREATE TABLE IF NOT EXISTS users (
    id SERIAL PRIMARY KEY,
    username VARCHAR(50) UNIQUE NOT NULL,
    password TEXT NOT NULL,
    role VARCHAR(20) DEFAULT 'user',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

jika sudah jalankan php menggunakan `php -S localhost:8000` atau gunakan server development kalian (xampp, laragon, etc)

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

Akses folder tersebut lalu buka salah satu file session, apa yang anda lihat?

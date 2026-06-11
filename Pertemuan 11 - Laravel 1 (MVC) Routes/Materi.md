# Pertemuan 11: Laravel 1 (MVC) Routes

## Pengenalan Laravel
- Laravel adalah framework PHP yang digunakan untuk membangun aplikasi web maupun API.
- Laravel pertama kali dikembangkan oleh Taylor Otwell dan dirilis pada tahun 2011.
- Laravel bersifat open source dan dapat digunakan secara gratis. Selain menggunakannya, kita juga dapat berkontribusi dalam pengembangannya melalui komunitas Laravel.
  
## Kenapa Laravel
- Saat ini Laravel merupakan salah satu framework PHP yang paling pupuler.
- Banyak perusahaan menggunakan Laravel sebagai framework utama untuk mengembangkan aplikasi web berbasis PHP.
- Laravel memiliki ekosistem yang besar dengan berbagai tools dan layanan pendukung, sehingga memudahkan proses pengembangan dan integrasi aplikasi.

## Instalasi Laravel

### [Herd For Windows](https://herd.laravel.com/windows):

**Step 1: Install Laravel Herd for Windows**

Akses situs resmi Laravel Herd di https://herd.laravel.com/windows. Pada halaman tersebut, klik tombol **Download for Windows** untuk mengunduh installer Laravel Herd.

Tunggu hingga proses unduh selesai. Setelah selesai, akan tersedia file installer dengan nama seperti `Herd-1.11.1-setup.exe` (versi dapat berbeda sesuai versi terbaru yang tersedia saat praktikum dilakukan).

**Step 2: Run Laravel Herd Installer**

Setelah proses unduh selesai, jalankan installer Laravel Herd dengan memilih **Run as Administrator**, kemudian ikuti langkah-langkah instalasi hingga selesai.

![run](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*dsZxEb_q66QjqdE5GAHC5w.png)

> **Catatan**: Laravel Herd memerlukan hak akses administrator agar dapat menambahkan service **HerdHelper**, yang digunakan untuk mengelola file _hosts_, memetakan direktori project, dan menghubungkan project Laravel ke domain _.test_.

**Step3: Run Laravel Herd**

![lets](https://cdn.jsdelivr.net/gh/gungunpriatna/tes-repositori@master/how-to/install-tools/laravel-herd/1%20tampilan%20awal%20setelah%20install.png)

Setelah proses instalasi selesai, buka aplikasi **Laravel Herd** yang telah terpasang. Saat pertama kali dijalankan, Laravel Herd akan menampilkan proses setup awal untuk menyiapkan lingkungan pengembangan.

Klik tombol **Let's get started** untuk memulai proses konfigurasi awal Laravel Herd.

Laravel Herd akan mengunduh dan memasang beberapa komponen yang diperlukan, seperti PHP, Node.js, dan tools pendukung lainnya.

![php](https://cdn.jsdelivr.net/gh/gungunpriatna/tes-repositori@master/how-to/install-tools/laravel-herd/2%20install%20php%208.3.png)

Setelah proses instalasi komponen selesai, akan muncul halaman aktivasi **Laravel Herd Pro**. Pilih **Skip for now** untuk melanjutkan tanpa menggunakan fitur berbayar.

![skip](https://cdn.jsdelivr.net/gh/gungunpriatna/tes-repositori@master/how-to/install-tools/laravel-herd/3.%20aktivasi%20laravel%20herd%20pro.png)

Setelah setup selesai, akan muncul halaman **Setup Completed**. Klik tombol **Open Dashboard** untuk membuka dashboard Laravel Herd.

![open](https://cdn.jsdelivr.net/gh/gungunpriatna/tes-repositori@master/how-to/install-tools/laravel-herd/4%20tampilan%20setup%20laravel%20herd%20selesai.png)

Dashboard Laravel Herd menampilkan berbagai informasi dan fitur yang dapat digunakan untuk mengelola lingkungan pengembangan, seperti status service yang sedang berjalan, pengaturan PHP, serta akses cepat untuk mengelola project Laravel.

![dashboard](https://cdn.jsdelivr.net/gh/gungunpriatna/tes-repositori@master/how-to/install-tools/laravel-herd/5%20tampilan%20dashboard%20laravel%20herd.png)

**Step 4: Memeriksa Instalasi PHP, Laravel, Composer, dan Node.js**

Setelah proses setup selesai, pastikan PHP, Laravel Installer, Composer, dan Node.js telah terpasang dengan benar. Buka **Command Prompt**, **Windows Terminal**, atau **Cmder**, kemudian jalankan perintah berikut:

```
php --version
laravel --version
composer --version
node --version
```

Jika proses instalasi berhasil, terminal akan menampilkan informasi versi dari masing-masing komponen seperti berikut:

```
C:\Users\[nama user]>php --version
PHP 8.3.12 (cli) (built: Sep 24 2024 20:22:14) (NTS Visual C++ 2019 x64)
Copyright (c) The PHP Group
Zend Engine v4.3.12, Copyright (c) Zend Technologies
    with Zend OPcache v8.3.12, Copyright (c), by Zend Technologies

C:\Users\[nama user]>laravel --version
Laravel Installer 5.8.5

C:\Users\[nama user]>composer --version
Composer version 2.7.7 2024-06-10 22:11:12
PHP version 8.3.12 (C:\Users\InformatikaUMMI\.config\herd\bin\php83\php.exe)
Run the "diagnose" command to get more detailed diagnostics output.

C:\Users\[nama user]>node --version
v23.0.0
```

### [Herd For MacOS](https://herd.laravel.com):

### Herd for macOS

**Step 1: Download dan Install Laravel Herd**

Buka situs resmi Laravel Herd di https://herd.laravel.com, kemudian klik tombol **Download for macOS**.

![mac](https://i.postimg.cc/G2Hftx1v/image.png)

Setelah proses unduh selesai, jalankan installer dan ikuti proses instalasi hingga selesai.

**Step 2: Buka aplikasi Herd nya**

Setelah proses instalasi selesai, buka aplikasi **Laravel Herd** untuk memastikan aplikasi telah terpasang dan dapat berjalan dengan baik.

Jika Laravel Herd berhasil dijalankan, maka proses instalasi telah selesai dan lingkungan pengembangan Laravel siap digunakan.

**Step 3: Cek Environment di Terminal**

Setelah proses instalasi selesai, Laravel Herd akan menyiapkan lingkungan pengembangan yang telah dilengkapi dengan PHP, Laravel Installer, Composer, dan Node.js.

Untuk memastikan seluruh komponen telah terpasang dengan benar, buka **Terminal** lalu jalankan perintah berikut:

```
herd --version
php --version
laravel --version
composer --version
node --version
```

## Membuat Project Laravel

Setelah Laravel Herd berhasil terpasang dan seluruh komponen dapat digunakan, kita dapat membuat project Laravel baru.

Buka Terminal, Command Prompt, Windows Terminal, atau Cmder, kemudian jalankan perintah berikut:

```bash
laravel new belajar-laravel
```

Tunggu hingga proses pembuatan project selesai, kemudian masuk ke direktori project:
```bash
cd belajar-laravel
```

Selanjutnya buka folder project menggunakan Visual Studio Code:
```bash
code .
```

Pada project inilah kita akan mempelajari konsep MVC, Routing, Controller, dan View pada Laravel.

## Konsep MVC di Laravel

Laravel menggunakan arsitektur **MVC (Model-View-Controller)** untuk memisahkan logika aplikasi, tampilan, dan pengelolaan data. Dengan pendekatan ini, kode menjadi lebih terstruktur, mudah dikelola, dan mudah dikembangkan.

- **Model**: Berfungsi untuk berinteraksi dengan database. Model bertanggung jawab dalam mengelola data dan logika bisnis aplikasi.
- **View**: Bertugas menampilkan data kepada pengguna. Pada Laravel, View biasanya berupa file `.blade.php` yang berada di folder `resources/views`.
- **Controller**: Berfungsi sebagai penghubung antara Model dan View. Controller menerima request dari pengguna, memproses data yang diperlukan, kemudian mengembalikan response berupa View atau data lainnya.

### Ilustrasi Singkat:

![mvc](https://www.rumahweb.com/journal/wp-content/uploads/2024/09/Laravel-MVC-concept.webp)

## Struktur Folder Utama Laravel (Terkait MVC)

Laravel memiliki banyak folder dan file bawaan. Namun, pada praktikum ini kita akan lebih sering menggunakan beberapa folder berikut:

```text
app
├── Http
│   └── Controllers
│
├── Models
│
resources
└── views
```

- `app/Models` → Menyimpan file Model yang digunakan untuk berinteraksi dengan database.
- `app/Http/Controllers` → Menyimpan file Controller yang menangani request dan menghubungkan Model dengan View.
- `resources/views` → Menyimpan file View (Blade) yang digunakan untuk menampilkan halaman kepada pengguna.

## Routing di Laravel

Routing adalah mekanisme yang digunakan untuk menghubungkan URL dengan fungsi atau controller yang akan dijalankan.

Pada Laravel, route untuk aplikasi web umumnya didefinisikan pada file `routes/web.php`. Melalui file ini, kita dapat menentukan halaman atau URL apa saja yang dapat diakses oleh pengguna.

### Contoh Route Sederhana

```php
use Illuminate\Support\Facades\Route;

Route::get('/', function () {
    return view('welcome');
});
```

Penjelasan:

- `Route::get()` digunakan untuk menangani request HTTP dengan method GET.
- `/` merupakan URL path yang merepresentasikan halaman utama (_homepage_) aplikasi.
- `function () { ... }` merupakan fungsi yang akan dijalankan ketika URL tersebut diakses.
- `return view('welcome');` digunakan untuk menampilkan view bernama `welcome`, yang secara default berada pada file `resources/views/welcome.blade.php`.

## Membuat Controller dan View di Laravel

Pada contoh sebelumnya, route langsung mengembalikan sebuah view menggunakan fungsi (_closure_). Namun, pada aplikasi yang lebih kompleks, logika aplikasi biasanya dipisahkan ke dalam **Controller** agar kode lebih terstruktur dan mudah dikelola.

Pada bagian ini, kita akan belajar cara membuat **Controller** dan **View** di Laravel, kemudian menghubungkannya melalui **route**.

### 1. Membuat Controller

Laravel menyediakan perintah Artisan untuk membuat Controller secara otomatis.

Jalankan perintah berikut pada terminal:

```bash
php artisan make:controller HomeController
```

Setelah perintah dijalankan, Laravel akan membuat file controller baru pada lokasi `app/Http/Controllers/HomeController.php`

### 2. Menulis Method / Function di Controller

Buka file `app/Http/Controllers/HomeController.php`, kemudian ubah isinya menjadi:

```php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;

class HomeController extends Controller
{
    public function index()
    {
        return view('home');
    }

    public function about()
    {
        return view('about');
    }
}
```

Penjelasan:
- `index()` digunakan untuk menampilkan halaman Home.
- `about()` digunakan untuk menampilkan halaman About.

### 3. Membuat View

#### a. Membuat View home.blade.php

Buat file berikut:
```php
resources/views/home.blade.php
```

Isi dengan kode berikut: 

```html
<!DOCTYPE html>
<html>
<head>
    <title>Halaman Home</title>
</head>
<body>
    <h1>Selamat datang di halaman Home</h1>
</body>
</html>
```

#### b. Membuat View about.blade.php

Buat file berikut:
```php
resources/views/about.blade.php
```

Isi dengan kode berikut: 

```html
<!DOCTYPE html>
<html>
<head>
    <title>Tentang Kami</title>
</head>
<body>
    <h1>Ini adalah halaman Tentang Kami</h1>
</body>
</html>
```


### 4. Menambahkan Route ke Controller

Buka file `routes/web.php` lalu tambahkan kode ini:

```php
use App\Http\Controllers\HomeController;

Route::get('/home', [HomeController::class, 'index']);
Route::get('/about', [HomeController::class, 'about']);
```

Penjelasan:
- Ketika pengguna mengakses `/home`, Laravel akan menjalankan method `index()` pada `HomeController`.
- Ketika pengguna mengakses `/about`, Laravel akan menjalankan method `about()` pada `HomeController`.

### 5. Jalankan kode laravel

Jalankan dengan:

```bash
php artisan serve
```

Kemudian buka browser dan kunjungi:
- http://localhost:8000/home
- http://localhost:8000/about

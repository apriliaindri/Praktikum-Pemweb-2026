# Pertemuan 11: Laravel 1 (MVC) Routes

## Pengenalan Laravel
- Laravel adalah framework di PHP untuk membuat Web atau API
- Laravel pertama kali dibuat oleh Taylor Otwell tahun 2011
- Laravel adalah framework yang open source dan gratis, sehingga kita bisa menggunakannya tanpa biaya dan juga bisa berkontribusi ke projectnya 

## Kenapa Laravel
- Saat ini Laravel adalah framework paling populer di PHP
- Banyak perusahaan yang sudah menggunakan Laravel sebagai framework pilihan ketika menggunakan PHP
- Laravel juga memiliki ekosistem yang sangat besar, terutama dari ekosistem teknologi pendukung, sehingga ketika menggunakan Laravel, kita bisa mengintegrasikan dengan teknologi pendukung nya dengan lebih mudah

## Instalasi Laravel

### [Herd For Windows](https://herd.laravel.com/windows):

**Step 1: Install Laravel Herd for Windows**

Sekarang kita akses situr resmi (https://herd.laravel.com/windows). Pada halaman web Laravel Herd Kita bisa lihat button _Download for Windows_. Untuk memulai proses download Laravel Herd installer, tekan button tersebut. Kita tunggu sampai proses download selesai. Setelah selesai kita bisa lihat ada file Herd-1.11.1-setup.exe (Versi laravel herd installer pada saat panduan ini ditulis).

**Step 2: Run Laravel Herd Installer**

Setelah laravel herd installer selesai kita download, kita run installler dengan cara run as adminstrator, lalu ikuti langkah-langkahnya sampai proses install selesai.

![run](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*dsZxEb_q66QjqdE5GAHC5w.png)

Catatan: Laravel herd perlu permission sebagai admin supaya installer dapat menambahkan HerdHelper service yang bertanggung jawab untuk memperbaharui file _hosts_, map direktori dan link project ke domain _.test_.

**Step3: Run Laravel Herd**

![lets](https://cdn.jsdelivr.net/gh/gungunpriatna/tes-repositori@master/how-to/install-tools/laravel-herd/1%20tampilan%20awal%20setelah%20install.png)

Setelah proses instalasi selesai, selanjutnya kita bisa run langsung laravel herd yang sudah kita install. Ketika pertama kali laravel herd kita run, kita akan membuka windows untuk setup awal. Untuk melanjutkan, kita tekan button _Let's get started_ untuk memulai proses setup awal laravel herd.

Selanjutnya laravel herd akan mendownload php, node js dan tools lainnya.

![php](https://cdn.jsdelivr.net/gh/gungunpriatna/tes-repositori@master/how-to/install-tools/laravel-herd/2%20install%20php%208.3.png)

Setelah proses download selesai, selanjutnya akan masuk ke windows untuk aktivasi laraverd herd pro. Kita bisa tekan link _Skip for now_ untuk menyelesaikan proses setup laravel herd.

![skip](https://cdn.jsdelivr.net/gh/gungunpriatna/tes-repositori@master/how-to/install-tools/laravel-herd/3.%20aktivasi%20laravel%20herd%20pro.png)

Selanjutnya kita bisa lihat windows setup completed. Kita bisa pilih tekan button Open Dashboard untuk membuka dashboard Laravel herd.

[open](https://cdn.jsdelivr.net/gh/gungunpriatna/tes-repositori@master/how-to/install-tools/laravel-herd/4%20tampilan%20setup%20laravel%20herd%20selesai.png)

Kita bisa lihat tampilan dashboard laravel herd. Pada dashboard kita bisa lihat informasi seperti service yang aktif, menu untuk laravel herd pro, dan quick access dengan button ke halaman untuk mengelola project kita.

[dashboard](https://cdn.jsdelivr.net/gh/gungunpriatna/tes-repositori@master/how-to/install-tools/laravel-herd/5%20tampilan%20dashboard%20laravel%20herd.png)

**Step 4: Cek versi php, laravel, composer dan nodejs**

Selanjutnya kita akan coba cek php, laravel, composer dan nodejs yang terinstall dengan run command berikut ini di command prompt windows atau Cmder.

```
php --version
laravel --version
composer --version
node --version
```

Ketika command di atas kita run akan tampil output berikut ini.

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

**Step 1: Download the Aplicacion Herd for MacOS**

![mac](https://i.postimg.cc/G2Hftx1v/image.png)

Kalau untuk ini langsung aja ke websitenya langsung klik Download fow macos (https://herd.laravel.com)

**Step 2: Buka aplikasi Herd nya**

Buka aplikasi Herd nya untuk mastiin kalau bener" sudah bisa jalan.

**Step 3: Cek Environment di Terminal**

Setelah proses pemasangan selesai, Kamu memiliki lingkungan pengembangan PHP dan Laravel yang berfungsi penuh. Ini berarti kamu dapat memiliki PHP, Laravel, dan komposer dari terminal Anda:

```
herd --version
php --version
laravel --version
composer --version
node --version
```

## Konsep MVC di Laravel

Laravel menggunakan arsitektur **MVC** yang merupakan singkatan dari:

- **Model**: Berfungsi untuk berinteraksi dengan database. Model bertanggung jawab dalam mengelola data dan logika bisnis aplikasi.
- **View**: Menampilkan data kepada user. Biasanya berupa file `.blade.php` yang berada di dalam folder `resources/views`.
- **Controller**: Menjadi penghubung antara Model dan View. Controller menerima request dari user, memprosesnya, dan mengembalikan response (biasanya berupa View).

### Ilustrasi Singkat:

![mvc](https://www.rumahweb.com/journal/wp-content/uploads/2024/09/Laravel-MVC-concept.webp)

## Struktur Folder Utama Laravel (Terkait MVC)

- `app/Models` → Tempat menyimpan file Model
- `app/Http/Controllers` → Tempat menyimpan file Controller
- `resources/views` → Tempat menyimpan file View (Blade)

## Routing di Laravel

Routing adalah bagian penting dari Laravel. File route utama Laravel berada di `routes/web.php`
Di sinilah kita mendefinisikan URL dan menghubungkannya ke fungsi atau controller.

### Contoh Route Sederhana

```php
use Illuminate\Support\Facades\Route;

Route::get('/', function () {
    return view('welcome');
});
```

Penjelasan:

- Route::get() artinya menerima HTTP GET.
- '/' adalah URL path.
- `function () { return view('welcome'); }` adalah aksi ketika URL diakses. Dalam hal ini mengembalikan view bernama welcome.

## Membuat Controller dan View di Laravel

Pada bagian ini kita akan belajar cara membuat Controller dan View di Laravel, serta menghubungkannya menggunakan route.

### 1. Membuat Controller

Laravel menyediakan perintah artisan untuk membuat controller.

```bash
php artisan make:controller HomeController
```

Setelah dijalankan, Laravel akan otomatis membuat controller di app/Http/Controllers/HomeController.php

### 2. Menulis Method / Function di Controller

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
- index() akan menampilkan halaman home.
- about() akan menampilkan halaman about.

### 3. Membuat View

#### a. Membuat View home.blade.php

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
- Ketika user membuka /home, akan ditampilkan view home.blade.php
- Ketika user membuka /about, akan ditampilkan view about.blade.php

### 5. Jalankan kode laravel

Jalankan dengan:

```bash
php artisan serve
```

Kemudian buka browser dan kunjungi:
- http://localhost:8000/home
- http://localhost:8000/about

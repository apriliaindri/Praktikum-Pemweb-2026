# Laravel Migration, Seeder, Factory, dan Authentication

## 1. Migration

### Pengertian

Migration adalah fitur Laravel yang memungkinkan pengelolaan versi skema database menggunakan kode PHP. Setiap perubahan struktur database ditulis dalam file migration sehingga skema database menjadi lebih terstruktur, terdokumentasi, dan mudah dikelola.

### Kelebihan Menggunakan Migration

* Menghindari inkonsistensi struktur database.
* Memudahkan kolaborasi dalam tim.
* Mendukung rollback jika terjadi kesalahan.
* Dapat dikelola menggunakan Git atau version control lainnya.

### Perintah Dasar

```bash
php artisan make:migration create_users_table
php artisan migrate
php artisan migrate:rollback
```

### Contoh Migration

```php
// database/migrations/xxxx_xx_xx_create_products_table.php

public function up()
{
    Schema::create('products', function (Blueprint $table) {
        $table->id();
        $table->string('name');
        $table->double('price');
        $table->timestamps();
    });
}
```

---

## 2. Seeder dan Factory

### Pengertian

#### Seeder

Seeder digunakan untuk mengisi data awal atau data dummy ke dalam database. Biasanya digunakan saat proses testing dan pengembangan aplikasi.

#### Factory

Factory digunakan untuk menghasilkan data dummy secara otomatis menggunakan library Faker.

### Kelebihan Seeder dan Factory

* Menghemat waktu pengisian data.
* Memudahkan proses testing.
* Dapat menghasilkan data dalam jumlah besar.
* Mendukung proses CI/CD.

### Langkah-Langkah Penggunaan

### A. Membuat Factory

```bash
php artisan make:factory ProductFactory --model=Product
```

```php
// database/factories/ProductFactory.php

public function definition()
{
    return [
        'name' => $this->faker->word(),
        'price' => $this->faker->randomFloat(2, 1000, 100000),
    ];
}
```

### B. Membuat Seeder

```bash
php artisan make:seeder ProductSeeder
```

```php
// database/seeders/ProductSeeder.php

public function run()
{
    \App\Models\Product::factory(10)->create();
}
```

### C. Menjalankan Seeder Tertentu

```bash
php artisan db:seed --class=ProductSeeder
```

### D. Menjalankan Semua Seeder

Tambahkan pada file `DatabaseSeeder.php`:

```php
public function run()
{
    $this->call(ProductSeeder::class);
}
```

Kemudian jalankan:

```bash
php artisan db:seed
```

---

## 3. Authentication

Authentication adalah proses verifikasi identitas pengguna sebelum dapat mengakses sistem atau fitur tertentu.

### A. Authentication Manual (Vanilla Laravel)

### 1. Migration dan Model User

Laravel secara default sudah menyediakan tabel `users`.

```php
$table->string('name');
$table->string('email')->unique();
$table->timestamp('email_verified_at')->nullable();
$table->string('password');
```

### 2. Routing

Tambahkan route untuk register, login, dan logout.

```php
// routes/web.php

use App\Http\Controllers\AuthController;

Route::get('/register', [AuthController::class, 'showRegisterForm']);
Route::post('/register', [AuthController::class, 'register']);

Route::get('/login', [AuthController::class, 'showLoginForm'])->name('login');
Route::post('/login', [AuthController::class, 'login']);

Route::post('/logout', [AuthController::class, 'logout'])->name('logout');
```

### 3. Controller

Buat controller:

```bash
php artisan make:controller AuthController
```

```php
use App\Models\User;
use Illuminate\Http\Request;
use Illuminate\Support\Facades\Auth;
use Illuminate\Support\Facades\Hash;

class AuthController extends Controller
{
    public function showRegisterForm()
    {
        return view('auth.register');
    }

    public function register(Request $request)
    {
        $request->validate([
            'name' => 'required',
            'email' => 'required|email|unique:users',
            'password' => 'required|min:6|confirmed',
        ]);

        User::create([
            'name' => $request->name,
            'email' => $request->email,
            'password' => Hash::make($request->password),
        ]);

        return redirect('/login');
    }

    public function showLoginForm()
    {
        return view('auth.login');
    }

    public function login(Request $request)
    {
        $credentials = $request->only('email', 'password');

        if (Auth::attempt($credentials)) {
            $request->session()->regenerate();
            return redirect()->intended('/dashboard');
        }

        return back()->withErrors([
            'email' => 'Login gagal. Periksa kembali email dan password.',
        ]);
    }

    public function logout(Request $request)
    {
        Auth::logout();

        $request->session()->invalidate();
        $request->session()->regenerateToken();

        return redirect('/login');
    }
}
```

### 4. View Blade

Buat folder:

```text
resources/views/auth/
├── login.blade.php
└── register.blade.php
```

#### login.blade.php

```html
<form method="POST" action="/login">
    @csrf
    <input name="email" type="email" placeholder="Email">
    <input name="password" type="password" placeholder="Password">
    <button type="submit">Login</button>
</form>
```

#### register.blade.php

```html
<form method="POST" action="/register">
    @csrf
    <input name="name" type="text" placeholder="Name">
    <input name="email" type="email" placeholder="Email">
    <input name="password" type="password" placeholder="Password">
    <input name="password_confirmation" type="password" placeholder="Confirm Password">
    <button type="submit">Register</button>
</form>
```

### 5. Proteksi Halaman

Gunakan middleware `auth` pada route yang ingin dibatasi.

```php
Route::get('/dashboard', function () {
    return view('dashboard');
})->middleware('auth');
```

---

### B. Authentication Menggunakan Starter Kit

Laravel menyediakan starter kit yang mempermudah implementasi authentication.

### Laravel Breeze

#### Instalasi

```bash
composer require laravel/breeze --dev
php artisan breeze:install
npm install
npm run dev
php artisan migrate
```

#### Menjalankan Aplikasi

```bash
php artisan serve
```

#### Akses

```text
http://localhost:8000/register
http://localhost:8000/login
```

### Laravel UI

Sebagai alternatif selain Breeze:

```bash
composer require laravel/ui
php artisan ui bootstrap --auth
npm install
npm run dev
php artisan migrate
```
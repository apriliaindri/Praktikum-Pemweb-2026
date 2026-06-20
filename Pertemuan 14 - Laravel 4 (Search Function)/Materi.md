# Laravel 4 (Search Function)

## 1. Pengenalan Search
Pencarian (search) merupakan fitur penting dalam aplikasi web yang memungkinkan pengguna menemukan data tertentu dari kumpulan data yang besar. Laravel menyediakan berbagai cara untuk mengimplementasikan fitur pencarian secara mudah, fleksibel, dan efisien.

### Konsep Pencarian dalam Laravel

- Basic Search: Pencarian sederhana yang menggunakan query `WHERE` untuk memfilter data berdasarkan kata kunci tertentu.
  
- Pagination with Search: Kombinasi antara fitur pencarian dan paginasi untuk menampilkan hasil secara bertahap, sehingga meningkatkan kenyamanan dan pengalaman pengguna saat mengakses data dalam jumlah besar.

### Metode Implementasi Pencarian

- Query Builder: Menggunakan metode `where()` dan `orWhere()` untuk melakukan pencarian data secara langsung melalui query database.

- Eloquent: Memanfaatkan fitur Eloquent ORM untuk melakukan pencarian dengan sintaks yang lebih mudah dan fleksibel.

- Laravel Scout: Digunakan untuk implementasi pencarian full-text yang lebih canggih dan mendukung pencarian yang lebih cepat serta skalabel.

## Third-party Packages: Menggunakan package seperti Algolia atau Elasticsearch

## 2. Persiapan Proyek

### Membuat Model, Migration, dan Controller

```bash
# Membuat model dengan migration dan controller sekaligus
php artisan make:model Student -mc

# Atau membuat secara terpisah
php artisan make:model Student
php artisan make:migration create_students_table
php artisan make:controller StudentController --resource
```

### Migration Students

```php
// database/migrations/xxxx_xx_xx_create_students_table.php
<?php

use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

return new class extends Migration
{
    public function up()
    {
        Schema::create('students', function (Blueprint $table) {
            $table->id();
            $table->string('name');
            $table->text('bio');
            $table->date('date_of_birth');
            $table->enum('gender', ['male', 'female', 'other'])->nullable();
            $table->timestamps();
            $table->softDeletes();
        });
    }

    public function down()
    {
        Schema::dropIfExists('students');
    }
};
```

### Model Student

```php
// app/Models/Student.php
<?php

namespace App\Models;

use Illuminate\Database\Eloquent\Factories\HasFactory;
use Illuminate\Database\Eloquent\Model;

class Student extends Model
{
    use HasFactory;

    protected $fillable = [
        'name',
        'bio',
        'date_of_birth',
        'gender',
    ];

    protected $casts = [
        'date_of_birth' => 'date',
    ];
}
```

### Menjalankan Migration

```bash
php artisan migrate
```

---

## 3. Membuat Controller

### Membuat Controller

```php
// app/Http/Controllers/StudentController.php
<?php

namespace App\Http\Controllers;

use App\Models\Student;
use Illuminate\Http\Request;

class StudentController extends Controller
{
    public function index(Request $request)
    {
        $search = $request->input('search');

        $students = Student::when($search, function ($query, $search) {
            $query->where('name', 'like', "%{$search}%")
            ->orWhere('bio', 'like', "%$search%");
        })->paginate(10)->withQueryString();

        return view('students.index', compact('students', 'search'));
    }


    public function show(Student $student)
    {
        return view('students.show', compact('student'));
    }
}
```

---

## 4. Routing

### Resource Routes

```php
// routes/web.php
<?php

use App\Http\Controllers\StudentController;
use Illuminate\Support\Facades\Route;

Route::get('/', function () {
    return view('welcome');
});

Route::resource('products', StudentController::class)->only([
    'index', 'show'
]);
```

### Route List

Resource route akan menghasilkan route berikut:

| Method | URI                   | Action | Route Name       |
| ------ | --------------------- | ------ | ---------------- |
| GET    | `/products`           | index  | `products.index` |
| GET    | `/products/{product}` | show   | `products.show`  |

---

## 5. Views Blade

### Layout Template

```html
<!-- resources/views/layouts/app.blade.php -->
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>@yield('title', 'Laravel Search')</title>
    <link
      href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/css/bootstrap.min.css"
      rel="stylesheet"
    />
  </head>
  <body>
    <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
      <div class="container">
        <a class="navbar-brand" href="{{ route('students.index') }}"
          >Student List</a
        >
      </div>
    </nav>

    <div class="container mt-4">
      @if(session('success'))
      <div class="alert alert-success">{{ session('success') }}</div>
      @endif @yield('content')
    </div>

    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/js/bootstrap.bundle.min.js"></script>
  </body>
</html>
```

### Index View (Read)

```html
<!-- resources/views/students/index.blade.php -->

@extends('layouts.app')

@section('title', 'Student List Search')

@section('content')

    <div class="d-flex justify-content-between mb-3">
        <h2>Student List</h2>

        <form action="{{ route('students.index') }}" method="GET" class="d-flex">
            <input type="text" name="search" class="form-control me-2" placeholder="Search by name"
                value="{{ request('search') }}">
            <button class="btn btn-outline-primary" type="submit">Search</button>
        </form>
    </div>

    @if ($students->isEmpty())
        <div class="alert alert-info">No students found.</div>
    @else
        <table class="table table-bordered table-striped">
            <thead class="table-dark">
                <tr>
                    <th>#</th>
                    <th>Name</th>
                    <th>Bio</th>
                    <th>Date of Birth</th>
                    <th>Gender</th>
                    <th>Created At</th>
                    <th>Actions</th>
                </tr>
            </thead>
            <tbody>
                @foreach ($students as $student)
                    <tr>
                        <td>{{ $loop->iteration }}</td>
                        <td>{{ $student->name }}</td>
                        <td>{{ Str::limit($student->bio, 50) }}</td>
                        <td>{{ $student->date_of_birth->format('Y-m-d') }}</td>
                        <td>{{ ucfirst($student->gender) }}</td>
                        <td>{{ $student->created_at->format('Y-m-d') }}</td>
                        <td>
                            <a href="{{ route('students.show', $student->id) }}" class="btn btn-sm btn-info">View</a>
                        </td>
                    </tr>
                @endforeach
            </tbody>
        </table>

        <div class="justify-content-center">
            {{ $students->links('pagination::bootstrap-5') }}
        </div>
    @endif
@endsection

```

### Show View

```html
<!-- resources/views/students/show.blade.php -->

@extends('layouts.app')

@section('title', 'Student Details')

@section('content')
    <div class="card">
        <div class="card-header">
            <h4>Student Details</h4>
        </div>
        <div class="card-body">
            <p><strong>Name:</strong> {{ $student->name }}</p>
            <p><strong>Bio:</strong> {{ $student->bio }}</p>
            <p><strong>Date of Birth:</strong> {{ $student->date_of_birth->format('Y-m-d') }}</p>
            <p><strong>Gender:</strong> {{ ucfirst($student->gender) }}</p>
            <p><strong>Created At:</strong> {{ $student->created_at->format('Y-m-d H:i') }}</p>
        </div>
        <div class="card-footer">
            <a href="{{ route('students.index') }}" class="btn btn-secondary">Back</a>
        </div>
    </div>
@endsection

```
---

## 7. Seeder untuk Testing

```bash
# Buat Factory
php artisan make:factory StudentFactory --model=Student

# Buat Seeder
php artisan make:seeder StudentSeeder
```

### Buat Factory Sederhana

```php
// database/factories/StudentFactory.php
<?php

namespace Database\Factories;

use Illuminate\Database\Eloquent\Factories\Factory;

/**
 * @extends \Illuminate\Database\Eloquent\Factories\Factory<\App\Models\Student>
 */
class StudentFactory extends Factory
{
    public function definition(): array
    {
        return [
            'name' => $this->faker->name(),
            'bio' => $this->faker->paragraph(),
            'date_of_birth' => $this->faker->date('Y-m-d', '-18 years'),
            'gender' => $this->faker->randomElement(['male', 'female', 'other']),
        ];
    }
}
```

### Buat Seeder

```php
// database/seeders/StudentSeeder.php
<?php

namespace Database\Seeders;

use Illuminate\Database\Seeder;
use App\Models\Student;

class StudentSeeder extends Seeder
{
    public function run(): void
    {
        Student::factory()->count(20)->create();
    }
}
```

### Daftarkan Seeder
```php
// database/seeders/DatabaseSeeder.php
<?php

namespace Database\Seeders;

use App\Models\User;
// use Illuminate\Database\Console\Seeds\WithoutModelEvents;
use Illuminate\Database\Seeder;

class DatabaseSeeder extends Seeder
{
    /**
     * Seed the application's database.
     */
    public function run(): void
    {
        $this->call([
            StudentSeeder::class,
        ]);
    }
}
```

```bash
# Jalankan Seeder
php artisan migrate:fresh --seed

# Bila Perlu, Migrate Fresh
php artisan migrate:fresh --seed

```

---

## 8. Test

### Menjalankan Aplikasi

### Test Manual

1. Buka `http://localhost:8000/students`
2. Test Search, nama ataupun bio

---

## Referensi

- [Laravel Controllers](https://laravel.com/docs/controllers)
- [Laravel Eloquent](https://laravel.com/docs/eloquent)
- [Laravel Blade Templates](https://laravel.com/docs/blade)
- [Laravel Pagination](https://laravel.com/docs/pagination)

---

# Pertemuan 12: Laravel 3 (CRUD Operations)

## 1. Pengenalan CRUD

CRUD adalah singkatan dari Create, Read, Update, Delete - operasi dasar yang diperlukan untuk mengelola data dalam aplikasi web. Dalam Laravel, CRUD dapat diimplementasikan dengan mudah menggunakan Eloquent ORM dan resource controllers.

### Konsep CRUD

- **Create**: Menambah data baru
- **Read**: Membaca/menampilkan data
- **Update**: Mengubah data yang sudah ada
- **Delete**: Menghapus data

---

## 2. Persiapan Proyek

### Membuat Model, Migration, dan Controller

```bash
# Membuat model dengan migration dan controller sekaligus
php artisan make:model Product -mc

# Atau membuat secara terpisah
php artisan make:model Product
php artisan make:migration create_products_table
php artisan make:controller ProductController --resource
```

### Migration Products

```php
// database/migrations/xxxx_xx_xx_create_products_table.php
<?php

use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

return new class extends Migration
{
    public function up()
    {
        Schema::create('products', function (Blueprint $table) {
            $table->id();
            $table->string('name');
            $table->text('description');
            $table->decimal('price', 10, 2);
            $table->integer('stock');
            $table->string('category');
            $table->timestamps();
        });
    }

    public function down()
    {
        Schema::dropIfExists('products');
    }
};
```

### Model Product

```php
// app/Models/Product.php
<?php

namespace App\Models;

use Illuminate\Database\Eloquent\Factories\HasFactory;
use Illuminate\Database\Eloquent\Model;

class Product extends Model
{
    use HasFactory;

    protected $fillable = [
        'name',
        'description',
        'price',
        'stock',
        'category'
    ];

    protected $casts = [
        'price' => 'decimal:2',
    ];
}
```

### Menjalankan Migration

```bash
php artisan migrate
```

---

## 3. Resource Controller

Resource controller menyediakan struktur lengkap untuk operasi CRUD dengan method yang sudah standar.

### Membuat Resource Controller

```php
<?php
// app/Http/Controllers/ProductController.php

namespace App\Http\Controllers;

use App\Models\Product;
use Illuminate\Http\Request;

class ProductController extends Controller
{
    /**
     * Display a listing of the resource.
     */
    public function index()
    {
        $products = Product::paginate(10);
        return view('products.index', compact('products'));
    }

    /**
     * Show the form for creating a new resource.
     */
    public function create()
    {
        return view('products.create');
    }

    /**
     * Store a newly created resource in storage.
     */
    public function store(Request $request)
    {
        $request->validate([
            'name' => 'required|string|max:255',
            'description' => 'required|string',
            'price' => 'required|numeric|min:0',
            'stock' => 'required|integer|min:0',
            'category' => 'required|string|max:100',
        ]);

        Product::create($request->all());

        return redirect()->route('products.index')
            ->with('success', 'Product created successfully.');
    }

    /**
     * Display the specified resource.
     */
    public function show(Product $product)
    {
        return view('products.show', compact('product'));
    }

    /**
     * Show the form for editing the specified resource.
     */
    public function edit(Product $product)
    {
        return view('products.edit', compact('product'));
    }

    /**
     * Update the specified resource in storage.
     */
    public function update(Request $request, Product $product)
    {
        $request->validate([
            'name' => 'required|string|max:255',
            'description' => 'required|string',
            'price' => 'required|numeric|min:0',
            'stock' => 'required|integer|min:0',
            'category' => 'required|string|max:100',
        ]);

        $product->update($request->all());

        return redirect()->route('products.index')
            ->with('success', 'Product updated successfully.');
    }

    /**
     * Remove the specified resource from storage.
     */
    public function destroy(Product $product)
    {
        $product->delete();

        return redirect()->route('products.index')
            ->with('success', 'Product deleted successfully.');
    }
}
```

---

## 4. Routing

### Resource Routes

```php
// routes/web.php
<?php

use App\Http\Controllers\ProductController;
use Illuminate\Support\Facades\Route;

Route::get('/', function () {
    return view('welcome');
});

// Resource route untuk products
Route::resource('products', ProductController::class);

// Atau jika ingin membatasi hanya beberapa method
Route::resource('products', ProductController::class)->only([
    'index', 'show', 'create', 'store', 'edit', 'update', 'destroy'
]);
```

### Route List

Resource route akan menghasilkan route berikut:

| Method    | URI                      | Action  | Route Name       |
| --------- | ------------------------ | ------- | ---------------- |
| GET       | `/products`                | index   | `products.index`   |
| GET       | `/products/create`         | create  | `products.create`  |
| POST      | `/products`                | store   | `products.store`   |
| GET       | `/products/{product}`      | show    | `products.show`    |
| GET       | `/products/{product}/edit` | edit    | `products.edit`    |
| PUT/PATCH | `/products/{product}`      | update  | `products.update`  |
| DELETE    | `/products/{product}`      | destroy | `products.destroy` |

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
    <title>@yield('title', 'Laravel CRUD')</title>
    <link
      href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/css/bootstrap.min.css"
      rel="stylesheet"
    />
  </head>
  <body>
    <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
      <div class="container">
        <a class="navbar-brand" href="{{ route('products.index') }}"
          >Product Manager</a
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
<!-- resources/views/products/index.blade.php -->
@extends('layouts.app') @section('title', 'Products List') @section('content')
<div class="d-flex justify-content-between align-items-center mb-3">
  <h1>Products</h1>
  <a href="{{ route('products.create') }}" class="btn btn-primary"
    >Add New Product</a
  >
</div>

<div class="table-responsive">
  <table class="table table-striped">
    <thead>
      <tr>
        <th>ID</th>
        <th>Name</th>
        <th>Category</th>
        <th>Price</th>
        <th>Stock</th>
        <th>Actions</th>
      </tr>
    </thead>
    <tbody>
      @forelse ($products as $product)
      <tr>
        <td>{{ $product->id }}</td>
        <td>{{ $product->name }}</td>
        <td>{{ $product->category }}</td>
        <td>Rp {{ number_format($product->price, 0, ',', '.') }}</td>
        <td>{{ $product->stock }}</td>
        <td>
          <div class="btn-group" role="group">
            <a
              href="{{ route('products.show', $product) }}"
              class="btn btn-info btn-sm"
              >View</a
            >
            <a
              href="{{ route('products.edit', $product) }}"
              class="btn btn-warning btn-sm"
              >Edit</a
            >
            <form
              action="{{ route('products.destroy', $product) }}"
              method="POST"
              class="d-inline"
            >
              @csrf @method('DELETE')
              <button
                type="submit"
                class="btn btn-danger btn-sm"
                onclick="return confirm('Are you sure?')"
              >
                Delete
              </button>
            </form>
          </div>
        </td>
      </tr>
      @empty
      <tr>
        <td colspan="6" class="text-center">No products found.</td>
      </tr>
      @endforelse
    </tbody>
  </table>
</div>

{{ $products->links() }} @endsection
```

### Create View

```html
<!-- resources/views/products/create.blade.php -->
@extends('layouts.app')

@section('title', 'Add New Product')

@section('content')
<div class="row">
    <div class="col-md-8">
        <h1>Add New Product</h1>

        <form action="{{ route('products.store') }}" method="POST">
            @csrf

            <div class="mb-3">
                <label for="name" class="form-label">Product Name</label>
                <input type="text" class="form-control @error('name') is-invalid @enderror"
                       id="name" name="name" value="{{ old('name') }}" required>
                @error('name')
                    <div class="invalid-feedback">{{ $message }}</div>
                @enderror
            </div>

            <div class="mb-3">
                <label for="description" class="form-label">Description</label>
                <textarea class="form-control @error('description') is-invalid @enderror"
                          id="description" name="description" rows="4" required>{{ old('description') }}</textarea>
                @error('description')
                    <div class="invalid-feedback">{{ $message }}</div>
                @enderror
            </div>

            <div class="row">
                <div class="col-md-4">
                    <div class="mb-3">
                        <label for="price" class="form-label">Price</label>
                        <input type="number" class="form-control @error('price') is-invalid @enderror"
                               id="price" name="price" step="0.01" value="{{ old('price') }}" required>
                        @error('price')
                            <div class="invalid-feedback">{{ $message }}</div>
                        @enderror
                    </div>
                </div>
                <div class="col-md-4">
                    <div class="mb-3">
                        <label for="stock" class="form-label">Stock</label>
                        <input type="number" class="form-control @error('stock') is-invalid @enderror"
                               id="stock" name="stock" value="{{ old('stock') }}" required>
                        @error('stock')
                            <div class="invalid-feedback">{{ $message }}</div>
                        @enderror
                    </div>
                </div>
                <div class="col-md-4">
                    <div class="mb-3">
                        <label for="category" class="form-label">Category</label>
                        <select class="form-control @error('category') is-invalid @enderror"
                                id="category" name="category" required>
                            <option value="">Select Category</option>
                            <option value="Electronics" {{ old('category') == 'Electronics' ? 'selected' : '' }}>Electronics</option>
                            <option value="Clothing" {{ old('category') == 'Clothing' ? 'selected' : '' }}>Clothing</option>
                            <option value="Books" {{ old('category') == 'Books' ? 'selected' : '' }}>Books</option>
                            <option value="Sports" {{ old('category') == 'Sports' ? 'selected' : '' }}>Sports</option>
                        </select>
                        @error('category')
                            <div class="invalid-feedback">{{ $message }}</div>
                        @enderror
                    </div>
                </div>
            </div>

            <div class="mb-3">
                <button type="submit" class="btn btn-primary">Create Product</button>
                <a href="{{ route('products.index') }}" class="btn btn-secondary">Cancel</a>
            </div>
        </form>
    </div>
</div>
@endsection
```

### Show View

```html
<!-- resources/views/products/show.blade.php -->
@extends('layouts.app') @section('title', 'Product Details') @section('content')
<div class="row">
  <div class="col-md-8">
    <div class="card">
      <div
        class="card-header d-flex justify-content-between align-items-center"
      >
        <h5 class="mb-0">Product Details</h5>
        <div>
          <a
            href="{{ route('products.edit', $product) }}"
            class="btn btn-warning btn-sm"
            >Edit</a
          >
          <a
            href="{{ route('products.index') }}"
            class="btn btn-secondary btn-sm"
            >Back to List</a
          >
        </div>
      </div>
      <div class="card-body">
        <table class="table table-borderless">
          <tr>
            <th width="150">ID:</th>
            <td>{{ $product->id }}</td>
          </tr>
          <tr>
            <th>Name:</th>
            <td>{{ $product->name }}</td>
          </tr>
          <tr>
            <th>Description:</th>
            <td>{{ $product->description }}</td>
          </tr>
          <tr>
            <th>Price:</th>
            <td>Rp {{ number_format($product->price, 0, ',', '.') }}</td>
          </tr>
          <tr>
            <th>Stock:</th>
            <td>{{ $product->stock }}</td>
          </tr>
          <tr>
            <th>Category:</th>
            <td>{{ $product->category }}</td>
          </tr>
          <tr>
            <th>Created:</th>
            <td>{{ $product->created_at->format('d M Y H:i') }}</td>
          </tr>
          <tr>
            <th>Updated:</th>
            <td>{{ $product->updated_at->format('d M Y H:i') }}</td>
          </tr>
        </table>
      </div>
    </div>
  </div>
</div>
@endsection
```

### Edit View

```html
<!-- resources/views/products/edit.blade.php -->
@extends('layouts.app')

@section('title', 'Edit Product')

@section('content')
<div class="row">
    <div class="col-md-8">
        <h1>Edit Product</h1>

        <form action="{{ route('products.update', $product) }}" method="POST">
            @csrf
            @method('PUT')

            <div class="mb-3">
                <label for="name" class="form-label">Product Name</label>
                <input type="text" class="form-control @error('name') is-invalid @enderror"
                       id="name" name="name" value="{{ old('name', $product->name) }}" required>
                @error('name')
                    <div class="invalid-feedback">{{ $message }}</div>
                @enderror
            </div>

            <div class="mb-3">
                <label for="description" class="form-label">Description</label>
                <textarea class="form-control @error('description') is-invalid @enderror"
                          id="description" name="description" rows="4" required>{{ old('description', $product->description) }}</textarea>
                @error('description')
                    <div class="invalid-feedback">{{ $message }}</div>
                @enderror
            </div>

            <div class="row">
                <div class="col-md-4">
                    <div class="mb-3">
                        <label for="price" class="form-label">Price</label>
                        <input type="number" class="form-control @error('price') is-invalid @enderror"
                               id="price" name="price" step="0.01" value="{{ old('price', $product->price) }}" required>
                        @error('price')
                            <div class="invalid-feedback">{{ $message }}</div>
                        @enderror
                    </div>
                </div>
                <div class="col-md-4">
                    <div class="mb-3">
                        <label for="stock" class="form-label">Stock</label>
                        <input type="number" class="form-control @error('stock') is-invalid @enderror"
                               id="stock" name="stock" value="{{ old('stock', $product->stock) }}" required>
                        @error('stock')
                            <div class="invalid-feedback">{{ $message }}</div>
                        @enderror
                    </div>
                </div>
                <div class="col-md-4">
                    <div class="mb-3">
                        <label for="category" class="form-label">Category</label>
                        <select class="form-control @error('category') is-invalid @enderror"
                                id="category" name="category" required>
                            <option value="">Select Category</option>
                            <option value="Electronics" {{ old('category', $product->category) == 'Electronics' ? 'selected' : '' }}>Electronics</option>
                            <option value="Clothing" {{ old('category', $product->category) == 'Clothing' ? 'selected' : '' }}>Clothing</option>
                            <option value="Books" {{ old('category', $product->category) == 'Books' ? 'selected' : '' }}>Books</option>
                            <option value="Sports" {{ old('category', $product->category) == 'Sports' ? 'selected' : '' }}>Sports</option>
                        </select>
                        @error('category')
                            <div class="invalid-feedback">{{ $message }}</div>
                        @enderror
                    </div>
                </div>
            </div>

            <div class="mb-3">
                <button type="submit" class="btn btn-primary">Update Product</button>
                <a href="{{ route('products.show', $product) }}" class="btn btn-secondary">Cancel</a>
            </div>
        </form>
    </div>
</div>
@endsection
```

---

## 6. Validasi dan Error Handling

### Form Request Validation

Untuk validasi yang lebih kompleks, buat Form Request:

```bash
php artisan make:request ProductRequest
```

```php
// app/Http/Requests/ProductRequest.php
<?php

namespace App\Http\Requests;

use Illuminate\Foundation\Http\FormRequest;

class ProductRequest extends FormRequest
{
    public function authorize()
    {
        return true;
    }

    public function rules()
    {
        $rules = [
            'name' => 'required|string|max:255',
            'description' => 'required|string',
            'price' => 'required|numeric|min:0',
            'stock' => 'required|integer|min:0',
            'category' => 'required|string|max:100',
        ];

        // Jika sedang update, tambahkan rule unique untuk email
        if ($this->isMethod('put') || $this->isMethod('patch')) {
            $rules['name'] = 'required|string|max:255|unique:products,name,' . $this->product->id;
        } else {
            $rules['name'] = 'required|string|max:255|unique:products,name';
        }

        return $rules;
    }

    public function messages()
    {
        return [
            'name.required' => 'Nama produk wajib diisi.',
            'name.unique' => 'Nama produk sudah ada.',
            'price.min' => 'Harga tidak boleh negatif.',
            'stock.min' => 'Stok tidak boleh negatif.',
        ];
    }
}
```

### Menggunakan Form Request di Controller

```php
// Di ProductController.php
use App\Http\Requests\ProductRequest;

public function store(ProductRequest $request)
{
    Product::create($request->validated());
    return redirect()->route('products.index')
        ->with('success', 'Product created successfully.');
}

public function update(ProductRequest $request, Product $product)
{
    $product->update($request->validated());
    return redirect()->route('products.index')
        ->with('success', 'Product updated successfully.');
}
```

---

## 7. Seeder untuk Testing

```php
// database/seeders/ProductSeeder.php
<?php

namespace Database\Seeders;

use App\Models\Product;
use Illuminate\Database\Seeder;

class ProductSeeder extends Seeder
{
    public function run()
    {
        $products = [
            [
                'name' => 'Laptop ASUS ROG',
                'description' => 'Gaming laptop with high performance',
                'price' => 15000000,
                'stock' => 10,
                'category' => 'Electronics'
            ],
            [
                'name' => 'Kemeja Batik',
                'description' => 'Traditional Indonesian shirt',
                'price' => 200000,
                'stock' => 50,
                'category' => 'Clothing'
            ],
            [
                'name' => 'Buku Pemrograman Web',
                'description' => 'Complete guide to web development',
                'price' => 150000,
                'stock' => 30,
                'category' => 'Books'
            ]
        ];

        foreach ($products as $product) {
            Product::create($product);
        }
    }
}
```

---

## 8. Testing CRUD

### Menjalankan Aplikasi

```bash
# Jalankan migration dan seeder
php artisan migrate:fresh --seed

# Jalankan server
php artisan serve
```

### Test Manual

1. Buka `http://localhost:8000/products`
2. Test semua operasi CRUD:
   - Create: Tambah produk baru
   - Read: Lihat daftar dan detail produk
   - Update: Edit produk yang ada
   - Delete: Hapus produk

---

## 9. Best Practices

### Model Relationships

Jika memiliki tabel categories terpisah:

```php
// app/Models/Product.php
public function category()
{
    return $this->belongsTo(Category::class);
}

// app/Models/Category.php
public function products()
{
    return $this->hasMany(Product::class);
}
```

### Soft Deletes

Untuk tidak menghapus data secara permanen:

```php
// Di migration
$table->softDeletes();

// Di model
use Illuminate\Database\Eloquent\SoftDeletes;

class Product extends Model
{
    use HasFactory, SoftDeletes;
}
```

### API Resource (Bonus)

Untuk membuat API CRUD:

```bash
php artisan make:resource ProductResource
```

```php
// app/Http/Resources/ProductResource.php
public function toArray($request)
{
    return [
        'id' => $this->id,
        'name' => $this->name,
        'description' => $this->description,
        'price' => $this->price,
        'stock' => $this->stock,
        'category' => $this->category,
        'created_at' => $this->created_at->format('Y-m-d H:i:s'),
        'updated_at' => $this->updated_at->format('Y-m-d H:i:s'),
    ];
}
```

---

## Referensi

- [Laravel Controllers](https://laravel.com/docs/controllers)
- [Laravel Eloquent](https://laravel.com/docs/eloquent)
- [Laravel Validation](https://laravel.com/docs/validation)
- [Laravel Blade Templates](https://laravel.com/docs/blade)
- [Laravel Pagination](https://laravel.com/docs/pagination)

---

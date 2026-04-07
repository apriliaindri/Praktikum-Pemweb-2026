# Pengenalan Javascript dan DOM

## Apa Itu JavaScript

**JavaScript** adalah bahasa pemrograman yang digunakan untuk membuat halaman website menjadi **interaktif** dan **dinamis**.

Dalam pengembangan web, JavaScript biasanya digunakan bersama **HTML** dan **CSS**.  
- **HTML** berfungsi untuk menyusun struktur halaman  
- **CSS** untuk mengatur tampilan  
- **JavaScript** berperan dalam menambahkan **logika dan interaksi** pada website  

Dengan JavaScript, halaman web dapat merespons tindakan pengguna tanpa perlu memuat ulang halaman. Hal ini membuat pengalaman pengguna menjadi lebih **cepat** dan **responsif**.

### Contoh Penggunaan JavaScript

Beberapa contoh penggunaan JavaScript antara lain:

- Menampilkan pesan saat tombol diklik  
- Melakukan validasi input pada form  
- Membuat animasi sederhana pada halaman web  

JavaScript merupakan salah satu teknologi utama dalam pengembangan web modern karena kemampuannya dalam membuat website lebih **interaktif** dan **responsif**.


## Cara Mengimplementasikan JavaScript

### 1. Langsung di File HTML dengan Tag `<script>`

JavaScript dapat langsung dituliskan di dalam file HTML menggunakan tag `<script>`. Biasanya, tag ini diletakkan di dalam `<body>` atau `<head>`.

Berikut contoh penggunaannya:

```html
<html>
<head>
  <title>Belajar JavaScript</title>
</head>
<body>
  <h1>Hello World</h1>

  <script>
    alert("Halo, ini modal popup dari JavaScript");
  </script>
</body>
</html>
```
> **Catatan:**
> Penulisan JavaScript langsung di HTML cocok untuk contoh sederhana atau pembelajaran, namun untuk proyek yang lebih besar disarankan menggunakan file terpisah.

### 2. Menggunakan File Terpisah (External JavaScript)

Selain ditulis langsung di HTML, JavaScript juga bisa dibuat dalam file terpisah dengan ekstensi `.js`. Cara ini lebih rapi dan direkomendasikan untuk proyek yang lebih besar.

#### File `script.js`
```javascript
const text = "Halo, ini modal popup dari JavaScript";
alert(text);
```

#### `index.html`
```html
<html>
<head>
  <title>Belajar JavaScript</title>
</head>
<body>
  <h1>Hello World</h1>

  <script src="script.js"></script>
</body>
</html>
```
> **Catatan:**
> Menggunakan file terpisah membuat kode lebih rapi, mudah dikelola, dan lebih profesional dibandingkan menulis langsung di HTML.

## Variabel & Tipe Data

## Operator & Percabangan

## Perulangan (Looping)

## Fungsi

## DOM (Document Object Model)

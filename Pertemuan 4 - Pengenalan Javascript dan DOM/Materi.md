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

### Variabel 
---
Variabel digunakan untuk menyimpan data dalam JavaScript.

### 1. `let` dan `var`

Variabel dengan `let` dan `var` bersifat **mutable**, artinya nilainya dapat diubah.

#### Contoh:

```javascript
let angka1 = 5;
const angka2 = 2;

angka1 += angka2;

console.log(angka1);

// Output: 7
```

### 2. `const`

Variabel dengan  `const ` bersifat **immutable**, artinya tidak dapat diubah (tidak bisa di-assign ulang).

#### Contoh:

```javascript
let angka1 = 5;
const angka2 = 2;

angka2 += angka1;

console.log(angka1);

// Output: Error
```
Meskipun bersifat immutable, variabel dengan `const` masih dapat digunakan untuk menyimpan array atau object, di mana isi (value) di dalamnya tetap dapat dimodifikasi.

```javascript
const buah = ['apel', 'jeruk'];

buah.push('mangga');
console.log(buah); 
// Output: ['apel', 'jeruk', 'mangga']

buah = ['pisang']; 
console.log(buah); 
// Output: Error
```

### Tipe Data
---

Tipe data digunakan untuk menentukan jenis nilai yang disimpan dalam variabel pada JavaScript. Berikut beberapa tipe data dasar dalam JavaScript:

### 1. String
String digunakan untuk menyimpan teks.

```javascript
let text = "Halo";
```

### 2. Number
Number digunakan untuk menyimpan angka, baik bilangan bulat maupun desimal.

```javascript
let angka1 = 3;
const angka2 = 4.21;
```

### 3. Boolean
Boolean digunakan untuk menyimpan nilai logika, yaitu `true` atau `false`.

```javascript
let isAngka = true;
```

### 4. Undefined
Undefined adalah nilai default dari variabel yang belum diberi nilai.

```javascript
let result;
```

### 5. Null
Null digunakan untuk menyatakan bahwa sebuah variabel sengaja dikosongkan.

```javascript
let result = null;
```

## Operator & Percabangan

### Operator
---
Operator digunakan untuk melakukan operasi pada variabel dan nilai dalam JavaScript.

### 1. Operator Aritmatika
Digunakan untuk melakukan perhitungan matematika.

```javascript
let a = 1;
let b = 2;
let hasil = a + b;

console.log(hasil); 
// Output: 3
```

### 2. Operator Perbandingan 
Digunakan untuk membandingkan dua nilai dan menghasilkan nilai boolean (`true` atau `false`).

```javascript
5 == '5';    // true  (nilai sama, tipe diabaikan)
5 === '5';   // false (nilai sama, tapi tipe berbeda)
```

### 3. Operator Logika 
Digunakan untuk operasi logika.

```javascript
true && false;   // false (AND)
true || false;   // true  (OR)
!true;           // false (NOT)
```

### Percabangan
---
Percabangan adalah struktur yang digunakan untuk mengambil keputusan berdasarkan kondisi tertentu.

```javascript
let nilai = 80;
const kkm = 75;

if (nilai >= kkm) {
  console.log('Anda lulus');
} else {
  console.log('Maaf, tidak lulus');
}
```

## Perulangan (Looping)

## Fungsi

## DOM (Document Object Model)

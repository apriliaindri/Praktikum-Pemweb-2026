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
Perulangan adalah struktur dalam pemrograman yang digunakan untuk menjalankan suatu perintah secara berulang selama kondisi tertentu terpenuhi.

### 1. Perulangan `for`
Perulangan `for` digunakan untuk menjalankan kode secara berulang dengan jumlah yang sudah ditentukan.

```javascript
for (let i = 1; i <= 5; i++) {
  console.log("Perulangan ke-" + i);
}
```

### 2. Perulangan `while`

Perulangan `while` digunakan untuk menjalankan kode selama kondisi bernilai true.

```javascript
let angka = 1;

while (angka <= 3) {
  console.log("Angka: " + angka);
  angka++;
}
```

### 3. Perulangan `for...in`

Perulangan `for...in` digunakan untuk mengakses properti (key) dari sebuah object.

```javascript
let siswa = {
  nama: "Dina",
  umur: 13,
  kelas: "8A"
};

for (let key in siswa) {
  console.log(key + ": " + siswa[key]);
}
```

### 4. Perulangan `for...of`

Perulangan `for...of` digunakan untuk mengambil nilai dari array atau string.

#### Contoh dengan array:

```javascript
let buah = ["apel", "jeruk", "mangga"];

for (let item of buah) {
  console.log(item);
}
```
#### Contoh dengan string:

```javascript
let teks = "Halo";

for (let huruf of teks) {
  console.log(huruf);
}
```

## Fungsi

Fungsi digunakan untuk membungkus kode agar dapat digunakan kembali.

### 1. Deklarasi Fungsi (Klasik)

Digunakan untuk mendefinisikan fungsi dengan nama tertentu.

```javascript
function halo(nama) {
  return "Halo, " + nama;
}

console.log(halo("Budi"));
// Output: Halo, Budi
```

### 2. Function Expression

Function Expression adalah cara membuat fungsi dengan menyimpannya ke dalam variabel.

```javascript
const halo = function(nama) {
  return "Halo, " + nama;
};

console.log(halo("Budi"));
// Output: Halo, Budi
```

### 3. Arrow Function

Arrow function adalah cara penulisan fungsi yang lebih singkat dibandingkan fungsi biasa.

```javascript
const halo = (nama) => {
  return "Halo, " + nama;
};

console.log(halo("Budi"));
// Output: Halo, Budi
```
Arrow function tidak memiliki `this` sendiri, sehingga tidak cocok digunakan pada object method yang membutuhkan `this`.
```javascript
const orang = {
  nama: "Rani",
  sapa: () => {
    return "Halo, aku " + this.nama; // ❌ this undefined
  }
};
```

## DOM (Document Object Model)

### Apa itu DOM?

DOM (Document Object Model) adalah representasi dari halaman web dalam bentuk struktur seperti pohon (tree) yang dapat dibaca dan dimanipulasi oleh JavaScript.

### Contoh

#### HTML

```html
<body>
  <h1>Halo!</h1>
  <p>Selamat datang di website</p>
</body>
```

#### Struktur DOM

```text
Document
└── html
    └── body
        ├── h1
        └── p
```

### Mengakses HTML dengan DOM
Ada beberapa cara untuk mengakses elemen HTML menggunakan DOM:

| Cara | Fungsi |
|------|--------|
| `getElementById("id")` | Mengambil elemen berdasarkan id |
| `getElementsByClassName("class")` | Mengambil semua elemen berdasarkan class |
| `getElementsByTagName("tag")` | Mengambil semua elemen berdasarkan tag |
| `querySelector("selector")` | Mengambil elemen pertama yang sesuai CSS selector |
| `querySelectorAll("selector")` | Mengambil semua elemen yang sesuai CSS selector |

### Mengubah Konten dan Properti dengan DOM

Beberapa cara untuk mengubah konten dan properti elemen HTML menggunakan DOM:

| Aksi | Contoh |
|------|--------|
| Mengubah teks | `element.textContent = "Halo!"` |
| Mengubah HTML | `element.innerHTML = "Hai!"` |
| Mengubah atribut | `element.setAttribute("href", "https://google.com")` |
| Menghapus atribut | `element.removeAttribute("src")` |

### Mengubah CSS dengan DOM

CSS pada elemen HTML dapat diubah menggunakan properti `style` di JavaScript.

```javascript
const box = document.getElementById("kotak");

// mengubah warna background
box.style.backgroundColor = "red";

// mengubah ukuran teks
box.style.fontSize = "20px";
```

### Menambah dan Menghapus Elemen HTML

Elemen HTML dapat ditambahkan atau dihapus menggunakan JavaScript melalui DOM.

#### Contoh

```javascript
// membuat elemen baru
const paragraf = document.createElement("p");
paragraf.textContent = "Paragraf baru!";

// menambahkan ke halaman
document.body.appendChild(paragraf);

// menghapus elemen
paragraf.remove();
```

### Event Listener

Event Listener adalah fungsi yang akan dijalankan ketika suatu event (kejadian) terjadi pada elemen HTML.

#### Contoh Penggunaan

- Klik tombol → menampilkan pesan  
- Hover ke elemen → mengubah tampilan  
- Input teks → menampilkan perubahan secara langsung  

#### Bentuk Dasar

```javascript
element.addEventListener("event", function() {
  // aksi
});
```

Contoh Event Listener pada Javascript:
```javascript
const tombol = document.querySelector("#klik");

tombol.addEventListener("click", function() {
  alert("Tombol diklik!");
});
```

#### Jenis-Jenis Event pada Event Listener

| Event | Kapan Terjadi |
|------|--------------|
| `"click"` | Ketika elemen diklik |
| `"mouseover"` | Saat kursor masuk ke elemen |
| `"mouseout"` | Saat kursor keluar dari elemen |
| `"keydown"` | Saat tombol keyboard ditekan |
| `"keyup"` | Saat tombol keyboard dilepas |
| `"input"` | Saat pengguna mengetik dalam input field |
| `"submit"` | Saat form dikirim |
| `"change"` | Saat isi input berubah (biasanya select, radio) |

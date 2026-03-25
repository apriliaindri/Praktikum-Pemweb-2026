# Pengenalan dan Pendalaman HTML

## Pengertian HTML 
![Gambar](HTML.png)

HTML (HyperText Markup Language) adalah bahasa dasar untuk membuat halaman web. HTML digunakan untuk menyusun elemen-elemen dalam sebuah halaman agar dapat ditampilkan di browser.

### Anatomi Elemen HTML 

Elemen HTML adalah salah satu bagian dari HTML dalam membangun halaman web. Elemen ini digunakan untuk mendefinisikan elemen-elemen yang ditampilkan dalam halaman web. Ada beberapa hal untuk membangun elemen HTML itu sendiri. Berikut adalah bagan dari anatomi elemen HTML.

![Gambar](Anatomi HTML.png)

Berikut adalah pembahasan dari masing-masing bagian dari bagan di atas.

Berikut adalah pembahasan dari masing-masing bagian dari bagan di atas.

| Item           | Keterangan |
|----------------|-----------|
| Tag Pembuka    | Berisi nama tag dari elemen yang akan dibuat dan dibungkus dengan angle bracket `< >`. Contohnya adalah `<p>` untuk membuat elemen paragraf (paragraph). |
| Konten         | Konten dari elemen. Contohnya teks sebagai konten dari elemen paragraf. |
| Tag Penutup    | Sama seperti tag pembuka, tetapi terdapat garis miring sebelum nama elemennya (`</p>`). Ini menandakan akhir dari elemen HTML. Kesalahan umum pemula adalah melupakan tag ini sehingga elemen menjadi tidak valid. |

### Atribute Elemen di HTML 

Dalam membuat elemen HTML, ada satu hal yang dapat dilakukan, yaitu memberi atribut. Atribut dapat memberi informasi-informasi tambahan untuk elemen HTML. Informasi ini tidak akan tampil dalam halaman web, tetapi ia dapat menentukan perilaku elemen biasanya. Berikut adalah anatomi dari atribut elemen untuk memperjelas pemahaman kamu.

![Gambar](Att HTML.png)

### Anatomi Dokumen HTML

Pada dasarnya, dokumen HTML memerlukan struktur dasar untuk menampilkan halaman web dengan baik. Halaman web seharusnya memiliki susunan elemen HTML yang tampak seperti berikut.

![Gambar](Anatomi Dokumen HTML.jpeg)

Keterangan:

- `<!DOCTYPE html>` → Menandakan bahwa ini adalah dokumen HTML.

- `<html>` → Elemen utama yang membungkus seluruh isi halaman.

- `<head>` → Bagian kepala yang berisi informasi meta dan judul halaman.

- `<title>` → Menentukan judul yang muncul di tab browser.

- `<body>` → Bagian utama tempat konten halaman web ditampilkan.

Dokumen di atas sebetulnya akan membentuk sebuah hierarki elemen atau yang biasa disebut dengan DOM Tree (pohon DOM). Ini dapat Temen" analogikan seperti silsilah keluarga. Kurang lebih, berikut adalah DOM Tree yang terbentuk dari dokumen HTML di atas.

![Gambar](DOM Tree.png)

### Elemen dan Tag Dasar dalam HTML

| Elemen                  | Tag HTML                | Kegunaan |
|-------------------------|------------------------|----------|
| Heading                 | `<h1> - <h6>`          | Membuat judul atau heading |
| Paragraf                | `<p>`                  | Membuat sebuah paragraf |
| Divisi                  | `<div>`                | Membuat sebuah divisi atau wadah untuk mengelompokkan elemen lain |
| Gambar                  | `<img src="gambar.jpg">` | Menampilkan gambar |
| Tautan / Link           | `<a href="url">`       | Membuat teks hyperlink |
| Daftar Berurutan        | `<ol>`                 | Membuat sebuah daftar dengan nomor |
| Daftar Tidak Berurutan  | `<ul>`                 | Membuat sebuah daftar dengan bullet |
| Item                    | `<li>`                 | Membuat item di dalam tag `<ul>` atau `<ol>` |
| Garis Horizontal        | `<hr>`                 | Membuat sebuah garis horizontal |
| Baris Baru              | `<br>`                 | Membuat sebuah baris baru |

### Contoh Penggunaan Tag Dasar HTML

```html
<!DOCTYPE html>
<html>
<head>
    <title>Belajar HTML</title>
</head>
<body>
    <h1>Judul Utama</h1>
    <h2>Judul Kedua</h2>
    <p>Ini adalah sebuah paragraf yang menjelaskan sesuatu.</p>
    
    <a href="https://www.google.com">Kunjungi Google</a>
    
    <img src="gambar.jpg" alt="Gambar Contoh">
    
    <h3>Daftar Belanja</h3>
    <ul>
        <li>Apel</li>
        <li>Pisang</li>
        <li>Jeruk</li>
    </ul>
    
    <h3>Langkah-langkah Memasak</h3>
    <ol>
        <li>Siapkan bahan.</li>
        <li>Panaskan wajan.</li>
        <li>Masak hingga matang.</li>
    </ol>
</body>
</html>
```

## Semantic HTML: Mengorganisasikan Halaman Konten

Website memiliki hierarki konten yang sama seperti dokumen sehari-hari yang kita baca, majalah, dan koran. Jadi, hierarki pada sebuah website merupakan hal yang penting. Tentu elemen yang terdapat pada HTML perlu kita kelompokkan menjadi beberapa bagian.

![Gambar](Semantic HTML.jpeg)

Kita dapat menggunakan beberapa elemen dalam HTML untuk mengelompokkan sebuah elemen dengan jelas dan memiliki arti (semantic meaning). Elemen-elemen ini memiliki nama sesuai dengan fungsi atau peran dari elemen tersebut.

![Gambar](Semantic Meaning.jpeg)

### Semantic VS Non-Semantic HTML

![Gambar](Semantic vs Non Semantic.png)

#### Generic Elements
HTML menyediakan dua tipe elemen umum (generic element) yang bisa kita kustomisasi untuk menggambarkan konten kita dengan tepat, yaitu div dan span. Elemen ini akan terlibat jika tidak ada semantic element sesuai di HTML.

- Div
Elemen `<div>` merupakan sebuah wadah (container) yang bersifat umum untuk menampung beberapa konten. Elemen ini tidak akan memberikan efek apa pun pada konten atau layout sebelum menerapkan sebuah style menggunakan CSS.

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Div Element</title>
    <link rel="stylesheet" href="styles.css">
  </head>
  <body>
    <div class="shadowbox">
      <p>
        Paragraf ini berada di dalam elemen div, tetapi ia akan ditampilkan sama seperti paragraf
        biasanya. Elemen ini lebih sering digunakan untuk mengelompokkan sebuah konten sehingga
        dapat memudahkan styling dengan menggunakan atribut class atau id.
      </p>
    </div>
  </body>
</html>
```

- Span
Elemen `<span>` memberikan manfaat yang sama seperti `<div>`, bedanya elemen ini digunakan sebagai phrase elements dan tidak terdapat line breaks ketika menggunakannya. Sederhananya, `<span>` merupakan sebuah `<div>` yang digunakan dalam sebuah baris teks yang dapat diwadahi oleh paragraf, list, heading, atau lainnya.

```html
<style>
  .phone {
    font-weight: bold;
  }
</style>

<ul>
  <li>Agil: <span class="phone">08123xxx</span></li>
  <li>Widy: <span class="phone">08222xxx</span></li>
  <li>Gilang: <span class="phone">08333xxx</span></li>
</ul>
```







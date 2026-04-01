# Pengenalan dan Pendalaman CSS 

## Pengantar CSS

### Pengantar Pengenalan CSS
![Gambar](CSS.png)

Website akan terlihat kurang menarik tanpa adanya CSS. **CSS (Cascading Style Sheet)** merupakan standar dari *W3C* yang digunakan untuk mengatur tampilan atau visualisasi halaman HTML. CSS bersifat *declarative language*, yaitu digunakan untuk mendeklarasikan nilai-nilai yang berfungsi mengatur tampilan elemen HTML di browser.

### Keuntungan dan Cara CSS Bekerja
Dengan menerapkan CSS, tampilan website akan menjadi lebih menarik.  
Berikut beberapa keuntungan menggunakan CSS:

- **Mengatur layout dengan presisi**  
  CSS memungkinkan kita membuat tampilan website yang rapi dan terstruktur, bahkan menyerupai desain dokumen cetak.

- **Menghindari penulisan berulang**  
  Styling dapat diterapkan ke banyak halaman HTML hanya dengan satu file CSS, sehingga lebih efisien.

- **Didukung oleh banyak browser**  
  Hampir semua browser modern sudah mendukung CSS, minimal CSS versi 2, dan sebagian besar sudah mendukung CSS versi 3.


### Menulis Aturan Styling
Dalam CSS, sebuah *rule* terdiri dari dua bagian utama:

- **Selector**  
  Bagian yang digunakan untuk menentukan elemen HTML mana yang akan diberi styling.

- **Declaration**  
  Bagian yang berisi aturan atau instruksi styling yang akan diterapkan pada selector.

![Gambar](AturanStyling.jpeg)

### Melampirkan Styling pada Dokumen HTML

Berikut adalah beberapa cara untuk melampirkan CSS ke dalam dokumen HTML:

---
### 1. External Style Sheet

**External Style Sheet** adalah file terpisah yang berisi kumpulan aturan CSS. File ini memiliki ekstensi `.css` dan dihubungkan ke dokumen HTML. Metode ini merupakan cara yang paling direkomendasikan karena lebih rapi dan efisien. Selain itu, satu file CSS dapat digunakan untuk mengatur tampilan pada banyak halaman HTML sekaligus.

#### Keunggulan:
- Dapat digunakan di banyak halaman  
- Lebih rapi dan terstruktur  
- Mudah dikelola  

```html
<head>
  <meta charset="UTF-8" />
  <title>Judul Dokumen</title>

  <!-- Impor berkas CSS Anda -->
  <link rel="stylesheet" href="style.css">
</head>
```

### 2. Embedded Style Sheet
**Embedded Style Sheet** adalah aturan CSS yang dituliskan langsung di dalam dokumen HTML menggunakan elemen `<style>`. Biasanya, penulisan CSS ini ditempatkan di dalam bagian `<head>` pada dokumen HTML.

```html
<head>
  <meta charset="UTF-8" />
  <title>Judul Dokumen</title>

  <style>
    h1 {
      color: green;
    }
  </style>
</head>
```

### 3. Inline Style

**Inline Style** adalah cara menerapkan CSS langsung pada elemen HTML menggunakan atribut `style`.

```html
<p style="color: green;">Konten dari elemen HTML</p>
```

Jika ingin menambahkan lebih dari satu properti, gunakan semicolon (;) sebagai pemisah:
```html
<p style="color: green; font-size: 18px;">Contoh teks</p>
```

> **Catatan:**  
> Inline style biasanya digunakan untuk kebutuhan khusus dan tidak disarankan untuk penggunaan dalam skala besar karena sulit dikelola.

## Konsep Dasar CSS

### CSS Conception

Sebelum membahas styling lebih lanjut, penting untuk memahami beberapa konsep dasar dalam CSS yang membantu kita memahami bagaimana CSS bekerja dalam mengatur tampilan elemen HTML serta bagaimana aturan styling saling berinteraksi, sehingga kita dapat menulis kode yang lebih terstruktur, efisien, dan mudah dikelola.

### Inheritance

Styling pada CSS bersifat *inheritance*, yaitu beberapa properti dapat diwariskan dari elemen induk (*parent*) ke elemen di dalamnya (*child elements*).

Sebagai contoh, aturan CSS yang diterapkan pada elemen `<body>` akan secara otomatis memengaruhi seluruh elemen di dalamnya. Begitu juga jika pada elemen `<footer>` diberikan properti `color: white`, maka seluruh teks di dalam `<footer>` akan mengikuti warna tersebut.

Hal ini menunjukkan bahwa pemahaman terhadap struktur dokumen HTML sangat penting dalam penggunaan CSS.

#### Contoh:

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8" />
  <title>CSS Inheritance Example</title>

  <link rel="stylesheet" href="styles.css" />
</head>
<body>
  <header>
    <h1>Inheritance di CSS</h1>
  </header>
  <main>
    <h2>Lorem Ipsum</h2>

    <article>
      <h3>Lorem, ipsum dolor.</h3>
      <p>
        Pellentesque venenatis mi sit amet erat tincidunt auctor. Curabitur tincidunt tellus ac
        convallis dictum. Morbi luctus leo eget leo luctus elementum. Cras at ligula eu elit
        blandit venenatis.
      </p>
    </article>
  </main>
  <footer>
    <p>Hak Cipta &copy; 2023</p>
  </footer>
</body>
</html>
```

```css
body {
  font-family: sans-serif;
}

footer {
  color: white;
}
```
Berikut adalah hasil penerapan contoh studi kasus di atas.

![Gambar](Inheritance.jpeg) 

> **Catatan:**  
> Tidak semua properti CSS dapat diwariskan. Contohnya, properti seperti `margin` dan `padding` tidak akan diwariskan secara otomatis.

### Group Selector

Jika beberapa selector memiliki properti yang sama, kita dapat menggabungkannya menggunakan *group selector*. Dengan cara ini, penulisan kode menjadi lebih ringkas dan dapat menghindari pengulangan yang tidak perlu.
```css
h2 {
  color: #00A2C6;
}

h3 {
  color: #00A2C6;
}
```
Dalam kasus seperti di atas, kita dapat menuliskan beberapa selector sekaligus dalam satu *rule*. Gunakan tanda koma (`,`) untuk memisahkan setiap selector.

Perhatikan contoh berikut:
```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>Judul Dokumen</title>

    <link rel="stylesheet" href="styles.css">
  </head>
  <body>
    <h2>Judul dengan Heading 2</h2>
    <h3>Judul dengan Heading 3</h3>
  </body>
</html>
```

```css
h2, h3 {
  color: #00A2C6;
}
```

### Rule Order

Sesuai dengan namanya, *cascading* berarti “mengalir”. Dalam CSS, aturan styling dibaca dari atas ke bawah. Oleh karena itu, urutan penulisan *rule* sangat penting, terutama ketika terjadi konflik antar styling. Konflik dapat terjadi ketika beberapa aturan diterapkan pada elemen yang sama dan saling menimpa.

Sebagai contoh, jika pada *external CSS* elemen `<p>` diberi warna merah, tetapi pada *embedded CSS* diberi warna biru, maka warna yang akan ditampilkan adalah warna yang terakhir didefinisikan, yaitu biru. Hal ini terjadi karena CSS mengikuti prinsip *cascading*, yaitu aturan yang ditulis paling akhir akan memiliki prioritas lebih tinggi.

Perhatikan contoh berikut:

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>Judul Dokumen</title>

    <link rel="stylesheet" href="styles.css">

    <style>
      p {
        color: blue;
      }
    </style>
  </head>
  <body>
    <p>
      Sesuai dengan namanya cascading yang artinya <q>mengalir</q>, alur kerja CSS dalam membaca
      kode pun seperti itu. Mengalir dari atas ke bawah sehingga kita harus memperhatikan urutan
      dalam penulisan rules <i>styling</i>.
    </p>
  </body>
</html>
```

```css
p {
  color: red;
}
```

Namun, kita dapat memaksa sebuah properti CSS agar memiliki prioritas lebih tinggi dengan menggunakan keyword `!important`. Dengan menambahkan `!important` di akhir nilai properti, aturan tersebut akan tetap diterapkan meskipun ada aturan lain yang ditulis setelahnya.

```css
p {
  color: red !important;
}
```

> **Catatan:**  
> Gunakan `!important` hanya jika benar-benar diperlukan. Sebaiknya pahami terlebih dahulu aturan urutan (*cascading*) dalam CSS agar penggunaan `!important` dapat diminimalkan.

Berikut adalah beberapa konsep yang telah dipelajari terkait styling pada CSS:
- **Rule**: Aturan styling yang diterapkan pada elemen HTML. Sebuah *rule* terdiri dari *selector* dan *declaration*.
- **Selector**: Bagian yang digunakan untuk menentukan elemen HTML yang akan diberi styling.
- **Declaration**: Bagian dari *rule* yang berisi pasangan properti dan nilai (*property: value*).
- **External Style Sheet**: Berkas terpisah (berekstensi `.css`) yang berisi satu atau lebih *rule* dan digunakan untuk mengatur tampilan beberapa halaman HTML.
- **Embedded Style Sheet**: Kumpulan *rule* yang dituliskan langsung di dalam dokumen HTML menggunakan elemen `<style>`.
- **Inline Style**: Styling yang diterapkan langsung pada elemen HTML melalui atribut `style`.

## Pendalaman CSS
### Pengantar Pendalaman CSS

Pada modul ini, kita akan mempelajari CSS secara lebih mendalam. Beberapa topik yang akan dibahas meliputi berbagai jenis *selector*, pengaturan teks (*text formatting*), pewarnaan, *box model*, *positioning*, hingga penyusunan layout pada website menggunakan teknik *floating*.

## Selector Dasar
CSS memiliki berbagai jenis *selector* yang digunakan untuk menargetkan elemen tertentu dalam dokumen HTML.  

Pada modul sebelumnya, kita telah mempelajari pengertian *selector* dan cara penggunaannya. Selector yang telah digunakan tersebut termasuk dalam kategori *basic selector*.  

Berikut adalah beberapa jenis *basic selector* dalam CSS:
- Type Selector  
- Class Selector  
- ID Selector  
- Attribute Selector  
- Universal Selector  

Selanjutnya, kita akan membahas masing-masing *selector* tersebut satu per satu.

--- 
### 1. Type Selector
Type selector menggunakan nama elemen sebagai target untuk diterapkannya *rule*. Dengan kata lain, ketika menggunakan selector ini, *rule* akan diterapkan pada seluruh elemen target yang ada pada dokumen HTML. Contohnya sebagai berikut.

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>Judul Dokumen</title>
    <link rel="stylesheet" href="styles.css" />
  </head>
  <body>
    <span>
      Ini merupakan sebuah teks yang berada pada elemen span. Seharusnya elemen
      ini ditampilkan dengan warna teks merah.
    </span>
    <p>
      Ini merupakan sebuah teks yang berada pada elemen paragraf, teks ini tidak
      seharusnya tidak akan terpengaruh oleh rule.
    </p>
    <span>
      Ini merupakan sebuah teks yang berada pada elemen span lainnya. Seharusnya
      elemen ini ditampilkan dengan warna teks merah juga.
    </span>
  </body>
</html>
```

```css
/* Semua elemen span */
span {
  color: red;
}
```

Jika berkas tersebut dibuka pada browser, teks yang berada pada setiap elemen `<span>` akan berwarna merah.

### 2. Class Selector

Class selector menetapkan target elemen berdasarkan nilai dari atribut `class` yang diterapkan pada elemen tersebut. Penulisan selector diawali dengan tanda titik (`.`), kemudian diikuti dengan nama class. Contohnya sebagai berikut.

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>Judul Dokumen</title>

    <link rel="stylesheet" href="styles.css" />
  </head>
  <body>
    <p class="red">Paragraf dengan teks berwarna merah</p>
    <p class="skyblue-bg">Paragraf dengan background berwarna biru langit</p>
    <p class="fancy">Paragraf dengan gaya fancy</p>
    <p>
      Paragraf yang menampilkan teks dengan warna standar tanpa menerapkan
      styling
    </p>
  </body>
</html>
```

```css
.red {
  color: red;
}

.skyblue-bg {
  background-color: skyblue;
}

.fancy {
  font-weight: bold;
  text-shadow: 4px 4px 3px #77f;
}
```

### 3. ID Selector

ID selector menetapkan target elemen berdasarkan nilai dari atribut `id` yang diterapkan pada elemen tersebut. Mirip dengan `class`, atribut `id` dapat digunakan pada berbagai elemen HTML dan umumnya dimanfaatkan untuk memberikan identitas pada elemen generik, seperti `<div>` dan `<span>`. Namun, atribut `id` tidak bersifat *shareable*. Artinya, nilai `id` harus unik dan hanya digunakan pada satu elemen saja.  

Untuk menuliskan selector menggunakan `id`, kita menggunakan tanda pagar (`#`) atau yang dikenal sebagai *hash*. Berikut contohnya.


```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>Judul Dokumen</title>

    <link rel="stylesheet" href="styles.css" />
  </head>
  <body>
    <div id="special">
      <p>Ini merupakan konten di dalam sebuah div yang diberi id special.</p>
    </div>
    <div>
      <p>Ini merupakan konten di dalam sebuah div biasa.</p>
    </div>
  </body>
</html>
```
```css
#special {
  background-color: skyblue;
}
```

> Perlu ditekankan bahwa `id` bersifat unik dan hanya digunakan pada satu elemen. Jika ingin menerapkan *rule* pada banyak elemen, sebaiknya gunakan atribut `class` dibandingkan `id`.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>Judul Dokumen</title>
    <style>
      #special {
        background-color: skyblue;
      }
    </style>
  </head>
  <body>
    <div id="special">
      <p>Ini merupakan konten di dalam sebuah div yang diberi id special.</p>
    </div>

    <!-- ini merupakan contoh yang salah dalam penerapan id -->
    <div id="special">
      <p>Ini merupakan konten di dalam sebuah div biasa.</p>
    </div>
  </body>
</html>
```
### 4. Attribute Selector

Attribute selector merupakan cara untuk menetapkan target elemen berdasarkan atribut yang digunakan, atau bahkan lebih spesifik berdasarkan nilai dari atribut tersebut. Contohnya sebagai berikut.

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>Attribute Selector</title>

    <link rel="stylesheet" href="styles.css" />
  </head>
  <body>
    <ul>
      <li><a href="#internal">Internal link</a></li>
      <li><a href="http://example.com">Example link</a></li>
      <li><a href="#InSensitive">Insensitive internal link</a></li>
      <li><a href="http://example.org">Example org link</a></li>
    </ul>
  </body>
</html>
```

```css
ul {
  font-size: 18px;
}

/* <a> element yang menerapkan href attribute */
a[href] {
  color: blue;
}

/* <a> element yang menerapkan nilai pada href dengan awalan "#" */
a[href^='#'] {
  background-color: gold;
}

/* <a> element yang menerapkan nilai pada href yang mengandung teks "example" */
a[href*='example'] {
  background-color: silver;
}

/* <a> element yang menerapkan nilai pada href yang mengandung teks "insensitive" tidak mementingkan huruf kapital*/
a[href*='insensitive' i] {
  color: cyan;
}

/* <a> element yang menerapkan nilai pada href dengan akhiran ".org" */
a[href$='.org'] {
  color: red;
}
```

### 5. Universal Selector  

Universal selector digunakan untuk menargetkan seluruh elemen dalam dokumen HTML. Namun, selector ini juga dapat digunakan secara lebih spesifik dengan menggabungkannya bersama selector lain. Berikut contohnya.

```html
<!DOCTYPE html>
<html lang="id">
  <head>
    <meta charset="UTF-8" />
    <title>Judul Dokumen</title>

    <link rel="stylesheet" href="styles.css" />
  </head>
  <body>
    <p>
      Ini merupakan paragraf biasa atau tidak menerapkan atribut apapun. Maka
      teks pada paragraf ini akan berwarna hijau
    </p>
    <p lang="en-us">
      This is an English paragraph contains en-us value of lang attribute, so
      this text will be green and italic.
    </p>

    <h1>Ini merupakan sebuah header biasa</h1>
    <h1 lang="en-us">This is an English Header</h1>

    <p class="warning">
      Perhatikan paragraf ini! Paragraf ini merupakan paragraf yang memiliki
      kelas bernilai warning, sehingga teks dari paragraf ini akan berwarna
      merah
    </p>

    <div id="content">
      <p>
        Ini merupakan sebuah teks di dalam sebuah div yang memiliki id bernilai
        "content", seharusnya paragraf ini dibungkus dalam border yang memiliki
        padding 20px
      </p>
    </div>
  </body>
</html>
```

```css
/* Menargetkan seluruh tipe elemen */
* {
  color: green;
}

/* Menargetkan seluruh tipe elemen yang mengandung nilai "en" pada atribut lang */
*[lang^='en'] {
  font-style: italic;
}

/* Menargetkan seluruh tipe elemen yang memiliki nilai "warning" pada atribut class */
*.warning {
  color: red;
}

/* Menargetkan seluruh tipe elemen yang memiliki nilai "content" pada atribut id */
*#content {
  border: 1px solid blue;
  padding: 20px;
}
```

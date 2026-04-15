# Pengenalan JQuery

## Apa itu JQuery?

**JQuery** adalah library Javascript yang dibuat untuk mempermudah penulisan kode Javascript. Pada pertemuan sebelumnya, kita tahu bahwa kita bisa melakukan hal-hal seperti:

- Menangani Event
- Mengubah isi halaman
- Menampilkan / menyembunyikan elemen

Tapi, kadang kode tersebut bisa menjadi panjang atau rumit. Nah, JQuery hadir untuk membuat kode itu menjadi lebih pendek, mudah, dan cepat ditulis. Contohnya sebagai berikut:

```
// Javascript biasa
const tombol = document.getElementById("tombol");
tombol.addEventListener("click", function() {
  alert("tombol diklik!");
})

// JQuery
$("#tombol").click(function() {
  alert("tombol diklik!");
})
```


## Cara Menggunakan JQuery
Terdapat 2 cara untuk menggunakan JQuery:

### 1. Menggunakan CDN
Cara ini adalah cara yang paling mudah untuk menggunakan JQuery. Kamu cukup copy `script` dari website resmi JQuery, kemudian paste kode `script` tersebut pada souce code HTML kalian.

```
<script src="https://code.jquery.com/jquery-3.x.x.min.js"></script>
```

### 2. Install JQuery pada Projek Kalian
1. Buka situs https://jquery.com/download/
2. Download JQuery
3. Simpan file tersebut di folder projek kalian
4. Tambahkan `script` dengan path file JQuery kalian

```
<script src="jquery-3.x.x.min.js"></script>
```

## Sintaks JQuery
jQuery selalu dimulai dengan tanda dolar ($), diikuti dengan selector dan aksi. Struktur sintaks JQuery:

```
$(selector).action();
```

- selector: elemen HTML yang ingin kamu pilih
- action(): apa yang ingin kamu lakukan terhadap elemen itu

Contoh penggunaan sintaks JQuery:

```
$("p").hide(); // Menyembunyikan semua paragraf
```


## Menunggu Halaman Selesai Dimuat
Agar jQuery bekerja setelah semua elemen halaman selesai dimuat, kita bisa menambahkan sintaks berikut:

```
$(document).ready(function() {
  // kode jQuery yang lain di sini
});
```


## Selektor JQuery
Sama seperti CSS, kita bisa memilih elemen pada JQuery berdasarkan:

### ID

```
$("#judul")  // pilih elemen dengan id="judul"
```

### Class

```
$(".kotak")  // pilih semua elemen dengan class="kotak"
```

### Tag

```
$("h1")  // pilih semua elemen <h1>
```

### Kombinasi

```
$("div.kotak")  // pilih semua <div> dengan class "kotak"
```

Contoh kode:

```
<!DOCTYPE html>
<html>
<head>
  <title>Dasar jQuery</title>
</head>
<body>

<h1 id="judul">Selamat Datang!</h1>
<p class="teks">Ini adalah paragraf.</p>
<button id="sembunyi">Sembunyikan</button>

<script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
<script>
  $(function() {
    $("#sembunyi").click(function() {
      $("#judul").hide();
      $(".teks").hide();
    });
  });
</script>

</body>
</html>
```


## Manipulasi DOM
### Mengubah Teks dan HTML
#### `.text()`

```
// Ambil teks
let isi = $("p").text();

// Ubah teks
$("p").text("Teks baru");
```

#### `.html()`

```
// Ambil isi HTML
let isi = $("#judul").html();

// Ubah isi dengan HTML
$("#judul").html("<i>Halo Dunia!</i>");
```

### Mengubah Nilai Input
Untuk mengubah nilai input, kita bisa menggunakan `.val()`. Berikut adalah contoh penggunaannya:

```
// Ambil nilai
let nama = $("#inputNama").val();

// Ubah nilai
$("#inputNama").val("Nama baru");
```

### Menambah dan Menghapus Elemen
#### Menambahkan isi di dalam akhir elemen - `.append()`

```
$("#kontainer").append("<p>Paragraf baru di akhir</p>");
```

#### Menambahkan isi di dalam awal elemen - `.prepend()`

```
$("#kontainer").prepend("<p>Paragraf baru di awal</p>");
```

#### Menghapus elemen - `.remove()`

```
$(".iklan").remove();
```

### Mengubah Attribut dan Class
#### Mengubah attribut (href, class, src, dll) - `.attr()`

```
$("img").attr("src", "gambar-baru.jpg");
```

#### Menambahkan class - `.addClass()`

```
$("#box").addClass("aktif");
```

#### Menghapus class - `.removeClass()`

```
$("#box").removeClass("aktif");
```

#### Toggle class - `.toggleClass()`

```
$("#box").toggleClass("aktif");
```


## Event Handling Pada JQuery
### Apa itu Event?
Event (peristiwa) adalah aksi dari pengguna atau hal yang terjadi di halaman, seperti:

- Klik tombol
- Arahkan mouse (hover)
- Mengetik sesuatu
- Scroll halaman

### Event pada JQuery

| Event |	Kapan Terjadi |
| ----- | ------------- |
| click() |	Saat elemen diklik |
| dblclick() | Saat diklik dua kali |
| hover() |	Saat mouse masuk/keluar |
| focus() |	Saat input mendapat fokus (diklik) |
| blur() |	Saat input kehilangan fokus |
| change() |	Saat isi input berubah |
| keyup()	| Saat tombol keyboard dilepas |
| keydown()	| Saat tombol keyboard dalam perjalanan ditekan |
| keypress() | Saat tombol ditekan |

Contoh event handling pada JQuery

```
$("#kotak").dblclick(function() {
  $(this).css("background", "green");
});

$("input").focus(function() {
  $(this).css("background-color", "lightyellow");
});

$("input").blur(function() {
  $(this).css("background-color", "white");
});
```

### Event Binding dengan `.on()`
Untuk semua jenis event, kita juga bisa memakai `.on()`. Contohnya:

```
$("#tombol").on("click", function() {
  alert("Klik pakai .on()");
});
```

Kita juga dapat menambahkan beberapa event sekaligus dengan menggunakan `.on()`

```
$("p").on({
  mouseenter: function(){
    $(this).css("background-color", "lightgray");
  },
  mouseleave: function(){
    $(this).css("background-color", "lightblue");
  },
  click: function(){
    $(this).css("background-color", "yellow");
  }
});
```


## Efek dan Animasi Pada JQuery
### Efek Dasar
#### `.hide()` dan `.show()`
Digunakan untuk menyembunyikan dan menampilkan elemen. Contoh:

```
$("#box").hide();
$("#box").show();
```

#### `.toggle()`
Digunakan untuk menampilkan elemen jika disembunyikan, dan sebaliknya. Contoh:

```
$("#box").toggle();
```

#### Menambahkan Durasi
Kita juga dapat mengatur durasi efek dalam milidetik atau dapat dengan menggunakan durasi bawaan. Contoh:

```
$("#box").hide(1000);      // 1 detik
$("#box").show("slow");
$("#box").toggle("fast");
```

### Efek Fade
#### `.fadeIn()` dan `.fadeOut()`

```
$("#box").fadeOut(1000);
$("#box").fadeIn(1000);
```

#### `.fadeToggle()`

```
$("#box").fadeToggle("slow");
```

#### `.fadeTo()`
Kita juga dapat melakukan custom terhadap durasi dan transparasi efek fade. Contoh:

```
$("#box").fadeTo(1000, 0.5); // jadi setengah transparan
```

### Efek Slide
#### `.slideUp()` dan `.slideDown()`

```
$("#box").slideUp(500);
$("#box").slideDown("fast");
```

#### `.slideToggle()`

```
$("#box").slideToggle();
```

### Efek Kustom
Kita bisa membuat animasi kita sendiri dengan menggunakan properti CSS numerik (seperti width, height, opacity, dll). Contoh:

```
$("#box").animate({
  width: "300px",
  height: "200px",
  opacity: 0.5
}, 1000);
```

### Efek Berantai
Kita bisa menggabungkan beberapa efek sekaligus dalam satu baris. Contoh:

```
$("#box").slideUp(500).slideDown(500).fadeOut(500);
```

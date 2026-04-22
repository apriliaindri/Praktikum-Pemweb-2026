# Apa itu AJAX?
AJAX (**Asynchronous JavaScript and XML**) adalah teknik yang digunakan untuk mengirim dan menerima data dari server tanpa perlu me-refresh halaman web. 
AJAX dapat digunakan untuk melakukan *fetch* data di background dan meng-update bagian tertentu dari halaman secara dinamis tanpa me-reload seluruh halaman.

## Kenapa Menggunakan AJAX?
- Untuk memperbarui bagian halaman web tanpa me-refresh seluruh halaman.  
- Untuk mengambil data dari server dan menampilkannya secara dinamis.  
- Untuk mengirim data ke server tanpa me-reload halaman.

## Konsep Dasar AJAX
- **Asynchronous**: Browser tidak perlu menunggu request selesai diproses, sehingga halaman tetap interaktif.  
- **HTTP Request**: AJAX bekerja dengan mengirimkan HTTP request seperti GET atau POST ke server.  
- **JavaScript & JSON**: Data yang dikirim atau diterima dari server umumnya menggunakan format JSON.

## Bagaimana AJAX Bekerja?
Biasanya alur kerja AJAX adalah sebagai berikut:

- User melakukan aksi (misalnya klik tombol).  
- Request AJAX dikirim ke server.  
- Server memproses request dan mengirimkan data sebagai response.  
- Response diterima oleh JavaScript untuk kemudian ditampilkan atau digunakan untuk meng-update halaman.

# Teknik Modern AJAX
`fetch()` adalah API JavaScript modern yang digunakan untuk membuat request AJAX. `fetch()` lebih sederhana karena menggunakan *Promise*, sehingga memudahkan dalam menangani proses asynchronous.

### Contoh dasar penggunaan `fetch()`

```javascript
fetch("https://jsonplaceholder.typicode.com/posts") // Mengambil data dari API
  .then((response) => response.json()) // Mengubah response menjadi format JSON
  .then((data) => console.log(data)) // Mengolah data yang diterima melalui console
  .catch((error) => console.error("Error:", error)); // Menangani error
```

```html
<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <title>Contoh Fetch API</title>
</head>
<body>

<h2>Contoh Fetch API</h2>

<script>
fetch("https://jsonplaceholder.typicode.com/users") // Mengambil data dari API
  .then((response) => response.json()) // Mengubah response menjadi format JSON
  .then((data) => console.log(data)) // Mengolah data yang diterima melalui console
  .catch((error) => console.error("Error:", error)); // Menangani error
</script>

</body>
</html>
```

### Penjelasan

- `fetch()` : Mengirim request ke server (API) untuk mengambil data secara asynchronous.
- `response` : Hasil awal dari request, masih berupa data mentah (belum bisa langsung digunakan).
- `response.json()` : Mengonversi response menjadi format JSON agar bisa dibaca oleh JavaScript.
- `response.text()` : Digunakan untuk membaca response dalam bentuk teks biasa.
- `.then()` : Menjalankan proses lanjutan setelah Promise berhasil.
- `data` : Data hasil konversi dari response yang siap digunakan (biasanya object/array).
- `console.log()` : Menampilkan data ke console browser.
- `.catch()` : Menangani error jika request gagal.


# Fetch Local File (XML atau Teks)
Untuk mengambil (*fetch*) file lokal seperti file teks atau XML, kode harus dijalankan melalui server lokal (misalnya menggunakan Node.js, Python, atau Live Server di VS Code). Hal ini karena browser tidak mengizinkan akses langsung ke file lokal demi alasan keamanan.

### Contoh Fetch File Lokal

```javascript
fetch("example.txt") // Path ke file teks lokal
  .then((response) => response.text()) // Membaca response sebagai teks
  .then((text) => console.log(text)) // Menampilkan isi file
  .catch((error) => console.error("Error:", error)); // Error handling
```
### Mengirim Permintaan POST dengan `fetch()`

Anda dapat menggunakan `fetch()` untuk mengirim permintaan **POST** ke server, misalnya untuk mengirim data seperti JSON atau data form.

### Contoh Mengirim Data JSON dengan `fetch()`

```javascript
const data = {
  username: "April",
  email: "april@gmail.com",
};

fetch("https://example.com/submit", {
  method: "POST", // Mengirim data ke server
  headers: {
    "Content-Type": "application/json", // Memberitahu server bahwa data dalam format JSON
  },
  body: JSON.stringify(data), // Mengubah objek JavaScript menjadi JSON
})
  .then((response) => response.json())
  .then((data) => console.log("Success:", data))
  .catch((error) => console.error("Error:", error));
```

# AJAX dan jQuery
## Menggunakan GET
Dengan menggunakan jQuery, proses melakukan request AJAX GET menjadi lebih mudah dan ringkas.

### Contoh AJAX GET dengan jQuery

```html
<button id="getData">Ambil Data</button>

<script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
<script>
  $('#getData').on('click', function() {
    $.ajax({
      url: 'https://jsonplaceholder.typicode.com/posts',
      method: 'GET',
      success: function(data) {
        console.log('Data berhasil diambil:', data);
      },
      error: function(error) {
        console.error('Terjadi kesalahan:', error);
      }
    });
  });
</script>
```
### Penjelasan

- `$.ajax()` : Digunakan untuk mengirim request AJAX (pada contoh ini menggunakan metode GET).  
- `url` : Alamat endpoint API yang akan diakses.  
- `method: 'GET'` : Menentukan metode HTTP yang digunakan.  
- `success` : Callback yang dijalankan ketika request berhasil dan data diterima.  
- `error` : Callback yang dijalankan ketika terjadi kesalahan pada request.

## Menggunakan POST

```html
<button id="sendData">Send Data</button>

<script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
<script>
  $('#sendData').on('click', function() {
    var jsonData = {
      username: 'addin',
      email: 'addin@sidoarjo.com'
    };

    $.ajax({
      url: 'https://example.com/submit',    // URL server
      type: 'POST',                         // Metode POST
      contentType: 'application/json',      // Mengirim data dalam format JSON
      data: JSON.stringify(jsonData),       // Mengubah objek JavaScript menjadi JSON
      success: function(response) {
        console.log('Success:', response);  // Menangani response berhasil
      },
      error: function(error) {
        console.error('Error:', error);     // Menangani error
      }
    });
  });
</script>
```
### Penjelasan

- `contentType: 'application/json'` : Memberitahu server bahwa data yang dikirim dalam format JSON.  
- `JSON.stringify(jsonData)` : Mengubah objek JavaScript menjadi string JSON sebelum dikirim ke server.

## Menggunakan Form
jQuery mempermudah penggunaan AJAX, terutama dalam menangani kompatibilitas antar-browser. Berikut adalah cara mengirim permintaan POST dan data form menggunakan jQuery.

### Mengirim Data Form Menggunakan POST (Tanpa JSON)

```html
<form id="FormSederhana">
  <input type="text" id="username" name="username" placeholder="Username">
  <input type="email" id="email" name="email" placeholder="Email">
  <button type="submit">Submit</button>
</form>

<script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
<script>
  $('#FormSederhana').on('submit', function(event) {
    event.preventDefault(); // Mencegah form melakukan refresh halaman

    var formData = $(this).serialize(); // Mengubah data form menjadi format key=value

    $.ajax({
      url: 'https://example.com/submit', // URL server
      type: 'POST',                     // Metode POST
      data: formData,                   // Data form yang dikirim
      success: function(response) {
        console.log('Success:', response); // Response jika berhasil
      },
      error: function(error) {
        console.error('Error:', error); // Response jika terjadi kesalahan
      }
    });
  });
</script>
```
### Penjelasan

- `$(this).serialize()` : Mengubah data form menjadi format string `key=value` (contoh: `username=addin&email=addin@sidoarjo.com`).  
- `$.ajax()` : Digunakan untuk mengirim request AJAX, dalam contoh ini menggunakan metode POST dengan data dari form.

# Contoh Program Sederhana
Cobalah menjalankan HTML berikut untuk mencoba penggunaan AJAX dan jQuery dalam mengambil data dari API dan menampilkannya secara dinamis.

```html
<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8" />
  <title>AJAX Demo</title>
  <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>

  <style>
    .card {
      border: 1px solid #ccc;
      border-radius: 8px;
      padding: 16px;
      margin: 10px 0;
      background-color: #f9f9f9;
      box-shadow: 2px 2px 5px rgba(0, 0, 0, 0.1);
      max-width: 200px;
      height: 100%;
      overflow: scroll;
    }

    button {
      width: 100%;
      height: 100px;
      font-size: larger;
      font-weight: 400;
    }

    #postsContainer {
      display: flex;
      justify-content: center;
      align-items: center;
      gap: 10px;
      height: 350px;
      margin-top: 50px;
    }
  </style>
</head>

<body>
  <button id="loadPosts">Ambil Data</button>
  <div id="postsContainer"></div>

  <script>
    function shuffleArray(array) {
      return array.sort(() => Math.random() - 0.5);
    }

    $("#loadPosts").on("click", function () {
      $.ajax({
        url: "https://jsonplaceholder.typicode.com/posts",
        method: "GET",
        dataType: "json",
        success: function (data) {
          $("#postsContainer").empty();

          const shuffled = shuffleArray(data);
          const randomFive = shuffled.slice(0, 5);

          randomFive.forEach(function (post) {
            const card = `
              <div class="card">
                <h3>${post.title}</h3>
                <p>${post.body}</p>
              </div>
            `;
            $("#postsContainer").append(card);
          });
        },
        error: function () {
          $("#postsContainer").html("<p>Gagal mengambil data.</p>");
        },
      });
    });
  </script>
</body>
</html>
```

### Penjelasan Singkat

- Tombol **Ambil Data** digunakan untuk memicu request AJAX.  
- `$.ajax()` digunakan untuk mengambil data dari API `jsonplaceholder.typicode.com/posts`.  
- Data yang diterima kemudian diacak menggunakan fungsi `shuffleArray()`.  
- Hanya 5 data pertama yang diambil dan ditampilkan.  
- Data ditampilkan dalam bentuk card secara dinamis menggunakan jQuery.

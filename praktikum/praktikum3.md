# Dasar Teori 

## Express
Express.js adalah framework web app untuk Node.js yang ditulis dengan bahasa
pemrograman JavaScript. Framework open source ini dibuat oleh TJ Holowaychuk
pada tahun 2010 lalu. <br>

Integrasi MongoDB dan Express 2
Express.js adalah framework back end. Artinya, ia bertanggung jawab untuk mengatur
fungsionalitas website, seperti pengelolaan routing dan session, permintaan HTTP,
penanganan error, serta pertukaran data di server.<br>

## Mongoose
Mongoose adalah pustaka berbasis Node.js yang digunakan untuk pemodelan data
pada MongoDB. Mongoose menyediakan feature diantaranya, model data application
berbasis Schema. Dan juga termasuk built-in type casting, validation, query building,
business logic hooks dan masih banyak lagi yang menjadi ke andalan mongoose.

## Async Await
Async sendiri merupakan sebuah fungsi yang mengembalikan sebuah Promise. Await
sendiri merupakan fungsi yang hanya berjalan di dalam Async. Await bertujuan untuk
menunda jalannya Async hingga proses dari Await tersebut berhasil dieksekusi.

## Model
Model merupakan bagian yang bertugas untuk menyiapkan, mengatur, memanipulasi,
dan mengorganisasikan data yang ada di database.

## Controller
Controller merupakan bagian yang menjadi tempat berkumpulnya logika pemrograman
yang digunakan untuk memisahkan organisasi data pada database. Dalam beberapa
kasus, controller menjadi penghubung antara model dan view pada arsitektur MVC

## Route
Router mengatur pintu masuk yang berupa request pada aplikasi, mereka memilah dan
mengolah request url untuk kemudian diproses sesuai dengan tujuan akhir url tersebut.
Bisa jadi url tersebut berfungsi untuk mengambil data kemudian menampilkannya,
menghapus data, menampilkan form, sampai mengolah session.

# Kebutuhan Instalasi
1. NodeJS
2. API Client (seperti postman, Insomnia, RapidAPI, dll)

# Langkah Percobaan
## Percobaan instalasi NodeJS
1. Buka halaman
```https://nodejs.org/en```<br><br>
![Hasil Screenshot](../prak3/img1.jpg) <br>
2. Download dan jalankan node setup <br><br>
![Hasil Screenshot](../prak3/img2.jpg) <br>
3. Setelah instalasi selesai jalankan command ```node -v``` untuk memeriksa apakah NodeJS sudah terinstall <br><br>
![Hasil Screenshot](../prak3/img3.jpg) <br>

## Inisiasi project Express dan pemasangan package
1. Lakukan pembuatan folder dengan nama express-mongodb dan masuk ke dalam
folder tersebut lalu buka melalui text editor masing-masing. <br>
2. Lakukan npm init untuk mengenerate file package.json dengan menggunakan
command ```npm init -y``` <br>
![Hasil Screenshot](../prak3/img4.jpg) <br>
3. Lakukan instalasi express, mongoose, dan dotenv dengan menggunakan command
```npm i express mongoose dotenv``` <br><br>
![Hasil Screenshot](../prak3/img5.jpg) <br>

## Koneksi Express ke MongoDB
1. Buatlah file index.js pada root folder dan masukkan kode di bawah ini: <br>
   ```javascript
   require('dotenv').config();
   const express = require('express');
   const mongoose = require('mongoose');
   const app = express();
   app.use(express.json());
   app.get('/', (req, res) => {
   res.status(200).json({
   message: '<nama>,<nim>'
   })
   })
   const PORT = 8000;
   app.listen(PORT, () => {
   console.log(`Running on port ${PORT}`);
   })
   ```
    <br><br>
   ![Hasil Screenshot](../prak3/img6.jpg) <br>
   Setelah itu coba jalankan aplikasi dengan command ```node index.js```<br><br>
   ![Hasil Screenshot](../prak3/img7.jpg) <br>
2. Lakukan pembuatan file **.env** dan masukkan baris berikut: <br>
   ```javascript
   PORT = 5000
   ```
   <br><br>
   ![Hasil Screenshot](../prak3/img8.jpg) <br><br>
   Setelah itu ubahlah kode pada listening port menjadi berikut dan coba jalankan aplikasi kembali <br>
   ```
   ...
   const PORT = process.env.PORT || 8000;
   app.listen(PORT, () => {
   console.log(`Running on port ${PORT}`);
   })
   ```
   <br><br>
   ![Hasil Screenshot](../prak3/img9.jpg) <br><br>
4. Copy connection string yang terdapat pada compas atau atlas dan paste kan pada **.env** seperti berikut : <br>
   ```javascript
   MONGO_URI=<Connection string masing-masing>
   ```
   <br><br>
   ![Hasil Screenshot](../prak3/img10.jpg) <br>
   ![Hasil Screenshot](../prak3/img11.jpg) <br><br>
6. Tambahkan baris kode berikut pada file index.js <br>
   ```javascript
   require('dotenv').config();
   const express = require('express');
   const mongoose = require('mongoose');
   mongoose.connect(process.env.MONGO_URI);
   const db = mongoose.connection;
   db.on('error', (error) => {
   console.log(error);
   });
   db.once('connected', () => {
   console.log('Mongo connected');
   })
   ...
   ```
   <br><br>
   ![Hasil Screenshot](../prak3/img12.jpg) <br>
   Setelah itu coba jalankan aplikasi kembali <br><br>

## Pembuatan routing 
1. Lakukan pembuatan direktori routes di tingkat yang sama dengan index.js. <br><br>
2. Buatlah file book.route.js di dalamnya<br><br>
![Hasil Screenshot](../prak3/img13.jpg) <br>
3. Tambahkan baris kode berikut untuk fungsi getAllBooks <br><br>
```javascript
const router = require('express').Router();
router.get('/', function getAllBooks(req, res) {
res.status(200).json({
message: 'mendapatkan semua buku'
})
})
module.exports = router;
``` 
<br><br>

![Hasil Screenshot](../prak3/img14.jpg) <br><br>
4. Lakukan hal yang sama untuk getOneBook, createBook, updateBook, dan deleteBook <br>
```javascript
const router = require('express').Router();
...
router.get('/:id', function getOneBook(req, res) {
const id = req.params.id;
res.status(200).json({
message: 'mendapatkan satu buku',
id,
})
})
router.post('/', function createBook(req, res) {

res.status(200).json({
message: 'membuat buku baru'
})
})
router.put('/:id', function updateBook(req, res) {
const id = req.params.id;
res.status(200).json({
message: 'memperbaharui satu buku',
id,
})
})
router.delete('/:id', function deleteBook(req, res) {
const id = req.params.id;
res.status(200).json({
message: 'menghapus satu buku',
id,
})
})
module.exports = router;
```
<br><br>

![Hasil Screenshot](../prak3/img15.jpg) <br><br>
5. Lakukan import book.route.js pada file index.js dan tambahkan baris kode berikut : <br>
```javascript
require('dotenv').config();
const express = require('express');
const mongoose = require('mongoose');
const bookRoutes = require('./routes/book.route'); //
...
app.get('/', (req, res) => {
res.status(200).json({
message: '<nama>,<nim>'
})
})
app.use('/books', bookRoutes); //
const PORT = process.env.PORT || 8000;
app.listen(PORT, () => {
console.log(`Running on port ${PORT}`);
})
```
<br><br>

![Hasil Screenshot](../prak3/img16.jpg) <br>
![Hasil Screenshot](../prak3/img17.jpg)<br>
6. Uji salah satu endpoint dengan Postman<br><br>
![Hasil Screenshot](../prak3/img18.jpg) <br><br>

## Pembuatan controller
1. Lakukan pembuatan direktori controllers di tingkat yang sama dengan index.js. <br>
2. Buatlah file book.controller.js di dalamnya <br><br>
![Hasil Screenshot](../prak3/img19.jpg) <br>
3. Salin baris kode dari routes untuk fungsi getAllBooks <br> 
```javascript
function getAllBooks(req, res) {
res.status(200).json({
message: 'mendapatkan semua buku'
})
};
module.exports = {
getAllBooks,
}
```
<br>

4. Lakukan hal yang sama untuk getOneBook, createBook, updateBook, dan deleteBook <br>
```javascript
...
function getOneBook(req, res) {
const id = req.params.id;
res.status(200).json({
message: 'mendapatkan satu buku',
id,
})
}
function createBook(req, res) {
res.status(200).json({
message: 'membuat buku baru'
})
}
function updateBook(req, res) {
const id = req.params.id;
res.status(200).json({
message: 'memperbaharui satu buku',
id,
})
}
function deleteBook(req, res) {
const id = req.params.id;
res.status(200).json({
message: 'menghapus satu buku',
id,
})
}
module.exports = {
getAllBooks,
getOneBook, //
createBook, //
updateBook, //
deleteBook //
}
```
<br><br>

![Hasil Screenshot](../prak3/img20.jpg) <br><br>
5. Lakukan import book.controller.js pada file book.route.js <br>
```javascript
const router = require('express').Router();
const book = require('../controllers/book.controller'); //
...
module.exports = router;
```
<br>

6. Lakukan perubahan pada fungsi agar dapat memanggil fungsi dari book.controller.js <br>
```javascript
const router = require('express').Router();
const book = require('../controllers/book.controller');
router.get('/', book.getAllBooks);
router.get('/:id', book.getOneBook);
router.post('/', book.createBook);
router.put('/:id', book.updateBook);
router.delete('/:id', book.deleteBook);
module.exports = router;
```
<br><br>

![Hasil Screenshot](../prak3/img21.jpg) <br><br>
7. Lakukan pengujian kembali, pastikan response tetap sama <br>
![Hasil Screenshot](../prak3/img22.jpg) <br><br>

## Pembuatan model
Berikut gambaran bentuk data dari modul sebelumnya <br>

<table>
 	<tr>
 		<td> title </td>
 		<td> string </td>
 	</tr>
 	<tr>
 		<td> author </td>
 		<td> string </td>
 	</tr>
  <tr>
 		<td> year </td>
 		<td> number </td>
 	</tr>
  <tr>
 		<td> pages </td>
 		<td> number </td>
 	</tr>
  <tr>
 		<td> summary </td>
 		<td> string </td>
 	</tr>
  <tr>
 		<td> publisher </td>
 		<td> string </td>
 	</tr>
 </table>

 1. Lakukan pembuatan direktori models di tingkat yang sama dengan index.js <br>
 2. Buatlah file book.model.js di dalamnya <br><br>
![Hasil Screenshot](../prak3/img23.jpg) <br><br>
 3. Tambahkan baris kode berikut sesuai dengan tabel di atas <br>
```javascript
const mongoose = require('mongoose');
const bookSchema = new mongoose.Schema({
title: {
type: String
},
author: {
type: String
},
year: {
type: Number
},
pages: {
type: Number
},
summary: {
type: String
},
publisher: {
type: String
}
})
module.exports = mongoose.model('book', bookSchema);
```
<br><br>

![Hasil Screenshot](../prak3/img24.jpg) <br><br>

## Operasi CRUD 
1. Hapus semua data pada collection books <br><br>
![Hasil Screenshot](../prak3/img25.jpg) <br><br>
2. Lakukan import book.model.js pada file book.controller.js <br><br>
```javascript
const Book = require('../models/book.model');
...
```
<br><br>
![Hasil Screenshot](../prak3/img26.jpg) <br><br>
3. Lakukan perubahan pada fungsi createBook <br><br>
```javascript
const Book = require('../models/book.model');
...
async function createBook(req, res) {
const book = new Book({
title: req.body.title,
author: req.body.author,
year: req.body.year,
pages: req.body.pages,
summary: req.body.summary,
publisher: req.body.publisher,
})
try {
const savedBook = await book.save();
res.status(200).json({
message: 'membuat buku baru',
book: savedBook,

})
} catch (error) {
res.status(500).json({
message: 'kesalahan pada server',
error: error.message,
})
}
}
...
```
<br>

![Hasil Screenshot](../prak3/img27.jpg) <br><br>
4. Buatlah dua buah buku dengan data di bawah ini dengan Postman <br><br>
```javascript
{
"title": "Dilan 1990",
"author": "Pidi Baiq",
"year": 2014,
"pages": 332,
"summary": "Mirea, anata wa utsukushī",
"publisher": "Pastel Books"
}
```
<br><br>
```javascript
{
"title": "Dilan 1991",
"author": "Pidi Baiq",
"year": 2015,
"pages": 344,
"summary": "Watashi ga kare o aishite iru to ittara",
"publisher": "Pastel Books"
}
```
<br><br>
![Hasil Screenshot](../prak3/img28.jpg) <br><br>
![Hasil Screenshot](../prak3/img29.jpg) <br><br>
6. Lakukan perubahan pada fungsi getAllBooks <br>
```javascript
   const Book = require('../models/book.model');
async function getAllBooks(req, res) {
try {
const books = await Book.find();
res.status(200).json({
message: 'mendapatkan semua buku',
books,
})
} catch (error) {
res.status(500).json({
message: 'kesalahan pada server',
error: error.message,

})
}
}
...
```
<br><br>
![Hasil Screenshot](../prak3/img30.jpg) <br><br>
6. Lakukan perubahan pada fungsi getOneBook <br>
```javascript
const Book = require('../models/book.model');
...
async function getOneBook(req, res) {
const id = req.params.id;
try {
const book = await Book.findById(id);
res.status(200).json({
message: 'mendapatkan satu buku',
book,
})
} catch (error) {
res.status(500).json({
message: 'kesalahan pada server',
error: error.message,
})
}
}
...
```
<br><br>
![Hasil Screenshot](../prak3/img31.jpg) <br><br>
7. Tampilkan semua buku dengan Postman <br><br>
![Hasil Screenshot](../prak3/img32.jpg) <br><br>
8. Tampilkan buku Dilan 1990 dengan Postman <br><br>
![Hasil Screenshot](../prak3/img33.jpg) <br><br>
9. Lakukan perubahan pada fungsi updateBook <br>
```javascript
const Book = require('../models/book.model');
...
async function updateBook(req, res) {
const id = req.params.id;
try {
const book = await Book.findByIdAndUpdate(
id, req.body, { new: true }
)
res.status(200).json({
message: 'memperbaharui satu buku',
book,
})
} catch (error) {
res.status(500).json({
message: 'kesalahan pada server',
error: error.message,
})
}
}
...
```
<br><br>
![Hasil Screenshot](../prak3/img34.jpg) <br><br>
10. Ubah judul buku Dilan 1991 menjadi “NAMA PANGGILAN 1991” dengan Postman <br><br>
![Hasil Screenshot](../prak3/img35.jpg) <br><br>
11. Lakukan perubahan pada fungsi deleteBook <br>
```javascript
const Book = require('../models/book.model');
...
async function deleteBook(req, res) {
const id = req.params.id;
try {
const book = await Book.findByIdAndDelete(id);
res.status(200).json({
message: 'menghapus satu buku',
book,
})
} catch (error) {
res.status(500).json({
message: 'kesalahan pada server',
error: error.message,
})
}
}
...
```
![Hasil Screenshot](../prak3/img36.jpg) <br><br>
13. Hapus buku Dilan 1990 dengan Postman.<br><br>
![Hasil Screenshot](../prak3/img37.jpg) <br><br>

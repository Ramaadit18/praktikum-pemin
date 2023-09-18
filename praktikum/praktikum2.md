# Proses CRUD Pada MongoDB Compass dan MongoDB Shell

* ## MongoDB Compass
  MongoDB Compass merupakan alat bantu berbasis GUI yang digunakan untuk melakukan operasi CRUD tanpa harus menggunakan command line. Dengan menggunakan MongoDB Compass, kita dapat melakukan analisis dan kueri data dalam lingkungan visual. Di bawah ini merupakan langkah-langkah untuk melakukan operasi CRUD pada MongoDB Compass: <br>
  a. Melakukan koneksi ke MongoDB <br>
     ![Hasil Screenshot connection](../prak2/img0.jpg) <br>
  b. Buat database baru dengan menekan tanda plus "+", maka MongoDB Compass akan menampilkan input form seperti di bawah <br>
     ![Hasil Screenshot new database](../prak2/2.jpg) <br>
  c. Isi informasi yang ada dan klik "Create Database". Database baru akan dibuat oleh MongoDB Compass <br>
     ![Hasil Screenshot new database](../prak2/3.jpg) <br>
  c. Pada percobaan ini, proses CREATE dilakukan dengan insert buku pertama dengan melakukan klik "Add Data", pilih "Insert Document", <br>
     ![Hasil Screenshot create](../prak2/4.jpg) <br>
  isi dengan data yang diinginkan dan klik "Next" <br>
     ![Hasil Screenshot create](../prak2/5.jpg) <br>
  d. Lakukan insert buku kedua dengan cara yang sama <br>
     ![Hasil Screenshot create](../prak2/6.jpg) <br>
  e. Proses READ dilakukan dengan cara mencari buku dengan author "Osamu Dazai" dengan mengisi filter yang diinginkan dan klik "Find" <br>
     ![Hasil Screenshot read](../prak2/7.jpg) <br>
     ![Hasil Screenshot read](../prak2/8.jpg) <br>
  f. Sedangkan untuk proses UPDATE, dilakukan perubahan summary pada buku "No Longer Human" menjadi "Buku yang bagus (NAMA,NIM) dengan melakukan klik "Edit Document" (berlambang pensil), mengisi nilai summary yang baru, dan melakukan klik "Update" <br>
     ![Hasil Screenshot update](../prak2/9.jpg) <br>
     ![Hasil Screenshot update](../prak2/10.jpg) <br>
  g. Proses DELETE, dilakukan dengan cara penghapusan pada buku "I Am a Cat" dengan melakukan klik "Remove Document" (berlambang tong sampah) dan melakukan klik "Delete" <br>
     ![Hasil Screenshot delete](../prak2/11.jpg) <br>
     
* ## MongoDB Shell
  MongoDB Shell merupakan tool untuk melakukan aktivitas CRUD yang berbasis Command Line Interface (CLI). MongoDB Shell dapat diakses langsung dari MongoDB Compass atau menggunakan perintah mongosh pada Command Prompt. Berikut adalah langkah-langkah untuk melakukan CRUD pada MongoDB Shell: <br>
  a. Lakukan koneksi ke MongoDB dengan menjalankan command ```mongosh``` pada terminal yang ada di OS <br>
     ![Hasil Screenshot mongosh](../prak2/12.jpg) <br>
  b. Lihat list database yang ada di server dengan menjalankan command ```show dbs``` <br>
     ![Hasil Screenshot show dbs](../prak2/13.jpg) <br>
    Untuk berpindah ke database "bookstore" gunakan command ```use bookstore``` dan memastikan database telah berpindah dengan melihat tulisan sebelum tanda ">" <br>
     ![Hasil Screenshot use bookstore](../prak2/14.jpg) <br>
  Untuk melihat collection yang ada pada database tersebut gunakan command ```show collection``` <br>
     ![Hasil Screenshot show collection](../prak2/15.jpg) <br>
  c. Proses CREATE pada MongoDB Shell dapat dilakukan secara satu per satu atau langsung membuat banyak. Untuk membuat objek baru, dilakukan insert buku "Overlord I" dengan menggunakan command ```db.books.insertOne(data)``` <br>
     ![Hasil Screenshot create](../prak2/16.jpg) <br>
  d. Sementara untuk membuat objek baru lebih dari satu, dilakukan insert buku "The Setting Sun" dan "Hujan" dengan insert many dengan menggunakan command ```db.books.insertMany(data)``` <br>
     ![Hasil Screenshot create](../prak2/17.jpg) <br>
  e. Aktivitas READ, dilakukan dengan pencarian buku dengan menggunakan command ```db.books.find()``` untuk melakukan pencarian semua buku <br>
     ![Hasil Screenshot read](../prak2/18.jpg) <br>
  f. Tampilkan seluruh buku dengan author "Osamu Dazai" dengan mengisi argument pada find() dengan menggunakan command ```db.books.find({filter})``` <br>
     ![Hasil Screenshot read](../prak2/19.jpg) <br>
  g. Proses UPDATE dapat dilakukan dengan melakukan perubahan summary pada buku "Hujan" menjadi "Buku yang bagus (NAMA, NIM) dengan menggunakan command ```db.books.updateOne({filter}, {$set: {data yang ingin diupdate}})``` <br>
     ![Hasil Screenshot update](../prak2/20.jpg) <br>
  h. Lakukan perubahan publisher menjadi "Yen Press" pada semua buku "Osamu Dazai" dengan menggunakan command ```db.books.updateMany({filter}, {$set: {data yang ingin diupdate}})``` <br>
     ![Hasil Screenshot update](../prak2/21.jpg) <br>
  i. Proses DELETE, dilakukan dengan penghapusan pada buku "Overlord I" dengan menggunakan command ```db.books.deleteOne({argument})``` <br>
     ![Hasil Screenshot delete](../prak2/22.jpg) <br>
  j. Lakukan penghapusan pada semua buku "Osamu Dazai" dengan menggunakan command ```db.books.deleteMany({argument})``` <br>
     ![Hasil Screenshot delete](../prak2/23.jpg) <br>
Untuk melihat hasil dari proses CRUD di atas, dapat dilakukan pencarian seluruh buku menggunakan command ```db.books.find()```
     ![Hasil Screenshot delete](../prak2/24.jpg) <br>


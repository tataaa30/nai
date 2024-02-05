#Buat web dinamis dengan node.js,msql.i dan biodata siswa.md

Persiapkan Proyek Node.js:
Buat direktori proyek dan inisialisasikan proyek Node.js dengan perintah berikut di terminal:

bash
Copy code
mkdir biodata-siswa
cd biodata-siswa
npm init -y
Install Modul yang Diperlukan:
Install modul express sebagai framework web dan mysql2 sebagai driver MySQL dengan perintah:

bash
Copy code
npm install express mysql2
Buat Berkas Utama (app.js):
Buat berkas app.js sebagai berkas utama aplikasi Anda:

javascript
Copy code
const express = require('express');
const mysql = require('mysql2');

const app = express();
const port = 3000;

// Koneksi ke MySQL
const connection = mysql.createConnection({
  host: 'localhost',
  user: 'username', // Ganti dengan username MySQL Anda
  password: 'password', // Ganti dengan password MySQL Anda
  database: 'sekolah'
});

connection.connect((err) => {
  if (err) {
    console.error('Error connecting to MySQL:', err);
    return;
  }
  console.log('Connected to MySQL');
});

// Definisikan rute
app.get('/', (req, res) => {
  // Ambil data siswa dari MySQL
  connection.query('SELECT * FROM siswa', (error, results) => {
    if (error) throw error;
    res.json(results);
  });
});

// Jalankan server
app.listen(port, () => {
  console.log(`Server berjalan di http://localhost:${port}`);
});
Buat Tabel MySQL:
Pastikan tabel siswa sudah dibuat di MySQL sesuai dengan langkah-langkah sebelumnya.

Jalankan Aplikasi:
Jalankan aplikasi Node.js dengan perintah:

bash
Copy code
node app.js
Akses http://localhost:3000 di browser untuk melihat data siswa yang diambil dari MySQL.

Ekspansi Aplikasi:
Sesuaikan dan ekspansikan aplikasi sesuai kebutuhan Anda. Anda dapat menambahkan rute untuk menampilkan formulir tambah siswa, mengedit, dan lainnya. Gunakan templating engine seperti EJS atau Pug untuk merender halaman HTML.

Pastikan untuk mengganti nilai username dan password pada koneksi MySQL dengan nilai yang sesuai dengan konfigurasi MySQL Anda. Selain itu, pastikan MySQL server berjalan dan dapat diakses dari aplikasi Node.js.

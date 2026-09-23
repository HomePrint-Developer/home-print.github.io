# Home Print

Home Print adalah platform layanan cetak dokumen dan foto berbasis web. Aplikasi ini dirancang untuk memberikan kemudahan bagi pengguna dalam menentukan spesifikasi cetak secara interaktif, menghitung biaya transaksi dan ongkos kirim secara otomatis menggunakan integrasi peta, serta memfasilitasi komunikasi pesanan langsung ke WhatsApp admin.

Platform ini juga dilengkapi dengan halaman dasbor khusus admin untuk manajemen stok barang, varian kertas foto, penyedia alat cerdas pembuat dokumen (CV/Lamaran & Nota Resmi otomatis), serta pengelolaan kritik dan saran dari pelanggan dengan sistem keamanan maksimal untuk skala aplikasi web statis.

---

## Fitur Utama

### Antarmuka Pelanggan

- **Tema Gelap & Terang (Dark/Light Mode)**: Dukungan tema visual yang dinamis dan elegan yang tersimpan pada memori _Local Storage_, dilengkapi dengan _bubble tooltip_ interaktif untuk memandu pengguna baru.
- **Pilihan Jasa Kondisional (Modal UI)**: Pemisahan alur spesifikasi antara layanan _Print & Fotocopy_ dengan layanan _Cetak Foto_ dan _Jasa Lainnya_ (pembuatan CV) secara terstruktur.
- **Integrasi Peta Interaktif**: Menggunakan Leaflet.js dan OpenStreetMap untuk menentukan titik lokasi pengantaran secara akurat oleh pengguna.
- **Kalkulasi Biaya & Ongkir Cerdas**: Menghitung subtotal cetak berdasarkan lembar, ukuran, opsi jilid, produk tambahan, dan ongkos kirim berbasis jarak mengemudi riil (OSRM API) dengan tarif **Rp3.000/KM** serta pengunci **Tarif Minimum Rp5.000** untuk proteksi jarak dekat.
- **Gateway QRIS & WhatsApp**: Menyediakan QRIS untuk pembayaran elektronik instan dan otomatis menyusun format pesan teks manifes pesanan (nota digital) untuk dikirim ke WhatsApp admin.
- **Kolom Kritik & Saran Anonim**: Halaman umpan balik bagi pelanggan untuk mengirimkan masukan secara langsung tanpa memerlukan nomor telepon, menjamin 100% bebas dari risiko kebocoran privasi data.

### Panel & Alat Admin (Admin Tools)

- **Autentikasi Gerbang Login Terpadu**: Proteksi halaman internal dari serangan _Bypass Direct URL Access_ menggunakan satpam _Session Storage_ JavaScript di sisi klien. Login terintegrasi di halaman utama menggunakan antarmuka _Pop-Up Modal_.
- **Manajemen Stok & Kertas Terpusat (SPA Feel)**: Fitur memantau, menambah, mengubah (edit), dan menghapus data stok barang/ATK serta varian kertas foto. Seluruh interaksi form (tambah maupun edit data) kini terpusat menggunakan antarmuka _Modal/Pop-Up_ UI yang elegan, menggantikan _prompt_ bawaan browser, sehingga memberikan pengalaman instan tanpa perlu memuat ulang (reload) halaman.
- **Pusat Alat Admin (PDF Generators)**:
  1. **Dokumen Generator Engine**: Mesin otomatis untuk membuat _Curriculum Vitae_ (CV) dan Surat Lamaran Kerja (Margin Narrow A4) yang langsung dapat di-ekspor ke PDF menggunakan pustaka `html2pdf.js`.
  2. **Generator Nota Resmi**: Alat untuk mencetak lembaran nota kosong ber-seri (cth: `HP-000001`) secara massal. Sistem akan melacak seri terakhir di database Firebase, menanamkan teks langsung ke _template_ PDF menggunakan `pdf-lib`, dan merekam riwayatnya kembali ke server.
- **Manajemen Feedback Interaktif & Aman**:
  - Tampilan tabel masukan dengan sistem paginasi ketat (maksimal 10 data per halaman).
  - Fitur hapus data kontekstual yang aman dari pembajakan hak akses luar berkat aturan _Firebase Rules_ terbaru (`!data.exists() || !newData.exists()`).
  - **Interactive Masking Mode**: Tombol toggle ikon mata (_Eye Icon_) untuk menyamarkan nama pelanggan secara instan (contoh: `Zainal Ilmi` diubah menjadi `Z***** I***`) guna menjaga privasi dari pandangan sekilas.

---

## Keamanan & Validasi Database (Firebase Rules)

Database dilindungi dari serangan _Database Deface_ dan _Malicious Code Injection_ menggunakan aturan validasi ketat level server:

1. **Type Checking**: Node harga dan sisa stok dikunci wajib menggunakan `.isNumber()`.
2. **Length Restrict**: Panjang karakter nama dibatasi maksimal 50 karakter dan pesan masukan maksimal 500 karakter untuk mencegah ledakan kuota database (_Buffer Overflow_).
3. **XSS Protection**: Logika penayangan data pada halaman admin bermigrasi penuh menggunakan properti `.textContent` murni, sehingga skrip HTML berbahaya (`<script>`) yang sengaja disisipkan peretas akan dicetak sebagai teks biasa dan gagal dieksekusi oleh browser.

---

## Teknologi yang Digunakan

- **Frontend**: HTML5, Tailwind CSS (Desain Modern, Glassmorphism, Responsive & Dark Mode)
- **Backend & Database**: Firebase Realtime Database (Firebase SDK v12.15.0)
- **Peta & Geokoding**: Leaflet.js, OpenStreetMap, OSRM (Open Source Routing Machine) API
- **Pemrosesan File PDF**:
  - `html2pdf.js` (Rendering halaman web HTML ke file PDF)
  - `pdf-lib` (Manipulasi, penambahan teks dinamis, dan modifikasi template PDF)

---

## Struktur File Proyek

- `index.html` - Halaman beranda pelanggan (Berisi trigger ke pemesanan & _login modal_ admin).
- `pesan.html` - Formulir layanan percetakan (Print, Fotocopy, Cetak Foto & Ongkir Peta).
- `jasa.html` - Formulir layanan jasa lainnya (Pembuatan CV/Lamaran & Pengetikan).
- `feedback.html` - Halaman untuk pelanggan mengirim masukan/saran anonim.
- `index-admin.html` - Hub dasbor utama admin (Manajemen stok barang, kertas, dan akses ke menu alat).
- `feedback-admin.html` - Panel administrasi untuk mengelola masukan/feedback.
- `generate-file.html` - Dasbor alat pembuat file CV & Lamaran (Dokumen Generator).
- `nota-kosong.html` - Dasbor alat pencetak seri nota fisik otomatis secara massal.
- `close.html` / `maintenance.html` - Halaman pengalihan interaktif (Hold Traffic) jika layanan sedang tutup/perbaikan.

_(Catatan: File usang seperti `login.html` dan `add_stok.html` telah dilebur ke dalam bentuk interaksi Pop-Up / Modal)._

---

## Konfigurasi dan Instalasi

1. **Klon Repositori**
   ```bash
   git clone [https://github.com/HomePrint-Developer/home-print.github.io.git](https://github.com/HomePrint-Developer/home-print.github.io.git)

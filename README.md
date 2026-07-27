# Home Print

Home Print adalah platform layanan cetak dokumen dan foto berbasis web. Aplikasi ini dirancang untuk memberikan kemudahan bagi pengguna dalam menentukan spesifikasi cetak secara interaktif, menghitung biaya transaksi dan ongkos kirim secara otomatis menggunakan integrasi peta, serta memfasilitasi komunikasi pesanan langsung ke WhatsApp admin. Platform ini juga dilengkapi dengan halaman khusus admin untuk manajemen stok barang, varian kertas foto, serta pengelolaan kritik dan saran dari pelanggan dengan sistem keamanan maksimal untuk skala aplikasi web statis.

---

## Fitur Utama

### Antarmuka Pelanggan
* **Pilihan Jasa Kondisional**: Form interaktif yang memisahkan alur spesifikasi antara layanan Print & Fotocopy dengan layanan Cetak Foto secara dinamis.
* **Integrasi Peta Interaktif**: Menggunakan Leaflet.js dan OpenStreetMap untuk menentukan titik lokasi pengantaran secara akurat oleh pengguna.
* **Kalkulasi Biaya & Ongkir Cerdas**: Menghitung subtotal cetak berdasarkan lembar, ukuran, opsi jilid, produk tambahan, dan ongkos kirim berbasis jarak mengemudi riil (OSRM API) dengan tarif **Rp3.000/KM** serta pengunci **Tarif Minimum Rp5.000** untuk proteksi jarak dekat.
* **Gateway QRIS & WhatsApp**: Menyediakan QRIS untuk pembayaran elektronik instan dan otomatis menyusun format pesan teks manifes pesanan (nota digital) untuk dikirim ke WhatsApp admin.
* **Kolom Kritik & Saran Anonim**: Halaman umpan balik bagi pelanggan untuk mengirimkan masukan secara langsung tanpa memerlukan data privasi nomor telepon, menjamin 100% bebas dari risiko kebocoran data.

### Panel Admin
* **Autentikasi Gerbang Login**: Proteksi halaman internal dari serangan *Bypass Direct URL Access* menggunakan satpam *Session Storage* JavaScript di sisi klien.
* **Manajemen Stok Real-Time**: Fitur untuk memantau, menambah, mengubah, dan menghapus data stok barang atau alat tulis kantor (ATK) langsung ke database Firebase.
* **Manajemen Varian Kertas**: Fitur untuk mengelola jenis-jenis kertas foto yang tersedia di database secara dinamis agar pilihan dropdown di sisi pelanggan selalu mutakhir.
* **Manajemen Feedback Interaktif & Aman**: 
  * Tampilan tabel masukan dengan sistem paginasi ketat (maksimal 10 data per halaman).
  * Fitur hapus data kontekstual yang aman dari pembajakan hak akses luar berkat aturan *Firebase Rules* terbaru (`!data.exists() || !newData.exists()`).
  * **Interactive Masking Mode**: Tombol toggle ikon mata (Eye Icon) untuk menyamarkan nama pelanggan secara instan (contoh: `Zainal Ilmi` diubah menjadi `Z***** I***`) guna menjaga privasi dari intipan orang luar.

---

## Keamanan & Validasi Database (Firebase Rules)

Database dilindungi dari serangan *Database Deface* dan *Malicious Code Injection* menggunakan aturan validasi ketat level server:
1. **Type Checking**: Node harga dan sisa stok dikunci wajib menggunakan `.isNumber()`.
2. **Length Restrict**: Panjang karakter nama dibatasi maksimal 50 karakter dan pesan masukan maksimal 500 karakter untuk mencegah ledakan kuota database (*Buffer Overflow*).
3. **XSS Protection**: Logika penayangan data pada halaman admin bermigrasi penuh menggunakan properti `.textContent` murni, sehingga skrip HTML berbahaya (`<script>`) yang sengaja disisipkan peretas akan dicetak sebagai teks biasa dan gagal dieksekusi oleh browser.

---

## Teknologi yang Digunakan

* **Frontend**: HTML5, Tailwind CSS (Desain Modern dengan Gaya Glassmorphic Dark Mode pada Halaman Tertentu)
* **Backend & Database**: Firebase Realtime Database (Firebase SDK v12.15.0)
* **Peta & Geokoding**: Leaflet.js, OpenStreetMap, OSRM (Open Source Routing Machine) API

---

## Struktur File Proyek

* `index.html` - Halaman utama beranda untuk pelanggan.
* `pesan.html` - Formulir pemesanan layanan print, fotocopy, dan cetak foto (Sistem Ongkir Rp3.000/KM).
* `feedback.html` - Halaman pengisian kritik dan saran privasi oleh pelanggan.
* `login.html` - Halaman autentikasi masuk untuk administrator.
* `index-admin.html` - Dasbor utama admin untuk manajemen stok dan varian kertas.
* `add_stok.html` - Formulir untuk menambah item stok barang baru oleh admin.
* `feedback-admin.html` - Panel administrasi real-time untuk membaca, menyensor, dan menghapus masukan pelanggan.

---

## Konfigurasi dan Instalasi

1. **Klon Repositori**
   ```bash
   git clone [https://github.com/username/home-print.git](https://github.com/username/home-print.git)
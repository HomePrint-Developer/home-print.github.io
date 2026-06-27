# Home Print

Home Print adalah platform layanan cetak dokumen dan foto berbasis web. Aplikasi ini dirancang untuk memberikan kemudahan bagi pengguna dalam menentukan spesifikasi cetak secara interaktif, menghitung biaya transaksi dan ongkos kirim secara otomatis menggunakan integrasi peta, serta memfasilitasi komunikasi pesanan langsung ke WhatsApp admin. Platform ini juga dilengkapi dengan halaman khusus admin untuk manajemen stok barang, varian kertas foto, serta pengelolaan kritik dan saran dari pelanggan.

---

## Fitur Utama

### Antarmuka Pelanggan
* **Pilihan Jasa Kondisional**: Form interaktif yang memisahkan alur spesifikasi antara layanan Print & Fotocopy dengan layanan Cetak Foto.
* **Integrasi Peta Interaktif**: Menggunakan Leaflet.js dan OpenStreetMap untuk menentukan titik lokasi pengantaran secara akurat.
* **Kalkulasi Biaya Otomatis**: Menghitung subtotal cetak berdasarkan lembar, ukuran, opsi jilid, produk tambahan, dan ongkos kirim berbasis jarak (OSRM API).
* **Gateway QRIS & WhatsApp**: Menyediakan QRIS untuk pembayaran elektronik dan otomatis menyusun format pesan teks manifes pesanan untuk dikirim ke WhatsApp admin.
* **Kolom Kritik & Saran Minimalis**: Halaman umpan balik bagi pelanggan untuk mengirimkan nama dan isi masukan secara langsung tanpa memerlukan data privasi nomor telepon.

### Panel Admin
* **Manajemen Stok Real-Time**: Fitur untuk memantau, menambah, mengubah, dan menghapus data stok barang atau alat tulis kantor (ATK).
* **Manajemen Varian Kertas**: Fitur untuk mengelola jenis-jenis kertas foto yang tersedia di database secara dinamis.
* **Manajemen Feedback Interaktif**: Panel khusus untuk memantau masukan pelanggan dengan sistem paginasi (10 data per halaman) dan fitur hapus data kontekstual.

---

## Teknologi yang Digunakan

* **Frontend**: HTML5, Tailwind CSS (Desain Modern dengan Gaya Glassmorphic Dark Mode pada Halaman Tertentu)
* **Backend & Database**: Firebase Realtime Database (Firebase SDK v12.15.0)
* **Peta & Geokoding**: Leaflet.js, OpenStreetMap, OSRM (Open Source Routing Machine) API

---

## Struktur File Proyek

* `index.html` - Halaman utama beranda untuk pelanggan.
* `pesan.html` - Formulir pemesanan layanan print, fotocopy, dan cetak foto.
* `feedback.html` - Halaman pengisian kritik dan saran oleh pelanggan.
* `login.html` - Halaman autentikasi masuk untuk administrator.
* `index-admin.html` - Dasbor utama admin untuk manajemen stok dan varian kertas.
* `add_stok.html` - Formulir untuk menambah item stok barang baru oleh admin.
* `feedback-admin.html` - Panel administrasi real-time untuk membaca dan menghapus masukan pelanggan.

---

## Konfigurasi dan Instalasi

1. **Klon Repositori**
   ```bash
   git clone [https://github.com/username/home-print.git](https://github.com/username/home-print.git)

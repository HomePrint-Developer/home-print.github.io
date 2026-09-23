# Home Print

Home Print adalah platform layanan cetak dokumen dan foto berbasis web. Aplikasi ini dirancang untuk memberikan kemudahan bagi pengguna dalam menentukan spesifikasi cetak secara interaktif, menghitung biaya transaksi dan ongkos kirim secara otomatis menggunakan integrasi peta, serta memfasilitasi komunikasi pesanan langsung ke WhatsApp admin. 

Platform ini juga dilengkapi dengan halaman khusus admin untuk manajemen stok barang, varian kertas foto, mesin pembuat dokumen otomatis (CV & Lamaran), serta pengelolaan kritik dan saran dari pelanggan dengan sistem keamanan maksimal untuk skala aplikasi web statis.

---

## Fitur Utama

### Antarmuka Pelanggan
* **Tema Gelap & Terang (Dark/Light Mode)**: Dukungan tema visual yang dinamis dan elegan dengan memori *Local Storage*, dilengkapi dengan *bubble tooltip* interaktif untuk memandu pengguna baru.
* **Pilihan Jasa Kondisional**: Form interaktif yang memisahkan alur spesifikasi antara layanan Print & Fotocopy dengan layanan Cetak Foto secara dinamis.
* **Integrasi Peta Interaktif**: Menggunakan Leaflet.js dan OpenStreetMap untuk menentukan titik lokasi pengantaran secara akurat oleh pengguna.
* **Kalkulasi Biaya & Ongkir Cerdas**: Menghitung subtotal cetak berdasarkan lembar, ukuran, opsi jilid, produk tambahan, dan ongkos kirim berbasis jarak mengemudi riil (OSRM API) dengan tarif **Rp3.000/KM** serta pengunci **Tarif Minimum Rp5.000** untuk proteksi jarak dekat.
* **Gateway QRIS & WhatsApp**: Menyediakan QRIS untuk pembayaran elektronik instan dan otomatis menyusun format pesan teks manifes pesanan (nota digital) untuk dikirim ke WhatsApp admin.
* **Kolom Kritik & Saran Anonim**: Halaman umpan balik bagi pelanggan untuk mengirimkan masukan secara langsung tanpa memerlukan data privasi nomor telepon, menjamin 100% bebas dari risiko kebocoran data.

### Panel Admin
* **Autentikasi Gerbang Login (Sistem Modal)**: Proteksi halaman internal dari serangan *Bypass Direct URL Access* menggunakan satpam *Session Storage* JavaScript di sisi klien. Login kini terintegrasi langsung di beranda menggunakan antarmuka *Pop-Up Modal*.
* **Manajemen Stok & Kertas Terpusat (SPA Feel)**: Fitur untuk memantau, menambah, mengubah, dan menghapus data stok barang/ATK serta varian kertas foto. Seluruh interaksi penambahan data menggunakan sistem *Modal/Pop-Up* yang modern tanpa perlu berpindah-pindah halaman.
* **Dokumen Generator Engine**: Mesin terintegrasi pembuat *Curriculum Vitae* (CV) dan Surat Lamaran Kerja secara otomatis. Fitur ini mensimulasikan kertas fisik A4 Margin Narrow dan dapat langsung diekspor menjadi format file PDF menggunakan pustaka `html2pdf.js`.
* **Manajemen Feedback Interaktif & Aman**: 
  * Tampilan tabel masukan dengan sistem paginasi ketat (maksimal 10 data per halaman).
  * Fitur hapus data kontekstual yang aman dari pembajakan hak akses luar berkat aturan *Firebase Rules* terbaru (`!data.exists() || !newData.exists()`).
  * **Interactive Masking Mode**: Tombol toggle ikon mata (*Eye Icon*) untuk menyamarkan nama pelanggan secara instan (contoh: `Zainal Ilmi` diubah menjadi `Z***** I***`) guna menjaga privasi dari intipan orang luar.

---

## Keamanan & Validasi Database (Firebase Rules)

Database dilindungi dari serangan *Database Deface* dan *Malicious Code Injection* menggunakan aturan validasi ketat level server:
1. **Type Checking**: Node harga dan sisa stok dikunci wajib menggunakan `.isNumber()`.
2. **Length Restrict**: Panjang karakter nama dibatasi maksimal 50 karakter dan pesan masukan maksimal 500 karakter untuk mencegah ledakan kuota database (*Buffer Overflow*).
3. **XSS Protection**: Logika penayangan data pada halaman admin bermigrasi penuh menggunakan properti `.textContent` murni, sehingga skrip HTML berbahaya (`<script>`) yang sengaja disisipkan peretas akan dicetak sebagai teks biasa dan gagal dieksekusi oleh browser.

---

## Teknologi yang Digunakan

* **Frontend**: HTML5, Tailwind CSS (Desain Modern, Glassmorphism, & Dukungan Dark Mode)
* **Backend & Database**: Firebase Realtime Database (Firebase SDK v12.15.0)
* **Peta & Geokoding**: Leaflet.js, OpenStreetMap, OSRM (Open Source Routing Machine) API
* **Ekspor Dokumen**: html2pdf.js (Untuk rendering canvas ke file PDF)

---

## Struktur File Proyek

* `index.html` - Halaman beranda utama pelanggan (berisi *trigger* pemesanan & *login modal* admin).
* `pesan.html` - Formulir pemesanan layanan percetakan (Print, Fotocopy, Cetak Foto & Ongkir Peta).
* `jasa.html` - Formulir pemesanan layanan jasa lainnya (seperti pengetikan, pembuatan CV/Lamaran).
* `index-admin.html` - Dasbor utama admin untuk manajemen stok barang dan varian kertas foto.
* `generate-file.html` - Dasbor *Dokumen Generator Engine* (Pembuat CV dan Surat Lamaran ke PDF).
* `feedback.html` - Halaman pelanggan untuk mengirimkan kritik dan saran privasi.
* `feedback-admin.html` - Panel administrasi *real-time* untuk manajemen *feedback*.
* `close.html` / `maintenance.html` - Halaman penahan *traffic* interaktif apabila layanan sedang ditutup sementara atau dalam perbaikan/pemeliharaan.

---

## Konfigurasi dan Instalasi

1. **Klon Repositori**
   ```bash
   git clone [https://github.com/username/home-print.git](https://github.com/username/home-print.git)

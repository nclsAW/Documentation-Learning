# TP-AEX-0003 Cart Management & Recommended Items

## Objective & Scope

***

* **Dependency:** Pengujian modul ini bergantung pada ketersediaan produk di katalog (TP-AEX-0002). Selain itu, untuk pengujian _Cart Persistence_ (retensi keranjang belanja setelah autentikasi), modul ini membutuhkan akun terdaftar yang aktif dari TP-AEX-0001.
* **In-Scope:** Pengujian fungsional penambahan produk ke keranjang belanja melalui halaman katalog (/products) dan halaman detail produk, modifikasi kuantitas produk sebelum ditambahkan, penambahan item langsung dari widget _Recommended Items_ di _home page_, penghapusan item dari keranjang (tombol X), verifikasi ketersediaan serta kalkulasi total harga pada halaman keranjang (/view\_cart), dan validasi persistensi item keranjang saat pengguna melakukan _login_.
* **Out-of-Scope:** Pengujian pengubahan kuantitas produk secara langsung di dalam halaman keranjang belanja (_inline quantity editing_) serta penggunaan kode kupon / diskon promo (karena fitur tersebut tidak tersedia pada situs Automation Exercise).

## Environment & Test Setup

***

* **Target URL:** [Automation Exercise - Checkout](https://automationexercise.com/view_cart)
* **Browser/Platform:** Google Chrome (Latest Version) / Desktop.
* **Test Data Requirement:**
  * Kredensial akun uji terdaftar dari TP-AEX-0001 untuk pengujian retensi keranjang setelah login.
  * Menyiapkan variasi produk uji (minimal 2 produk berbeda) dari katalog.
  * Variasi angka kuantitas (angka bulat positif seperti 4, serta masukan tidak valid seperti 0 atau angka negatif).

&#x20;

## Test Strategy & Approach

***

* **Positive Testing:** Menambahkan produk tunggal maupun ganda ke keranjang belanja, mengubah kuantitas pada halaman detail produk sebelum klik _Add to cart_, menambahkan produk dari carousel _Recommended Items_, memverifikasi rincian tabel keranjang (_Item Name, Price, Quantity, Total Price_), menghapus item dari keranjang hingga bersih, dan memastikan item yang dimasukkan sebelum _login_ tetap tersimpan di dalam keranjang setelah _login_ berhasil.
* **Negative Path:** Menginput kuantitas bernilai 0, angka negatif, atau karakter non-numerik pada input kuantitas di halaman detail produk untuk memvalidasi _input sanitization_ / penolakan sistem, serta mengakses halaman keranjang dalam kondisi kosong untuk memastikan UI menampilkan indikator keranjang kosong secara benar.
* **Data Consistency & Calculation Validation:** Memastikan kalkulasi Total Price pada tiap baris produk bernilai tepat (Price $\times$ Quantity), serta memastikan jumlah _badge/item count_ di header selaras dengan jumlah barang sesungguhnya di keranjang.

&#x20;

## Risks & Dependencies

***

* **Dependencies:** Pengujian modul ini menjadi prasyarat (_prerequisite_) utama sebelum mengeksekusi alur pembuatan pesanan pada TP-AEX-0004 (Checkout, Payment & Order Processing).
* **Risks & Mitigation:**
  * _Risk:_ Sesi lokal (cookies/local storage) menyimpan sisa item dari eksekusi test sebelumnya sehingga jumlah produk di keranjang menjadi tidak akurat.
  * _Mitigation:_ Terapkan langkah pembersihan (_Clear Cart_ atau _Clear Cookies/Browser Storage_) pada tahapan _pre-condition_ atau _post-condition_ di setiap skenario pengujian.

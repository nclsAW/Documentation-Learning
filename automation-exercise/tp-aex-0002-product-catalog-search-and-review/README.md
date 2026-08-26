# TP-AEX-0002 Product Catalog, Search & Review

## Objective & Scope

***

* **Dependency:** Pengujian modul ini bergantung pada ketersediaan data katalog produk (_master product list_) yang telah terpasang pada basis data aplikasi. Untuk fungsionalitas penjelajahan katalog, pencarian, dan filter produk tidak memerlukan status _login_, namun pengujian fitur penambahan ulasan (_Write Your Review_) memerlukan identitas pengirim (dapat diisi secara manual atau menggunakan nama dari sesi pengguna terdaftar).
* **In-Scope:** Pengujian fungsional pada navigasi halaman katalog utama (/products), verifikasi tampilan detail produk (/product\_details/{id}), fungsionalitas _Search Bar_ untuk pencarian nama produk, filter navigasi produk berdasarkan Kategori & Sub-kategori (_Women, Men, Kids_), filter produk berdasarkan Brand (_Polo, H\&M, Madame, dll_), serta pengiriman form ulasan produk (_Write Your Review_).
* **Out-of-Scope:** Pengujian opsi pengurutan (_sorting price/alphabetical_) dan pengujian sistem rekomendasi berbasis _AI/machine learning_ (karena fitur tersebut tidak tersedia pada halaman katalog Automation Exercise).



## Environment & Test Setup

***

* **Target URL:** [Automation Exercise - All Products](https://automationexercise.com/products)
* **Browser/Platform:** Google Chrome (Latest Version) / Desktop.
* **Test Data Requirement:**
  * Menyiapkan kata kunci pencarian produk yang valid (contoh: Dress, Top. Tshirt) dan kata kunci tidak valid (contoh: XYZ123NonExistent).
  * Data pengirim ulasan produk: Nama, Email valid, dan teks ulasan (_review body_).
  * Nama kategori, sub-kategori, dan brand yang aktif pada _sidebar_ halaman produk.

## Test Strategy & Approach

***

* **Positive Testing:** Mengeksekusi penjelajahan katalog produk, memverifikasi kelengkapan elemen detail produk (_Product Name, Category, Price, Availability, Condition, Brand_), melakukan pencarian produk dengan kata kunci yang sesuai, memfilter produk berdasarkan hierarki kategori dan brand, serta mengunggah ulasan produk hingga muncul pesan konfirmasi sukses (_"Thank you for your review."_).
* **Negative Path:** Memasukkan kata kunci pencarian yang tidak ada di katalog untuk memvalidasi penanganan tampilan produk kosong (_empty search result_), mengosongkan _field_ wajib pada form ulasan (_Name, Email, atau Review text_), serta memasukkan format email tidak valid pada form ulasan untuk memvalidasi _error handling_ / mekanisme penolakan sistem.
* **Filter & Search Result State Validation:** Memastikan produk yang ditampilkan pada grid pencarian atau filter kategori/brand benar-benar sesuai dengan parameter yang dipilih (misal: saat memilih kategori _Women -> Dress_, seluruh produk yang muncul berada dalam kategori _Dress_).

## Risks & Dependencies

***

* **Dependencies:** Data produk yang ada di modul ini menjadi prasyarat (_prerequisite_) bagi pengujian TP-AEX-0003 (Cart Management) dan TP-AEX-0004 (Checkout & Order).
* **Risks & Mitigation:**
  * _Risk:_ Perubahan data atau penghapusan item produk dari sisi basis data dapat menyebabkan ID produk tidak ditemukan (_404 Not Found_) saat pengujian detail produk.
  * _Mitigation:_ Pengujian detail produk selalu dimulai dari pencarian/klik dinamis pada halaman katalog utama (/products), bukan mengakses URL dengan _hardcoded product ID_.

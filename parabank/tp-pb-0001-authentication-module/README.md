# TP-PB-0001 Authentication Module

## Objective & Scope

***

* **Objective:** Memvalidasi seluruh mekanisme akses pengguna (registrasi, masuk, dan keluar) untuk memastikan keamanan akun dan hanya nasabah sah yang dapat mengakses sistem perbankan.
* **In-Scope:** Pengujian fungsional dan keamanan dasar pada modul _User Registration_, _User Login_, dan _User Logout_.
* **Out-of-Scope:** Pengujian transaksi finansial internal (berada di TP-0001) dan manajemen informasi profil (berada di TP-0003).

## Environment & Test Setup

***

* **Target URL:** `[https://parabank.parasoft.com/parabank/index.htm](https://parabank.parasoft.com/parabank/index.htm)`
* **Browser/Platform:** Google Chrome (Latest Version) / Desktop.
* **Test Data Requirement:**
  * Tidak memerlukan prasyarat akun yang sudah ada karena _tester_ akan membuat akun baru dari awal pada fase registrasi.
  * Siapkan _dummy string_ untuk _username_ dan kredensial invalid guna memvalidasi _error handling_ form otentikasi.

## Test Strategy & Approach

***

* **Positive Testing:** Mengeksekusi alur pendaftaran dan _login_ menggunakan data yang 100% valid untuk memvalidasi keberhasilan akses, pengalihan halaman (_redirect_), dan pembuatan sesi.
* **Negative Path:** Memasukkan kredensial salah, mendaftarkan _username_ yang sama, dan mengosongkan _field mandatory_ untuk memastikan sistem mengembalikan pesan _error_ yang tepat.
* **Session Management:** Memastikan sistem menghentikan sesi secara total saat _logout_, serta memvalidasi keamanan _cache browser_ (memastikan pengguna tidak bisa kembali ke _dashboard_ melalui tombol _Back_ setelah _logout_).

## Risk & Dependencies

***

* **Dependency:** Modul ini adalah fondasi gerbang utama. Modul Core Banking (TP-0001) dan Profile Management (TP-0003) berstatus _Blocked_ dan tidak bisa dieksekusi jika TP-0002 memiliki _bug_ kritis pada fitur _Login_ atau _Registration_.
* **Mitigation:** Prioritaskan eksekusi pengujian pada modul ini terlebih dahulu di _board_ Kanban sebelum menjalankan pengujian transaksi.

# TP-AEX-0001 Authentication & Account Management

## Objective & Scope

***

* **Dependency:** Pengujian modul ini berjalan sebagai landasan utama (_baseline_) aplikasi. Pengujian registrasi, login, dan hapus akun tidak memiliki dependensi ke modul lain, namun data akun yang berhasil dibuat di modul ini menjadi syarat mutlak (_dependency_) untuk pengujian alur keranjang belanja, _checkout/order_, dan pengisian _review_ pada modul-modul berikutnya.
* **In-Scope:** Pengujian fungsional pada form pendaftaran pengguna baru (_User Registration_), validasi pembuatan akun lengkap (_Enter Account Information_ & _Address Details_), login pengguna dengan kredensial valid dan invalid, penanganan pendaftaran email ganda (_duplicate email_), status sesi aktif (_Logged in as username_), fungsi _Logout_, serta proses penghapusan akun (_Delete Account_).
* **Out-of-Scope:** Pengujian fungsionalitas pemulihan kata sandi (_Forgot/Reset Password_) dan autentikasi berbasis OAuth pihak ketiga (seperti Login via Google/Facebook) karena fitur tersebut tidak tersedia pada situs Automation Exercise, serta pengujian _load/performance test_ pada server otentikasi.

## Environment & Test Setup

***

* **Target URL:** [Automation Exercise - Signup / Login](https://automationexercise.com/login)
* **Browser/Platform:** Google Chrome (Latest Version) / Desktop.
* **Test Data Requirement:**
  * Menyiapkan data kredensial baru yang belum pernah terdaftar (Nama, Email unik, Password, Tanggal Lahir, serta Detail Alamat Lengkap).
  * Menyiapkan data kredensial yang sudah terdaftar (_existing user_) untuk pengujian alur _duplicate registration_.
  * Menyiapkan variasi masukan tidak valid (_invalid format email_, _wrong password_, dan _blank mandatory fields_).

## Test Strategy & Approach

***

* **Positive Testing:** Mengeksekusi pendaftaran akun baru hingga sukses, memverifikasi keterbacaan sesi pengguna aktif pada _header_ navigasi, melakukan _logout_ dan _re-login_ menggunakan kredensial yang telah dibuat, serta mengeksekusi fitur _Delete Account_ untuk memastikan akun dapat dihapus secara permanen dari basis data.
* **Negative Path:** Memasukkan parameter tidak valid (mendaftarkan akun menggunakan email yang sudah ada di sistem, mengosongkan _field_ wajib saat proses pengisian data akun, memasukkan _password_ atau email yang salah pada form login, serta memasukkan _string_ email tanpa simbol `@` atau domain) untuk memvalidasi _error handling_ dan kemunculan pesan peringatan sistem.
* **Session & State Transition Validation:** Memastikan sistem mengarahkan halaman pengguna (_redirection_) secara tepat setelah otentikasi berhasil, membatasi akses halaman terlindungi ketika sesi telah _logged out_, serta memastikan akun yang telah berstatus _Deleted_ tidak dapat digunakan kembali untuk proses login.

## Risks & Dependencies

***

* **Dependencies:** Pengujian modul ini menjadi prasyarat (_prerequisite_) bagi pengujian **TP-CHECKOUT** (alur _Place Order_) dan **TP-CART** (alur _Cart Persistence after Login_).
* **Risks & Mitigation:**
  * _Risk:_ Akun uji tersisa di dalam basis data sehingga menyebabkan kegagalan saat pengujian diulang (_duplicate email error_).
  * _Mitigation:_ Wajib mengeksekusi langkah _Delete Account_ di akhir alur _Happy Path_ atau menggunakan generator _random email_ (misal: `testuser_timestamp@mail.com`) untuk setiap siklus pengujian.

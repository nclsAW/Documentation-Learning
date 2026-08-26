# TP-AEX-0007 Backend API Testing Validation

## Objective & Scope

***

* **Dependency:** Pengujian modul API ini berfokus pada lapisan backend (application programming interface) dan dapat dieksekusi secara independen dari antarmuka UI. Namun, untuk pengujian autentikasi dan pembuatan akun via API (seperti Verify Login, Create Account, dan Delete Account), data kredensial yang dikirimkan harus terintegrasi dengan basis data utama aplikasi.
* **In-Scope:** Pengujian fungsionalitas seluruh endpoint API REST yang disediakan situs Automation Exercise ([https://automationexercise.com/api\_list](https://automationexercise.com/api_list)), mencakup metode HTTP GET (Get All Products List, Get All Brands List, Get User Detail), HTTP POST (Search Product, Verify Login, Create Account), HTTP PUT (Update Account), serta HTTP DELETE (Delete Account). Pengujian meliputi validasi status kode HTTP (200 OK, 201 Created, 400 Bad Request, 404 Not Found, 405 Method Not Allowed), struktur format respons JSON, serta pesan kesalahan (Response Message).
* **Out-of-Scope:** Pengujian beban dan performa API (Load & Performance Testing) tingkat lanjut, pengujian keamanan API (Penetration Testing / Rate Limiting), serta autentikasi berbasis Bearer Token / OAuth2 kompleks (karena endpoint Automation Exercise menggunakan parameter form-data/x-www-form-urlencoded sederhana).

## Environment & Test Setup

***

* **Target Base URL:** [Automation Exercise](https://automationexercise.com/api)
* **Testing Client / Framework:** Postman / REST Assured / Bruno / Playwright API Request Context.
* **Test Data Requirement:**
  * Endpoint GET/POST Produk: Parameter kata kunci pencarian (contoh: search\_product = top, tshirt).
  * Endpoint Autentikasi API: Parameter email dan password valid/invalid.
  * Endpoint Manajemen Akun API: Parameter payload lengkap pendaftaran akun (name, email, password, address, city, zipcode, dll).

## Test Strategy & Approach

***

* **Positive Testing:** Mengirimkan permintaan HTTP GET untuk mengambil daftar seluruh produk dan brand dengan ekspektasi status kode 200 OK, mengirimkan permintaan HTTP POST Search Product dengan parameter yang sesuai, memverifikasi fungsi Verify Login dengan kredensial yang tepat, serta mengeksekusi alur pembuatan (POST), pembaruan (PUT), dan penghapusan (DELETE) akun via API hingga mendapatkan status kode 200/201 beserta pesan konfirmasi yang sesuai.
* **Negative Path:** Mengirimkan metode HTTP yang tidak didukung pada endpoint tertentu (contoh: POST to All Products List atau DELETE to Verify Login) untuk memvalidasi kemunculan status kode 405 Method Not Allowed, mengirimkan permintaan POST tanpa parameter wajib (seperti search\_product atau email) untuk memvalidasi kemunculan status kode 400 Bad Request, serta mengirimkan kredensial login yang salah untuk memvalidasi status kode 404 Not Found.
* **Schema & Contract Validation:** Memastikan skema JSON yang diterima pada respons API memiliki tipe data yang valid (string, integer, array) dan struktur kunci (keys) sesuai dengan dokumentasi API resmi.

## Risks & Dependencies

***

* **Dependencies:** Membutuhkan kestabilan server backend Automation Exercise agar respons API tidak mengalami kegagalan akibat internal server error (500).
* **Risks & Mitigation:**
  * _Risk:_ Format request payload yang dikirimkan menggunakan header Content-Type yang salah (misal: JSON raw alih-alih form-data / x-www-form-urlencoded) dapat menyebabkan API mengembalikan respons error yang membingungkan.
  * _Mitigation:_ Pastikan konfigurasi request header dan body type di API client disesuaikan persis dengan spesifikasi dokumentasi resmi (api\_list) sebelum eksekusi otomatis dijalankan.

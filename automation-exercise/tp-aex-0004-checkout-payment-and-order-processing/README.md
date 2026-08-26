# TP-AEX-0004 Checkout, Payment & Order Processing

## Objective & Scope

***

* **Dependency:** Pengujian modul ini sangat bergantung pada keberhasilan TP-AEX-0001 (Authentication & Account Management) untuk penyediaan data akun/alamat dan TP-AEX-0003 (Cart Management) untuk penyediaan item di dalam keranjang belanja. Tanpa adanya produk di keranjang dan sesi akun terdaftar, siklus checkout hingga pembayaran tidak dapat diproses.
* **In-Scope:** Pengujian fungsional pada alur Proceed to Checkout melalui 3 skenario (Register While Checkout, Register Before Checkout, dan Login Before Checkout), verifikasi kesesuaian Delivery Address dan Billing Address dengan data registrasi, pengisian catatan pesanan (Comment/Description), pemprosesan transaksi pada form Payment (Name on Card, Card Number, CVC, Expiration Date), verifikasi halaman konfirmasi pesanan (Order Placed!), serta fungsionalitas pengunduhan faktur (Download Invoice PDF).
* **Out-of-Scope:** Pengujian integrasi ke payment gateway pihak ketiga yang menggunakan verifikasi OTP/3D Secure (seperti Midtrans/Stripe live), simulasi pengiriman barang fisik oleh kurir logistik, dan pengiriman email konfirmasi transaksi otomatis ke server SMTP eksternal.

## Environment & Test Setup

***

* **Target URL:**[Automation Exercise - Checkout](https://automationexercise.com/checkout)
* **Browser/Platform:** Google Chrome (Latest Version) / Desktop.
* **Test Data Requirement:**
  * Akun terdaftar beserta data alamat lengkap dari TP-AEX-0001.
  * Produk yang sudah berada di dalam keranjang belanja dari TP-AEX-0003.
  * Data dummy kartu kredit (Test Card Credentials): Nama Pemilik Kartu, Nomor Kartu 16 Digit, CVC 3 Digit, dan Bulan/Tahun Kadaluarsa.
  * Storage/Download folder pada sistem lokal yang siap untuk memvalidasi berkas faktur (Invoice PDF).

## Test Strategy & Approach

***

* **Positive Testing:** Memproses checkout dengan berbagai kondisi autentikasi, memvalidasi bahwa alamat pengiriman dan penagihan yang tercantum pada halaman checkout persis sama dengan data akun saat pendaftaran, melakukan konfirmasi pembayaran hingga muncul pesan 'Your order has been placed successfully!', serta mengeksekusi tombol Download Invoice untuk memastikan berkas PDF terunduh secara sempurna.
* **Negative Path:** Mengosongkan field pembayaran wajib (Card Number, CVC, atau Expiration Date), menginput nomor kartu dengan jumlah digit yang kurang/format tidak valid, serta memicu proses Proceed to Checkout saat keranjang dalam keadaan kosong untuk memvalidasi mekanisme penolakan atau error handling sistem.
* **Data Integration & Document Validation:** Memastikan total tagihan pada ringkasan pesanan (Review Your Order) selaras dengan total harga di keranjang, serta memverifikasi bahwa berkas Invoice yang diunduh berformat PDF dan memuat nomor transaksi yang sesuai.

## Risks & Dependencies

***

* **Dependencies:** Pengujian bergantung pada ketersediaan data akun dari TP-AEX-0001 dan item di keranjang dari TP-AEX-0003.
* **Risks & Mitigation:**
  * _Risk:_ Kegagalan pengunduhan berkas Invoice akibat pemblokiran pop-up / otorisasi download pada browser (Browser Download Restriction).
  * _Mitigation:_ Pastikan pengaturan browser dalam kondisi mengizinkan automatic download untuk domain [Automation Exercise](http://automationexercise.com/) sebelum eksekusi pengujian dijalankan.

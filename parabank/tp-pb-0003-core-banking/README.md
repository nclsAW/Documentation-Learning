# TP-PB-0003 Core Banking

## Objective & Scope

***

* **Objective:** Memvalidasi seluruh fungsi transaksi finansial utama di dalam sistem ParaBank untuk memastikan perpindahan dana, pembuatan rekening baru, kalkulasi saldo, dan logika perbankan berjalan secara akurat dan _real-time_.
* **In-Scope:** Pengujian fungsional pada modul _Open New Account_, _Transfer Funds_, _Bill Pay_, dan _Request Loan_.
* **Out-of-Scope:** Pengujian keamanan otentikasi (berada di TP-0002) dan manajemen profil serta pelacakan riwayat (berada di TP-0003).

## Environment & Test Setup

***

* **Target URL:** `[https://parabank.parasoft.com/parabank/index.htm](https://parabank.parasoft.com/parabank/index.htm)`
* **Browser/Platform:** Google Chrome (Latest Version) / Desktop.
* **Test Data Requirement:**
  * Membutuhkan satu akun _dummy_ aktif (hasil registrasi dari modul TP-0002) yang dalam keadaan _logged in_.
  * Akun wajib memiliki minimal satu rekening utama (_Checking Account_) dengan saldo (_balance_) awal yang mencukupi untuk mengeksekusi pengujian transfer dan pembayaran tagihan.

## Test Strategy & Approach

***

* **Positive Testing:** Mengeksekusi skenario transaksi menggunakan parameter yang valid (nominal positif, saldo asal mencukupi, _down payment_ proporsional) untuk memastikan perpindahan dana sukses dan tercatat di sistem.
* **Negative Path:** Memasukkan nilai anomali (transfer melebihi saldo yang tersedia, _down payment_ pinjaman terlalu rendah, _input_ huruf atau simbol pada _field_ nominal) untuk memvalidasi _error handling_ dan penolakan transaksi yang aman.
* **Security & Validation:** Memastikan sistem mengimplementasikan prinsip "Never Trust the Client" di mana validasi limit saldo atau persetujuan pinjaman dilakukan murni di _server-side_ agar tidak bisa dimanipulasi melalui _browser_.

## Risks & Dependencies

***

* **Dependency:** Eksekusi pengujian ini sangat bergantung (terblokir) pada keberhasilan TP-0002. Jika fitur pendaftaran atau _login_ bermasalah, _tester_ tidak bisa mengakses _dashboard_ transaksi sama sekali.
* **Risk:** Lingkungan _database_ ParaBank bersifat publik dan sering melakukan _auto-reset_ secara berkala yang bisa menghapus data rekening uji.
* **Mitigation:** Selalu buat akun _dummy_ baru sesaat sebelum fase pengujian TP-0001 dieksekusi jika data akun uji sebelumnya hilang terhapus oleh server.

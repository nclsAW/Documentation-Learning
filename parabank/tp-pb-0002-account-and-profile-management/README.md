# TP-PB-0002 Account & Profile Management

## Objective & Scope

***

* **Objective:** Memvalidasi mekanisme pelacakan data nasabah (ringkasan saldo, riwayat transaksi) dan pembaruan profil untuk memastikan sinkronisasi data berjalan akurat serta antarmuka menampilkan informasi yang tepat.
* **In-Scope:** Pengujian fungsional pada modul _Accounts Overview_, _Find Transactions_, dan _Update Contact Info_.
* **Out-of-Scope:** Pengujian otentikasi akun (berada di TP-0002) dan eksekusi transaksi finansial inti (berada di TP-0001).

## Environment & Test Setup

***

* **Target URL:** `[https://parabank.parasoft.com/parabank/index.htm](https://parabank.parasoft.com/parabank/index.htm)`
* **Browser/Platform:** Google Chrome (Latest Version) / Desktop.
* **Test Data Requirement:**
  * Membutuhkan akun _dummy_ yang sudah terdaftar dan dalam keadaan _logged in_ (dari modul TP-0002).
  * Khusus untuk pengujian pencarian, akun wajib sudah memiliki riwayat mutasi/transaksi (dari eksekusi modul TP-0001).

## Test Strategy & Approach

***

* **Positive Testing:** Mengeksekusi pencarian riwayat menggunakan kriteria yang valid (ID, Tanggal, Nominal), memastikan tabel _Overview_ memunculkan kalkulasi total saldo yang benar, dan menyimpan data pembaruan kontak yang valid.
* **Negative Path:** Mengosongkan _field_ wajib (seperti _Zip Code_) saat melakukan pembaruan profil, atau mencari transaksi menggunakan rentang tanggal yang tidak logis (misal: tanggal _To_ lebih kecil dari _From_).
* **Data Integrity Testing:** Memastikan pembaruan informasi kontak benar-benar tersimpan dan tercermin secara _real-time_ di seluruh sistem aplikasi.

## Risks & Dependencies

***

* **Dependency:** Eksekusi modul ini sangat bergantung pada keberhasilan TP-0002 (untuk masuk ke sistem). Fitur _Find Transactions_ (IS-009) juga mensyaratkan TP-0001 sudah dieksekusi agar _database_ memiliki data _dummy_ transaksi yang bisa dicari.
* **Mitigation:** Lakukan eksekusi TP-0003 di fase akhir, setelah _tester_ menyelesaikan _flow Authentication_ dan _Core Banking_.

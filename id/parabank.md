# ParaBank

## Description <a href="#description" id="description"></a>

***

ParaBank adalah aplikasi simulasi Retail Banking berbasis web yang dirancang khusus untuk praktik dan pengujian perangkat lunak. Aplikasi ini menyediakan fungsionalitas perbankan online yang komprehensif, mencakup pembukaan rekening baru (Open New Account), pemeriksaan saldo & riwayat transaksi (Accounts Overview), transfer dana antarrekening (Transfer Funds), pembayaran tagihan (Bill Pay), pengajuan pinjaman (Apply for a Loan), hingga administrasi profil pengguna dan database reset.

## Test Objective & Scope <a href="#test-objective-and-scope" id="test-objective-and-scope"></a>

***

* **Tujuan Pengujian:** Memvalidasi keandalan fungsionalitas utama (core banking operations), memastikan integritas saldo dan pembaruan riwayat transaksi setelah aksi finansial, serta menguji validasi input pada form transaksi untuk mencegah kesalahan data.
* **In Scope:**
  * **User Onboarding & Auth:** Registrasi akun baru (Register), Login/Logout, dan Forgot Login Info.
  * **Account Management:** Open New Account (Checking/Savings) dan Accounts Overview (pengecekan saldo & detail transaksi).
  * **Fund Operations:** Transfer Funds antarrekening internal dan Bill Pay (pembayaran ke vendor eksternal).
  * **Credit & Loan Services:** Apply for a Loan (pengajuan pinjaman berdasarkan saldo dan down payment).
  * **Customer Profile:** Update Contact Info dan penyesuaian detail alamat.
* **Out of Scope:** Automated Security/Penetration Testing, Stress/Load Testing di level infrastruktur server, dan pengujian API backend secara terpisah (fokus pada End-to-End Manual UI Testing).

## Test Environment <a href="#test-environment" id="test-environment"></a>

***

| **Parameter**        | **Detail**                                                                                           |
| -------------------- | ---------------------------------------------------------------------------------------------------- |
| URL                  | [https://parabank.parasoft.com/parabank/index.htm](https://parabank.parasoft.com/parabank/index.htm) |
| Browser              | Google Chrome                                                                                        |
| OS                   | Windows 11                                                                                           |
| Test Management Tool | Jira                                                                                                 |
| Documentation Tool   | Confluence                                                                                           |

## Execution Summary & Metrics <a href="#execution-summary-and-metrics" id="execution-summary-and-metrics"></a>

***

### Overall Test Case Execution Status <a href="#overall-test-case-execution-status" id="overall-test-case-execution-status"></a>

| **Status**      | **Jumlah Test Case** | **Persentase** |
| --------------- | -------------------- | -------------- |
| Passed          | 51                   | 78.46%         |
| Failed          | 14                   | 21.54%         |
| Blocked         | 0                    | 0%             |
| Total Test Case | 65                   | 100%           |

### Defect Summary by Severity <a href="#defect-summary-by-severity" id="defect-summary-by-severity"></a>

| **Severity**     | **Open** | **Resolved/Closed** | **Total Bug** |
| ---------------- | -------- | ------------------- | ------------- |
| Critical/Blocker | 3        |                     | 3             |
| High             | 8        |                     | 8             |
| Medium           |          |                     |               |
| Low/Minor        | 3        |                     | 3             |
| Total            | 14       |                     | 14            |

## Detail Break-down Task/Module <a href="#detail-break-down-task-module" id="detail-break-down-task-module"></a>

***

### Module 1: Authentication (TP-PB-0001) <a href="#module-1-authentication-tp-pb-0001" id="module-1-authentication-tp-pb-0001"></a>

* **Related Ticket:**
  * PB-0001 \[QA] User Registration
  * PB-0002 \[QA] User Login
  * PB-0003 \[QA] User Logout
* **Coverage:** Manajemen alur pengguna masuk ke sistem, pembuat akun baru, dan pemutusan sesi pengguna.
* **Highlight Log:**
  * Proses User Registration berhasil membuat kredensial baru dan otomatis membuatkan rekening awal secara paralel.
  * Fungsi Login dan Logout berjalan stabil, namun ditemukan catatan ketiadaan sanitasi input spasi pada username baru.

### Module 2: Account & Profile Management (TP-PB-0002) <a href="#module-2-account-and-profile-management-tp-pb-0002" id="module-2-account-and-profile-management-tp-pb-0002"></a>

* **Related Ticket:**
  * PB-0004 \[QA] Accounts Overview
  * PB-0005 \[QA] Find Transactions
  * PB-0006 \[QA] Update Contact Info
  * PB-0007 \[QA] Open New Account
* **Coverage:** Manajemen informasi rekening, pelacakan riwayat transaksi, pembaruan profil pengguna, dan pembukaan jenis rekening tambahan (Savings/Checking).
* **Highlight Log:**
  * Open New Account sukses menerbitkan nomor rekening baru dan memotong deposit secara akurat dari akun utama.
  * Fitur Find Transactions mengalami eror respons server ketika pencarian dilakukan menggunakan rentang tanggal kosong.

### Module 3: Core Banking (TP-PB-0003) <a href="#module-3-core-banking-tp-pb-0003" id="module-3-core-banking-tp-pb-0003"></a>

* **Related Ticket:**
  * PB-0008 \[QA] Transfer Funds
  * PB-0009 \[QA] Bill Pay
  * PB-0010 \[QA] Request Loan
* **Coverage:** Transaksi finansial utama yang melibatkan pemindahan dana, pembayaran tagihan eksternal, dan pengajuan pinjaman.
* **Highlight Log:**
  * Fitur Transfer Funds berjalan lancar dan memperbarui saldo kedua rekening secara akurat.
  * Bill Pay menemukan isu kritis di mana transaksi nominal negatif masih lolos eksekusi.
  * Request Loan merespons keputusan (Approved/Denied) secara konsisten berdasarkan kalkulasi Down Payment.

## Key Defect Log <a href="#key-defect-log" id="key-defect-log"></a>

***

| **Jira Key** | **Bug Summary**                                                                                                                                                                                                                                                                                                                | **Severity** | **Status** | **Module**          |
| ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------ | ---------- | ------------------- |
| KAN-20       | Sistem berhasil menghentikan sesi di server saat logout, namun gagal membersihkan cache browser karena tidak menerapkan header Cache-Control. Akibatnya, data sensitif pada dashboard masih dapat diintip oleh pengguna lain dengan cara menekan tombol Back pada navigasi browser.                                            | Critical     | Open       | User Logout         |
| KAN-21       | Pencarian dengan data fiktif tidak menyebabkan sistem crash, tetapi aplikasi tidak menyediakan Empty State berupa pesan "Data tidak ditemukan". Hal ini menampilkan tabel kosong melompong yang berpotensi membingungkan pengguna terkait status hasil pencarian.                                                              | Low          | Open       | Find Transactions   |
| KAN-22       | Validasi pada form registrasi tidak menerapkan fungsi trimming spasi dan meloloskan kolom wajib diisi (kecuali Phone #). Alhasil, pendaftaran dapat diselesaikan hanya dengan memasukkan karakter spasi (" "), yang berisiko merusak integritas data pengguna di database.                                                     | High         | Open       | Register            |
| KAN-23       | Validasi form pada halaman Update Contact Info tidak menerapkan trimming spasi dan meloloskan kolom wajib diisi tanpa peringatan (kecuali field Phone #). Akibatnya, pengguna dapat memperbarui data profil hanya dengan memasukkan karakter spasi (" "), yang berisiko merusak integritas data di database.                   | High         | Open       | Update Contact Info |
| KAN-26       | Sistem gagal memvalidasi ketersediaan dana saat proses pembuatan akun baru (Open New Account). Aplikasi tetap mengizinkan pemotongan deposit sebesar $100 dari rekening sumber yang sedang bersaldo negatif, sehingga akun baru berhasil dibuat sementara hutang pada rekening sumber semakin membengkak.                      | High         | Open       | Open New Account    |
| KAN-27       | Fitur Transfer Funds tidak memiliki validasi server-side untuk menolak transaksi yang melebihi batas saldo aktif. Sistem tetap memproses transfer nominal besar ($500 dari saldo $100), menyebabkan rekening pengirim berubah menjadi minus (-$400) dan saldo penerima bertambah tanpa adanya konfirmasi penanganan overdraft. | Critical     | Open       | Transfer Funds      |
| KAN-28       | Fitur Transfer Funds tidak memiliki validasi nilai nominal minimal, sehingga mengizinkan kalkulasi matematika terbalik dengan angka negatif (-$10,000). Transaksi tetap diproses hingga menyebabkan saldo pengirim bertambah secara ilegal dan saldo penerima terpotong menjadi minus.                                         | Critical     | Open       | Transfer Funds      |
| KAN-29       | Sistem gagal memvalidasi ketersediaan opsi rekening pada modul Transfer Funds, sehingga mengizinkan pengguna memilih nomor rekening pengirim dan penerima yang sama. Walaupun tidak mengubah jumlah saldo riil, transaksi tetap dinyatakan sukses dan menghasilkan log history yang mubazir.                                   | High         | Open       | Transfer Funds      |
| KAN-30       | Sistem validasi server-side pada modul Bill Pay tidak mengecek ketersediaan dana sebelum memproses transaksi. Aplikasi tetap meloloskan pembayaran tagihan sebesar $500 dari rekening yang hanya bersaldo $100, memicu pemotongan dana secara tidak sah hingga saldo menjadi minus (-$400).                                    | High         | Open       | Bill Pay            |
| KAN-31       | Sistem Request Loan tidak memiliki penanganan validasi mandatory field saat kolom Down Payment dikosongkan. Alih-alih menampilkan pesan error yang ramah pengguna, kegagalan validasi ini memicu unhandled exception (HTTP 500) di backend dengan pesan generic "An internal error has occurred and has been logged."          | High         | Open       | Request Loan        |
| KAN-32       | Fitur Request Loan gagal memvalidasi tipe data input angka pada formulir pengajuan. Ketika pengguna memasukkan karakter non-numerik, sistem tidak mencegat format yang tidak valid tersebut (client/server-side) dan justru mengalami crash/unhandled exception (HTTP 500) dari sisi backend.                                  | High         | Open       | Request Loan        |

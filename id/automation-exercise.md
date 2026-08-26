# Automation Exercise

## Description <a href="#description" id="description"></a>

***

Dokumen ini merangkum cakupan pengujian fungsional End-to-End (E2E) antarmuka web (UI) dan integrasi Application Programming Interface (API) pada platform Automation Exercise. Pengujian mencakup siklus lengkap e-commerce, mulai dari manajemen akun pengguna, eksplorasi katalog produk, pengelolaan keranjang, alur transaksi & checkout, layanan bantuan, navigasi umum, hingga validasi lapisan backend REST API.

## Test Objective & Scope <a href="#test-objective-and-scope" id="test-objective-and-scope"></a>

***

### Tujuan Penelitian:  <a href="#tujuan-penelitian" id="tujuan-penelitian"></a>

* Memastikan seluruh fitur fungsional utama (autentikasi, katalog, keranjang belanja, _order/checkout_, dan formulir kontak) berjalan sesuai spesifikasi alur bisnis.
* Memvalidasi konsistensi data antara _frontend_ antarmuka pengguna dan _backend_ REST API.
* Mengidentifikasi kegagalan alur, ketidaksesuaian validasi formulir, serta _response status code_ / format JSON pada endpoint API.

### In-Scope: <a href="#in-scope" id="in-scope"></a>

* **TP-0001**: Registrasi akun, validasi data pengguna & alamat, login (valid/invalid), duplikasi email, status sesi aktif, logout, & hapus akun.
* **TP-0002**: Navigasi katalog (/products), detail produk, _search bar_, filter Kategori/Sub-kategori, filter Brand, & pengiriman ulasan produk.
* **TP-0003**: Penambahan item ke keranjang (katalog/detail/rekomendasi), modifikasi kuantitas awal, hapus item, kalkulasi total harga, & persistensi keranjang pasca-login.
* **TP-0004**: Alur checkout (3 variasi skenario), verifikasi alamat pengiriman/penagihan, input _payment card_, konfirmasi pesanan (_Order Placed_), & unduh invoice (PDF).
* **TP-0005**: Navigasi halaman Contact Us, pengisian formulir, unggah lampiran berkas, penanganan dialog pop-up JavaScript (_Alert OK_), & pesan konfirmasi sukses.
* **TP-0006**: Navigasi halaman Test Cases, langganan newsletter (_footer subscription_) pada Home & Cart, serta tombol _scroll up_ (tombol & manual).
* **TP-0007**: Validasi endpoint REST API (GET, POST, PUT, DELETE) mencakup status kode HTTP (200, 201, 400, 404, 405), struktur payload JSON, & pesan error backend.

### Out-of-Scope: <a href="#out-of-scope" id="out-of-scope"></a>

* Fitur _Forgot / Reset Password_ dan autentikasi OAuth pihak ketiga (Google/Facebook).
* Pengurutan produk (_sorting price/alphabetical_) dan sistem rekomendasi berbasis AI/ML.
* Pengubahan kuantitas produk secara langsung di dalam keranjang (_inline edit_) & penggunaan kode voucher/promo.
* Integrasi _payment gateway live_ dengan verifikasi 3D Secure / OTP.
* Pengiriman email notifikasi/blast otomatis via SMTP eksternal & integrasi Helpdesk/CRM pihak ketiga.
* Uji performa, _load/stress testing_, _penetration testing_, serta _cross-browser legacy / mobile layout responsiveness testing_.

## Test Environment <a href="#test-environment" id="test-environment"></a>

***

| **Parameter**        | **Detail**                                             |
| -------------------- | ------------------------------------------------------ |
| URL                  | [Automation Exercise](https://automationexercise.com/) |
| Browser              | Google Chrome                                          |
| OS                   | Windows 11                                             |
| Test Management Tool | Jira                                                   |
| Documentation Tool   | Confluence                                             |

## Execution Summary & Metrics <a href="#execution-summary-and-metrics" id="execution-summary-and-metrics"></a>

***

### Overall Test Case Execution Status <a href="#overall-test-case-execution-status" id="overall-test-case-execution-status"></a>

| **Status**      | **Jumlah Test Case** | **Persentase** |
| --------------- | -------------------- | -------------- |
| Passed          | 60                   | 98%            |
| Failed          | 2                    | 2%             |
| Blocked         | 0                    | 0%             |
| Total Test Case | 62                   | 100%           |

### Defect Summary by Severity <a href="#defect-summary-by-severity" id="defect-summary-by-severity"></a>

| **Severity**     | **Open** | **Resolved/Closed** | **Total Bug** |
| ---------------- | -------- | ------------------- | ------------- |
| Critical/Blocker | 0        | 0                   | 0             |
| High             | 1        | 0                   | 1             |
| Medium           | 1        | 0                   | 1             |
| Low/Minor        | 0        | 0                   | 0             |
| Total            | 2        | 0                   | 2             |

## Detail Break-down Task/Module <a href="#detail-break-down-task-module" id="detail-break-down-task-module"></a>

***

### Module 1: Authentication & Account Management (TP-AEX-0001) <a href="#module-1-authentication-and-account-management-tp-aex-0001" id="module-1-authentication-and-account-management-tp-aex-0001"></a>

* **Related Ticket:**
  * AEX-0001 \[QA] User Registration & Account Creation
  * AEX-0002 \[QA] User Login & Session Management
* **Coverage**: Manajemen siklus akun pengguna mencakup pendaftaran baru, validasi kredensial login/logout, penanganan email duplikat, verifikasi status sesi aktif, serta penghapusan akun permanen.
* **Highlight Log:**
  * Alur registrasi, login, dan _account deletion_ tervalidasi sukses dengan data tersimpan sinkron di database.
  * Validasi error pendaftaran email ganda muncul sesuai ekspektasi (_"Email Address already exist!"_).

### Module 2: Product Catalog, Search & Review (TP-AEX-0002) <a href="#module-2-product-catalog-search-and-review-tp-aex-0002" id="module-2-product-catalog-search-and-review-tp-aex-0002"></a>

***

* **Related Ticket:**
  * AEX-0003 \[QA] Product Browsing & Category Filter
* **Coverage**: Eksplorasi katalog produk, navigasi hierarki kategori/sub-kategori, pemfilteran berdasarkan merek (_brand_), fungsionalitas bilah pencarian, dan pengiriman ulasan produk.
* **Highlight Log:**
  * Pencarian dan pemfilteran kategori/brand menampilkan produk yang relevan tanpa _broken images_.
  * Form ulasan produk berhasil mengirimkan data dan memunculkan notifikasi sukses (_"Thank you for your review."_).

### Module 3: Cart Management & Recommended Items (TP-AEX-0003) <a href="#module-3-cart-management-and-recommended-items-tp-aex-0003" id="module-3-cart-management-and-recommended-items-tp-aex-0003"></a>

***

* R**elated Ticket:**
  * AEX-0004 \[QA] Cart Operations & Items Persistence
* **Coverage**: Penambahan produk ke keranjang belanja, manipulasi kuantitas item, penambahan via widget _Recommended Items_, penghapusan item, kalkulasi subtotal/total harga, dan retensi data keranjang pasca-login.
* **Highlight Log:**
  * Kalkulasi harga dan persistensi isi keranjang belanja saat berpindah status sesi (guest ke login) berjalan normal.
  * Ditemukan anomali pada _badge counter_ keranjang di navbar yang tidak ter-_update_ otomatis saat item ditambahkan dari _Recommended Items_ tanpa _reload_ halaman.

### Module 4: Checkout, Payment & Order Processing (TP-AEX-0004) <a href="#module-4-checkout-payment-and-order-processing-tp-aex-0004" id="module-4-checkout-payment-and-order-processing-tp-aex-0004"></a>

***

* R**elated Ticket:**
  * AEX-0005 \[QA] Checkout Flow & Order Confirmation
  * AEX-0006 \[QA] Payment Execution & Invoice Download
* **Coverage**: Validasi alur _end-to-end checkout_ (3 alur skenario), verifikasi integritas data alamat pengiriman/penagihan, input formulir kartu pembayaran, konfirmasi pesanan, dan pengunduhan berkas _invoice_.
* **Highlight Log:**
  * Ketiga skenario alur _checkout_ hingga pembuatan order (_Order Placed!_) berhasil diproses secara mulus.
  * Ditemukan kendala pada fitur unduh faktur di mana berkas PDF yang dihasilkan berukuran kosong (0 KB).

### Module 5: Customer Support & Contact Us (TP-AEX-0005) <a href="#module-5-customer-support-and-contact-us-tp-aex-0005" id="module-5-customer-support-and-contact-us-tp-aex-0005"></a>

***

* R**elated Ticket:**
  * AEX-0007 \[QA] Contact Us Submission & File Attachment
* **Coverage**: Pengujian formulir layanan bantuan pelanggan, pengunggahan lampiran berkas, penanganan konfirmasi dialog pop-up JavaScript (_Alert OK_), verifikasi notifikasi sukses, dan tombol kembali ke halaman utama.
* **Highlight Log:**
  * _Alert confirmation browser_ berhasil tertangani secara otomatis dan formulir kontak berhasil terkirim (_"Success! Your details have been submitted successfully."_).
  * Validasi tipe file unggahan berjalan stabil untuk format umum (dokumen/gambar).

### Module 6: UI, Navigation & Footer Subscription (TP-AEX-0006) <a href="#module-6-ui-navigation-and-footer-subscription-tp-aex-0006" id="module-6-ui-navigation-and-footer-subscription-tp-aex-0006"></a>

***

* R**elated Ticket:**
  * AEX-0008 \[QA] Page Navigation & Scroll Behavior
  * AEX-0009 \[QA] Footer Email Subscription
* **Coverage**: Validasi navigasi menu statis, verifikasi fungsi pendaftaran _newsletter_ pada _footer_ di berbagai halaman, serta uji fungsi tombol _scroll up_ otomatis dan manual.
* **Highlight Log:**
  * Input langganan _newsletter_ berhasil menampilkan respon sukses (_"You have been successfully subscribed!"_) secara instan.
  * Animasi tombol kembali ke atas (_Scroll Up_) bergerak mulus mengembalikan viewport ke posisi teratas halaman.

### Module 7: Backend API Testing Validation (TP-AEX-0007) <a href="#module-7-backend-api-testing-validation-tp-aex-0007" id="module-7-backend-api-testing-validation-tp-aex-0007"></a>

***

* R**elated Ticket:**
  * AEX-0010 \[QA] Products & Brands API Validation
  * AEX-0011 \[QA] Authentication & User Account API Validation
* **Coverage**: Validasi kontrak antarmuka backend REST API mencakup verifikasi status kode HTTP (200, 201, 400, 404, 405), skema JSON _response payload_, serta ketepatan _error response message_.
* **Highlight Log:**
  * Seluruh endpoint pembuatan, pembaruan, login, dan penghapusan akun via API berhasil berinteraksi langsung dengan basis data.
  * Ditemukan inkonsistensi skema status code pada endpoint POST `/api/searchProduct` yang tetap mengembalikan status `200 OK` meskipun parameter wajib tidak dikirimkan.

## Key Defect Log <a href="#key-defect-log" id="key-defect-log"></a>

***

| **Jira Key** | **Bug Summary**                                                                                                                                                                                                                      | **Severity** | **Status** | **Module**     |
| ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------ | ---------- | -------------- |
| KAN-83       | Ketiadaan validasi batas minimum (< 1) pada input _Quantity_ berisiko merusak kalkulasi total harga, integritas stok (_inventory logic_), dan memicu _negative subtotal_ jika nilai lebih dari/sama dengan 0 diproses ke _checkout_. | S2           | Open       | Cart Module    |
| KAN-84       | Form pembayaran menerima nomor kartu dengan jumlah digit di bawah standar industri tanpa validasi (misal: algoritma Luhn/panjang karakter standar 16 digit), berpotensi meloloskan _invalid payload_ ke payment gateway.             | S1           | Open       | Payment Module |

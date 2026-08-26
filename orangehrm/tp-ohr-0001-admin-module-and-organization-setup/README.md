# TP-OHR-0001 Admin Module & Organization Setup

## Objective & Scope

***

* **Objective:** Memvalidasi seluruh fungsi konfigurasi master data organisasi di dalam sistem OrangeHRM untuk memastikan pembaruan profil perusahaan, pembuatan lokasi cabang, dan pemetaan struktur hierarki departemen berjalan akurat dan valid.
* **In-Scope:** Pengujian fungsional pada modul Organization Information, Location Management, dan Organization Structure / Hierarchy.
* **Out-of-Scope:** Pengujian pengelolaan hak akses user/role dan pengalokasian karyawan ke dalam struktur departemen.

## Environment & Test Setup

***

* **Target URL:** [OrangeHRM](https://opensource-demo.orangehrmlive.com/)
* **Browser/Platform:** Google Chrome (Latest Version) / Desktop.
* **Test Data Requirement:**
  * Membutuhkan satu akun uji dengan hak akses System Administrator (Full Privileges).
  * Lingkungan database dalam kondisi clean state atau menggunakan seed data standar OrangeHRM.

## Test Strategy & Approach

***

* **Positive Testing:** Mengeksekusi skenario konfigurasi menggunakan parameter valid (nama perusahaan lengkap, format alamat/lokasi valid, pemetaan parent-child departemen yang logis) untuk memastikan data berhasil disimpan dan direfleksikan di UI.
* **Negative Path:** Memasukkan nilai anomali (mengosongkan mandatory field, input karakter ilegal/terlalu panjang, membuat duplikasi nama lokasi/departemen, menghapus parent node yang memiliki child) untuk memvalidasi error handling dan pesan peringatan sistem.
* **CRUD & Hierarchy Validation:** Memastikan operasi Create, Read, Update, dan Delete berjalan konsisten pada UI serta pohon hierarki organisasi tidak broken saat terjadi perubahan struktur.

## Risks & Dependencies

***

* **Dependency:** Pengujian modul ini menjadi fondasi utama. Jika modul Admin/Organization gagal menyimpan data, pengujian modul PIM (Personal Information Management) dan Recruitment akan terhambat (blocked).
* **Risk:** Penghapusan lokasi atau node departemen utama secara tidak sengaja dapat merusak asosiasi data karyawan atau entitas lain di modul turunan.
* **Mitigation:** Lakukan backup database awal sebelum eksekusi pengujian destruktif (seperti pengetesan fungsi delete node/location) atau gunakan skenario uji di environment isolasi.

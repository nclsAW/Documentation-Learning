# TP-OHR-0002 Personnel Information Management

## Objective & Scope

***

* **Objective:** Memvalidasi fungsionalitas modul **Dynamic Employee Profiling (DEP)** mencakup manajemen profil karyawan, pendaftaran (manual & bulk import), fleksibilitas data kustom (_custom fields & attachments_), hingga ekstraksi laporan (_employee reporting_) agar terintegrasi dengan akurat.
* **In-Scope:**
  1. _Employee Onboarding & Import:_ Penambahan karyawan manual & _Bulk Upload via CSV/Excel_.
  2. _Data Flexibility:_ Pengelolaan _Custom Fields_ dan pengunggahan _Attachments/Documents_.
  3. _Employee Search & Custom Reporting:_ Filter pencarian data karyawan dan pembuatan _Custom Reports_.
* **Out-of-Scope:** Konfigurasi master data dasar struktur organisasi/jabatan (ditangani di TP-OHR-0001) dan pengaturan hak akses/role login level aplikasi.

## Environment & Test Setup

***

* **Target URL:** [OrangeHRM](https://opensource-demo.orangehrmlive.com/)
* **Browser/Platform:** Google Chrome (Latest Version) / Desktop.
* **Test Data Requirement:**
  * Membutuhkan akun uji dengan role HR Admin atau System Administrator.
  * Master data organisasi, jabatan (Job Title), dan status kepegawaian (Employment Status) sudah terkonfigurasi dari TP-OHR-0001.
  * Menyiapkan berkas sample untuk pengujian: file CSV/Excel dengan format data karyawan yang valid dan invalid, serta file dokumen (PDF/JPG/PNG) dengan variasi ukuran berkas.

## Test Strategy & Approach

***

* **Positive Path:** Memastikan alur pendaftaran karyawan (manual/bulk), _upload_ dokumen, pembuatan _custom field_, dan eksekusi laporan kustom berjalan lancar sesuai nilai parameter valid.
* **Negative Path:** Menguji pertahanan sistem (_error handling_) terhadap masukan anomali (file import dengan header salah, batas _file size attachment_ melampaui limit, _mandatory fields_ dikosongkan, dan format tipe data _custom field_ yang tidak sesuai).
* **Data Integrity & Export Validation:** Memastikan file dokumen tidak terkorupsi saat diunduh ulang (_download check_) dan hasil ekspor laporan (CSV/PDF) presisi sesuai kriteria filter.

## Risks & Dependencies

***

* **Dependency:** Pengujian ini sangat bergantung pada keberhasilan TP-OHR-0001. Jika master data jabatan (job titles), departemen, dan lokasi kantor belum dikonfigurasi di Modul 1, maka penambahan karyawan dengan profil lengkap di modul PIM ini tidak bisa dilakukan.
* **Risk:** Pengujian bulk upload menggunakan dataset besar dapat mengonsumsi waktu eksekusi yang lama atau berpotensi menggandakan data karyawan (duplicate entries) jika error handling parser file tidak berjalan optimal.
* **Mitigation:** Gunakan dataset sampel bulk upload skala kecil hingga sedang (10–50 baris data) untuk fase awal pengetesan, serta pastikan fitur rollback atau opsi hapus massal (bulk delete) berfungsi dengan baik sebelum tes dijalankan.

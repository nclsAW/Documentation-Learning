# TP-AEX-0005 Customer Support & Contact Us

## Objective & Scope

***

* **Dependency:** Pengujian modul ini berjalan secara independen dan tidak memiliki dependensi wajib ke modul otentikasi maupun katalog. Pengisian form kontak dapat dilakukan oleh pengguna anonim (guest) maupun pengguna terdaftar.
* **In-Scope:** Pengujian fungsional pada navigasi ke halaman Contact Us ([Automation Exercise - Contact Us](https://automationexercise.com/contact_us) ), pengisian form kontak (Name, Email, Subject, Message), pengunggahan berkas lampiran (Upload File), submit form beserta konfirmasi dialog pop-up JavaScript (Alert OK), verifikasi pesan sukses (Success! Your details have been submitted successfully.), serta navigasi kembali ke halaman utama melalui tombol Home.
* **Out-of-Scope:** Pengujian pengiriman email otomatis secara real-time ke inbox admin/server SMTP eksternal, pengujian batas waktu (timeout) koneksi server, serta verifikasi penerimaan tiket bantuan pada sistem Helpdesk/CRM pihak ketiga.

## Environment & Test Setup

***

* **Target URL:**[Automation Exercise - Contact Us](https://automationexercise.com/contact_us)
* **Browser/Platform:** Google Chrome (Latest Version) / Desktop.
* **Test Data Requirement:**
  * Data pengirim: Nama lengkap, format email valid (contoh: [user\_test@mail.com](mailto:user_test@mail.com)), subjek pesan, dan isi pesan teks.
  * Berkas lampiran uji: Menyiapkan file sampel berukuran ringan (contoh: file gambar JPG/PNG atau dokumen TXT/PDF dengan ukuran di bawah 2MB).
  * Variasi masukan invalid: Format email tanpa simbol @ atau tanpa domain, serta kondisi form kosong.

## Test Strategy & Approach

***

* **Positive Testing:** Mengisi seluruh field pada form Contact Us dengan data valid, melampirkan berkas sampel, menekan tombol Submit, menyetujui konfirmasi alert browser (JavaScript Popup Alert), memverifikasi kemunculan elemen pesan sukses, dan memastikan tombol Home mengarahkan pengguna kembali ke halaman utama dengan lancar.
* **Negative Path:** Mengosongkan field wajib (seperti Name, Email, atau Message), menginput format email yang tidak sesuai standar, serta mengunggah berkas lampiran yang tidak didukung atau berukuran sangat besar untuk memvalidasi mekanisme penolakan / error handling browser dan sistem.
* **Pop-Up & Navigation State Validation:** Memastikan sistem dapat menangani event dialog konfirmasi JavaScript (Alert OK/Cancel) secara otomatis pada skenario automasi, serta memastikan form terulang bersih (reset) setelah pengiriman berhasil.

## Risks & Dependencies

***

* **Dependencies:** Tidak ada dependensi ke modul lain.
* **Risks & Mitigation:**
  * _Risk:_ Dialog pop-up konfirmasi browser (JavaScript Alert) dapat memblokir jalannya alur pengujian otomatis (Test Automation execution) jika tidak ditangani dengan event listener/alert handling handler yang tepat.
  * _Mitigation:_ Pastikan skrip automasi pengujian telah mengimplementasikan penanganan alert (seperti driver.switchTo().alert().accept() atau page.on('dialog')) sebelum memicu tombol Submit.

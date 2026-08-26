# TP-AEX-0006 UI, Navigation & Footer Subscription

## Objective & Scope

***

* **Dependency:** Pengujian modul ini berjalan secara independen dan tidak memiliki dependensi wajib ke modul lain. Fitur navigasi, langganan email pada footer, dan fungsi gulir halaman dapat diakses langsung dari halaman utama maupun halaman pendukung lainnya.
* **In-Scope:** Pengujian fungsional pada navigasi ke halaman Test Cases ([Automation Practice Website for UI Testing - Test Cases](https://automationexercise.com/test_cases) ), validasi pendaftaran langganan newsletter (Subscription) di bagian footer pada Home Page dan Cart Page, verifikasi pesan konfirmasi sukses langganan (You have been successfully subscribed!), serta fungsionalitas tombol gulir ke atas (Scroll Up menggunakan tombol panah kanan bawah) dan gulir ke atas secara manual tanpa tombol.
* **Out-of-Scope:** Pengujian pengiriman email blast otomatis ke pelanggan newsletter, pengujian responsivitas tata letak UI di berbagai resolusi layar perangkat seluler/tablet (Mobile Responsiveness Testing), serta pengujian lintas peramban versi lama (Cross-Browser Legacy Testing).

## Environment & Test Setup

***

* **Target URL:**[Automation Exercise](https://automationexercise.com/)
* **Browser/Platform:** Google Chrome (Latest Version) / Desktop.
* **Test Data Requirement:**
  * Format email valid untuk langganan newsletter (contoh: [subscriber\_test@mail.com](mailto:subscriber_test@mail.com)).
  * Format email tidak valid tanpa simbol @ atau tanpa domain (contoh: subscriber\_invalid).

## Test Strategy & Approach

***

* **Positive Testing:** Menavigasi ke halaman Test Cases dan memastikan halaman berulang dengan judul/konten yang sesuai, melakukan gulir halaman ke bawah (scroll down) hingga bagian footer, menginput email valid pada kolom Subscription di Home Page maupun Cart Page, memverifikasi pesan sukses langganan, serta memvalidasi efek gulir kembali ke atas (scroll up) saat tombol panah ditekan atau gulir manual dilakukan hingga teks utama di bagian atas terlihat kembali.
* **Negative Path:** Menginput format email yang salah pada kolom langganan newsletter atau mengosongkan kolom input sebelum menekan tombol panah langganan untuk memvalidasi mekanisme penolakan / validasi HTML5 bawaan browser.
* **UI State & Scroll Behavior Validation:** Memastikan tombol panah Scroll Up muncul secara dinamis saat posisi halaman berada di paling bawah dan menghilang/berfungsi mengembalikan tampilan posisi layar (_viewport_) tepat ke bagian paling atas (_header/hero banner_).

## Risks & Dependencies

***

* **Dependencies:** Tidak ada dependensi ke modul lain.
* **Risks & Mitigation:**
  * _Risk:_ Elemen widget footer Subscription tertutup oleh iklan pihak ketiga (Google Ads overlay) sehingga gagal diinteraksi oleh skrip pengujian otomatis.
  * _Mitigation:_ Terapkan mekanisme pengabaian atau penutupan iframe iklan (_Ad-blocker / script injection_) pada tahapan persiapan tes automasi.

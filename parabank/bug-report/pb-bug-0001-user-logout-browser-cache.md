# PB-BUG-0001 \[User Logout] Browser Cache

## Document Details

***

Priority: P0

Severity: S0

## Description

***

Ditemukan celah keamanan ringan pada alur penghentian sesi. Setelah user logout, data sensitif pada halaman dashboard terakhir masih dapat diintip oleh orang lain yang melakukan akses ke laptop user dengan tombol Back pada browser.

## Pre-conditions

***

* User menggunakan browser Google Chrome desktop
* Pengguna sudah memiliki akun terdaftar dan dalam posisi login aktif di halaman dashboard.

## Step to Reproduce

***

1. Buka halaman dashboard utama ParaBank (Accounts Preview, Transfer Funds, dsb).
2. Klik tombol “Log Out” pada menu navigasi kiri.
3. Pastikan sistem mengarahkan kembali ke halaman depan/login.
4. Klik tombol “Back” (Kembali) pada navigasi bawaan browser Chrome.
5. Amati tampilan layar yang muncul.

## Expected vs Actual

***

Expected Result: Akses ditolak total, browser cache dibersihkan secara paksa, sehingga tombol Back tidak memunculkan data lama dan user tetap diminta login ulang.

Actual Result: Sesi di dalam server sudah mati, namun browser cache tidak dibersihkan, sehingga data saldo dan informasi dashboard terakhir masih dapat dilihat jika menggunakan fitur Back pada browser.

## Environment & Evidence

***

Environment: Production

Evidence:

* [https://drive.google.com/file/d/1jP4pSNFagyhKVojtNrQEPHLDusxfFWw5/view?usp=drive\_link](https://drive.google.com/file/d/1jP4pSNFagyhKVojtNrQEPHLDusxfFWw5/view?usp=drive_link)

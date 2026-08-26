# OHR-BUG-0005 \[Search & Custom Reporting] Unintuive Report Search Behavior

## Document Details

***

Priority: P3

Severity: S3

## Description

***

Fitur pencarian Laporan Kustom tidak mendukung free-text substring search. Pencarian gagal memfilter data jika user tidak mengeklik opsi dari dropdown suggestion.

## Pre-condition

***

1. User sudah login dengan akun Admin/HR Manager.
2. Berada di modul Reports (Laporan).
3. Sudah ada minimal 2-3 data kustom laporan di dalam database.

## Steps to Reproduce

***

1. Navigasi ke halaman 'Custom Reports'.
2. Ketik sebagian nama laporan pada kolom pencarian (contoh: "Leave").
3. Jangan klik opsi suggestion yang muncul di dropdown.
4. Tekan tombol 'Enter' atau klik tombol 'Search'.

## Expected vs Actual

***

Expected Result: Tabel otomatis memfilter dan menampilkan semua laporan yang mengandung kata kunci "Leave" (substring / %LIKE% matching).

Actual Result: Tabel tidak memfilter data apa pun / menampilkan pesan error karena sistem mewajibkan user untuk memilih nilai secara eksplisit dari dropdown suggestion.

## Environment & Evidence

***

**Environment:** Production

**Evidence:**

* [https://drive.google.com/file/d/1i8gtWz-KHGzBF-RW9BQ3A5p8cDx-ruEo/view?usp=sharing](https://drive.google.com/file/d/1i8gtWz-KHGzBF-RW9BQ3A5p8cDx-ruEo/view?usp=sharing)

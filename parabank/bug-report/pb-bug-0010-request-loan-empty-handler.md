# PB-BUG-0010 \[Request Loan] Empty Handler

## Document Details

***

Priority: P1

Severity: S1

## Description

***

Terjadi kegagalan penanganan validasi _field mandatory_ pada fitur **Request Loan**. Ketika pengguna mengajukan pinjaman dengan mengosongkan kolom _Down Payment_, sistem tidak mencegat _request_ di tingkat _client-side_ maupun _server-side validation_. Akibatnya, terjadi _unhandled exception_ di _backend_ yang mengembalikan _HTTP status 500_ dan menampilkan pesan kesalahan _generic_: _"An internal error has occurred and has been logged."_

## Pre-conditions

***

1. Pengguna telah _login_ ke dalam aplikasi ParaBank.
2. Memiliki setidaknya 1 rekening aktif.

## Steps to Reproduce

***

1. Navigasi ke menu **Request Loan** pada _sidebar_ sebelah kiri.
2. Masukkan jumlah pinjaman yang valid pada kolom **Loan Amount** (misal: `1000`).
3. **Biarkan kosong (empty/null)** pada kolom **Down Payment**.
4. Pilih rekening aktif pada dropdown **From Account**.
5. Klik tombol **Apply Now**.
6. Amati tampilan pesan kesalahan yang muncul di layar.

## Expected vs Actual

***

**Expected Result**

* Sistem memblokir pengajuan transaksi sebelum atau saat validasi formulir diproses.
* Tampil pesan kesalahan validasi yang informatif dan ramah pengguna (_user-friendly_), misalnya: _"Down Payment is required"_ atau _"Please fill in the Down Payment field"_.
* Pengguna tetap berada di halaman formulir tanpa mengalami _system crash_.

**Actual Result**

* Aplikasi mengalami _unhandled exception_ (Internal Server Error).
* Tampil pesan kesalahan sistem berwarna merah: _"An internal error has occurred and has been logged."_

## Environment & Evidence

***

**Environment:** Production

**Evidence:**

* [https://drive.google.com/file/d/1KSa7zCY0LRBzbjW0\_pFkiAlJvM62V7jY/view?usp=sharing](https://drive.google.com/file/d/1KSa7zCY0LRBzbjW0_pFkiAlJvM62V7jY/view?usp=sharing)

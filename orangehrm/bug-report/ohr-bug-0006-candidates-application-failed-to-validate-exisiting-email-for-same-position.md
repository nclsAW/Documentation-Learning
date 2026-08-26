# OHR-BUG-0006 \[Candidates Application] Failed to Validate Exisiting Email for Same Position

## Document Details

***

Priority: P1

Severity: S1

## Description

***

Sistem mengizinkan pendaftaran ganda (_duplicate registration_) ketika memasukkan kandidat baru dengan alamat email yang sudah terdaftar pada posisi/lowongan (_vacancy_) yang sama.

## Pre-condition

***

* Kandidat dengan alamat email tertentu sudah terdaftar sebelumnya pada lowongan (_vacancy_) yang sama.
* Pengguna berada di halaman **Add Candidates**.

## Steps to Reproduce

***

1. Masukkan **Full Name** lain (nama kandidat baru).
2. Pilih **Vacancy** yang sama dengan data kandidat yang sudah terdaftar.
3. Masukkan **Email** yang sama dengan email kandidat yang sudah terdaftar pada lowongan tersebut.
4. Klik tombol **Save**.

## Expected vs Actual

***

**Expected Result:** Sistem menolak pendaftaran ganda dan menampilkan pesan peringatan error (misal: _"Already exists"_ / _"Email already registered for this vacancy"_), serta data kandidat tidak tersimpan.

**Actual Result:** Sistem gagal menolak pendaftaran ganda (proses simpan berhasil / tidak menampilkan validator error yang sesuai, sehingga hasil pengujian dinyatakan **Gagal**).

## Environment & Evidence

***

**Environment:** Production

**Evidence:**

* [https://drive.google.com/file/d/1tvlt71Ml3HJBgGDac73DEYmVaUuBQ\_EQ/view?usp=sharing](https://drive.google.com/file/d/1tvlt71Ml3HJBgGDac73DEYmVaUuBQ_EQ/view?usp=sharing)

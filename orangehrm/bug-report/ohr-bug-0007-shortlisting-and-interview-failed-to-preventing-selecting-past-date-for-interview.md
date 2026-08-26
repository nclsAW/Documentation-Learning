# OHR-BUG-0007 \[Shortlisting & Interview] Failed to Preventing Selecting Past Date for Interview

## Document Details

***

Priority: P1

Severity: S1

## Description

***

Sistem gagal mencegah penjadwalan wawancara pada tanggal yang sudah berlalu (_past date_). Pengguna dapat menyimpan jadwal wawancara meskipun menggunakan tanggal di masa lalu tanpa munculnya blokir atau pesan error validasi dari sistem.

## Pre-condition

***

* Pengguna memiliki akses ke modul Recruitment / Schedule Interview.
* Pengguna berada di formulir penjadwalan wawancara (_Schedule Interview Form_).

## Steps to Reproduce

***

1. Isi kolom **Interview Title** dan **Interviewer** dengan data yang valid.
2. Pada kolom **Date**, masukkan tanggal kemarin atau tanggal lain di masa lalu (_past date_).
3. Klik tombol **Save**.

## Expected vs Actual

***

* **Expected Result:** Sistem menolak penjadwalan dan menampilkan _validation error message_ (misal: _"Should be a future date"_ / _"Invalid Date"_), serta data jadwal tidak tersimpan.
* **Actual Result:** Sistem mengizinkan penjadwalan pada tanggal yang telah berlalu (proses simpan berhasil tanpa menampilkan _validation error message_, sehingga hasil pengujian dinyatakan **Gagal**).

## Environment & Evidence

***

**Environment:** Production

**Evidence:**

* [https://drive.google.com/file/d/1grkKbEdEBPiVU1pB7T1Vdoq\_4HFXMGIa/view?usp=drive\_link](https://drive.google.com/file/d/1grkKbEdEBPiVU1pB7T1Vdoq_4HFXMGIa/view?usp=drive_link)

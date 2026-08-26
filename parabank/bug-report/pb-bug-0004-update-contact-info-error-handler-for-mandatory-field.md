# PB-BUG-0004 \[Update Contact Info] Error Handler for Mandatory Field

## Document Details

***

Priority: P1

Severity: S1

## Description

***

Sistem validasi form di beberapa area seperti pada halaman Update Contact Info tidak melakukan _trimming_ spasi dan gagal mendeteksi field kosong pada beberapa kolom _mandatory_. Akibatnya, user dapat mendaftar maupun memperbarui data menggunakan input berupa karakter spasi saja (`" "`) atau membiarkan field wajib dalam keadaan kosong tanpa muncul peringatan validasi (kecuali pada field _Phone #_).

## Pre-conditions

***

1. User mengakses halaman Update Contact Info dengan akun yang terdaftar
2. User berada di masing-masing halaman form target.

## Steps to Reproduce

***

1. Pada field mandatory (Nama, Alamat, dll), masukkan karakter spasi (`" "`) atau biarkan kosong.
2. Kosongkan semua field mandatory lainnya.
3. Klik tombol **"Update Contact"**.

## Expected vs Actual

***

**Expected Result:**

* Semua _field mandatory_ wajib memotong spasi (_trim_) sebelum validasi.
* Sistem menolak _submit_ jika input hanya berupa spasi atau kosong.
* Menampilkan pesan peringatan validasi pada masing-masing field: _"Field ini wajib diisi dan tidak boleh hanya berisi spasi"_.

**Actual Result:**

* Form berhasil di-_submit_ tanpa ada peringatan _error_ sama sekali (kecuali field _Phone #_).
* Data kosong/spasi berhasil tersimpan ke sistem.

## Environment & Evidence

***

**Environment:** Production

**Evidence:**

* [https://drive.google.com/file/d/1wX-xu7-MyPLnff2w4Y7iFqpSGxJxwKvq/view?usp=drive\_link](https://drive.google.com/file/d/1wX-xu7-MyPLnff2w4Y7iFqpSGxJxwKvq/view?usp=drive_link)
* [https://drive.google.com/file/d/1BGcyBeu-0gdV2Vzdgf5U3fbO5HY2i-5c/view?usp=drive\_link](https://drive.google.com/file/d/1BGcyBeu-0gdV2Vzdgf5U3fbO5HY2i-5c/view?usp=drive_link)

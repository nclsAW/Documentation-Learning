# PB-BUG-0003 \[Authentication - Register] Missing Whitespace Validation on Mandatory Fields

## Document Details

***

Priority: P1

Severity: S1

## Description

***

Sistem validasi form di beberapa area aplikasi Registrasi tidak melakukan _trimming_ spasi dan gagal mendeteksi field kosong pada beberapa kolom _mandatory_. Akibatnya, user dapat mendaftar maupun memperbarui data menggunakan input berupa karakter spasi saja (`" "`) atau membiarkan field wajib dalam keadaan kosong tanpa muncul peringatan validasi (kecuali pada field _Phone #_).

## Pre-conditions

***

1. User mengakses halaman Registrasi
2. User berada di masing-masing halaman form target.

## Steps to Reproduce

***

1. Buka halaman Registrasi.
2. Pada field mandatory (Nama, Alamat, dll), masukkan karakter spasi (`" "`) atau biarkan kosong.
3. Kosongkan semua field mandatory lainnya.
4. Klik tombol **"Register"**.

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
* [https://drive.google.com/file/d/15rJTE2y9Bzal2DdPeIIF\_NRlTX505oO0/view?usp=sharing](https://drive.google.com/file/d/15rJTE2y9Bzal2DdPeIIF_NRlTX505oO0/view?usp=sharing)

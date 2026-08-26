# OHR-BUG-0004 \[User Management] Failed to Validate Existing Username in Each Account

## Document Details

***

Priority: P1

Severity: S1

## Description

***

Pada modul _User Management_, sistem gagal melakukan validasi keberadaan akun (_existing user/username check_) untuk karyawan yang telah memiliki akun sebelumnya. Sistem mengizinkan pembuatan akun baru dengan _User Role_ ESS menggunakan karyawan yang sama ("Tester Tester"), sehingga terjadi duplikasi pembuatan akun untuk satu karyawan (_duplicate account assignment_).

## Pre-conditions

***

* User terautentikasi dan login sebagai **System Admin**.
* Karyawan dengan nama **"Tester Tester"** sudah terdaftar di sistem PIM dan **sudah memiliki akun User aktif**.

## Steps to Reproduce

***

1. Navigasi ke menu **Admin** -> **User Management** -> **Users**.
2. Klik tombol **Add** untuk menambah User baru.
3. Pilih **User Role**: `ESS`.
4. Ketik dan pilih **Employee Name**: `"Tester Tester"`.
5. Isi field **Username** dan **Password** baru.
6. Klik tombol **Save**.

## Expected vs Actual

***

#### **Expected Result**

Sistem menolak pembuatan akun ganda untuk karyawan yang sama dan menampilkan pesan error validasi (misal: _"Employee already has a user account"_).

#### **Actual Result**

Sistem menerima inputan tersebut, tidak memblokir proses simpan, dan berhasil membuat akun ganda (_duplicate account_) untuk karyawan **"Tester Tester"**.

## Environment & Evidence

***

**Environemnt:** Production

**Evidence:**

* [https://drive.google.com/file/d/1Jn8tQy6oPeIun9AJTuzMWGu37GfdgtBl/view?usp=drive\_link](https://drive.google.com/file/d/1Jn8tQy6oPeIun9AJTuzMWGu37GfdgtBl/view?usp=drive_link)

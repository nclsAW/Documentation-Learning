# OHR-BUG-0003 \[Job Titles] Failed to Validate Existing Employee in the Job Title

## Document Details

***

Priority: P1

Severity: S1

## Description

***

Pada modul Job Titles di OrangeHRM, sistem mengizinkan pengguna untuk menghapus Job Title yang saat ini masih terikat aktif dengan satu atau lebih data karyawan (Employee). Sistem tidak memblokir atau menampilkan pesan pencegahan integrity constraint, sehingga data Job Title tetap terhapus dari database dan berpotensi menyebabkan data karyawan menjadi inkonsisten (orphaned record).

## Pre-condition

***

* User terautentikasi dan login ke OrangeHRM sebagai System Admin.
* Terdapat minimal satu Job Title (contoh: "Software Engineer") yang terhubung/digunakan oleh minimal satu data karyawan aktif (Employee).

## Steps to Reproduce

***

1. Navigasi ke menu Admin -> Job -> Job Titles.
2. Cari dan centang/pilih Job Title yang sedang terikat dengan karyawan (contoh: "Software Engineer").
3. Klik tombol Delete Selected (atau ikon Tong Sampah pada baris terkait).
4. Pada pop-up konfirmasi dialog, klik Yes, Delete.

## Expected vs Actual

***

#### **Expected Result**

Sistem seharusnya menolak/memblokir proses penghapusan dan menampilkan pesan peringatan/pencegahan (misal: _"Cannot delete Job Title because it is assigned to one or more employees"_), sehingga data _Job Title_ tetap aman dan tersimpan di dalam sistem.

#### **Actual Result**

Sistem berhasil mengeksekusi proses penghapusan, menampilkan pesan _Toast/Notification_ sukses, dan menghapus _Job Title_ tersebut dari daftar, meskipun data karyawan terkait masih ada.

## Enviroment & Evidence

***

**Environment:** Production

**Evidence:**

* [https://drive.google.com/open?id=1h9UduQDWCiaFASW4sLECeltwxIhrN8hC\&usp=drive\_fs](https://drive.google.com/open?id=1h9UduQDWCiaFASW4sLECeltwxIhrN8hC\&usp=drive_fs)

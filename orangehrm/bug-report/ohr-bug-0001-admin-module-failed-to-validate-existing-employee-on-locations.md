# OHR-BUG-0001 \[Admin Module] Failed to Validate Existing Employee on Locations

## Document Details

***

Priority: P1

Severity: S1

## Description

***

Saat melakukan penghapusan lokasi di modul _Organization Locations_, sistem secara otomatis memblokir proses penghapusan dan memunculkan pesan peringatan apabila lokasi tersebut masih terikat dengan data karyawan (_Employee_). Berdasarkan spesifikasi/kebutuhan yang diharapkan, sistem seharusnya tetap mengizinkan aksi hapus tersebut dan secara sukses menghapus lokasi target beserta keterikatannya pada data karyawan tanpa tertolak oleh validasi sistem.

## Pre-condition

***

* User terautentikasi dan login sebagai System Admin.
* Terdapat setidaknya satu data lokasi (contoh: Lokasi B) yang sudah terhubung/terikat dengan data karyawan (_Employee_).

## Steps to Reproduce

***

1. Navigasi ke menu Admin -> Organization -> Locations.
2. Cari Lokasi B lalu klik tombol Delete (Hapus).

## Expected vs Actual

***

#### **Expected Result**

Sistem berhasil menghapus Lokasi B secara menyeluruh beserta keterikatan data karyawannya, tanpa memunculkan pesan pencegahan atau membatalkan aksi hapus.

#### **Actual Result**

Sistem menolak proses penghapusan dan menampilkan pesan pencegahan/peringatan bahwa lokasi tidak dapat dihapus karena masih terikat dengan data lain.

## Environment & Evidence

***

**Environment:** Production

**Evidence:**

* [https://drive.google.com/open?id=1m6wx173AY5Id\_Ozhp59NNMR6lpCj\_xad\&usp=drive\_fs](https://drive.google.com/open?id=1m6wx173AY5Id_Ozhp59NNMR6lpCj_xad\&usp=drive_fs)

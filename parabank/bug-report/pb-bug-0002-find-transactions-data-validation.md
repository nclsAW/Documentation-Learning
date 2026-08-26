# PB-BUG-0002 \[Find Transactions] Data Validation

## Document Details

***

Priority: P2

Severity: S3

## Description

***

Sistem tidak menampilkan pesan peringatan (_error handler_ / _empty state_) ketika _user_ melakukan pencarian atau _filtering_ menggunakan data fiktif (data yang tidak terdapat di database). Sistem hanya menampilkan tabel kosong tanpa _feedback_ apapun. Masalah ini ditemukan pada tiga skenario pengujian (Test ID) dengan akar masalah yang sama.

## Pre-conditions

***

1. _User_ sudah memiliki akses ke halaman \[Sebutkan nama halamannya, misal: _Find Transactions / Search_] di sistem ParaBank.
2. Tidak ada data transaksi/record yang cocok dengan kriteria pencarian fiktif yang akan digunakan.

## Steps to Reproduce

***

* Buka halaman \[Sebutkan nama halamannya, misal: _Find Transactions_].
* Pada form pencarian/filter, masukkan data fiktif yang dipastikan tidak ada di database (Lakukan secara bergiliran untuk 3 kriteria dari Test ID terkait, misal: ID Transaksi tidak valid, Tanggal yang tidak valid, atau Nominal fiktif).
* Klik tombol **\[Search / Filter / Find]**.
* Perhatikan respon dari sistem pada bagian tabel hasil pencarian.

## Expected vs Actual

***

**Expected Result:** Sistem berhasil menangani validasi negatif tanpa _crash_ dan menampilkan pesan informatif di area tabel hasil pencarian, seperti _"Data tidak ditemukan"_, _"No transactions found"_, atau _feedback_ lain yang relevan.

**Actual Result:** Sistem tidak _crash_ (berhasil menahan _error_), tetapi gagal menampilkan pesan peringatan. Sistem hanya menampilkan struktur tabel yang kosong melompong, sehingga membingungkan _user_ terkait status pencarian.

## Environment & Evidence

***

**Environment:** Production

**Evidence:**

* [https://drive.google.com/file/d/1JY1GE4tpArn\_iSqiHnG2X9s8lVLOvHaL/view?usp=sharing](https://drive.google.com/file/d/1JY1GE4tpArn_iSqiHnG2X9s8lVLOvHaL/view?usp=sharing)

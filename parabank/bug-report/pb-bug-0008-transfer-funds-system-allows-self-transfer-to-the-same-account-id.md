# PB-BUG-0008 \[Transfer Funds] System Allows Self-Transfer to the Same Account ID

## Document Details

***

Priority: P1

Severity: S1

## Description

***

Fitur transfer dana tidak memiliki validasi untuk mencegah pengguna memilih sumber rekening (_From Account_) dan rekening tujuan (_To Account_) yang sama. Sistem mengizinkan transaksi transfer ke rekening sendiri diproses hingga sukses, yang menghasilkan log transaksi redundant tanpa perubahan saldo riil.

## Pre-conditions

***

1. Pengguna telah _login_ ke dalam sistem ParaBank.
2. Memiliki setidaknya 1 rekening aktif (misal: Rekening A).

## Steps to Reproduce

***

1. Navigasi ke menu **Transfer Funds**.
2. Masukkan nominal transfer yang valid (misal: `$100`).
3. Pilih **Rekening A** pada dropdown _From Account_.
4. Pilih **Rekening A** yang sama pada dropdown _To Account_.
5. Klik tombol **Transfer**.
6. Amati respon sistem dan histori transaksi.

## Expected vs Actual

***

**Expected Result**

* Transaksi **ditolak** oleh sistem sebelum tombol submit diproses atau saat validasi request.
* Tampil pesan kesalahan yang relevan, misalnya: _"Source and destination accounts cannot be the same"_.
* Tidak ada request transfer yang dikirim/diproses ke server.

**Actual Result**

* Transaksi **berhasil diproses** (_Success message_ muncul).
* Sistem melakukan proses pemotongan dan penambahan dana ke akun yang sama.
* Terbuat entri log transaksi baru yang sebenarnya tidak perlu (_redundant entry_).

## Environment & Evidence

***

**Environment:** Production

**Evidence:**

* [https://drive.google.com/file/d/1Y9hBb9eUwXKMNkqHWBjqhO6DOaxRueWi/view?usp=sharing](https://drive.google.com/file/d/1Y9hBb9eUwXKMNkqHWBjqhO6DOaxRueWi/view?usp=sharing)

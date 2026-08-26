# PB-BUG-0006 \[Transfer Funds] Insufficient Transfer Funds

## Document Details

***

Priority: P0

Severity: S0

## Description

***

Terjadi kegagalan validasi _server-side_ pada fitur transfer bank ketika Pengguna melakukan transfer dengan nominal yang melebihi jumlah saldo yang tersedia. Sistem tetap memproses transaksi hingga selesai, menambah saldo ke rekening penerima, dan mengubah saldo rekening pengirim menjadi bernilai negatif (minus).

## Pre-conditions

***

1. Pengguna telah _login_ ke akun ParaBank.
2. Rekening A (Pengirim) memiliki saldo aktif kurang dari $100 (misal: $100).
3. Rekening B (Penerima) dalam kondisi aktif dan siap menerima dana.

## Steps to Reproduce

***

1. Navigasi ke menu **Transfer Funds**.
2. Masukkan jumlah transfer sebesar **$500** pada kolom _Amount_.
3. Pilih **Rekening A** pada dropdown _From Account_ (saldo: $100).
4. Pilih **Rekening B** pada dropdown _To Account_.
5. Klik tombol **Transfer**.
6. Amati pesan konfirmasi transaksi dan periksa sisa saldo pada menu **Accounts Overview**.

## Expected vs Actual

***

**Expected Result**

* Transaksi **ditolak** oleh sistem.
* Tampil pesan kesalahan (error message) yang relevan, misalnya: _"Transfer failed: Insufficient funds in the selected account"_.
* Saldo pada Rekening A dan Rekening B tidak mengalami perubahan.

**Actual Result**

* Transaksi **berhasil diproses** tanpa ada blokir atau instruksi konfirmasi _overdraft_.
* Saldo Rekening A berkurang secara terbalik menjadi **-$400** (minus).
* Saldo Rekening B tetap bertambah sebesar **$500**.

## Environment & Evidence

***

**Environment:** Production

**Evidence:**

* [https://drive.google.com/file/d/1ElxeEoMmat0QzzmBFyiw1Bo98zEMzSXR/view?usp=sharing](https://drive.google.com/file/d/1ElxeEoMmat0QzzmBFyiw1Bo98zEMzSXR/view?usp=sharing)

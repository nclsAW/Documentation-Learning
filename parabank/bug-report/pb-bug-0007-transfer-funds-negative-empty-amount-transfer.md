# PB-BUG-0007 \[Transfer Funds] Negative/Empty Amount Transfer

## Document Details

***

Priority: P0

Severity: S0

## Description

***

Terjadi kegagalan validasi _input/nominal validation_ pada fitur transfer bank ketika Pengguna memasukkan angka bernilai negatif (misal: `-10000`). Sistem memproses nilai negatif tersebut dengan logika matematika dasar tanpa filter, sehingga menyebabkan saldo Rekening Pengirim (Rekening B) bertambah, sedangkan saldo Rekening Penerima (Rekening A) justru terpotong/menjadi minus seolah-olah ditagih utang.

## Pre-conditions

***

1. Pengguna telah _login_ ke dalam sistem ParaBank.
2. Memiliki akses ke Rekening B (sebagai Pengirim) dan Rekening A (sebagai Penerima).
3. Saldo awal pada kedua rekening bernilai positif/normal.

## Steps to Reproduce

***

1. Navigasi ke menu Transfer Funds.
2. Masukkan nominal angka negatif sebesar `-10000` pada kolom _Amount_.
3. Pilih Rekening B pada dropdown _From Account_ (Pengirim).
4. Pilih Rekening A pada dropdown _To Account_ (Penerima).
5. Klik tombol Transfer.
6. Amati mutasi saldo pada menu Accounts Overview.

## Expected vs Actual

***

**Expected Result**

* Transaksi **ditolak** oleh sistem pada saat validasi formulir.
* Tampil pesan kesalahan (error message) yang relevan, misalnya: _"Invalid amount. Amount must be greater than zero"_.
* Saldo pada Rekening B maupun Rekening A tidak berubah sama sekali.

**Actual Result**

* Transaksi **berhasil diproses** tanpa adanya validasi angka negatif.
* Akibat operasi matematika terbalik (`Saldo + (-Nominal)`), saldo **Rekening B** (Pengirim) justru bertambah sebesar **+$10,000**.
* Saldo **Rekening A** (Penerima) justru berkurang/terpotong sebesar **-$10,000** (menjadi utang/minus).

## Environment & Evidence

***

**Environment:** Production

**Evidence:**

* [https://drive.google.com/file/d/1OFfIJDxqx3-5PmYGEKQOyHY\_cDw1CS3Q/view?usp=sharing](https://drive.google.com/file/d/1OFfIJDxqx3-5PmYGEKQOyHY_cDw1CS3Q/view?usp=sharing)

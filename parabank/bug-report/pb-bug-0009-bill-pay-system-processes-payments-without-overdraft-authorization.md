# PB-BUG-0009 \[Bill Pay] System Processes Payments Without Overdraft Authorization

## Document Details

***

Priority: P1

Severity: S1

## Description

***

Terjadi kegagalan validasi _server-side_ pada fitur Pembayaran Tagihan (_Bill Pay_). Sistem tetap memproses transaksi pembayaran tagihan meskipun nominal pembayaran melebihi saldo aktif yang tersedia pada rekening sumber. Akibatnya, transaksi dinyatakan berhasil dan saldo rekening pengguna terpotong hingga bernilai negatif (minus).

## Pre-conditions

***

1. Pengguna telah _login_ ke dalam sistem ParaBank.
2. Memiliki rekening aktif dengan saldo terbatas (misal: Saldo = $100).
3. Memiliki data tagihan (_payee_) yang valid dengan jumlah tagihan melebihi saldo (misal: Tagihan = $500).

## Steps to Reproduce

***

1. Navigasi ke menu Bill Pay.
2. Lengkapi formulir _Payee Information_ (Nama, Alamat, Nomor Rekening Tujuan/Payee).
3. Masukkan nominal tagihan sebesar $500 pada kolom _Amount_.
4. Pilih rekening sumber yang hanya memiliki saldo $100 pada dropdown _From Account_.
5. Klik tombol Send Payment.
6. Periksa pesan respon dan status saldo pada menu Accounts Overview.

## Expected vs Actual

***

**Expected Result**

* Transaksi **ditolak** oleh sistem saat validasi pembayaran.
* Tampil pesan kesalahan yang relevan, misalnya: _"Payment failed: Insufficient funds in the selected account"_.
* Saldo rekening tidak berkurang dan pembayaran tagihan tidak diproses.

**Actual Result**

* Transaksi **berhasil diproses** (_"Bill Payment Complete"_).
* Saldo rekening sumber terpotong secara otomatis menjadi **-$400** (minus).

## Environment & Evidence

***

**Environment:** Production

**Evidence:**

* [https://drive.google.com/file/d/1KzwzzKo-dcPW4E7\_fxbVqRmFUu7s8Erf/view?usp=sharing](https://drive.google.com/file/d/1KzwzzKo-dcPW4E7_fxbVqRmFUu7s8Erf/view?usp=sharing)

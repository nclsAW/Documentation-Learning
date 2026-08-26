# PB-BUG-0005 \[Open New Account] Insufficient Funds

## Document Details

***

Priority: P1

Severity: S1

## Description

***

Ketika pengguna mencoba membuka akun baru di ParaBank dan mendanainya dengan mentransfer uang sebesar $100 dari rekening yang sudah ada yang memiliki **saldo minus**, sistem berhasil memproses permintaan tersebut. Akun baru berhasil dibuat dengan saldo positif, sedangkan saldo minus pada rekening sumber semakin bertambah hutangnya. Sistem gagal memvalidasi apakah rekening sumber memiliki dana yang cukup sebelum mengizinkan transfer.

## Pre-conditions

***

1. Pengguna sudah terdaftar dan berhasil masuk (_login_) ke aplikasi ParaBank.
2. Pengguna memiliki minimal satu rekening aktif yang posisinya **saldo minus** (contoh: Rekening #12345 dengan saldo -$50).

## Steps to Reproduce

***

1. Buka menu **"Open New Account"** (Buka Akun Baru) pada panel navigasi di sebelah kiri.
2. Pilih jenis akun yang ingin dibuka (misalnya: _Savings_ atau _Checking_).
3. Pada bagian penentuan dana, cari menu _dropdown_ **"from account #"** (dari rekening nomor).
4. Pilih nomor rekening yang saat ini memiliki **saldo minus**.
5. Klik tombol **"Open New Account"**.
6. Periksa saldo pada akun yang baru saja dibuat dan juga akun sumber.

## Expected vs Actual

***

*   **Expected Result:**

    Sistem harus menolak pembuatan akun baru dan menampilkan pesan error (misalnya: _"Transaction Failed: Insufficient funds in the source account"_ atau _"Transaksi Gagal: Dana di rekening sumber tidak mencukupi"_). Tidak boleh ada akun baru yang terbentuk dan tidak boleh ada transfer dana dari rekening bersaldo minus.
*   **Actual Result:**

    Sistem berhasil membuat akun baru tersebut. Akun baru menerima saldo sebesar $100, dan rekening sumber yang bersaldo minus tadi nilainya semakin berkurang/berhutang sebesar $100 lagi (misal: dari -$50 menjadi -$150), sehingga memicu akumulasi hutang yang tidak sah.

## Environment & Evidence

***

**Environment:** Production

**Evidence:**

* [https://drive.google.com/file/d/1jZMdQvAGP8BUQIRL\_nmawgENnP8S-REU/view?usp=drive\_link](https://drive.google.com/file/d/1jZMdQvAGP8BUQIRL_nmawgENnP8S-REU/view?usp=drive_link)

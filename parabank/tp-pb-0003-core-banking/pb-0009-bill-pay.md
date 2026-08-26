# PB-0009 Bill Pay

## User Story

***

Sebagai nasabah, saya ingin membayar tagihan ke pihak ketiga agar kewajiban finansial saya terselesaikan langsung dari sistem bank.

## Pre-condition

***

Pengguna memiliki saldo yang mencukupi untuk melakukan pembayaran tagihan.

## Acceptance Criteria

***

* Pembayaran berhasil diproses ketika semua data Payee (nama, alamat, rekening) dan nominal diisi dengan valid.
* Sistem menampilkan error dan menghentikan proses jika infornmasi esensial (seperti nomor rekening tujuan atau nama Payee) tidak diisi.
* Saldo rekening pengirim langsung terpotong secara akurat setelah status pembayaran sukses.

## Test Scenario

***

| **TP**     | **Scene ID** | **Test ID** | **Type** | **Priority** | **AC Ref** | **Pre-condition**                                        | **Step**                                                                                                                                               | **Expected**                                                                         | **Actual**                                                                                                | **Status** | **Notes**                                                                                                                                                        |
| ---------- | ------------ | ----------- | -------- | ------------ | ---------- | -------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------- | ---------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| TP-PB-0003 | PB-CB-0002   | PB-BP-0001  | POS      | P1           | 1,3        | User login dan memiliki saldo rekening yang mencukupi.   | <ol start="1"><li>Akses halaman Bill Pay</li><li>Isi Data Payee yang valid</li><li>Pilih akun yang akan membayar</li><li>Klik “Send Payment”</li></ol> | Transaksi sukses, konfirmasi pembayaran muncul, dan saldo pengirim terpotong akurat. | As Expected                                                                                               | PASSED     |                                                                                                                                                                  |
| TP-PB-0003 | PB-CB-0002   | PB-BP-0002  | NEG      | P1           | 2          | User login dan berada pada menu Bill Pay.                | Kosongkan field Payee Name lalu kirim formulir pembayaran.                                                                                             | Sistem menolak transaksi dan menampilkan pesan error field wajib diisi.              | As Expected                                                                                               | PASSED     |                                                                                                                                                                  |
| TP-PB-0003 | PB-CB-0002   | PB-BP-0003  | NEG      | P1           | 2          | User login dan berada pada menu Bill Pay.                | Kosongkan field Account / Verify Account lalu kirim formulir pembayaran.                                                                               | Sistem memblokir proses dan menampilkan peringatan nomor rekening wajib diisi.       | As Expected                                                                                               | PASSED     |                                                                                                                                                                  |
| TP-PB-0003 | PB-CB-0002   | PB-BP-0004  | NEG      | P2           | 2          | User login dan berada pada menu Bill Pay.                | Isi nomor rekening dan Verify Account dengan nilai yang berbeda.                                                                                       | Transaksi ditolak karena konfirmasi nomor rekening tujuan tidak sesuai.              | As Expected                                                                                               | PASSED     |                                                                                                                                                                  |
| TP-PB-0003 | PB-CB-0002   | PB-BP-0005  | NEG      | P1           | 1,3        | User login dan mengetahui total saldo rekening pengirim. | Kirim pembayaran tagihan dengan nominal melebihi sisa saldo yang ada.                                                                                  | Transaksi gagal diproses dan sistem menampilkan error saldo tidak mencukupi.         | Transaksi tetap dilanjutkan meski saldo pengguna tidka mencukupi dan saldo pengirim berubah menjadi minus | FAILED     | [KAN-30: PB-BUG-0009 \[Bill Pay\] System Processes Payments Without Overdraft Authorization \[ParaBank\]Bug Report](https://alldocs.atlassian.net/browse/KAN-30) |
| TP-PB-0003 | PB-CB-0002   | PB-BP-0006  | NEG      | P2           | 1          | User login dan berada pada menu Bill Pay.                | Isi field nominal menggunakan karakter huruf atau simbol khusus.                                                                                       | Form menolak submit dan menampilkan error format nominal harus valid/angka.          | As Expected                                                                                               | PASSED     |                                                                                                                                                                  |

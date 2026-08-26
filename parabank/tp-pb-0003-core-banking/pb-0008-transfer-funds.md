# PB-0008 Transfer Funds

## User Story

***

Sebagai nasabah, saya ingin mentransfer dana antar rekening internal agar dapat mengatur likuiditas keuangan saya.

## Pre-condition

***

Pengguna memiliki minimal dua nomor rekening yang berbeda di dalam satu akun.

## Acceptance Criteria

***

* Dana berhasil dipindahkan, saldo pada rekening asal berkurang dan rekening tujuan bertambah sesuai dengan nominal transfer.
* Sistem menolak transaksi jika nominal transfer yang dimasukkan melebihi total saldo yang tersedia di rekening asal.
* Sistem memvalidasi input agar hanya menerima format angka pada field nominal transfer.

## Test Scenario

***

| **TP**     | **Scene ID** | **Test ID** | **Type** | **Priority** | **AC Ref** | **Pre-condition**                                                                        | **Step**                                                         | **Expected**                                                      | **Actual**                                                                                     | **Status** | **Notes**                                                                                                                                                       |
| ---------- | ------------ | ----------- | -------- | ------------ | ---------- | ---------------------------------------------------------------------------------------- | ---------------------------------------------------------------- | ----------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- | ---------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| TP-PB-0003 | PB-CB-0001   | PB-TF-0001  | POS      | P1           | 1          | User login dengan dua rekening aktif, mengakses menu Transfer Funds, dan saldo mencukupi | Transfer nominal valid ke rekening tujuan yang berbeda           | Transaksi sukses, saldo asal berkurang dan saldo tujuan bertambah | As Expected                                                                                    | PASSED     |                                                                                                                                                                 |
| TP-PB-0003 | PB-CB-0001   | PB-TF-0002  | NEG      | P1           | 2          | User login dengan dua rekening aktif, mengakses menu Transfer Funds                      | Transfer nominal yang melebihi sisa saldo rekening asal          | Transaksi ditolak dengan pesan error saldo tidak mencukupi        | Transfer dilanjutkan, dan nominal pengirim dikurangi dan dibuat minus jika sudah melebihi.     | FAILED     | [KAN-27: PB-BUG-0006 \[Transfer Funds\] Insufficient Transfer Funds \[ParaBank\]Bug Report](https://alldocs.atlassian.net/browse/KAN-27)                        |
| TP-PB-0003 | PB-CB-0001   | PB-TF-0003  | NEG      | P2           | 3          | User login dan berada pada menu Transfer Funds.                                          | Transfer menggunakan input karakter huruf pada field nominal.    | Sistem menolak submit dan menampilkan pesan error                 | As Expected                                                                                    | PASSED     |                                                                                                                                                                 |
| TP-PB-0003 | PB-CB-0001   | PB-TF-0004  | NEG      | P2           | 3          | User login dan berada pada menu Transfer Funds.                                          | Transfer menggunakan input karakter simbol pada field nominal.   | Sistem menolak submit dan menampilkan error format tidak valid.   | As Expected                                                                                    | PASSED     |                                                                                                                                                                 |
| TP-PB-0003 | PB-CB-0001   | PB-TF-0005  | NEG      | P2           | 2,3        | User login dan berada pada menu Transfer Funds.                                          | Transfer menggunakan nominal bernilai nol atau angka negatif.    | Transaksi ditolak dengan peringatan nominal wajib lebih dari nol. | Transaksi dilanjutkan dan saldo penerima disedot saat nominal pengirim minus                   | FAILED     | [KAN-28: PB-BUG-0007 \[Transfer Funds\] Negative/Empty Amount Transfer \[ParaBank\]Bug Report](https://alldocs.atlassian.net/browse/KAN-28)                     |
| TP-PB-0003 | PB-CB-0001   | PB-TF-0006  | NEG      | P3           | 1          | User login dengan minimal satu rekening aktif.                                           | Transfer nominal valid dengan memilih rekening tujuan yang sama. | Sistem menolak transaksi karena rekening asal dan tujuan identik. | Sistem berhasil melanjutkan proses transfer dan saldo yang digunakan tidak berubah sama sekali | FAILED     | [KAN-29: PB-BUG-0008 \[Transfer Funds\] System Allows Self-Transfer to the Same Account ID \[ParaBank\]Bug Report](https://alldocs.atlassian.net/browse/KAN-29) |

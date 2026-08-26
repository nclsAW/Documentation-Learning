# PB-0010 Request Loan

## User Story

***

Sebagai nasabah, saya ingin mengajukan pinjaman dana agar mendapatkan tambahan modal untuk kebutuhan finansial.

## Pre-condition

***

Pengguna dalam status logged in dan berada di halaman pengajuan pinjaman.

## Acceptance Criteria

***

* Sistem secara otomatis menyetujui (Approved) dan membuatkan rekening pinjaman baru jika parameter nominal pinjaman dan Down Payment proporsional/memenuhi syarat.
* Sistem menolak (Rejected) pengajuan pinjaman jika nominal Down Payment terlalu rendah.
* Dana pinjaman yang disetujui langsung ditambahkan ke saldo rekening utama nasabah.

## Test Scenario

***

| **TP**     | **Scene ID** | **Test ID** | **Type** | **Priority** | **AC Ref** | **Pre-condition**                             | **Step**                                                                          | **Expected**                                                                   | **Actual**                                                   | **Status** | **Notes**                                                                                                                    |
| ---------- | ------------ | ----------- | -------- | ------------ | ---------- | --------------------------------------------- | --------------------------------------------------------------------------------- | ------------------------------------------------------------------------------ | ------------------------------------------------------------ | ---------- | ---------------------------------------------------------------------------------------------------------------------------- |
| TP-PB-0003 | PB-CB-0003   | PB-RL-0001  | POS      | P1           | 1,3        | User login dan berada pada menu Request Loan. | Ajukan pinjaman dengan persentase Down Payment yang memadai.                      | Pinjaman disetujui, rekening pinjaman baru dibuat, dan saldo utama bertambah.  | As Expected                                                  | PASSED     |                                                                                                                              |
| TP-PB-0003 | PB-CB-0003   | PB-RL-0002  | NEG      | P1           | 2          | User login dan berada pada menu Request Loan. | Ajukan pinjaman dengan nominal Down Payment yang sangat kecil/tidak proporsional. | Pengajuan pinjaman statusnya ditolak (Rejected) dan saldo utama tidak berubah. | As Expected                                                  | PASSED     |                                                                                                                              |
| TP-PB-0003 | PB-CB-0003   | PB-RL-0003  | NEG      | P2           | 2          | User login dan berada pada menu Request Loan. | Kosongkan atau isi nilai nol pada field Down Payment lalu submit.                 | Sistem memblokir pengajuan dan menampilkan error kewajiban pengisian DP.       | Sistem memblokir pengajuan tapi error handlingnya berlebihan | FAILED     | [KAN-31: PB-BUG-0010 \[Request Loan\] Empty Handler \[ParaBank\]Bug Report](https://alldocs.atlassian.net/browse/KAN-31)     |
| TP-PB-0003 | PB-CB-0003   | PB-RL-0004  | NEG      | P2           | 1          | User login dan berada pada menu Request Loan. | Isi field nominal pinjaman menggunakan huruf atau simbol khusus.                  | Form menolak submit dan menampilkan error format nominal harus angka.          | Sistem menolak submit dan mengalami internal error.          | FAILED     | [KAN-32: PB-BUG-0011 \[Request Loan\] Character Handler \[ParaBank\]Bug Report](https://alldocs.atlassian.net/browse/KAN-32) |
| TP-PB-0003 | PB-CB-0003   | PB-RL-0005  | NEG      | P2           | 1          | User login dan berada pada menu Request Loan. | Isi field Loan Amount atau Down Payment dengan angka negatif.                     | Transaksi ditolak oleh sistem karena nilai input bernilai tidak valid.         | As Expected                                                  | PASSED     |                                                                                                                              |

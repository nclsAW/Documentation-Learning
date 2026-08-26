# PB-0007 Open New Account

## User Story

***

Sebagai nasabah, saya ingin membuka rekening baru (Checking/Savings) agar dapat mengalokasikan dan memisahkan dana secara spesifik.

## Pre-condition

***

Pengguna sudah login dan memiliki setidaknya satu rekening utama yang memiliki saldo awal.

## Acceptance Criteria

***

* Sistem berhasil men-generate nomor rekening baru sesuai dengan tipe rekening yang dipilih.
* Sistem berhasil memindahkan dana awal (minimum deposit) dari rekening sumber ke rekening baru secara akurat dan real-time.

## Test Scenario

***

| **TP**     | **Scene ID** | **Test ID** | **Type** | **Priority** | **AC Ref** | **Pre-conditions**               | **Step**                                                                                                                                                                                                                                                                                                                                                                     | **Expected**                                                                                                                                                                       | **Actual**                                                                                           | **Status** | **Notes**                                                                                                                         |
| ---------- | ------------ | ----------- | -------- | ------------ | ---------- | -------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------- | ---------- | --------------------------------------------------------------------------------------------------------------------------------- |
| TP-PB-0002 | PB-APM-0004  | PB-ONA-0001 | POS      | P1           | 1,2        | Login dengan akun yang terdaftar | <ol start="1"><li>Buka halaman <em>Open New Account</em>.</li><li>Pilih tipe rekening <strong>CHECKING</strong> pada <em>dropdown/radio button</em>.</li><li>Pilih rekening sumber (<em>source account</em>) yang memiliki saldo cukup untuk <em>minimum deposit</em>.</li><li>Klik tombol <strong>OPEN NEW ACCOUNT</strong>.</li></ol>                                      | Sistem berhasil men-generate nomor rekening _Checking_ baru, dan memotong dana _minimum deposit_ dari rekening sumber ke rekening baru secara akurat dan _real-time_.              | As Expected                                                                                          | PASSED     |                                                                                                                                   |
| TP-PB-0002 | PB-APM-0004  | PB-ONA-0002 | POS      | P1           | 1,2        | Login dengan akun yang terdaftar | <ol start="1"><li>Buka halaman <em>Open New Account</em>.</li><li>Pilih tipe rekening <strong>SAVINGS</strong> pada <em>dropdown/radio button</em>.</li><li>Pilih rekening sumber (<em>source account</em>) yang memiliki saldo cukup untuk <em>minimum deposit</em>.</li><li>Klik tombol <strong>OPEN NEW ACCOUNT</strong>.</li></ol>                                       | Sistem berhasil men-generate nomor rekening _Savings_ baru, dan memotong dana _minimum deposit_ dari rekening sumber ke rekening baru secara akurat dan _real-time_.               | As Expected                                                                                          | PASSED     |                                                                                                                                   |
| TP-PB-0002 | PB-APM-0004  | PB-ONA-0003 | NEG      | P1           | 2          | Login dengan akun yang terdaftar | <ol start="1"><li>Buka halaman <em>Open New Account</em>.</li><li>Pilih tipe rekening apapun (<em>Checking</em> atau <em>Savings</em>).</li><li>Pilih rekening sumber (<em>source account</em>) yang saldonya <strong>0</strong> atau di bawah nominal <em>minimum deposit</em>.</li></ol><p> </p><ol start="4"><li>Klik tombol <strong>OPEN NEW ACCOUNT</strong>.</li></ol> | Sistem menolak pembuatan rekening baru, tidak melakukan pemotongan dana, dan memunculkan pesan _error_ bahwa saldo tidak mencukupi.                                                | Sistem melanjutkan pembuatan rekening dengan menambah hutang/saldo minus pada rekening yang dipilih. | FAILED     | [KAN-26: PB-BUG-0005 \[Open New Account\] Insufficient Funds \[ParaBank\]Bug Report](https://alldocs.atlassian.net/browse/KAN-26) |
| TP-PB-0002 | PB-APM-0004  | PB-ONA-0004 | POS      | P2           | 2          | Login dengan akun yang terdaftar | <ol start="1"><li>Catat saldo akhir dari rekening sumber sebelum proses pembukaan rekening.</li><li>Lakukan proses pembukaan rekening baru.</li><li>Setelah berhasil, cek detail mutasi/saldo pada rekening sumber dan rekening baru yang terbentuk.</li></ol>                                                                                                               | Nominal saldo di rekening sumber berkurang tepat sebesar _minimum deposit_, dan saldo di rekening baru bertambah tepat sebesar _minimum deposit_ di waktu yang sama (_real-time_). | As Expected                                                                                          | PASSED     |                                                                                                                                   |

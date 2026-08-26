# PB-0004 Accounts Overview

## User Story

***

Sebagai nasabah, saya ingin melihat ringkasan seluruh rekening yang saya milki agar dapat memantau saldo terkini.

## Pre-condition

***

Pengguna telah berhasil login dan memiliki satu rekening di dalam sistem.

## Acceptance Criteria

***

* Tabel Overview menampilkan semua nomor rekening dan saldo masing-masing secara akurat.
* Sistem menghitung dan menampilkan akumulasi total keseluruhan saldo (Total Balance) dengan benar di baris paling bawah.
* Setiap nomor rekening pada tabel berupa hyperlink yang dapat diklik dan mengarahkan pengguna ke halaman riwayat detail transaksi rekening tersebut.

## Test Scenario

***

| **TP**     | **Scene ID** | **Test ID** | **Priority** | **Type** | **AC Ref** | **Pre-condition**                                    | **Step**                                                                                                                                                                                                                        | **Expected**                                                                                                                                       | **Actual**  | **Status** | **Notes** |
| ---------- | ------------ | ----------- | ------------ | -------- | ---------- | ---------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------- | ----------- | ---------- | --------- |
| TP-PB-0002 | PB-APM-0001  | PB-OVR-0001 | P1           | POS      | 1,2,3      | Login dengan akun yang terdaftar.                    | <ol start="1"><li>Akses halaman account overview</li><li>Periksa data pada tabel overview</li></ol>                                                                                                                             | Data nomor rekening berhasil muncul pada tabel beserta dengan sisa uang dan total uang yang terakumulasi pada akun itu                             | As Expected | PASSED     |           |
| TP-PB-0002 | PB-APM-0001  | PB-OVR-0002 | P1           | POS      | 1,2        | Login dengan akun yang terdaftar.                    | <ol start="1"><li>Akses halaman account overview</li><li>Periksa data saldo dan total saldo pada tabel overview</li></ol>                                                                                                       | Angka yang ditampilkan pada baris **Total** di bagian bawah tabel harus cocok secara matematis dengan akumulasi seluruh saldo rekening di atasnya. | As Expected | PASSED     |           |
| TP-PB-0002 | PB-APM-0001  | PB-OVR-0003 | P1           | POS      | 3          | Login dengan akun yang terdaftar.                    | <ol start="1"><li>Berada di halaman <strong>Accounts Overview</strong>.</li><li>Arahkan kursor ke salah satu nomor rekening (pastikan kursor berubah menjadi <em>pointer</em>).</li><li>Klik nomor rekening tersebut.</li></ol> | Sistem mengarahkan pengguna ke halaman _Account Details_ / Riwayat Transaksi yang datanya sesuai dengan nomor rekening yang diklik.                | As Expected | PASSED     |           |
| TP-PB-0002 | PB-APM-0001  | PB-OVR-0004 | P2           | POS      | 1,2        | Login menggunakan akun dengan 1 rekening saja/fresh. | <ol start="1"><li>Navigasi ke <strong>Accounts Overview</strong>.</li><li>Periksa baris <strong>Total</strong>.</li></ol>                                                                                                       | Tabel hanya menampilkan 1 baris rekening, dan baris **Total** menampilkan nominal yang sama persis dengan saldo rekening tunggal tersebut.         | As Expected | PASSED     |           |

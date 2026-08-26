# AEX-BUG-0002 \[Payment Module] Failed to Validate Input Format for Credit Card

## Description

***

Sistem pada formulir pembayaran gagal memvalidasi format serta kelengkapan data kartu kredit/debit (seperti nomor kartu, tanggal kadaluarsa, dan kebutuhan data kartu lainnya). Akibatnya, sistem meloloskan dan memproses transaksi selama kolom-kolom input tersebut terisi, meskipun nilai atau format data yang dimasukkan tidak sesuai dengan standar validasi kartu pembayaran yang berlaku.

## Pre-condition

***

1. Berada di halaman /payment.

## Steps to Reproduce

***

1. Masukkan Card Number dengan jumlah digit kurang dari standar.
2. Isikan data lain secara lengkap.
3. Klik 'Pay and Confirm Order'.

## Expected vs Actual

***

**Expected Result:** Sistem menolak pengiriman pembayaran atau memicu validasi error format nomor kartu tidak sesuai standar.

**Actual Result:** Sistem tidak mengecek format nilai dari pada input kartu maupun tanggal dan kebutuhan data pada kartu dan melewatkannya selama terisi

## Environment & Evidence

***

**Environment:** Production

**Evidence:**

* [https://drive.google.com/file/d/1b6\_8LSzvU\_jGt5WTcOk5kGl\_vXs7S15q/view?usp=sharing](https://drive.google.com/file/d/1b6_8LSzvU_jGt5WTcOk5kGl_vXs7S15q/view?usp=sharing)

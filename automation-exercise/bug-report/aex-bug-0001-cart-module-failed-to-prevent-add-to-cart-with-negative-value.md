# AEX-BUG-0001 \[Cart Module] Failed to Prevent Add to Cart with Negative Value

## Description

***

Sistem pada halaman detail produk (/product\_details/{id}) gagal memvalidasi atau mencegah pengguna memasukkan jumlah kuantitas produk bernilai nol atau negatif (contoh: -1, 0) saat menekan tombol "Add to cart". Akibatnya, produk dengan jumlah tidak valid tersebut berhasil diproses dan masuk ke dalam keranjang belanja, yang dapat merusak perhitungan total kuantitas maupun total harga di dalam modul keranjang.

## Pre-condition

***

Pengguna berada di halaman detail produk, contohnya /product\_details/{id}.

## Steps to Reproduce

***

1. Buka halaman detail produk pada tautan /product\_details/1.
2. Temukan kolom input kuantitas (Quantity) pada halaman tersebut.
3. Hapus angka bawaan lalu masukkan angka negatif atau nol (misalnya: -5 atau 0).
4. Klik tombol **Add to cart**.
5. Klik tombol **View Cart** pada modal konfirmasi yang muncul untuk memeriksa isi keranjang.

## Expected vs Actual

***

**Expected Result** Sistem menolak atau mereset input tidak valid tersebut ke nilai minimum yang valid (1), atau menahan pengiriman form serta menampilkan pesan peringatan sehingga item bernilai 0 atau negatif tidak masuk ke dalam keranjang belanja.

**Actual Result** Sistem menerima input bernilai negatif atau nol tersebut tanpa adanya validasi, dan berhasil menambahkan produk ke dalam keranjang belanja dengan kuantitas bernilai negatif/nol sesuai input pengguna.

## Environment & Evidence

***

**Environment:** Production

**Evidence:**

* [https://drive.google.com/file/d/1I7g16-3ctjqeJ7H2OY-aRPx\_Lkymvwqb/view?usp=sharing](https://drive.google.com/file/d/1I7g16-3ctjqeJ7H2OY-aRPx_Lkymvwqb/view?usp=sharing)

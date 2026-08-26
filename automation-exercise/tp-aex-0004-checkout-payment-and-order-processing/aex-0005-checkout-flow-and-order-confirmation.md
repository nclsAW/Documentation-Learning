# AEX-0005 Checkout Flow & Order Confirmation

## User Story

***

Sebagai pengguna terdaftar yang memiliki produk di keranjang belanja, saya ingin memproses checkout dan memverifikasi rincian alamat serta pesanan saya agar saya dapat memastikan seluruh data transaksi sudah benar sebelum melakukan pembayaran.

## Pre-conditions

***

1. Browser Google Chrome versi terbaru terpasang dan terhubung ke internet.
2. Aplikasi web Automation Exercise dapat diakses melalui URL [Automation Exercise - Checkout](https://automationexercise.com/checkout) .
3. Menyiapkan akun terdaftar aktif dari modul pendaftaran yang memiliki data alamat lengkap.
4. Terdapat minimal 1 produk aktif di dalam keranjang belanja.
5. Sesi login telah aktif atau pengguna siap melakukan login/pendaftaran saat memicu proses checkout.

## Acceptance Criteria

***

1. Pengguna terdaftar dapat menekan tombol Proceed to Checkout pada halaman keranjang belanja dan langsung diarahkan ke halaman checkout.
2. Pengguna yang belum login saat menekan Proceed to Checkout akan ditampilkan modal peringatan untuk melakukan Login atau Register terlebih dahulu.
3. Halaman checkout menampilkan Alamat Pengiriman (Delivery Address) dan Alamat Penagihan (Billing Address) yang datanya persis sama dengan data akun pengguna saat pendaftaran.
4. Halaman checkout menampilkan tabel Review Your Order dengan rincian produk, kuantitas, dan total harga yang selaras dengan isi keranjang belanja.
5. Pengguna dapat mengisi teks catatan atau instruksi khusus pada kolom Comment di halaman checkout.
6. Pengguna dapat menekan tombol Place Order setelah meninjau pesanan dan sistem mengarahkan pengguna ke halaman pembayaran (Payment).
7. Sistem mencegah pengaktifan alur checkout jika keranjang belanja dalam keadaan kosong.

## Test Scenario

***

| **TP**      | **Scene ID**  | **Test ID**   | **Type** | **Priority** | **AC Ref** | **Pre-condition**                                                                                                    | **Step**                                                                                                                                                                                                                                                                     | **Expected**                                                                                                                                      | **Actual**  | **Status** | **Notes** |
| ----------- | ------------- | ------------- | -------- | ------------ | ---------- | -------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ----------- | ---------- | --------- |
| TP-AEX-0004 | AEX-CPOP-0001 | AEX-CFOC-0001 | POS      | P1           | 1,3,4,5,6  | <ol start="1"><li>User ter-login dengan alamat lengkap terdaftar.</li><li>Keranjang belanja terisi produk.</li></ol> | <ol start="1"><li>Di halaman /view_cart, klik 'Proceed To Checkout'.</li><li>Verifikasi Delivery Address &#x26; Billing Address.</li><li>Verifikasi rincian tabel Review Your Order.</li><li>Isikan catatan pada kolom Comment.</li><li>Klik tombol 'Place Order'.</li></ol> | Pengguna langsung masuk ke /checkout dengan alamat, billing, dan tabel pesanan yang auto-sync, lalu redirect ke /payment saat klik "Place Order". | As Expected | PASSED     |           |
| TP-AEX-0004 | AEX-CPOP-0001 | AEX-CFOC-0002 | NEG      | P1           | 2          | <ol start="1"><li>User berstatus Guest.</li><li>Keranjang belanja terisi produk.</li></ol>                           | <ol start="1"><li>Navigasi ke halaman /view_cart.</li><li>Klik tombol 'Proceed To Checkout'.</li></ol>                                                                                                                                                                       | Sistem menahan alur checkout dan memunculkan modal popup peringatan dengan opsi 'Register / Login' atau 'Continue On Cart'.                       | As Expected | PASSED     |           |
| TP-AEX-0004 | AEX-CPOP-0001 | AEX-CFOC-0003 | NEG      | P2           | 7          | <ol start="1"><li>User ter-login.</li><li>Keranjang belanja dalam kondisi kosong.</li></ol>                          | <ol start="1"><li>Akses halaman /view_cart.</li><li>Coba klik atau pemicu tombol 'Proceed To Checkout'.</li></ol>                                                                                                                                                            | Sistem mencegah pengaktifan checkout (tombol disabled atau menyajikan pesan keranjang kosong).                                                    | As Expected | PASSED     |           |

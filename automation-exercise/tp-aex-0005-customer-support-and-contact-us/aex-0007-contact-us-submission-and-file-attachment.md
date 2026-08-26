# AEX-0007 Contact Us Submission & File Attachment

## User Story

***

Sebagai pengunjung situs Automation Exercise, saya ingin mengirimkan pesan dan melampirkan berkas pendukung melalui formulir Contact Us agar saya dapat menghubungi tim dukungan pelanggan tanpa harus melakukan login terlebih dahulu.

## Pre-conditions

***

1. Browser Google Chrome versi terbaru terpasang dan terhubung ke internet.
2. Aplikasi web Automation Exercise dapat diakses melalui URL [https://automationexercise.com/contact\_us](https://automationexercise.com/contact_us) .
3. Menyiapkan data pengirim valid meliputi Nama, Email valid, Subjek, dan Isi Pesan.
4. Menyiapkan berkas lampiran sampel berukuran ringan (contoh: format JPG, PNG, TXT, atau PDF dengan ukuran di bawah 2MB).
5. Menyiapkan variasi masukan tidak valid seperti format email tanpa simbol @ atau domain, serta kondisi formulir kosong.

## Acceptance Criteria

***

1. Pengguna dapat mengakses halaman Contact Us dan sistem menampilkan formulir GET IN TOUCH secara lengkap beserta kolom unggah berkas.
2. Pengguna dapat mengisi Nama, Email, Subjek, Pesan, serta memilih berkas lampiran valid lalu menekan tombol Submit.
3. Sistem memicu dialog pop-up konfirmasi JavaScript (Alert) saat tombol Submit ditekan, dan memproses pengiriman ketika pengguna menekan OK.
4. Sistem menampilkan pesan keberhasilan "Success! Your details have been submitted successfully." setelah formulir berhasil dikirimkan.
5. Pengguna dapat menekan tombol Home pada halaman konfirmasi sukses dan sistem mengarahkan kembali ke halaman utama.
6. Sistem menahan pengiriman pesan dan memicu validasi error dari browser jika pengguna mengosongkan kolom wajib (Nama, Email, atau Pesan).
7. Sistem menolak submit formulir jika format email yang dimasukkan tidak memenuhi standar penulisan email.
8. Sistem menangani atau menolak pengunggahan jika berkas lampiran yang dipilih melebihi batas ukuran atau memiliki format yang tidak didukung.

## Test Scenario

***

| **TP**      | **Scene ID**  | **Test ID**   | **Type** | **Priority** | **AC Ref** | **Pre-condition**                                                                                                                                                 | **Step**                                                                                                                                                                                                                                                                                        | **Expected**                                                                                                                                                                                                                                                           | **Actual**  | **Status** | **Notes** |
| ----------- | ------------- | ------------- | -------- | ------------ | ---------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------- | ---------- | --------- |
| TP-AEX-0005 | AEX-CSCU-0001 | AEX-CUSF-0001 | POS      | P1           | 1,3,4,5,6  | <ol start="1"><li>User ter-login dengan akun terdaftar yang memiliki alamat lengkap.</li><li>Minimal 1 produk berada di keranjang belanja (/view_cart).</li></ol> | <ol start="1"><li>Buka halaman /view_cart, klik tombol 'Proceed To Checkout'.</li><li>Verifikasi Delivery Address &#x26; Billing Address.</li><li>Verifikasi rincian tabel Review Your Order.</li><li>Isikan catatan instruksi pada kolom Comment.</li><li>Klik tombol 'Place Order'.</li></ol> | Pengguna langsung diarahkan ke halaman /checkout dengan data alamat, rincian produk, kuantitas, serta total harga yang secara otomatis tersinkronisasi sesuai akun dan keranjang, hingga saat tombol Place Order diklik akan mengalihkan pengguna ke halaman /payment. | As Expected | PASSED     |           |
| TP-AEX-0005 | AEX-CSCU-0001 | AEX-CUSF-0002 | NEG      | P1           | 2          | <ol start="1"><li>User berstatus Guest (belum ter-login).</li><li>Minimal 1 produk berada di keranjang belanja (/view_cart).</li></ol>                            | <ol start="1"><li>Buka halaman /view_cart.</li><li>Klik tombol 'Proceed To Checkout'.</li></ol>                                                                                                                                                                                                 | Sistem menahan pengalihan ke halaman checkout dan menampilkan modal popup peringatan untuk melakukan Login atau Register.                                                                                                                                              | As Expected | PASSED     |           |
| TP-AEX-0005 | AEX-CSCU-0001 | AEX-CUSF-0002 | NEG      | P2           | 7          | <ol start="1"><li>User ter-login.</li><li>Keranjang belanja dalam keadaan kosong (0 item).</li></ol>                                                              | <ol start="1"><li>Akses halaman /view_cart.</li><li>Periksa status dan coba pemicu pada tombol 'Proceed To Checkout'.</li></ol>                                                                                                                                                                 | Sistem mencegah alur checkout (tombol disabled atau menampilkan indikator keranjang kosong).                                                                                                                                                                           | As Expected | PASSED     |           |

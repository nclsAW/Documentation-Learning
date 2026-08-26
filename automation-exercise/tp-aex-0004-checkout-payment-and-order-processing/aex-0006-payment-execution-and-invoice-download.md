# AEX-0006 Payment Execution & Invoice Download

## User Story

***

Sebagai pengguna yang sedang melakukan checkout, saya ingin memasukkan detail kartu pembayaran dan mengunduh faktur transaksi agar pembayaran pesanan saya terkonfirmasi dan saya memiliki bukti pembayaran berformat PDF.

## Pre-conditions

***

1. Browser Google Chrome versi terbaru terpasang dan terhubung ke internet.
2. Aplikasi web Automation Exercise berada pada halaman pembayaran via URL [https://automationexercise.com/payment](https://www.google.com/search?q=https://automationexercise.com/payment).
3. Pengaturan browser telah diizinkan untuk melakukan unduh otomatis (automatic download) berkas PDF dari situs Automation Exercise.
4. Menyiapkan data dummy kartu kredit valid (Nama Pemilik Kartu, 16 Digit Nomor Kartu, 3 Digit CVC, dan Expiration Month/Year).
5. Menyiapkan variasi data dummy kartu tidak valid (nomor kartu kurang digit atau kolom wajib diisi kosong).

## Acceptance Criteria

***

1. Pengguna dapat mengisi Nama Pemilik Kartu, Nomor Kartu, CVC, serta Bulan dan Tahun Kadaluarsa secara lengkap lalu menekan Pay and Confirm Order.
2. Sistem memproses pembayaran dan mengarahkan pengguna ke halaman konfirmasi pesanan dengan pesan "ORDER PLACED!" dan "Your order has been placed successfully!".
3. Sistem menolak pengiriman pembayaran dan memicu validasi error dari browser jika pengguna mengosongkan salah satu kolom wajib pembayaran.
4. Sistem menolak pengiriman pembayaran jika format atau jumlah digit nomor kartu tidak sesuai dengan standar input.
5. Pengguna dapat menekan tombol Download Invoice pada halaman konfirmasi pesanan dan sistem secara otomatis mengunduh berkas faktur berformat ke penyimpanan lokal.
6. Berkas faktur yang terunduh dapat dibuka dan memuat informasi rincian transaksi yang sesuai dengan pesanan yang baru dibuat.
7. Pengguna dapat menekan tombol Continue pada halaman konfirmasi pesanan untuk kembali ke halaman utama dalam kondisi keranjang belanja yang sudah kosong.

## Test Scenario

***

| **TP**      | **Scene ID**  | **Test ID**   | **Type** | **Priority** | **AC Ref** | **Pre-condition**                                                                                         | **Step**                                                                                                                                                                                                                                                 | **Expected**                                                                                                           | **Actual**                                                                                                                            | **Status** | **Notes**                                                                                                                                                                |
| ----------- | ------------- | ------------- | -------- | ------------ | ---------- | --------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------- | ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| TP-AEX-0004 | AEX-CPOP-0002 | AEX-PEID-0001 | POS      | P1           | 1,2,7      | <ol start="1"><li>User berada di halaman /payment.</li><li>Menyiapkan dummy kartu kredit valid.</li></ol> | <ol start="1"><li>Lengkapi Name on Card, Card Number (16 digit), CVC (3 digit), &#x26; Expiration Month/Year.</li><li>Klik 'Pay and Confirm Order'.</li><li>Verifikasi pesan di layar.</li><li>Klik tombol 'Continue' pada halaman konfirmasi.</li></ol> | Transaksi berhasil dilakukan dan terdapat invoice untuk diunduh.                                                       | As Expected                                                                                                                           | PASSED     |                                                                                                                                                                          |
| TP-AEX-0004 | AEX-CPOP-0002 | AEX-PEID-0002 | POS      | P1           | 5,6        | <ol start="1"><li>User berada di halaman /payment_done.</li></ol>                                         | <ol start="1"><li>Klik tombol 'Download Invoice'.</li><li>Buka berkas terunduh.</li></ol>                                                                                                                                                                | Invoice berhasil diunduh dan dapat dibuka                                                                              | As Expected                                                                                                                           | PASSED     |                                                                                                                                                                          |
| TP-AEX-0004 | AEX-CPOP-0002 | AEX-PEID-0003 | NEG      | P2           | 3          | <ol start="1"><li>Berada di halaman /payment.</li></ol>                                                   | <ol start="1"><li>Kosongkan salah satu kolom wajib (misal: CVC atau Expiration Year).</li><li>Isi kolom lainnya dengan data dummy.</li><li>Klik 'Pay and Confirm Order'.</li></ol>                                                                       | Sistem menahan pengiriman form pembayaran dan memicu HTML5 validation popup dari browser pada kolom wajib yang kosong. | As Expected                                                                                                                           | PASSED     |                                                                                                                                                                          |
| TP-AEX-0004 | AEX-CPOP-0002 | AEX-PEID-0004 | NEG      | P1           | 4          | <ol start="1"><li>Berada di halaman /payment.</li></ol>                                                   | <ol start="1"><li>Masukkan Card Number dengan jumlah digit kurang dari standar.</li><li>Isikan data lain secara lengkap.</li><li>Klik 'Pay and Confirm Order'.</li></ol>                                                                                 | Sistem menolak pengiriman pembayaran atau memicu validasi error format nomor kartu tidak sesuai standar.               | Sistem tidak mengecek format nilai dari pada input kartu maupun tanggal dan kebutuhan data pada kartu dan melewatkannya selama terisi | FAILED     | [KAN-84: AEX-BUG-0002 \[Payment Module\] Failed to Validate Input Format for Credit Card \[Automation Exercise\]Bug Report](https://alldocs.atlassian.net/browse/KAN-84) |

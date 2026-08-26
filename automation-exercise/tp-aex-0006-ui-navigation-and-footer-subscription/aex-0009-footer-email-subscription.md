# AEX-0009 Footer Email Subscription

## User Story

***

Sebagai pengunjung situs Automation Exercise, saya ingin memasukkan alamat email pada kolom Subscription di bagian footer agar saya dapat berlangganan pembaruan informasi dan promosi dari situs.

## Pre-conditions

***

1. Browser Google Chrome versi terbaru terpasang dan terhubung ke internet.
2. Aplikasi web Automation Exercise dapat diakses melalui URL [Automation Exercise](https://automationexercise.com/) atau [Automation Exercise - Checkout](https://automationexercise.com/view_cart) .
3. Menyiapkan data alamat email valid (contoh: [subscriber\_test@mail.com](mailto:subscriber_test@mail.com)).
4. Menyiapkan data masukan tidak valid seperti email tanpa simbol @ atau domain, serta kolom input kosong.

## Acceptance Criteria

***

1. Pengguna dapat melihat bagian footer yang memuat teks SUBSCRIPTION dan kolom input email pada halaman utama maupun halaman keranjang belanja.
2. Pengguna dapat memasukkan alamat email yang valid pada kolom Subscription lalu menekan tombol panah, dan sistem menampilkan pesan sukses "You have been successfully subscribed!".
3. Pesan konfirmasi keberhasilan langganan muncul secara transparan di area footer tanpa merusak tata letak elemen lainnya.
4. Sistem menolak pengiriman langganan dan memicu pesan validasi dari browser jika pengguna mengosongkan kolom input email saat menekan tombol submit.
5. Sistem menolak pengiriman langganan jika format email yang dimasukkan tidak memenuhi standar penulisan email.

## Test Scenario

***

| **TP**      | **Scene ID**  | **Test ID**  | **Type** | **Priority** | **AC Ref** | **Pre-condition**                                                                                                                                                                                                    | **Step**                                                                                                                                                                                                                                                                                                                                                   | **Expected**                                                                                                                                                                                                                  | **Actual**  | **Status** | **Notes** |
| ----------- | ------------- | ------------ | -------- | ------------ | ---------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------- | ---------- | --------- |
| TP-AEX-0006 | AEX-UNFS-0002 | AEX-FES-0001 | POS      | P1           | 1,2,3      | <ol start="1"><li>Browser Chrome terbuka.</li><li>Berada di Homepage atau Cart Page (/view_cart).</li><li>Menyiapkan email valid (<a href="mailto:subscriber_test@mail.com">subscriber_test@mail.com</a>).</li></ol> | <ol start="1"><li>Scroll ke bawah hingga area footer.</li><li>Verifikasi teks 'SUBSCRIPTION' &#x26; kolom input email.</li><li>Masukkan email valid (<a href="mailto:subscriber_test@mail.com">subscriber_test@mail.com</a>).</li><li>Klik tombol panah submit di sebelah kanan kolom.</li><li>Verifikasi kemunculan pesan konfirmasi di footer.</li></ol> | Form dan teks _SUBSCRIPTION_ teridentifikasi dengan jelas, pesan sukses _'You have been successfully subscribed!'_ muncul secara transparan di area footer, serta tata letak UI footer tetap stabil tanpa mengalami distorsi. | As Expected | PASSED     |           |
| TP-AEX-0006 | AEX-UNFS-0002 | AEX-FES-0002 | NEG      | P2           | 4          | Berada di area footer Homepage atau Cart Page.                                                                                                                                                                       | <ol start="1"><li>Kosongkan kolom input email pada widget Subscription.</li><li>Klik tombol panah submit.</li></ol>                                                                                                                                                                                                                                        | Sistem menahan pengiriman langganan dan memicu HTML5 validation popup dari browser pada kolom input yang kosong (misal: "Please fill out this field").                                                                        | As Expected | PASSED     |           |
| TP-AEX-0006 | AEX-UNFS-0002 | AEX-FES-0003 | NEG      | P2           | 5          | <ol start="1"><li>Berada di area footer Homepage atau Cart Page.</li></ol>                                                                                                                                           | <ol start="1"><li>Masukkan email tanpa '@' (contoh: subscriber_invalid).</li><li>Klik tombol panah submit.</li><li>Ubah email menjadi subscriber@ (tanpa domain) lalu klik submit.</li></ol>                                                                                                                                                               | Browser/Sistem memunculkan tooltip peringatan validasi format email (misal: "Please include an '@' in the email address..."). Form tidak ter-submit.                                                                          | As Expected | PASSED     |           |

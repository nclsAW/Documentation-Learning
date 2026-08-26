# AEX-0001 User Registration & Account Creation

## User Story

***

Saya ingin mendaftarkan akun baru dengan memberikan informasi pribadi yang valid dan alamat pengiriman yang valid, agar saya memiliki identitas yang terverifikasi untuk melakukan pembelian dan mengakses fitur-fitur yang khusus diperuntukkan bagi pengguna terdaftar.

## Pre-condition

***

* Browser Google Chrome (versi terbaru) terpasang dan dapat mengakses jaringan internet.
* Aplikasi web **Automation Exercise** berstatus _UP_ dan dapat diakses melalui URL target [https://automationexercise.com/signup](https://automationexercise.com/signup)
* Penguji telah menyiapkan set data uji:
  * **Data Baru (Unik):** String nama, alamat email unik (menggunakan format timestamp, contoh: `testuser_1710000000@mail.com`), kata sandi, tanggal lahir, dan detail alamat lengkap.
  * **Data Existing (Duplikat):** Alamat email yang sudah terdaftar sebelumnya di sistem.
  * **Data Invalid:** Format email tanpa `@` / domain, serta nilai kosong (_blank_) untuk field wajib (_mandatory fields_).

## Acceptance Criteria

***

1. Pengguna berhasil mendaftar akun baru saat memasukkan Name dan Email unik, lalu diarahkan ke formulir Enter Account Information.
2. Pengguna berhasil menyelesaikan pendaftaran setelah melengkapi seluruh kolom wajib dan sistem menampilkan pesan "ACCOUNT CREATED!".
3. Pengguna yang berhasil mendaftar dan menekan tombol Continue dialihkan ke halaman utama dengan status navigasi "Logged in as \[Username]".
4. Sistem menolak pendaftaran dan menampilkan pesan error "Email Address already exist!" jika email yang dimasukkan sudah terdaftar di basis data.
5. Sistem menahan proses pendaftaran dan menampilkan validasi error jika pengguna mengosongkan salah satu kolom wajib pada formulir pendaftaran.
6. Sistem menolak submit formulir pendaftaran jika format email yang dimasukkan tidak sesuai standar penulisan email.
7. Pengguna dapat menghapus akun secara permanen melalui tombol Delete Account dan sistem menampilkan pesan "ACCOUNT DELETED!" serta mengakhiri sesi login.

## Test Scenario

***

<table data-header-hidden data-search="false"><thead><tr><th></th><th></th><th></th><th></th><th></th><th></th><th></th><th></th><th></th><th></th><th></th><th></th></tr></thead><tbody><tr><td><strong>TP</strong></td><td><strong>Scene ID</strong></td><td><strong>Test ID</strong></td><td><strong>Type</strong></td><td><strong>Priority</strong></td><td><strong>AC Ref</strong></td><td><strong>Pre-condition</strong></td><td><strong>Step</strong></td><td><strong>Expected</strong></td><td><strong>Actual</strong></td><td><strong>Status</strong></td><td><strong>Notes</strong></td></tr><tr><td>TP-AEX-0001</td><td>AEX-AAM-0001</td><td>AEX-URAC-0001</td><td>POS</td><td>P1</td><td>1</td><td><ol start="1"><li>Aplikasi UP di <a href="https://automationexercise.com/login">Automation Exercise - Signup / Login</a></li><li>Penguji menyiapkan data unik.</li></ol></td><td><ol start="1"><li>Buka URL target.</li><li>Klik menu 'Signup / Login'.</li><li>Di form 'New User Signup!', masukkan Name (Test User) &#x26; Email unik.</li><li>Klik 'Signup'.</li></ol></td><td>Sistem menerima input dan mengarahkan pengguna ke halaman /signup (Enter Account Information) dengan Name &#x26; Email ter-prefill secara otomatis.</td><td>As Expected</td><td>PASSED</td><td> </td></tr><tr><td>TP-AEX-0001</td><td>AEX-AAM-0001</td><td>AEX-URAC-0002</td><td>POS</td><td>P1</td><td>2,3</td><td><ol start="1"><li>Pengguna berada di halaman formulir signup</li></ol></td><td><ol start="1"><li>Lengkapi seluruh field wajib di Account Information &#x26; Address Details.</li><li>Klik tombol 'Create Account'.</li><li>Verifikasi pesan di layar.</li><li>Klik tombol 'Continue'.</li></ol></td><td><ol start="1"><li>Sistem menyimpan data dan menampilkan pesan 'ACCOUNT CREATED!'.</li><li>Mengklik Continue mengarahkan ke Homepage dengan header navigasi menampilkan status 'Logged in as Test User'.</li></ol></td><td>As Expected</td><td>PASSED</td><td> </td></tr><tr><td>TP-AEX-0001</td><td>AEX-AAM-0001</td><td>AEX-URAC-0003</td><td>NEG</td><td>P1</td><td>4</td><td><ol start="1"><li>Penguji memiliki email yang sudah terdaftar di sistem.</li><li>Berada di halaman /login.</li></ol></td><td><ol start="1"><li>Masukkan Name &#x26; Email yang terdaftar.</li><li>Klik tombol 'Signup'.</li></ol></td><td>Sistem menahan proses pendaftaran, tetap di halaman /login, dan menampilkan pesan error 'Email Address already exist!' di bawah form.</td><td>As Expected</td><td>PASSED</td><td> </td></tr><tr><td>TP-AEX-0001</td><td>AEX-AAM-0001</td><td>AEX-URAC-0004</td><td>NEG</td><td>P2</td><td>5</td><td><ol start="1"><li>Berada di halaman /login.</li></ol></td><td><ol start="1"><li>Isi Password.</li><li>Kosongkan salah satu atau seluruh field wajib di Address Details</li><li>Klik tombol 'Create Account'.</li></ol></td><td>Sistem menahan pengiriman form dan memicu validasi browser (HTML5 required validation popup) pada kolom wajib yang kosong. Data tidak tersimpan.</td><td>As Expected</td><td>PASSED</td><td> </td></tr><tr><td>TP-AEX-0001</td><td>AEX-AAM-0001</td><td>AEX-URAC-0005</td><td>NEG</td><td>P2</td><td>6</td><td><ol start="1"><li>Berada di halaman /login.</li></ol></td><td><ol start="1"><li>Pada form 'New User Signup!', masukkan Name &#x26; Email tanpa karakter @.</li><li>Klik 'Signup'.</li></ol></td><td>Browser memunculkan tooltip peringatan validasi format email pada form Signup (misal: "Please include an '@' in the email address..."). Form tidak ter-submit.</td><td>As Expected</td><td>PASSED</td><td> </td></tr><tr><td>TP-AEX-0001</td><td>AEX-AAM-0001</td><td>AEX-URAC-0006</td><td>NEG</td><td>P2</td><td>6</td><td><ol start="1"><li>Berada di halaman /login.</li></ol></td><td><ol start="1"><li>Ubah email menjadi test@ (tanpa domain valid)</li><li>Klik 'Signup'.</li></ol></td><td>Browser memunculkan tooltip peringatan validasi format email (misal: "Please enter a part following ‘@'. 'Test@’ is incomplete"). Form tidak ter-submit.</td><td>As Expected</td><td>PASSED</td><td> </td></tr><tr><td>TP-AEX-0001</td><td>AEX-AAM-0001</td><td>AEX-URAC-0007</td><td>POS</td><td>P1</td><td>7</td><td><ol start="1"><li>Pengguna baru saja menyelesaikan registrasi dan sedang ter-login di aplikasi.</li><li>Berada di Homepage.</li></ol></td><td><ol start="1"><li>Klik tombol 'Delete Account' pada header navigasi.</li><li>Verifikasi pesan di layar.</li><li>Klik tombol 'Continue'.</li><li>Navigasi ke /login dan coba login menggunakan kredensial akun yang baru dihapus.</li></ol></td><td>Sistem menghapus akun, menampilkan pesan ACCOUNT DELETED!, mengakhiri sesi login.</td><td>As Expected</td><td>PASSED</td><td> </td></tr></tbody></table>

# PB-0002 User Login

## User Story

***

Sebagai nasabah terdaftar, saya ingin masuk ke akun saya agar dapat melakukan transaksi finansial.

## Pre-condition

***

Pengguna telah memiliki kredensial akun (username & password) yang valid.

## Acceptance Criteria

***

* Pengguna berhasil login dna langsung diarahkan ke dashboard (Accounts Overview).
* Sistem menolak akses dan menampilkan pesan error jika password yang dimasukkan salah.
* Sistem menolak akses jika username tidak ditemukan di database.

## Test Scenario <a href="#test-scenario" id="test-scenario"></a>

***

<table data-header-hidden data-search="false"><thead><tr><th></th><th></th><th></th><th></th><th></th><th></th><th></th><th></th><th></th><th></th><th></th><th></th></tr></thead><tbody><tr><td><strong>TP</strong></td><td><strong>Scene ID</strong></td><td><strong>Test ID</strong></td><td><strong>Pre-condition</strong></td><td><strong>Type</strong></td><td><strong>AC Ref</strong></td><td><strong>Step</strong></td><td><strong>Priority</strong></td><td><strong>Expected</strong></td><td><strong>Actual</strong></td><td><strong>Status</strong></td><td><strong>Notes</strong></td></tr><tr><td><p>TP-PB-0001</p><p> </p></td><td>PB-AUTH-0002</td><td>PB-LGN-0001</td><td>Pengguna berada di halaman beranda/login. Akun terdaftar di <em>database</em>.</td><td>POS</td><td>1</td><td><ol start="1"><li>Masukkan <em>Username</em> dan Password yang valid.</li><li>Klik tombol "Log In".</li></ol></td><td>P1</td><td>Login berhasil, sistem membuat sesi aktif, dan pengguna diarahkan ke halaman <em>Accounts Overview</em>.</td><td>As Expected</td><td>PASSED</td><td> </td></tr><tr><td><p>TP-PB-0001</p><p> </p></td><td>PB-AUTH-0002</td><td>PB-LGN-0002</td><td>Pengguna berada di halaman beranda/login. Akun terdaftar di <em>database</em>.</td><td>NEG</td><td>2</td><td><ol start="1"><li>Masukkan <em>Username</em> yang valid.</li><li>Masukkan <em>Password</em> yang salah/invalid.</li><li>Klik tombol "Log In".</li></ol></td><td>P1</td><td>Login gagal. Sistem menampilkan pesan <em>error</em>: <em>"</em>An internal error has occurred and has been logged.<em>"</em></td><td>As Expected</td><td>PASSED</td><td> </td></tr><tr><td><p>TP-PB-0001</p><p> </p></td><td>PB-AUTH-0002</td><td>PB-LGN-0003</td><td>Pengguna berada di halaman beranda/login.</td><td>NEG</td><td>2</td><td><ol start="1"><li>Masukkan <em>Username</em> yang tidak terdaftar/invalid.</li><li>Masukkan <em>Password</em> apa saja.</li><li>Klik tombol "Log In".</li></ol></td><td>P1</td><td>Login gagal. Sistem menampilkan pesan <em>error</em>: <em>"</em>An internal error has occurred and has been logged.<em>"</em></td><td>As Expected</td><td>PASSED</td><td> </td></tr><tr><td><p>TP-PB-0001</p><p> </p></td><td>PB-AUTH-0002</td><td>PB-LGN-0004</td><td>Pengguna berada di halaman beranda/login.</td><td>NEG</td><td>2</td><td><ol start="1"><li>Kosongkan <em>field Username</em>.</li><li>Masukkan <em>Password</em> yang valid.</li><li>Klik tombol "Log In".</li></ol></td><td>P1</td><td>Login ditolak. Sistem memunculkan peringatan wajib isi: <em>"Please enter a username and password."</em></td><td>As Expected</td><td>PASSED</td><td> </td></tr><tr><td><p>TP-PB-0001</p><p> </p></td><td>PB-AUTH-0002</td><td>PB-LGN-0005</td><td>Pengguna berada di halaman beranda/login.</td><td>NEG</td><td>2</td><td><ol start="1"><li>Masukkan <em>Username</em> yang valid.</li><li>Kosongkan <em>field Password</em>.</li><li>Klik tombol "Log In".</li></ol></td><td>P1</td><td>Login ditolak. Sistem memunculkan peringatan wajib isi: <em>"Please enter a username and password."</em></td><td>As Expected</td><td>PASSED</td><td> </td></tr><tr><td><p>TP-PB-0001</p><p> </p></td><td>PB-AUTH-0002</td><td>PB-LGN-0006</td><td>Pengguna berada di dalam halaman registrasi</td><td>NEG</td><td>2</td><td><ol start="1"><li>Kosongkan <em>field Username</em> dan <em>Password</em>.</li><li>Klik tombol "Log In".</li></ol></td><td>P1</td><td>Login ditolak. Sistem memunculkan peringatan wajib isi: <em>"Please enter a username and password."</em></td><td>As Expected</td><td>PASSED</td><td> </td></tr></tbody></table>

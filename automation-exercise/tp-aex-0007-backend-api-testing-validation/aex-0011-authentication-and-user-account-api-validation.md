# AEX-0011 Authentication & User Account API Validation

## User Story

***

Sebagai sistem terintegrasi, saya ingin mengelola data akun pengguna dan memverifikasi autentikasi melalui endpoint API agar proses autentikasi dan manajemen data pengguna dapat berjalan secara aman dan terstruktur di tingkat backend.

## Pre-conditions

***

* Klien API siap digunakan dan terhubung ke internet.
* Server backend Automation Exercise berstatus aktif dan dapat diakses melalui Base URL [Automation Exercise](https://automationexercise.com/api) .
* Menyiapkan payload data pendaftaran akun lengkap (Name, Email, Password, Address, City, Zipcode, dll.) menggunakan format x-www-form-urlencoded / form-data.
* Menyiapkan kredensial valid dan tidak valid untuk pengujian otentikasi login API.

## Acceptance Criteria

***

1. Pengguna dapat mengirimkan permintaan HTTP POST verifikasi login dengan email dan password yang tepat, lalu sistem mengembalikan status kode 200 OK beserta pesan konfirmasi keberhasilan login.
2. Pengguna dapat mengirimkan permintaan HTTP POST ke endpoint pendaftaran akun dengan payload lengkap, dan sistem mengembalikan status kode 201 Created atau 200 OK beserta pesan "User created!".
3. Pengguna dapat mengirimkan permintaan HTTP PUT ke endpoint pembaruan akun untuk mengedit detail profil, dan sistem mengembalikan status kode 200 OK beserta pesan "User updated!".
4. Pengguna dapat mengirimkan permintaan HTTP DELETE ke endpoint hapus akun dengan parameter email dan password, dan sistem mengembalikan status kode 200 OK beserta pesan "Account deleted!".
5. Pengguna dapat mengirimkan permintaan HTTP GET untuk mengambil detail data akun berdasarkan email yang terdaftar dan sistem mengembalikan status kode 200 OK beserta objek JSON data pengguna.
6. Sistem mengembalikan status kode 404 Not Found atau 400 Bad Request jika pengguna mengirimkan kredensial login yang salah atau tidak terdaftar.
7. Sistem mengembalikan status kode 400 Bad Request jika permintaan pendaftaran atau pembaruan akun dikirimkan tanpa parameter wajib.
8. Sistem mengembalikan status kode 405 Method Not Allowed jika pengguna mengirimkan metode HTTP yang tidak didukung pada endpoint otentikasi atau manajemen akun.

## Test Scenario

***

| **TP**      | **Scene ID**  | **Test ID**   | **Type** | **Priority** | **AC Ref** | **Pre-condition**                                                                   | **Step**                                                                                                                                                                                              | **Expected**                                                                                                       | **Actual**  | **Status** | **Notes** |
| ----------- | ------------- | ------------- | -------- | ------------ | ---------- | ----------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------ | ----------- | ---------- | --------- |
| TP-AEX-0007 | AEX-BATV-0002 | AEX-AUAA-0001 | POS      | P1           | 1          | User terdaftar di DB ([test@mail.com](mailto:okis_api@mail.com) / 123).             | <ol start="1"><li>Kirim HTTP POST request ke /api/verifyLogin dengan form-data email &#x26; password valid.</li><li>Verifikasi status code dan respons.</li></ol>                                     | Status code 200 OK, responseCode 200, dan message 'User exists!'.                                                  | As Expected | PASSED     |           |
| TP-AEX-0007 | AEX-BATV-0002 | AEX-AUAA-0002 | POS      | P1           | 2          | Data user baru dengan email unik ([test1@mail.com](mailto:okis_new_1710@mail.com)). | Kirim HTTP POST request ke /api/createAccount dengan seluruh payload wajib (name, email, password, address, city, dll).                                                                               | Status code 200/201, responseCode 201, dan message 'User created!'.                                                | As Expected | PASSED     |           |
| TP-AEX-0007 | AEX-BATV-0002 | AEX-AUAA-0003 | POS      | P1           | 3          | Akun aktif terdaftar di database.                                                   | <ol start="1"><li>Kirim HTTP PUT request ke /api/updateAccount dengan payload data profil yang diperbarui.</li><li>Verifikasi respons.</li></ol>                                                      | Status code 200 OK, responseCode 200, dan message 'User updated!'.                                                 | As Expected | PASSED     |           |
| TP-AEX-0007 | AEX-BATV-0002 | AEX-AUAA-0004 | POS      | P1           | 5          | Akun aktif terdaftar di database.                                                   | <ol start="1"><li>Kirim HTTP GET request ke /api/getUserDetailByEmail dengan query parameter email = <a href="mailto:okis_api@mail.com">test@mail.com</a>.</li><li>Verifikasi respons JSON.</li></ol> | Status code 200 OK, responseCode 200, mengembalikan objek detail profil user (name, email, address, dll).          | As Expected | PASSED     |           |
| TP-AEX-0007 | AEX-BATV-0002 | AEX-AUAA-0005 | POS      | P1           | 4          | Akun aktif siap dihapus ([test1@mail.com](mailto:okis_new_1710@mail.com) / 1234).   | <ol start="1"><li>Kirim HTTP DELETE request ke /api/deleteAccount dengan form-data email &#x26; password.</li><li>Verifikasi respons.</li></ol>                                                       | Status code 200 OK, responseCode 200, dan message 'Account deleted!'.                                              | As Expected | PASSED     |           |
| TP-AEX-0007 | AEX-BATV-0002 | AEX-AUAA-0006 | NEG      | P1           | 6          | Email tidak terdaftar atau password salah.                                          | <ol start="1"><li>Kirim HTTP POST request ke /api/verifyLogin dengan password salah.</li><li>Verifikasi status code dan message.</li></ol>                                                            | Status code 404 Not Found (atau responseCode 404) dengan message 'User not found!'.                                | As Expected | PASSED     |           |
| TP-AEX-0007 | AEX-BATV-0002 | AEX-AUAA-0007 | NEG      | P2           | 7          | API Client aktif.                                                                   | <ol start="1"><li>Kirim HTTP POST request ke /api/createAccount tanpa menyertakan parameter email.</li><li>Verifikasi respons.</li></ol>                                                              | Status code 400 Bad Request (atau responseCode 400) dengan message 'Bad request, email parameter is missing.'.     | As Expected | PASSED     |           |
| TP-AEX-0007 | AEX-BATV-0002 | AEX-AUAA-0008 | NEG      | P2           | 8          | API Client aktif.                                                                   | <ol start="1"><li>Kirim HTTP DELETE request ke endpoint /api/verifyLogin.</li><li>Verifikasi respons.</li></ol>                                                                                       | Status code 405 Method Not Allowed (atau responseCode 405) dengan message 'This request method is not supported.'. | As Expected | PASSED     |           |

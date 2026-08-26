# AEX-0010 Products & Brands API Validation

## Use Story

***

Sebagai pengembang atau sistem terintegrasi, saya ingin mengakses endpoint API produk dan brand dengan parameter yang valid agar saya menerima respons berformat JSON secara tepat beserta status kode HTTP yang sesuai.

## Pre-conditions

***

1. Klien API (Postman, REST Assured, Bruno, atau Playwright API Context) siap digunakan dan terhubung ke internet.
2. Server backend Automation Exercise berstatus aktif dan dapat diakses melalui Base URL [Automation Exercise](https://automationexercise.com/api) .
3. Menyiapkan parameter pencarian produk valid (contoh: search\_product = top atau tshirt) dan tidak valid/kosong.

## Acceptance Criteria

***

1. Pengguna dapat mengirimkan permintaan HTTP GET ke endpoint daftar produk dan sistem mengembalikan status kode 200 OK beserta seluruh katalog produk dalam format JSON.
2. Pengguna dapat mengirimkan permintaan HTTP GET ke endpoint daftar brand dan sistem mengembalikan status kode 200 OK beserta seluruh daftar brand dalam format JSON.
3. Pengguna dapat mengirimkan permintaan HTTP POST ke endpoint pencarian produk dengan parameter search\_product dan sistem mengembalikan status kode 200 OK beserta daftar produk yang cocok.
4. Sistem mengembalikan status kode 405 Method Not Allowed dan pesan kesalahan jika pengguna mengirimkan permintaan HTTP POST ke endpoint daftar produk.
5. Sistem mengembalikan status kode 400 Bad Request dan pesan kesalahan jika pengguna mengirimkan permintaan HTTP POST pencarian produk tanpa menyertakan parameter search\_product.
6. Respons JSON yang diterima memiliki struktur skema dan tipe data yang konsisten sesuai dengan dokumentasi API resmi.

## Test Scenario

***

| **TP**      | **Scene ID**  | **Test ID**   | **Type** | **Priority** | **AC Ref** | **Pre-condition**                                                                                                                 | **Step**                                                                                                                                                                              | **Expected**                                                                                                                                 | **Actual**  | **Status** | **Notes** |
| ----------- | ------------- | ------------- | -------- | ------------ | ---------- | --------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------- | ----------- | ---------- | --------- |
| TP-AEX-0007 | AEX-BATV-0001 | AEX-PBAV-0001 | POS      | P1           | 1,6        | <ol start="1"><li>API Client aktif.</li><li>Base URL: <a href="https://automationexercise.com/">Automation Exercise</a></li></ol> | <ol start="1"><li>Kirim HTTP GET request ke /api/productsList.</li><li>Verifikasi status code dan response body JSON.</li></ol>                                                       | Status code 200 OK, responseCode 200, mengembalikan array list products dengan tipe data string/integer yang konsisten sesuai skema.         | As Expected | PASSED     |           |
| TP-AEX-0007 | AEX-BATV-0001 | AEX-PBAV-0002 | POS      | P1           | 2,6        | <ol start="1"><li>API Client aktif.</li><li>Base URL: <a href="https://automationexercise.com/">Automation Exercise</a></li></ol> | <ol start="1"><li>Kirim HTTP GET request ke /api/brandsList.</li><li>Verifikasi status code dan response body JSON.</li></ol>                                                         | Status code 200 OK, responseCode 200, mengembalikan array list brands dengan struktur JSON yang valid.                                       | As Expected | PASSED     |           |
| TP-AEX-0007 | AEX-BATV-0001 | AEX-PBAV-0003 | POS      | P1           | 3,6        | <ol start="1"><li>API Client aktif.</li></ol><p> </p><ol start="2"><li>Siapkan parameter search_product = 'tshirt'.</li></ol>     | <ol start="1"><li>Kirim HTTP POST request ke /api/searchProduct dengan form-data (search_product: tshirt).</li><li>Verifikasi status code dan isi respons.</li></ol>                  | Status code 200 OK, responseCode 200, mengembalikan daftar produk yang relevan dengan kata kunci 'tshirt'.                                   | As Expected | PASSED     |           |
| TP-AEX-0007 | AEX-BATV-0001 | AEX-PBAV-0004 | NEG      | P2           | 4          | <ol start="1"><li>API Client aktif.</li></ol>                                                                                     | <ol start="1"><li>Kirim HTTP POST request ke endpoint /api/productsList.</li><li>Verifikasi status code dan pesan respons.</li></ol>                                                  | Status code 405 Method Not Allowed (atau responseCode 405) dengan pesan error 'This request method is not supported.'.                       | As Expected | PASSED     |           |
| TP-AEX-0007 | AEX-BATV-0001 | AEX-PBAV-0005 | NEG      | P2           | 5          | <ol start="1"><li>API Client aktif.</li></ol>                                                                                     | <ol start="1"><li>Kirim HTTP POST request ke endpoint /api/searchProduct tanpa menyertakan body parameter search_product.</li><li>Verifikasi status code dan pesan respons.</li></ol> | Status code 400 Bad Request (atau responseCode 400) dengan pesan error 'Bad request, search\_product parameter is missing in POST request.'. | As Expected | PASSED     |           |

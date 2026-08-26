# AEX-0003 Product Browsing & Category Filter

## User Story

***

Sebagai pengguna situs Automation Exercise, saya ingin menjelajahi katalog produk, menggunakan fitur pencarian, memfilter produk berdasarkan kategori dan brand, serta melihat detail produk dan memberikan ulasan agar saya dapat menemukan serta menilai informasi produk yang ingin saya beli secara akurat.

## Pre-conditions

***

1. Browser Google Chrome versi terbaru terpasang dan terhubung ke internet.
2. Aplikasi web Automation Exercise dapat diakses melalui URL [https://automationexercise.com/products](https://automationexercise.com/products) .
3. Basis data aplikasi telah terisi dengan katalog master produk yang aktif beserta kategori dan brand.
4. Menyiapkan kata kunci pencarian valid (contoh: Dress, Top, Tshirt) dan kata kunci tidak terdaftar (contoh: XYZ123NonExistent).
5. Menyiapkan data masukan form ulasan produk (Nama, Email valid, dan Teks Ulasan) serta variasi tidak valid (Email salah format, atau kolom wajib kosong).

## Acceptance Criteria

***

1. Pengguna dapat mengakses halaman All Products dan sistem menampilkan seluruh daftar katalog produk beserta sidebar filter kategori dan brand.
2. Pengguna dapat menekan tombol View Product pada salah satu item dan sistem mengarahkan ke halaman detail produk yang menampilkan Nama Produk, Kategori, Harga, Availability, Condition, dan Brand secara lengkap.
3. Pengguna dapat mencari produk menggunakan kata kunci valid pada search bar dan sistem menampilkan daftar produk yang relevan dengan kata kunci tersebut serta judul SEARCHED PRODUCTS.
4. Sistem menampilkan halaman pencarian kosong tanpa produk jika pengguna memasukkan kata kunci pencarian yang tidak ada di dalam katalog.
5. Pengguna dapat memilih opsi Kategori (Women, Men, Kids) beserta Sub-kategorinya pada sidebar dan sistem menampilkan daftar produk yang sesuai dengan hierarki kategori yang dipilih.
6. Pengguna dapat memilih salah satu nama Brand pada sidebar dan sistem memfilter halaman untuk hanya menampilkan produk yang berasal dari brand tersebut.
7. Pengguna dapat mengirimkan ulasan produk pada form Write Your Review dengan melengkapi Name, Email, dan Review text, lalu sistem menampilkan pesan konfirmasi keberhasilan "Thank you for your review.".
8. Sistem menolak pengiriman ulasan produk dan memicu pesan validasi jika pengguna mengosongkan salah satu kolom wajib atau memasukkan format email yang salah.

## Test Scenario

***

| **TP**      | **Scene ID**  | **Test ID**   | **Type** | **Priority** | **AC Ref** | **Pre-condition**                                                                                                                   | **Step**                                                                                                                                                   | **Expected**                                                                                                                                         | **Actual**  | **Status** | **Notes** |
| ----------- | ------------- | ------------- | -------- | ------------ | ---------- | ----------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- | ----------- | ---------- | --------- |
| TP-AEX-0002 | AEX-PCSR-0001 | AEX-PBCF-0001 | POS      | P1           | 1          | <ol start="1"><li>Aplikasi UP di <a href="https://automationexercise.com/products">Automation Exercise - All Products</a></li></ol> | <ol start="1"><li>Buka URL target.</li><li>Klik menu 'Products' pada header navigasi.</li></ol>                                                            | Sistem mengarahkan ke halaman /products menampilkan daftar produk, serta sidebar Category & Brands.                                                  | As Expected | PASSED     |           |
| TP-AEX-0002 | AEX-PCSR-0001 | AEX-PBCF-0002 | POS      | P1           | 2          | <ol start="1"><li>Berada di halaman /products.</li></ol>                                                                            | <ol start="1"><li>Pilih salah satu produk.</li><li>Klik tombol 'View Product'.</li></ol>                                                                   | Sistem mengarahkan ke /product\_details/{id} dan menampilkan detail lengkap: Product Name, Category, Price, Availability, Condition, dan Brand.      | As Expected | PASSED     |           |
| TP-AEX-0002 | AEX-PCSR-0001 | AEX-PBCF-0003 | POS      | P1           | 3          | <ol start="1"><li>Berada di halaman /products.</li><li>Menyiapkan kata kunci valid ('Dress').</li></ol>                             | <ol start="1"><li>Masukkan kata kunci 'Dress' pada search bar.</li><li>Klik tombol search.</li></ol>                                                       | Sistem mengarahkan ke halaman hasil pencarian, menampilkan judul 'SEARCHED PRODUCTS', dan menyajikan daftar produk yang relevan dengan 'Dress'.      | As Expected | PASSED     |           |
| TP-AEX-0002 | AEX-PCSR-0001 | AEX-PBCF-0004 | NEG      | P2           | 4          | <ol start="1"><li>Berada di halaman /products.</li></ol>                                                                            | <ol start="1"><li>Masukkan kata kunci 'XYZ' pada search bar.</li><li>Klik tombol search.</li></ol>                                                         | Sistem menampilkan halaman 'SEARCHED PRODUCTS' dalam kondisi kosong tanpa item produk.                                                               | As Expected | PASSED     |           |
| TP-AEX-0002 | AEX-PCSR-0001 | AEX-PBCF-0005 | POS      | P1           | 5          | <ol start="1"><li>Berada di halaman /products.</li><li>Sidebar Category aktif.</li></ol>                                            | <ol start="1"><li>Pada sidebar Category, klik kategori 'Women'.</li><li>Klik sub-kategori 'Dress'.</li></ol>                                               | Sistem mengarahkan ke /category\_products/{id} dan menampilkan judul 'WOMEN - DRESS PRODUCTS' beserta daftar produk yang sesuai.                     | As Expected | PASSED     |           |
| TP-AEX-0002 | AEX-PCSR-0001 | AEX-PBCF-0006 | POS      | P1           | 6          | <ol start="1"><li>Berada di halaman /products.</li><li>Sidebar Brands aktif.</li></ol>                                              | <ol start="1"><li>Pada sidebar Brands, klik salah satu brand (misal: 'Polo').</li></ol>                                                                    | Sistem mengarahkan ke /brand\_products/{brand\_name} dan hanya menampilkan produk yang diproduksi oleh brand Polo.                                   | As Expected | PASSED     |           |
| TP-AEX-0002 | AEX-PCSR-0001 | AEX-PBCF-0007 | POS      | P1           | 7          | <ol start="1"><li>Berada di halaman detail produk (/product_details/{id}).</li><li>Form 'Write Your Review' tampil.</li></ol>       | <ol start="1"><li>Isikan Name ('Test').</li><li>Isikan Email valid ('test@test.id').</li><li>Isikan Review text.</li><li>Klik tombol 'Submit'.</li></ol>   | Sistem memproses ulasan dan menampilkan pesan konfirmasi keberhasilan hijau 'Thank you for your review.' di bawah form.                              | As Expected | PASSED     |           |
| TP-AEX-0002 | AEX-PCSR-0001 | AEX-PBCF-0008 | NEG      | P2           | 8          | <ol start="1"><li>Berada di halaman detail produk (/product_details/{id}).</li></ol>                                                | <ol start="1"><li>Isikan Name dan Email, namun kosongkan Review text.</li><li>Klik tombol 'Submit'.</li></ol>                                              | Sistem menahan pengiriman ulasan dan memicu HTML5 validation popup dari browser pada kolom wajib yang kosong. Data tidak tersubmit.                  | As Expected | PASSED     |           |
| TP-AEX-0002 | AEX-PCSR-0001 | AEX-PBCF-0009 | NEG      | P2           | 8          | <ol start="1"><li>Berada di halaman detail produk (/product_details/{id}).</li></ol>                                                | <ol start="1"><li>Isikan Name dan Review text, namun kosongkan Email.</li><li>Klik tombol 'Submit'.</li></ol>                                              | Sistem menahan pengiriman ulasan dan memicu HTML5 validation popup dari browser pada kolom wajib yang kosong. Data tidak tersubmit.                  | As Expected | PASSED     |           |
| TP-AEX-0002 | AEX-PCSR-0001 | AEX-PBCF-0010 | NEG      | P2           | 8          | <ol start="1"><li>Berada di halaman detail produk (/product_details/{id}).</li></ol>                                                | <ol start="1"><li>Isikan Name ('Okis Reviewer').</li><li>Isikan Email tanpa karakter @</li><li>Isikan Review text.</li><li>Klik tombol 'Submit'.</li></ol> | Browser/Sistem memunculkan tooltip peringatan validasi format email (misal: "Please include an '@' in the email address..."). Form tidak ter-submit. | As Expected | PASSED     |           |

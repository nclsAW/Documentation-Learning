# AEX-0008 Page Navigation & Scroll Behavior

## User Story

***

Sebagai pengguna situs Automation Exercise, saya ingin menavigasi halaman dengan lancar dan menggunakan fitur gulir ke atas agar saya dapat kembali ke bagian utama halaman tanpa harus menggeser layar secara manual.

## Pre-conditions

***

1. Browser Google Chrome versi terbaru terpasang dan terhubung ke internet.
2. Aplikasi web Automation Exercise dapat diakses melalui URL [Automation Exercise](https://automationexercise.com/) .
3. Halaman web dimuat penuh sehingga elemen navigasi dan tombol gulir dapat diinteraksi secara normal.

## Acceptance Criteria

***

1. Pengguna dapat menekan menu Test Cases pada bar navigasi dan sistem mengarahkan ke halaman Test Cases secara sukses.
2. Pengguna dapat melakukan gulir layar ke bawah hingga ke bagian dasar halaman (footer) dan tombol panah Scroll Up muncul secara dinamis di sudut kanan bawah.
3. Pengguna dapat menekan tombol panah Scroll Up dan sistem secara otomatis mengembalikan tampilan layar tepat ke bagian teratas halaman (header / hero banner).
4. Teks utama pada bagian teratas halaman kembali terlihat jelas setelah proses Scroll Up otomatis berhasil dieksekusi.
5. Pengguna dapat melakukan gulir layar ke atas secara manual tanpa tombol dan sistem tetap menampilkan kembali bagian header halaman dengan tepat.

## Test Scenario

***

| **TP**      | **Scene ID**  | **Test ID**   | **Type** | **Priority** | **AC Ref** | **Pre-condition**                                                                              | **Step**                                                                                                                                                                                                     | **Expected**                                                                                                            | **Actual**  | **Status** | **Notes** |
| ----------- | ------------- | ------------- | -------- | ------------ | ---------- | ---------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------- | ----------- | ---------- | --------- |
| TP-AEX-0006 | AEX-UNFS-0001 | AEX-PNSB-0001 | POS      | P1           | 1          | <p>Berada di Homepage<br><a href="https://automationexercise.com/">Automation Exercise</a></p> | <ol start="1"><li>Klik menu 'Test Cases' pada header navigasi.</li></ol>                                                                                                                                     | Pengguna berhasil diarahkan ke halaman /test\_cases dan konten daftar test cases tampil dengan sukses.                  | As Expected | PASSED     |           |
| TP-AEX-0006 | AEX-UNFS-0001 | AEX-PNSB-0003 | POS      | P2           | 2,5        | <p>Berada di Homepage<br><a href="https://automationexercise.com/">Automation Exercise</a></p> | <ol start="1"><li>Lakukan scroll layar ke bawah hingga bagian footer.</li><li>Lakukan scroll layar kembali ke atas secara manual (tanpa menekan tombol panah).</li><li>Verifikasi posisi viewport.</li></ol> | Layar merespons pergerakan scroll manual secara mulus dan mengembalikan tampilan teratas halaman (header) secara tepat. | As Expected | PASSED     |           |

Related content<br>

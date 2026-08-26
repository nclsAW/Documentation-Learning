# OHR-0010 KPIs & Key Performance Indicators

## User Story

***

Sebagai HR Admin, saya ingin membuat indikator penilaian sesuai job title agar tolok ukur evaluasi kinerja karyawan terdefinisi dengan jelas.

## Pre-condition

***

* Pengguna terautentikasi sebagai System Administrator / HR Admin.
* Pengguna berada di modul Performance pada menu Configure / KPIs.
* Master data job title sudah terkonfigurasi di dalam sistem.

## Acceptance Criteria

***

1. Pembuatan KPI: Sistem dapat membuat dan menyimpan indikator penilaian kinerja baru serta menghubungkannya ke job title tertentu.
2. Pengaturan Bobot dan Batas Nilai: Sistem dapat menentukan skala nilai minimal dan maksimal untuk setiap indikator KPI yang dibuat.
3. Pembaruan KPI: Sistem dapat mengubah atau memperbarui detail indikator KPI yang sudah ada tanpa merusak data evaluasi yang berjalan.
4. Validasi Field Wajib: Mengosongkan nama indikator KPI atau tidak memilih job title terkait akan memicu pesan peringatan error.

## Test Scenario

***

| **TP**      | **Scene ID** | **Test ID**             | **Type** | **Priority** | **AC Ref** | **Pre-condition**                                                                                                                                      | **Step**                                                                                                                                                                                                         | **Expected**                                                                                                                           | **Actual**  | **Status** | **Notes** |
| ----------- | ------------ | ----------------------- | -------- | ------------ | ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------- | ----------- | ---------- | --------- |
| TP-OHR-0004 | OHR-PEV-0001 | <p>OHR-KPI-<br>0001</p> | POS      | P1           | 1,2        | <ol start="1"><li>Login sebagai HR Admin.</li><li>Navigasi ke Performance → Configure → KPIs.</li></ol>                                                | <ol start="1"><li>Klik tombol Add.</li><li>Masukkan Key Performance Indicator</li><li>Pilih Job Title = "QA Engineer".</li><li>Masukkan Minimum Rating = 1 dan Maximum Rating = 100</li><li>Klik Save.</li></ol> | KPI baru berhasil disimpan, pesan sukses muncul, dan KPI terdaftar di tabel Key Performance Indicators sesuai Job Title yang dipilih.  | As Expected | PASSED     |           |
| TP-OHR-0004 | OHR-PEV-0001 | OHR-KPI-0002            | NEG      | P1           | 4          | <ol start="1"><li>Login sebagai HR Admin.</li><li>Berada di halaman Add KPI.</li></ol>                                                                 | <ol start="1"><li>Kosongkan kolom Key Performance Indicator.</li><li>Biarkan Job Title pada posisi – Select –.</li><li>Klik tombol Save.</li></ol>                                                               | Sistem menolak menyimpan data dan menampilkan validation error message "Required" di bawah kolom KPI dan Job Title.                    | As Expected | PASSED     |           |
| TP-OHR-0004 | OHR-PEV-0001 | OHR-KPI-0003            | NEG      | P2           | 2          | <ol start="1"><li>Berada di halaman Add KPI.</li></ol>                                                                                                 | <ol start="1"><li>Masukkan Key Performance Indicator valid dan pilih Job Title.</li><li>Masukkan Minimum Rating = 100 dan Maximum Rating = 10.</li><li>Klik Save.</li></ol>                                      | Sistem menolak pembuatan KPI dan menampilkan pesan kesalahan validasi (misal: "Maximum Rating should be greater than Minimum Rating"). | As Expected | PASSED     |           |
| TP-OHR-0004 | OHR-PEV-0001 | OHR-KPI-0004            | POS      | P2           | 3          | <ol start="1"><li>KPI "Kecepatan Penyelesaian Tiket QA" sudah terdaftar di database.</li><li>Berada di halaman daftar KPIs.</li></ol>                  | <ol start="1"><li>Cari KPI tersebut dan klik ikon Edit (pensil).</li><li>Ubah Maximum Rating dari 100 menjadi 5.</li><li>Klik Save.</li></ol>                                                                    | Perubahan berhasil disimpan, pesan sukses muncul, dan nilai Maximum Rating pada tabel berubah menjadi 5.                               | As Expected | PASSED     |           |
| TP-OHR-0004 | OHR-PEV-0001 | OHR-KPI-0005            | POS      | P3           | 1          | <ol start="1"><li>Terdapat beberapa KPI yang terikat pada Job Title berbeda.</li><li>Berada di halaman utama Performance → Configure → KPIs.</li></ol> | <ol start="1"><li>Pilih Job Title = "QA Engineer" pada filter pencarian.</li><li>Klik tombol Search.</li></ol>                                                                                                   | Tabel hasil pencarian menyaring data dan hanya menampilkan daftar KPI yang terhubung dengan Job Title "QA Engineer".                   | As Expected | PASSED     |           |

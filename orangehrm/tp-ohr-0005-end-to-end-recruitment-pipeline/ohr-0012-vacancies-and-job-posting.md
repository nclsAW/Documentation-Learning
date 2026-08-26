# OHR-0012 Vacancies & Job Posting

## User Story

***

Sebagai **HR Admin / Recruiter**, saya ingin membuat dan mengonfigurasi lowongan pekerjaan (_Job Vacancy_) baru, agar posisi yang dibutuhkan perusahaan dapat dibuka dan menerima lamaran kandidat.

## Pre-condition

***

* Pengguna terautentikasi sebagai **HR Admin / Recruiter**.
* Pengguna berada di modul **Recruitment** pada sub-menu **Vacancies** (`/recruitment/viewJobVacancies`).
* Master data _Job Title_ dan akun _Hiring Manager_ sudah terdaftar di sistem.

## Acceptance Criteria

***

1. **Pembuatan Lowongan:** Sistem dapat membuat dan menyimpan lowongan pekerjaan baru dengan mengisi _Vacancy Name_, _Job Title_, _Hiring Manager_, dan _Number of Positions_.
2. **Status Lowongan (Active/Closed):** Sistem dapat mengatur status publikasi lowongan menjadi aktif (_Active_) atau menonaktifkannya (_Closed/Inactive_).
3. **Pembaruan Detail Lowongan:** Sistem dapat mengedit dan memperbarui informasi detail lowongan pekerjaan yang sudah tersimpan pada tabel.
4. **Validasi Mandatory Fields:** Mengosongkan kolom wajib (_Vacancy Name_, _Job Title_, atau _Hiring Manager_) akan memicu pesan peringatan validasi (_Required_).

## Test Scenario

***

| **TP**      | **Scene ID** | **Test ID**  | **Type** | **Priority** | **AC Ref** | **Pre-condition**                                                                                                                                    | **Step**                                                                                                                                                                                                                                                                                                      | **Expected**                                                                                                          | **Actual**  | **Status** | **Notes** |
| ----------- | ------------ | ------------ | -------- | ------------ | ---------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------- | ----------- | ---------- | --------- |
| TP-OHR-0005 | OHR-ERP-0001 | OHR-VJP-0001 | POS      | P1           | 1,2        | <ol start="1"><li>Login sebagai HR Admin / Recruiter.</li><li>Navigasi ke Recruitment → Vacancies.</li></ol>                                         | <ol start="1"><li>Klik tombol Add.</li><li>Masukkan Vacancy Name (misal: "Senior QA Automation").</li><li>Pilih Job Title = "QA Engineer".</li><li>Ketik dan pilih Hiring Manager.</li><li>Masukkan Number of Positions = 2.</li><li>Pastikan toggle/checkbox Active tercentang.</li><li>Klik Save.</li></ol> | Lowongan baru berhasil dibuat, pesan sukses muncul, dan lowongan terdaftar pada tabel Vacancies dengan status Active. | As Expected | PASSED     |           |
| TP-OHR-0005 | OHR-ERP-0001 | OHR-VJP-0002 | NEG      | P1           | 4          | <ol start="1"><li>Login sebagai HR Admin / Recruiter.</li><li>Berada di halaman Add Vacancy.</li></ol>                                               | <ol start="1"><li>Kosongkan kolom Vacancy Name.</li><li>Biarkan Job Title pada posisi – Select –.</li><li>Kosongkan Hiring Manager.</li><li>Klik tombol Save.</li></ol>                                                                                                                                       | Sistem menolak menyimpan dan menampilkan validation error message "Required" pada ketiga kolom wajib tersebut.        | As Expected | PASSED     |           |
| TP-OHR-0005 | OHR-ERP-0001 | OHR-VJP-0003 | POS      | P2           | 2          | <ol start="1"><li>Lowongan "Senior QA Automation" berstatus Active.</li><li>Berada di daftar Vacancies.</li></ol>                                    | <ol start="1"><li>Cari lowongan tersebut dan klik ikon Edit.</li><li>Hapus centang / nonaktifkan Active toggle.</li><li>Klik Save.</li></ol>                                                                                                                                                                  | Status lowongan berhasil diperbarui menjadi Closed / Inactive dan tidak menerima lamaran baru.                        | As Expected | PASSED     |           |
| TP-OHR-0005 | OHR-ERP-0001 | OHR-VJP-0004 | POS      | P2           | 3          | <ol start="1"><li>Lowongan "Senior QA Automation" sudah terdaftar di database.</li><li>Berada di halaman daftar Vacancies.</li></ol>                 | <ol start="1"><li>Klik ikon Edit pada lowongan terkait.</li><li>Ubah Number of Positions dari 2 menjadi 5.</li><li>Tambahkan teks pada kolom Description.</li><li>Klik Save.</li></ol>                                                                                                                        | Detail lowongan berhasil diperbarui dan data terbaru tampil pada tabel Vacancies.                                     | As Expected | PASSED     |           |
| TP-OHR-0005 | OHR-ERP-0001 | OHR-VJP-0005 | POS      | P3           | 1          | <ol start="1"><li>Terdapat beberapa lowongan dengan Job Title berbeda di database.</li><li>Berada di halaman utama Recruitment → Vacancies</li></ol> | <ol start="1"><li>Pilih Job Title = "QA Engineer" pada filter pencarian.</li><li>Klik tombol Search.</li></ol>                                                                                                                                                                                                | Tabel menyaring daftar dan hanya menampilkan lowongan yang memiliki Job Title "QA Engineer".                          | As Expected | PASSED     |           |

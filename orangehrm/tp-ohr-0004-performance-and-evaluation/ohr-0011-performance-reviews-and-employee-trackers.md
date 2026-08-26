# OHR-0011 Performance Reviews & Employee Trackers

## User Story

***

Sebagai Karyawan, Atasan, dan Rekan Kerja, saya ingin melakukan evaluasi mandiri (self-assessment), penilaian dari atasan, maupun peer review agar proses evaluasi kinerja berjalan secara menyeluruh.

## Pre-condition

***

* Pengguna terdaftar sebagai Karyawan, Atasan (Supervisor), atau Rekan Kerja (Peer).
* Siklus evaluasi kinerja (performance review cycle) telah diinisiasi oleh HR Admin.
* Pengguna berada di modul Performance pada menu Manage Reviews / My Reviews.

## Acceptance Criteria

***

1. Self-Assessment: Karyawan dapat mengisi dan mengirimkan formulir penilaian mandiri sesuai dengan indikator KPI yang ditentukan.
2. Penilaian Atasan: Atasan dapat meninjau, memberi skor, dan memberikan umpan balik pada formulir evaluasi bawahan langsungnya.
3. Peer Review: Rekan kerja yang ditunjuk dapat mengisi formulir evaluasi sejawat (peer review) untuk karyawan terkait.
4. Validasi Rentang Skor: Menginput skor evaluasi di luar skala/rentang nilai yang telah ditetapkan akan ditolak oleh sistem.

## Test Scenario

***

| **TP**      | **Scene ID** | **Test ID**  | **Type** | **Priority** | **AC Ref** | **Pre-condition**                                                                                                                                                                        | **Step**                                                                                                                                                                                                                  | **Expected**                                                                                                                                 | **Actual**  | **Status** | **Notes** |
| ----------- | ------------ | ------------ | -------- | ------------ | ---------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------- | ----------- | ---------- | --------- |
| TP-OHR-0004 | OHR-PEV-0002 | OHR-PRE-0001 | POS      | P1           | 1          | <ol start="1"><li>Karyawan login ke sistem.</li><li>HR Admin telah menginisiasi Performance Review status In Progress.</li><li>Navigasi ke Performance → My Reviews</li></ol>            | <ol start="1"><li>Klik Evaluate pada formulir review aktif.</li><li>Masukkan Rating mandiri pada kolom Self (misal: 4 dari skala 1-5).</li><li>Isi Comment evaluasi mandiri.</li><li>Klik tombol Save / Submit.</li></ol> | Evaluasi mandiri berhasil tersimpan, pesan sukses muncul, dan status progres formulir terbarui.                                              | As Expected | PASSED     |           |
| TP-OHR-0004 | OHR-PEV-0002 | OHR-PRE-0002 | POS      | P1           | 2          | <ol start="1"><li>Karyawan telah mengisi Self-Assessment.</li><li>Login sebagai Supervisor dari karyawan tersebut.</li><li>Navigasi ke Performance → Manage Reviews/My Reviews</li></ol> | <ol start="1"><li>Pilih formulir review karyawan uji.</li><li>Masukkan Rating pada kolom Supervisor.</li><li>Isi Supervisor Comment / Feedback.</li><li>Klik tombol Save / Submit.</li></ol>                              | Nilai dan umpan balik dari atasan berhasil tersimpan secara akurat mendampingi skor mandiri karyawan.                                        | As Expected | PASSED     |           |
| TP-OHR-0004 | OHR-PEV-0002 | OHR-PRE-0003 | NEG      | P1           | 3          | <ol start="1"><li>KPI terkonfigurasi dengan skala nilai 1 sampai 5.</li><li>User berada di halaman pengisian evaluasi kinerja (Evaluate).</li></ol>                                      | <ol start="1"><li>Masukkan nilai Rating = 10 (melebihi batas maksimal 5).</li><li>Klik tombol Save atau pindah fokus kolom.</li></ol>                                                                                     | Sistem menolak penginputan dan menampilkan validation error message (misal: "Should be less than or equal to 5" / "Invalid Rating").         | As Expected | PASSED     |           |
| TP-OHR-0004 | OHR-PEV-0002 | OHR-PRE-0004 | POS      | P2           | 4          | <ol start="1"><li>Evaluasi kinerja telah diselesaikan dan di-submit oleh Supervisor.</li><li>Status review berubah menjadi Approved / Completed.</li></ol>                               | <ol start="1"><li>Buka kembali formulir review karyawan terkait.</li><li>Coba ubah nilai Rating atau Comment</li></ol>                                                                                                    | Seluruh kolom input pada formulir dalam kondisi ter-lock (read-only), tombol edit/submit dinonaktifkan, dan skor tidak dapat diubah kembali. | As Expected | PASSED     |           |
| TP-OHR-0004 | OHR-PEV-0002 | OHR-PRE-0005 | POS      | P2           | 1,2        | <ol start="1"><li>User berada di halaman pengisian evaluasi kinerja.</li></ol>                                                                                                           | <ol start="1"><li>Masukkan Rating dan Comment parsial (belum lengkap seluruh KPI).</li><li>Klik tombol Save Draft.</li><li>Log out lalu log in kembali dan buka formulir yang sama.</li></ol>                             | Data nilai dan catatan yang diisi sebelumnya tetap tersimpan dalam bentuk draf dan status review tetap In Progress.                          | As Expected | PASSED     |           |

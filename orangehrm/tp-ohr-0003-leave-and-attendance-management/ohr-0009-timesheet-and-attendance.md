# OHR-0009 Timesheet & Attendance

## User Story

***

Sebagai Karyawan dan HR Admin, saya ingin mencatat jam kerja melalui clock-in/clock-out serta mengelola timesheet dan rekap absensi agar riwayat kehadiran tercatat dengan akurat.

## Pre-condition

***

* Pengguna terautentikasi di dalam sistem.
* Pengguna berada di modul Time pada menu Attendance atau Timesheets.

## Acceptance Criteria

***

1. Clock-in dan Clock-out: Karyawan dapat mencatat waktu masuk (clock-in) dan waktu keluar (clock-out) secara real-time.
2. Pencatatan Jam Kerja dan Lembur: Sistem dapat menghitung total jam kerja harian serta mencatat pengajuan jam lembur.
3. Rekap Absensi: HR Admin dapat menghasilkan dan melihat rekap absensi harian maupun bulanan seluruh karyawan.
4. Validasi Urutan Waktu: Melakukan clock-out sebelum melakukan clock-in atau menginput waktu keluar yang lebih awal dari waktu masuk akan ditolak oleh sistem.

## Test Scenario

***

| **TP**      | **Scene ID** | **Test ID**  | **Type** | **Priority** | **AC Ref** | **Pre-condition**                                                                                                                                                                          | **Step**                                                                                                                                                                   | **Expected**                                                                                                                              | **Actual**  | **Status** | **Notes** |
| ----------- | ------------ | ------------ | -------- | ------------ | ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------- | ----------- | ---------- | --------- |
| TP-OHR-0003 | OHR-LAM-0003 | OHR-TMA-0001 | POS      | P1           | 1          | <ol start="1"><li>Karyawan login ke sistem.</li><li>Status kehadiran saat ini: Punched Out.</li><li>Navigasi ke Time → Attendance → Punch In/Out.</li></ol>                                | <ol start="1"><li>Cek tanggal &#x26; waktu yang tertera.</li><li>Masukkan Note.</li><li>Klik tombol In (Punch In).</li></ol>                                               | Sistem berhasil mencatat waktu Punch In, pesan sukses muncul, dan halaman otomatis berubah menampilkan formulir Punch Out.                | As Expected | PASSED     |           |
| TP-OHR-0003 | OHR-LAM-0003 | OHR-TMA-0002 | POS      | P1           | 1,2        | <ol start="1"><li>Karyawan dalam status Punched In dari TC-OHR-TIM-ATT-001.</li><li>Berada di halaman Time → Attendance → Punch In/Out.</li></ol>                                          | <ol start="1"><li>Masukkan Note (misal: "Selesai Jam Kerja").</li><li>Klik tombol Out (Punch Out).</li><li>Navigasi ke Time → Attendance → My Records.</li></ol>           | Sistem mencatat waktu Punch Out dan menghitung total durasi jam kerja (Total Hours) secara akurat pada tabel riwayat My Records.          | As Expected | PASSED     |           |
| TP-OHR-0003 | OHR-LAM-0003 | OHR-TMA-0003 | NEG      | P1           | 4          | Karyawan berada di halaman Punch Out (misal waktu Punch In terdistribusi jam 08:00 AM).                                                                                                    | <ol start="1"><li>Ubah/edit kolom Time pada Punch Out menjadi jam 07:00 AM (lebih awal dari Punch In).</li><li>Klik tombol Out.</li></ol>                                  | Sistem menolak pencatatan dan menampilkan validation error message (misal: "Out time should be later than In time").                      | As Expected | PASSED     |           |
| TP-OHR-0003 | OHR-LAM-0003 | OHR-TMA-0004 | POS      | P2           | 2          | <ol start="1"><li>User login sebagai Karyawan.</li><li>Navigasi ke Time → Timesheets → My Timesheets.</li></ol>                                                                            | <ol start="1"><li>Klik Edit pada minggu berjalan.</li><li>Pilih Project &#x26; Activity.</li><li>Masukkan jumlah jam kerja harian (misal: 8 jam) dan jam lembur.</li></ol> | Timesheet berhasil disimpan/dikirimkan untuk persetujuan, dan kalkulasi Total Hours mingguan terakumulasi otomatis secara tepat.          | As Expected | PASSED     |           |
| TP-OHR-0003 | OHR-LAM-0003 | OHR-TMA-0005 | POS      | P2           | 2          | <ol start="1"><li>HR Admin login sebagai Admin.</li><li>Navigasi ke Time → Timesheets → Employee Timesheets.</li></ol>                                                                     | <ol start="1"><li>View salah satu laporan.</li><li>Klik tombol Reject</li></ol>                                                                                            | Status laporan berubah menjadi Rejected, sehingga laporan timesheet karyawan tidak diterima.                                              | As Expected | PASSED     |           |
| TP-OHR-0003 | OHR-LAM-0003 | OHR-TMA-0006 | POS      | P1           | 3          | <ol start="1"><li>HR Admin login ke sistem.</li><li>Beberapa karyawan telah memiliki riwayat Punch In/Out.</li><li>Navigasi ke Time → Reports → Attendance Total Summary Report.</li></ol> | <ol start="1"><li>Pilih rentang tanggal pencarian (From - To Date).</li><li>Pilih Job Title atau Employee Name (opsional).</li><li>Klik View / Generate.</li></ol>         | Sistem memproses dan menampilkan tabel rekapitulasi absensi seluruh karyawan lengkap dengan total jam kerja harian/bulanan secara akurat. | As Expected | PASSED     |           |

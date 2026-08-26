# TP-OHR-0003 Leave & Attendance Management

## Objective & Scope

***

* **Objective:** Memvalidasi seluruh fungsi pengelolaan cuti dan pencatatan absensi di dalam sistem OrangeHRM untuk memastikan pengaturan kuota cuti, alur persetujuan pengajuan (approval workflow), pencatatan jam kerja (timesheet/clock-in/out), dan kalkulasi rekap absensi berjalan secara akurat dan real-time.
* **In-Scope:** Pengujian fungsional pada modul Leave Configuration & Entitlements, Leave Application Workflow (pengajuan, notifikasi, persetujuan/penolakan oleh atasan), serta Timesheet & Attendance Tracking (clock-in/out, rekap lembur, dan laporan absensi).
* **Out-of-Scope:** Pengujian pemotongan gaji/payroll berdasarkan absensi dan pengujian integrasi hardware mesin absensi biometrik fisik.

## Environment & Test Setup

***

* **Target URL:** [OrangeHRM](https://opensource-demo.orangehrmlive.com/)
* **Browser/Platform:** Google Chrome (Latest Version) / Desktop.
* **Test Data Requirement:**
  * Membutuhkan minimal 2 akun uji aktif: 1 akun Employee (sebagai pengaju cuti/absensi) dan 1 akun Line Manager/Supervisor (sebagai approver) yang sudah terhubung dalam hierarki atasan-bawahan.
  * Master data karyawan (Employee Profiles) dari TP-OHR-0002 sudah siap dan aktif.
  * Konfigurasi tipe cuti (Leave Types seperti Cuti Tahunan, Sakit) dan kuota awal (Entitlements) sudah terisi untuk akun karyawan uji.

## Test Strategy & Approach

***

* **Positive Testing:** Mengeksekusi pengajuan cuti dengan saldo kuota mencukupi, melakukan simulasi approval/rejection oleh Supervisor, serta mencatat clock-in/clock-out sesuai jam kerja standar untuk memastikan alur kerja sukses dan status/saldo cuti terbarui secara real-time.
* **Negative Path:** Memasukkan parameter tidak valid (mengajukan cuti melebihi sisa kuota, pengajuan tanggal mundur tanpa izin, clock-out tanpa clock-in, atau input jam lembur bernilai negatif) untuk memvalidasi penolakan sistem dan error handling.
* **State Machine & Logic Validation:** Memastikan perubahan status pengajuan (Pending Approval → Approved / Rejected / Cancelled) merefleksikan pengembalian atau pemotongan kuota cuti secara konsisten.

## Risks & Dependencies

***

* **Dependency:** Pengujian modul ini sangat bergantung pada keberhasilan TP-OHR-0002 untuk relasi atasan-bawahan (Supervisor-Subordinate mapping) dan TP-OHR-0001 untuk alokasi zona waktu kantor. Jika struktur atasan belum terbentuk, alur approval workflow tidak dapat dieksekusi.
* **Risk:** Perbedaan konfigurasi zona waktu (timezone) antara server, lokasi kantor, dan browser tester dapat menyebabkan ketidaksesuaian pencatatan tanggal cuti atau timestamp clock-in/out.
* **Mitigation:** Pastikan zona waktu pada sistem OrangeHRM, database, dan perangkat tester telah disinkronkan ke zona waktu yang sama sebelum pengujian fungsi attendance dan leave dimulai.

# TP-OHR-0004 Performance & Evaluation

## Objective & Scope

***

* **Objective:** Memvalidasi fungsi penilaian kinerja karyawan di dalam sistem OrangeHRM untuk memastikan penyusunan indikator kinerja (KPIs), pembuatan performance reviews, serta mekanisme evaluasi mandiri dan penilaian dari atasan berjalan secara akurat dan terstruktur.
* **In-Scope:** Pengujian fungsional pada modul Key Performance Indicators (KPIs) & Tracker, pembuatan skema Performance Review/Appraisal, serta eksekusi Self-Assessment dan Supervisor Review.
* **Out-of-Scope:** Pengujian kalkulasi bonus/penyesuaian gaji berbasis hasil evaluasi kinerja dan konfigurasi master data jabatan.

## Environment & Test Setup

***

* **Target URL:** [OrangeHRM](https://opensource-demo.orangehrmlive.com/)
* **Browser/Platform:** Google Chrome (Latest Version) / Desktop.
* **Test Data Requirement:**
  * Membutuhkan minimal 2 akun uji aktif: 1 akun Employee (pihak yang dinilai) dan 1 akun Line Manager/Supervisor (penilai) yang sudah terikat dalam hierarki organisasi dari TP-OHR-0002.
  * Master data Job Title dari TP-OHR-0001 sudah tersedia untuk dipasangkan dengan indikator KPI terkait.

## Test Strategy & Approach

***

* **Positive Testing:** Mengeksekusi pembuatan indikator KPI sesuai jabatan, menginisiasi siklus review, mengisi nilai/skor evaluasi self-assessment dan supervisor review, serta menyelesaikannya hingga status Activated/Completed untuk memastikan skor akhir terkalkulasi dengan benar.
* **Negative Path:** Memasukkan parameter anomali (input nilai skor di luar rentang/skala yang ditentukan, menyimpan formulir review tanpa mengisi mandatory fields, atau mencoba mengubah skor evaluasi setelah status review difinalisasi/ditutup) untuk memvalidasi error handling dan proteksi data.
* **State Machine Validation:** Memastikan perubahan alur status evaluasi (Draft -> In Progress -> Submitted → Approved/Completed) berjalan secara konsisten dan membatasi hak akses edit sesuai peran user.

## Risks & Dependencies

***

* **Dependency:** Pengujian modul ini sangat bergantung pada keberhasilan TP-OHR-0001 dan TP-OHR-0002. Tanpa data jabatan dan struktur atasan yang valid, siklus penugasan evaluasi kinerja tidak dapat dibuat atau dikirim ke penilai.
* **Risk:** Perubahan status review yang dilakukan sebelum penilaian selesai dapat mengunci (lock) formulir sehingga skor tidak bisa di-input atau diperbaiki.
* **Mitigation:** Pastikan skenario pengujian mencakup verifikasi simpan sementara (Save Draft) sebelum melakukan submisi final (Submit/Approve).

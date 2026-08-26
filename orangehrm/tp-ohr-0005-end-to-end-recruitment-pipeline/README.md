# TP-OHR-0005 End-to-End Recruitment Pipeline

## Objective & Scope

***

* **Dependency:** Pengujian modul ini sangat bergantung pada keberhasilan TP-OHR-0001 dan TP-OHR-0002 Tanpa data jabatan dan struktur atasan yang valid, siklus penugasan evaluasi kinerja tidak dapat dibuat atau dikirim ke penilai.
* **In-Scope:** Pengujian fungsional pada modul _Vacancies Management_, pendaftaran kandidat (manual/apply), serta alur _Selection Pipeline_ (_Shortlist_, _Schedule Interview_, _Job Offer_, _Hire/Reject_).
* **Out-of-Scope:** Pengujian integrasi ke _Job Portal_ pihak ketiga (seperti LinkedIn/JobStreet) dan pengiriman email otomatis ke server SMTP eksternal.

## Environment & Test Setup

***

* **Target URL:** [OrangeHRM](https://opensource-demo.orangehrmlive.com/)
* **Browser/Platform:** Google Chrome (Latest Version) / Desktop.
* **Test Data Requirement:**
  * Membutuhkan akun uji dengan role HR Admin / Recruiter dan akun Hiring Manager/Interviewer.
  * Master data posisi/jabatan (Job Title) dan lokasi kantor sudah tersedia dari TP-OHR-0001.
  * Menyiapkan sampel file resume/CV kandidat (PDF/DOCX) dengan variasi ukuran dan format berkas.

## Test Strategy & Approach

***

* **Positive Testing:** Mengeksekusi pembuatan lowongan (vacancy), mendaftarkan kandidat baru beserta lampiran CV, memindahkan status kandidat secara berurutan (Shortlist → Schedule Interview -> Offer -> Hire), serta memverifikasi jadwal wawancara terkirim ke interviewer.
* **Negative Path:** Memasukkan parameter tidak valid (mengunggah berkas CV dengan format yang tidak didukung/terlalu besar, mengosongkan mandatory field data kandidat, menduplikat pendaftaran kandidat dengan email yang sama, atau menjadwalkan wawancara di masa lalu) untuk memvalidasi error handling dan penolakan sistem.
* **Pipeline Status Transition Validation:** Memastikan sistem membatasi perubahan status kandidat agar sesuai alur (misal: kandidat tidak bisa langsung di-Hire tanpa melalui tahap Shortlist/Interview terlebih dahulu) dan status lowongan berkurang saat kandidat berhasil di-Hire.

## Risks & Dependencies

***

* **Dependencies:** Pengujian bergantung pada TP-OHR-0001 (Master Job Titles) dan TP-OHR-0002 (Karyawan terdaftar sebagai Hiring Manager).
* **Risks & Mitigation:** Risk: Berkas CV terkorupsi saat diunggah. Mitigation: Sertakan pengujian _Download Check_ pada lampiran CV.

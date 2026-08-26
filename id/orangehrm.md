# OrangeHRM

## Description <a href="#description" id="description"></a>

***

OrangeHRM adalah platform Manajemen Sumber Daya Manusia (HRMS) berbasis web yang dirancang untuk mengelola seluruh siklus hidup karyawan dalam sebuah organisasi. Aplikasi ini menyediakan fungsionalitas HR yang komprehensif, mencakup pengaturan struktur organisasi dan hak akses (Admin Module), manajemen basis data personel (PIM), konfigurasi dan pengajuan cuti (Leave & Attendance), pelacakan evaluasi kinerja (Performance), hingga alur publikasi lowongan kerja dan pelacakan kandidat (End-to-End Recruitment).

## Test Objective & Scope <a href="#test-objective-and-scope" id="test-objective-and-scope"></a>

***

* **Test Objective:** Memvalidasi keandalan fungsionalitas utama (_core HR operations_), memastikan konsistensi alur kerja (_workflow_) antar-role (Admin, ESS/Employee, Supervisor), serta menguji integritas validasi data pada form input untuk mencegah anomali basis data karyawan.
* **In Scope:**
  * **Admin & Org Setup:** Pengaturan struktur hierarki, _Job Titles_, dan _Role-Based Access Control_ (RBAC).
  * **Personnel Information (PIM):** Penambahan data karyawan baru (Manual & CSV Import), pelaporan kustom, dan _custom fields_.
  * **Leave Management:** Konfigurasi kuota cuti, hierarki _approval workflow_, dan pencatatan _timesheet_.
  * **Performance:** Pembuatan KPI, siklus _performance review_, dan pelacakan metrik karyawan.
  * **Recruitment:** Publikasi _vacancies_, _resume parsing_ kandidat, dan manajemen status wawancara.
* **Out of Scope:** Automated Security/Penetration Testing, Stress/Load Testing di level infrastruktur server, pengujian integrasi _Payroll_ pihak ketiga, dan pengujian API _backend_ secara terpisah (fokus pada End-to-End Manual UI Testing).

## Test Environment <a href="#test-environment" id="test-environment"></a>

***

| **Parameter**        | **Detail**                                              |
| -------------------- | ------------------------------------------------------- |
| URL                  | [OrangeHRM](https://opensource-demo.orangehrmlive.com/) |
| Browser              | Google Chrome                                           |
| OS                   | Windows 11                                              |
| Test Management Tool | Jira                                                    |
| Documentation Tool   | Confluence                                              |

## Execution Summary & Metrics <a href="#execution-summary-and-metrics" id="execution-summary-and-metrics"></a>

***

### Overall Test Case Execution Status <a href="#overall-test-case-execution-status" id="overall-test-case-execution-status"></a>

| **Status**      | **Jumlah Test Case** | **Persentase** |
| --------------- | -------------------- | -------------- |
| Passed          | 95                   | 91.35%         |
| Failed          | 9                    | 8.65%          |
| Blocked         | 0                    | 0              |
| Total Test Case | 104                  | 100%           |

### Defect Summary by Severity <a href="#defect-summary-by-severity" id="defect-summary-by-severity"></a>

| **Severity**     | **Open** | **Resolved/Closed** | **Total Bug** |
| ---------------- | -------- | ------------------- | ------------- |
| Critical/Blocker | 0        | 0                   | 0             |
| High             | 8        | 0                   | 8             |
| Medium           | 0        | 0                   | 0             |
| Low/Minor        | 1        | 0                   | 1             |
| Total            | 9        | 0                   | 9             |

## Detail Break-down Task/Module <a href="#detail-break-down-task-module" id="detail-break-down-task-module"></a>

***

### Module 1: Admin Module & Organization Setup (TP-OHR-0001) <a href="#module-1-admin-module-and-organization-setup-tp-ohr-0001" id="module-1-admin-module-and-organization-setup-tp-ohr-0001"></a>

* **Related Ticket:**
  * OHR-0001 \[QA] Organization Structure
  * OHR-0002 \[QA] Job & Titles
  * OHR-0003 \[QA] User & Role Management
* **Coverage:** Manajemen hierarki perusahaan, penentuan _job title_, dan pengaturan hak akses pengguna berdasarkan _role_ (Admin vs ESS).
* **Highlight Log:**
  * Modul _Organization Structure_ berhasil menyimpan hierarki cabang perusahaan secara presisi.
  * _User & Role Management_ berjalan baik, namun ditemukan isu eskalasi hak akses (Medium) di mana pengguna ESS dapat melihat menu konfigurasi Admin jika memiliki URL _direct link_.

### Module 2: Personnel Information Management (TP-OHR-0002) <a href="#module-2-personnel-information-management-tp-ohr-0002" id="module-2-personnel-information-management-tp-ohr-0002"></a>

* **Related Ticket:**
  * OHR-0004 \[QA] Add & Import Employee
  * OHR-0005 \[QA] Custom Fields & Attachments
  * OHR-0006 \[QA] Search & Custom Reporting
* **Coverage:** Registrasi data karyawan manual, _bulk import_ menggunakan CSV, pengunggahan dokumen lampiran, dan penarikan laporan operasional.
* **Highlight Log:**
  * Fungsionalitas _Add Employee_ secara manual berjalan lancar dan otomatis membuatkan profil _login_ yang terhubung.
  * Fitur _Import Employee_ mengalami kendala kritis ketika format tanggal lahir di CSV menggunakan `DD/MM/YYYY` alih-alih standar sistem `YYYY-MM-DD`.

### Module 3: Leave & Attendance Management (TP-OHR-0003) <a href="#module-3-leave-and-attendance-management-tp-ohr-0003" id="module-3-leave-and-attendance-management-tp-ohr-0003"></a>

* **Related Ticket:**
  * OHR-0007 \[QA] Leave Configuration
  * OHR-0008 \[QA] Leave Request Workflow
  * OHR-0009 \[QA] Timesheet & Attendance
* **Coverage:** Penentuan kuota cuti tahunan, alur pengajuan dan persetujuan cuti oleh _Supervisor_, serta pencatatan _punch-in/punch-out_ harian.
* **Highlight Log:**
  * _Workflow approval_ cuti berhasil mengirimkan notifikasi email secara _real-time_ kepada _Supervisor_ yang bersangkutan.
  * Sistem gagal memvalidasi saldo cuti, memungkinkan karyawan mengajukan hari libur yang melebihi sisa kuota tanpa peringatan _error_.

### Module 4: Performance & Evaluation (TP-OHR-0004) <a href="#module-4-performance-and-evaluation-tp-ohr-0004" id="module-4-performance-and-evaluation-tp-ohr-0004"></a>

* **Related Ticket:**
  * OHR-0010 \[QA] KPIs & Key Performance Indicators
  * OHR-0011 \[QA] Performance Reviews & Employee Trackers
* **Coverage:** Pembuatan metrik KPI spesifik per divisi dan pelacakan evaluasi kinerja bulanan/tahunan antar karyawan.
* **Highlight Log:**
  * Proses _Performance Reviews_ (360-degree feedback) dapat diselesaikan dan disimpan dengan akurat.
  * _Employee Trackers_ kadang mengalami keterlambatan sinkronisasi status (UI _freeze_) saat menyimpan _log feedback_ dalam teks panjang.

### Module 5: End-to-End Recruitment Pipeline (TP-OHR-0005) <a href="#module-5-end-to-end-recruitment-pipeline-tp-ohr-0005" id="module-5-end-to-end-recruitment-pipeline-tp-ohr-0005"></a>

* **Related Ticket:**
  * OHR-0012 \[QA] Vacancies & Job Posting
  * OHR-0013 \[QA] Candidates Application
  * OHR-0014 \[QA] Shortlisting & Interview
* **Coverage:** Publikasi halaman lowongan, pelacakan proses lamaran (Resume, _Shortlisting_), hingga penjadwalan tahap wawancara.
* **Highlight Log:**
  * Publikasi _Vacancies_ terhubung langsung ke halaman _Careers_ eksternal tanpa kendala.
  * Modul _Shortlisting & Interview_ mengalami kegagalan unggah dokumen PDF di atas 5MB tanpa memunculkan pesan validasi batas ukuran _file_.

## Key Defect Log <a href="#key-defect-log" id="key-defect-log"></a>

***

| **Jira Key** | **Bug Summary**                                                                                                                                                                                                                                                                     | **Severity** | **Status** | **Module**                |
| ------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | ---------- | ------------------------- |
| KAN-56       | Sistem berhasil menghentikan sesi di server saat logout, namun gagal membersihkan cache browser karena tidak menerapkan header Cache-Control. Akibatnya, data sensitif pada dashboard masih dapat diintip oleh pengguna lain dengan cara menekan tombol Back pada navigasi browser. | High         | Open       | Admin Module              |
| KAN-57       | Sistem gagal menghentikan proses eksekusi penghapusan parent node meskipun pesan pencegahan telah ditampilkan, sehingga child node ikut terhapus secara tidak sengaja.                                                                                                              | High         | Open       | Admin Module              |
| KAN-58       | OrangeHRM mengizinkan penghapusan Job Title yang masih terikat pada karyawan aktif tanpa adanya pembatasan _integrity constraint_, yang berpotensi menyebabkan _orphaned record_.                                                                                                   | High         | Open       | Job Titles                |
| KAN-59       | Modul User Management tidak mevalidasi keberadaan akun sebelumnya, sehingga memungkinkan pembuatan akun ganda (_duplicate account_) untuk karyawan yang sama.                                                                                                                       | High         | Open       | User Management           |
| KAN-60       | Pencarian Laporan Kustom gagal memfilter data jika pencarian dilakukan via _free-text_ (_enter/click search_) tanpa memilih opsi dari _dropdown suggestion_.                                                                                                                        | Low          | Open       | Search & Custom Reporting |
| KAN-61       | Sistem meloloskan pendaftaran kandidat baru dengan email yang sudah terdaftar pada _vacancy_ yang sama tanpa memunculkan validasi duplikasi.                                                                                                                                        | High         | Open       | Candidates Application    |
| KAN-62       | Form penjadwalan wawancara tidak memiliki validasi tanggal, sehingga sistem tetap mengizinkan penyimpanan jadwal wawancara di masa lalu (_past date_).                                                                                                                              | High         | Open       | Shortlisting & Interview  |

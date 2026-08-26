# Introduction

Dokumentasi ini merupakan representasi penulisan teknis berbasis _black-box audit_ dan eksplorasi fungsional langsung pada lingkungan _production-ready/dummy staging_ publik. Dokumen disusun menggunakan standardisasi formal industri (SOP, arsitektur, dan integrasi API) untuk merekonstruksi alur sistem dari perspektif _technical writer_, meskipun proses penyusunannya tidak melalui tahapan SDLC/prosedur internal tim pengembang secara langsung.

### Metodologi & Ruang Lingkup:

* **Manual Testing Matrix (Happy, Negative & Edge Cases):** Pengujian fungsional modul difokuskan pada skenario _Happy Path_ (alur normal), _Negative Path_ (validasi input/error handling), serta pengujian _Edge Cases_ tertentu yang dipetakan sebagai bagian dari skenario negatif untuk melihat batas ketahanan sistem.
* **Module Breakdown & Scope Definition (Jira):** Setiap modul dipisahkan secara independen ke dalam Jira Task yang memuat deskripsi awal, batasan _scope_, dependensi fitur, serta _sub-task_ teknis terkait.
* **Issue Tracking & Bug Reporting (Jira):** Temuan anomali, _bug_, atau kegagalan validasi dicatat langsung sebagai _Issue/Bug Ticket_ pada modul yang bersangkutan, lengkap dengan _steps to reproduce_, _expected vs actual behavior_, dan _severity level_.
* **Centralized Live Feedback Document (Confluence):** _Catatan Adaptasi:_ Mengingat pengujian dilakukan langsung pada satu versi _live production dummy_ (bukan _multi-version release cycle_), pencatatan _feedback_ dan temuan sistemik disatukan ke dalam satu dokumen Live Documentation & Feedback Hub terpusat untuk seluruh aplikasi agar progres review tetap konsolidatif.

### Kategori Dokumentasi yang Tersedia:

* **Module Scope & Task Specifications (Jira Structure):**
  * Definisi fungsionalitas tiap modul aplikasi.
  * Rincian batasan kerja (_in-scope_ vs _out-of-scope_) dan kriteria penerimaan (_acceptance criteria_).
* **Test Scenario & Execution Logs:**
  * Matriks pengujian manual (_Happy Path_, _Negative Path_, dan _Edge Cases_).
  * Log eksekusi parameter input dan respons sistem nyata.
* **Issue Management & Bug Reports:**
  * Tiket pelaporan _bug_ berbasis modul di Jira.
  * Dokumentasi reproduksi masalah dan dampak teknisnya terhadap modul lain.
* **System Feedback & Review Runbook (Confluence Live Doc):**
  * Ringkasan evaluasi fungsional aplikasi secara menyeluruh.
  * Catatan _technical improvement_ dan rekomendasi perbaikan untuk iterasi berikutnya.

{% hint style="info" %}
Portofolio ini berfokus pada eksekusi manual dan dokumentasi terstruktur berdasarkan kapabilitas yang dapat diakses langsung. Detail dan metrik tambahan akan terus diperbarui secara berkala seiring berjalannya review teknis lanjutan maupun di proyek selanjutnya.
{% endhint %}

# OHR-0008 Leave Request Workflow

## User Story

***

Sebagai Karyawan dan Atasan, saya ingin mengajukan dan memproses persetujuan cuti agar pengajuan cuti tercatat dan statusnya dapat diperbarui.

## Pre-condition

***

* Pengguna terdaftar sebagai Karyawan (pengaju) dan Atasan/Line Manager (approver).
* Karyawan memiliki sisa kuota cuti yang cukup.
* Pengguna berada di modul Leave pada menu Apply / Leave List.

## Acceptance Criteria

***

1. Pengajuan Cuti: Karyawan dapat mengajukan cuti dengan memilih tipe cuti, tanggal, dan alasan pengajuan.
2. Notifikasi dan Status Pending: Setelah pengajuan dikirim, atasan menerima notifikasi dan status pengajuan menjadi pending approval.
3. Persetujuan dan Penolakan: Atasan dapat menyetujui (approve) atau menolak (reject) pengajuan cuti, dan sisa kuota cuti karyawan akan berkurang otomatis jika disetujui.
4. Validasi Sisa Kuota: Mengajukan cuti yang melebihi sisa kuota yang dimiliki akan ditolak oleh sistem.

## Test Scenario

***

| **TP**      | **Scene ID** | **Test ID**  | **Type** | **Priority** | **AC Ref** | **Pre-condition**                                                                                                                                                                                     | **Step**                                                                                                                                                                                                                               | **Expected**                                                                                                                             | **Actual**  | **Status** | **Notes** |
| ----------- | ------------ | ------------ | -------- | ------------ | ---------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- | ----------- | ---------- | --------- |
| TP-OHR-0002 | OHR-LAM-0002 | OHR-LRW-0001 | POS      | P1           | 1,2        | <ol start="1"><li>Karyawan login ke sistem.</li><li>Memiliki sisa kuota Cuti Tahunan = 12 hari.</li><li>Navigasi ke Leave → Apply.</li></ol>                                                          | <ol start="1"><li>Pilih Leave Type = "Cuti Tahunan 2026".</li><li>Masukkan From Date &#x26; To Date (misal: durasi 2 hari kerja).</li><li>Isi Comments = "Acara Keluarga".</li><li>Klik Apply.</li></ol>                               | Pengajuan berhasil dikirim, muncul pesan sukses, dan status pengajuan di daftar My Leave menjadi Pending Approval.                       | As Expected | PASSED     |           |
| TP-OHR-0002 | OHR-LAM-0002 | OHR-LRW-0002 | POS      | P1           | 2,3        | <ol start="1"><li>Pengajuan cuti 2 hari dari TC-OHR-LEV-007 dalam status Pending Approval.</li><li>Login sebagai Supervisor dari karyawan tersebut.</li><li>Navigasi ke Leave → Leave List.</li></ol> | <ol start="1"><li>Cari nama karyawan uji pada daftar pengajuan.</li><li>Klik tombol Approve pada baris pengajuan cuti tersebut.</li><li>Login kembali sebagai Karyawan dan cek menu Leave → My Leave Details / Entitlements.</li></ol> | Status pengajuan berubah menjadi Approved / Scheduled, dan sisa kuota cuti karyawan terpotong otomatis secara akurat (12 - 2 = 10 hari). | As Expected | PASSED     |           |
| TP-OHR-0002 | OHR-LAM-0002 | OHR-LRW-0003 | POS      | P2           | 3          | <ol start="1"><li>Karyawan mengajukan cuti baru (durasi 1 hari, sisa kuota 10 hari).</li><li>Login sebagai Supervisor.</li><li>Navigasi ke Leave → Leave List.</li></ol>                              | <ol start="1"><li>Cari pengajuan cuti karyawan tersebut.</li><li>Klik tombol Reject.</li><li>Cek kembali saldo kuota cuti karyawan.</li></ol>                                                                                          | Status pengajuan berubah menjadi Rejected, dan sisa kuota cuti karyawan tidak berkurang (tetap 10 hari).                                 | As Expected | PASSED     |           |
| TP-OHR-0002 | OHR-LAM-0002 | OHR-LRW-0004 | NEG      | P1           | 4          | <ol start="1"><li>Karyawan login ke sistem.</li><li>Memiliki sisa kuota cuti = 2 hari.</li><li>Navigasi ke Leave → Apply.</li></ol>                                                                   | <ol start="1"><li>Pilih Leave Type = "Cuti Tahunan 2026".</li><li>Masukkan rentang tanggal dengan durasi = 5 hari kerja.</li><li>Klik Apply.</li></ol>                                                                                 | Sistem menolak pengajuan dan menampilkan pesan peringatan error (misal: "Balance Exceeded" / "Should be less than leave balance").       | As Expected | PASSED     |           |
| TP-OHR-0002 | OHR-LAM-0002 | OHR-LRW-0005 | POS      | P2           | 3          | <ol start="1"><li>Karyawan memiliki pengajuan cuti berstatus Pending Approval.</li><li>Berada di menu Leave → My Leave.</li></ol>                                                                     | <ol start="1"><li>Cari pengajuan yang masih Pending.</li><li>Klik tombol Cancel.</li></ol>                                                                                                                                             | Status pengajuan berubah menjadi Cancelled, dan kuota cuti tidak mengalami pemotongan.                                                   | As Expected | PASSED     |           |

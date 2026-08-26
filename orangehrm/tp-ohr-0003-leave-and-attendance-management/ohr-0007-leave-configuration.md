# OHR-0007 Leave Configuration

## User Story

***

Sebagai HR Admin, saya ingin mengonfigurasi tipe cuti, mengalokasikan kuota (entitlements), agar aturan hak cuti karyawan terkonfigurasi dan terdistribusi sesuai kebijakan perusahaan.

## Pre-condition

***

* Pengguna terautentikasi dengan hak akses **System Administrator / HR Admin**.
* Pengguna berada di modul **Leave** pada menu **Configure / Entitlements**.
* Master data karyawan sudah terdaftar di sistem.

## Acceptance Criteria

***

1. **Konfigurasi Tipe Cuti:** Sistem dapat membuat dan menyimpan jenis cuti baru (seperti Cuti Tahunan atau Sakit) dengan nama yang unik.
2. **Alokasi Kuota (Entitlements):** Sistem dapat mengalokasikan jumlah kuota cuti kepada karyawan secara individu maupun massal (_bulk allocation_) untuk periode cuti tertentu.
3. **Validasi Kuota Tidak Valid:** Sistem menolak penginputan kuota cuti bernilai negatif, nol, atau format non-numerik dengan menampilkan pesan kesalahan yang sesuai.
4. **Validasi Duplikasi Tipe Cuti:** Sistem menolak pembuatan tipe cuti baru jika menggunakan nama jenis cuti yang sudah terdaftar di database.

## Test Scenario

***

| **TP**      | **Scene ID** | **Test ID**  | **Type** | **Priority** | **AC Ref** | **Pre-condition**                                                                                                                  | **Step**                                                                                                                                                                                                                                                            | **Expected**                                                                                                                 | **Actual**  | **Status** | **Notes** |
| ----------- | ------------ | ------------ | -------- | ------------ | ---------- | ---------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ----------- | ---------- | --------- |
| TP-OHR-0003 | OHR-LAM-0001 | OHR-LCF-0001 | POS      | P1           | 1          | <ol start="1"><li>Login sebagai HR Admin.</li><li>Navigasi ke Leave → Configure → Leave Types</li></ol>                            | <ol start="1"><li>Klik Add.</li><li>Masukkan <em>Name</em></li><li>Klik Save.</li></ol>                                                                                                                                                                             | Tipe cuti baru berhasil dibuat, pesan sukses muncul, dan nama jenis cuti terdaftar pada tabel _Leave Types_.                 | As Expected | PASSED     |           |
| TP-OHR-0003 | OHR-LAM-0001 | OHR-LCF-0002 | NEG      | P2           | 1,4        | <ol start="1"><li>Tipe cuti "Cuti Tahunan 2026" sudah ada di database.</li><li>Berada di halaman Add Leave Type.</li></ol>         | <ol start="1"><li>Masukkan <em>Name</em> dengan nama yang persis sama.</li><li>Klik Save.</li></ol>                                                                                                                                                                 | Sistem menolak penyimpanan dan menampilkan pesan kesalahan "Already exists".                                                 | As Expected | PASSED     |           |
| TP-OHR-0003 | OHR-LAM-0001 | OHR-LCF-0003 | POS      | P1           | 2          | <ol start="1"><li>Tipe cuti "Cuti Tahunan 2026" sudah aktif.</li><li>Navigasi ke Leave → Entitlements → Add Entitlements</li></ol> | <ol start="1"><li>Pilih <em>Add To</em> = "Individual Employee".</li><li>Ketik dan pilih nama Karyawan Uji.</li><li>Pilih <em>Leave Type</em> = "Cuti Tahunan 2026".</li><li>Masukkan <em>Entitlement</em> = 12.</li><li>Klik Save dan konfirmasi dialog.</li></ol> | Kuota cuti sebesar 12 hari berhasil ditambahkan ke saldo profil karyawan tersebut secara akurat.                             | As Expected | PASSED     |           |
| TP-OHR-0003 | OHR-LAM-0001 | OHR-LCF-0004 | POS      | P2           | 2          | <ol start="1"><li>Tipe cuti "Cuti Tahunan 2026" sudah aktif.</li><li>Berada di halaman Add Entitlements</li></ol>                  | <ol start="1"><li>Pilih <em>Add To</em> = "Multiple Employees".</li><li>Pilih <em>Sub Unit</em></li><li>Pilih <em>Leave Type</em></li><li>Masukkan <em>Entitlement</em> = 12.</li><li>Klik Save dan konfirmasi dialog.</li></ol>                                    | Sistem mengalokasikan kuota 12 hari secara serentak ke seluruh karyawan yang terdaftar di Sub Unit "Quality Assurance".      | As Expected | PASSED     |           |
| TP-OHR-0003 | OHR-LAM-0001 | OHR-LCF-0005 | NEG      | P1           | 3          | <ol start="1"><li>Berada di halaman Add Entitlements</li></ol>                                                                     | <ol start="1"><li>Pilih <em>Individual Employee</em> dan <em>Leave Type</em> valid.</li><li>Masukkan nilai <em>Entitlement</em> = -5.</li><li>Klik Save.</li></ol>                                                                                                  | Sistem menolak proses alokasi dan menampilkan pesan validasi error (misal: "Should be a number with upto 2 decimal places"). | As Expected | PASSED     |           |
| TP-OHR-0003 | OHR-LAM-0001 | OHR-LCF-0006 | NEG      | P2           | 3          | <ol start="1"><li>Berada di halaman Add Entitlements</li></ol>                                                                     | <ol start="1"><li>Pilih <em>Individual Employee</em> dan <em>Leave Type</em> valid.</li><li>Masukkan nilai <em>Entitlement</em> = ABC atau karakter spesial.</li><li>Klik Save.</li></ol>                                                                           | Sistem menolak proses alokasi dan menampilkan pesan validasi error (misal: "Should be a number with upto 2 decimal places"). | As Expected | PASSED     |           |

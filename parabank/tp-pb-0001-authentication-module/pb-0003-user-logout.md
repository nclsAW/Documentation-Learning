# PB-0003 User Logout

## User Story

***

Sebagai nasabah yang sedang login, saya ingin keluar dari sistem agar keamanan sesi akun saya tetap terjaga.

## Pre-condition

***

Pengguna dalam status logged in dan berada di dalam dashboard.

## Acceptance Criteria

***

* Sesi pengguna dihentikan dengan aman dan otomatis diarahkan kembali ke halaman utama (Customer Login).
* Pengguna tidak bisa mengakses kembali halaman dashboard dengan menekan tombol Back pada browser setelah berhasil logout.

## Test Scenario

***

<table data-header-hidden><thead><tr><th width="128"></th><th>Text</th><th></th><th></th><th></th><th></th><th></th><th></th><th></th><th></th><th></th><th></th></tr></thead><tbody><tr><td><strong>TP ID</strong></td><td><strong>Scene ID</strong></td><td><strong>Test ID</strong></td><td><strong>Type</strong></td><td><strong>AC Ref</strong></td><td><strong>Pre-condition</strong></td><td><strong>Step</strong></td><td><strong>Priority</strong></td><td><strong>Expected</strong></td><td><strong>Actual</strong></td><td><strong>Status</strong></td><td><strong>Notes</strong></td></tr><tr><td>TP-PB-0001</td><td>PB-AUTH-0003</td><td>PB-LGO-0001</td><td>POS</td><td>1</td><td>Pengguna sedang dalam kondisi <em>login</em> dan berada di halaman <em>dashboard</em> (Accounts Overview).</td><td><ol start="1"><li>Temukan dan klik tautan/tombol "Log Out".</li></ol></td><td>P1</td><td>Sesi berakhir dan pengguna otomatis diarahkan kembali ke halaman login.</td><td>As Expected</td><td>PASSED</td><td> </td></tr><tr><td>TP-PB-0001</td><td>PB-AUTH-0003</td><td>PB-LGO-0002</td><td>NEG</td><td>2</td><td>Pengguna baru saja berhasil melakukan <em>logout</em> dan berada di halaman beranda.</td><td><ol start="1"><li>Klik tombol "Back" (Kembali) pada <em>browser</em>.</li></ol></td><td>P1</td><td>Akses ditolak, tombol <em>Back</em> pada <em>browser</em> tidak bisa mem-<em>bypass</em> otentikasi (wajib <em>login</em> ulang).</td><td>Sesi server mati dan akses tombol mati, namun browser cache tida dibersihkan sehingga halaman terakhir masih bisa diakses melalui tombol Back.</td><td>FAILED</td><td><a href="https://alldocs.atlassian.net/browse/KAN-20">KAN-20: PB-BUG-0001 [User Logout] Browser Cache [ParaBank]Bug Report</a></td></tr><tr><td>TP-PB-0001</td><td>PB-AUTH-0003</td><td>PB-LGO-0003</td><td>NEG</td><td>2</td><td>Pengguna sudah dalam kondisi <em>logout</em> / tidak memiliki sesi aktif.</td><td><ol start="1"><li>Salin dan <em>paste</em> URL halaman internal.</li><li>Tekan Enter.</li></ol></td><td>P2</td><td>Akses URL langsung ditolak; sistem memaksa pengguna kembali ke halaman <em>login</em>.</td><td>As Expected</td><td>PASSED</td><td> </td></tr></tbody></table>

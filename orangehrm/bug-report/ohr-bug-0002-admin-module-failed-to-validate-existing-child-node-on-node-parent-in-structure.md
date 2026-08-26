# OHR-BUG-0002 \[Admin Module] Failed to Validate Existing Child Node on Node Parent, in Structure

## Document Details

***

Priority: P1

Severity: S1

## Description

***

Saat menghapus sebuah _parent node_ yang masih memiliki _child node_, sistem memunculkan pesan peringatan/pencegahan bahwa _parent node_ tidak bisa dihapus sebelum _child node_ dipindahkan atau dihapus terlebih dahulu. Namun, sistem tidak menghentikan eksekusi tersebut dan tetap melanjutkan proses penghapusan _parent node_ beserta _child node_-nya secara tidak sengaja.

## Pre-condition

***

* User terautentikasi dan memiliki akses untuk mengelola _node_ / struktur hierarki.
* Terdapat setidaknya satu _parent node_ yang memiliki satu atau lebih _child node_ aktif di dalam sistem.

## Step to Reproduce

***

1. Navigasi ke halaman pengelolaan _node_ / struktur hierarki.
2. Pilih _parent node_ yang masih memiliki _child node_.
3. Klik tombol **Delete** (Hapus) pada _parent node_ tersebut.

## Expected vs Actual

***

#### **Expected Result**

Sistem menampilkan pesan peringatan/pencegahan dan secara tegas **menghentikan/membatalkan** proses penghapusan sampai _child node_ dipindahkan atau dihapus terlebih dahulu oleh user.

#### **Actual Result**

Sistem menampilkan pesan peringatan/pencegahan, namun proses penghapusan tidak dihentikan dan tetap dilanjutkan sehingga _parent node_ beserta _child node_-nya terhapus.

## Environment & Evidence

***

**Environment:** Production

**Evidence:**

* [https://drive.google.com/open?id=1kaQ02otnL5uGZfnQ5dnWNEcISGRUTc4K\&usp=drive\_fs](https://drive.google.com/open?id=1kaQ02otnL5uGZfnQ5dnWNEcISGRUTc4K\&usp=drive_fs)

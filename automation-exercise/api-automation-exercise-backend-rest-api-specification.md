# \[API] Automation Exercise Backend REST API Specification

## Document Control <a href="#document-control" id="document-control"></a>

***

<table data-header-hidden data-search="false"><thead><tr><th width="166"></th><th></th></tr></thead><tbody><tr><td><strong>Property</strong></td><td><strong>Value</strong></td></tr><tr><td>Document Version</td><td>1.0.0</td></tr><tr><td>Environment</td><td>Production</td></tr><tr><td>URL</td><td><a href="https://automationexercise.com/">Automation Exercise</a></td></tr><tr><td>Author</td><td>@Nicolas Anelka</td></tr><tr><td>Date</td><td>Aug 14, 2026</td></tr><tr><td>Related TP</td><td><p><a href="https://alldocs.atlassian.net/browse/KAN-64">KAN-64: TP-AEX-0001 Authentication &#x26; Account Management [Automation Exercise]To Do</a></p><p><a href="https://alldocs.atlassian.net/browse/KAN-65">KAN-65: TP-AEX-0002 Product Catalog, Search &#x26; Review [Automation Exercise]To Do</a></p><p><a href="https://alldocs.atlassian.net/browse/KAN-66">KAN-66: TP-AEX-0003 Cart Management &#x26; Recommended Items [Automation Exercise]To Do</a></p><p><a href="https://alldocs.atlassian.net/browse/KAN-67">KAN-67: TP-AEX-0004 Checkout, Payment &#x26; Order Processing [Automation Exercise]To Do</a></p><p><a href="https://alldocs.atlassian.net/browse/KAN-68">KAN-68: TP-AEX-0005 Customer Support &#x26; Contact Us [Automation Exercise]To Do</a></p><p><a href="https://alldocs.atlassian.net/browse/KAN-69">KAN-69: TP-AEX-0006 UI, Navigation &#x26; Footer Subscription [Automation Exercise]To Do</a></p><p><a href="https://alldocs.atlassian.net/browse/KAN-70">KAN-70: TP-AEX-0007 Backend API Testing Validation [Automation Exercise]To Do</a></p></td></tr></tbody></table>

## Overview <a href="#overview" id="overview"></a>

***

Layanan antarmuka pemrograman backend (Automation Exercise REST API) menyediakan akses langsung ke data inti sistem e-commerce tanpa melalui antarmuka web. Layanan ini mencakup operasi pembacaan data publik (katalog produk dan brand), fungsi pencarian barang, otentikasi akun, hingga operasi _Create, Read, Update, Delete (CRUD)_ terhadap entitas akun pengguna.

#### Karakteristik & Protokol API: <a href="#karakteristik-and-protokol-api" id="karakteristik-and-protokol-api"></a>

* **Format Transfer Data:** Seluruh respons data dikirimkan dalam format standard JSON (JavaScript Object Notation).
* **Payload Encoding:** Endpoint yang menerima masukan (POST/PUT/DELETE) memproses body data menggunakan format application/x-www-form-urlencoded atau multipart/form-data (bukan raw JSON body).
* **State Behavior:** Setiap request bersifat _stateless_, di mana identitas atau parameter verifikasi dikirimkan langsung pada setiap pemanggilan endpoint.

## Base URL & Environment <a href="#base-url-and-environment" id="base-url-and-environment"></a>

***

| **Environment** | **URL**                                                | **Status** | **Access Scope** |
| --------------- | ------------------------------------------------------ | ---------- | ---------------- |
| Production      | [Automation Exercise](https://automationexercise.com/) | Active     | Public           |

## Authenticaation & Authorization Information <a href="#authenticaation-and-authorization-information" id="authenticaation-and-authorization-information"></a>

***

API backend pada platform Automation Exercise menggunakan pendekatan Parameter-Based Authentication / Credential In-Payload:

* **Mekanisme Otentikasi:** API tidak menggunakan Header Authorization berbasis Bearer Token, API Key, atau OAuth 2.0.
* **Otentikasi Operasi Terproteksi:** Validasi hak akses pada operasi akun (misal: verifikasi login, update profil, hapus akun, dan ambil detail profil) dilakukan secara langsung dengan menyertakan parameter email dan password di dalam Request Body atau Query Parameter.
* **Public Endpoints:** Endpoint katalog produk (/api/productsList) dan daftar brand (/api/brandsList) bersifat open access dan dapat diakses tanpa autentikasi apa pun.

## Global Requests Headers <a href="#global-requests-headers" id="global-requests-headers"></a>

***

| **Header Name** | **Recommended Value**                                      | **Usage Context**                                  |
| --------------- | ---------------------------------------------------------- | -------------------------------------------------- |
| Content-Type    | application/x-www-form-urlencoded atau multipart/form-data | untuk request POST, PUT, DELETE                    |
| Accept          | application/json                                           | Disarankan untuk memastikan respons berformat JSON |

## Global Response & Status Code Matrix <a href="#global-response-and-status-code-matrix" id="global-response-and-status-code-matrix"></a>

***

| **HTTP Status**        | **responseCode** | **Classification** | **Definisi & Kondisi**                                                 |
| ---------------------- | ---------------- | ------------------ | ---------------------------------------------------------------------- |
| 200 OK                 | 200              | Success            | Permintaan berhasil diproses dan data/pesan konfirmasi dikembalikan.   |
| 201 Created            | 201              | Success (Created)  | Akun pengguna baru berhasil dibuat pada endpoint pendaftaran.          |
| 400 Bad Request        | 400              | Client Error       | Parameter wajib (_mandatory parameters_) hilang atau tidak dikirimkan. |
| 404 Not Found          | 404              | Client Error       | Akun/entitas tidak ditemukan atau kredensial yang dikirimkan salah.    |
| 405 Method Not Allowed | 405              | Client Error       | HTTP Method yang digunakan tidak didukung oleh endpoint target.        |

## Module Classification <a href="#module-classification" id="module-classification"></a>

***

#### **Module 1: Products Catalog API** <a href="#module-1-products-catalog-api" id="module-1-products-catalog-api"></a>

Berfokus pada entitas produk dan pencarian katalog barang:

* `GET /api/productsList` -> Mengambil seluruh daftar katalog produk.
* `POST /api/productsList` -> Validasi penolakan method tidak didukung (HTTP 405).
* `POST /api/searchProduct` -> Melakukan pencarian produk dengan kata kunci.
* `POST /api/searchProduct` _(tanpa parameter)_ -> Validasi error parameter hilang (HTTP 400).

#### **Module 2: Brands API** <a href="#module-2-brands-api" id="module-2-brands-api"></a>

Berfokus pada entitas data brand/merk produk:

* `GET /api/brandsList` -> Mengambil seluruh daftar merk/brand aktif.
* `PUT /api/brandsList` -> Validasi penolakan method tidak didukung (HTTP 405).

#### **Module 3: User Authentication & Account Management API** <a href="#module-3-user-authentication-and-account-management-api" id="module-3-user-authentication-and-account-management-api"></a>

Berfokus pada otentikasi login dan operasi siklus hidup akun pengguna (CRUD):

* `POST /api/verifyLogin` -> Verifikasi kredensial login pengguna.
* `POST /api/verifyLogin` _(tanpa parameter / data salah)_ -> Validasi missing parameter (400) / user not found (404).
* `DELETE /api/verifyLogin` -> Validasi penolakan method tidak didukung (HTTP 405).
* `POST /api/createAccount` -> Mendaftarkan akun pengguna baru dengan payload lengkap.
* `PUT /api/updateAccount` -> Memperbarui data detail akun pengguna.
* `GET /api/getUserDetailByEmail` -> Mengambil rincian profil akun berdasarkan email terdaftar.
* `DELETE /api/deleteAccount` -> Menghapus akun pengguna secara permanen dari basis data.

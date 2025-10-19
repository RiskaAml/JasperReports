# 📄 Praktikum PBO: Implementasi Cetak Laporan dengan JasperReports

Proyek ini adalah bagian dari Laporan Praktikum Pemrograman Berorientasi Objek (PBO) yang mendemonstrasikan integrasi *library* **JasperReports** untuk fungsionalitas pencetakan laporan dinamis dari data *database*.

## 🎯 Tujuan Praktikum

1.  Mempelajari konsep dasar dan arsitektur **JasperReports**.
2.  Mampu mengintegrasikan *library* pendukung laporan ke dalam proyek NetBeans.
3.  Berhasil mendesain laporan (`.jrxml`) menggunakan **Jaspersoft Studio**.
4.  Mengimplementasikan *method* Java untuk mengambil data dari **PostgreSQL** dan menampilkannya sebagai laporan cetak.

---

## 🛠️ Stack Teknologi

| Kategori | Alat/Teknologi | Versi Digunakan | Peran |
| :--- | :--- | :--- | :--- |
| **Bahasa & Lingkungan** | Java Development Kit (JDK) | **24** | Lingkungan Kompilasi & Eksekusi. |
| **IDE** | Apache NetBeans | 27 | Lingkungan Pengembangan. |
| **Database** | PostgreSQL |  | Sumber data untuk laporan. |
| **Desain Laporan** | Jaspersoft Studio |  | Alat desain *standalone* untuk `.jrxml`. |

## 📦 Daftar Libraries (`.jar`)

Semua *file* `.jar` berikut **wajib** ditambahkan ke bagian **Libraries** pada proyek NetBeans.

| Nama File (.jar) | Fungsi Utama | Keterangan |
| :--- | :--- | :--- |
| `postgresql-42.6.0.jar` | Koneksi Database | **PostgreSQL JDBC Driver.** |
| `jasperreports-6.21.5.jar` | Mesin Pelaporan Inti | *Core engine* untuk memproses dan mencetak laporan. |
| `itext-2.1.7.jar` | Manipulasi PDF | Digunakan untuk menghasilkan/mengekspor laporan ke format PDF. |
| `groovy-all-2.4.21.jar` | Dukungan Groovy | Digunakan untuk ekspresi dan skrip kompleks dalam laporan. |
| `commons-logging-1.2.jar` | Abstraksi Logging | Layer standar untuk pencatatan aktivitas aplikasi. |
| *Library Common Lainnya* | *[commons-beanutils, collections, digester]* | Utilitas pendukung untuk memanipulasi objek Java dan XML. |

## ⚙️ Langkah Kerja (Integrasi)

Langkah-langkah utama dalam proses pencetakan laporan ini:

### 1. Desain Laporan

Karena **iReport Designer sudah tidak didukung**, desain dilakukan menggunakan **Jaspersoft Studio** (aplikasi mandiri).

-   Buat desain laporan visual (tabel, *header*, *footer*) dan tentukan kueri SQL untuk pengambilan data (misalnya: `SELECT * FROM transaksi`).
-   *File* hasil desain berekstensi **`.jrxml`**. Salin file ini ke *package* proyek NetBeans (misalnya di folder `/src/report`).

### 2. Implementasi Java

Aksi pencetakan diletakkan pada *class* khusus, misalnya `CetakLaporan.java`, yang dipanggil dari `TransaksiForm.java`.

1.  **Mendapatkan Koneksi:** Buat koneksi standar ke PostgreSQL.
2.  **Kompilasi dan Pengisian:**
    -   Kode memuat file **`.jrxml`** (desain).
    -   File tersebut **dikompilasi** (menjadi **`.jasper`**).
    -   **`JasperFillManager.fillReport()`** mengisi template laporan dengan data dari koneksi *database*.
3.  **Menampilkan Laporan:**
    -   Laporan yang sudah terisi data ditampilkan ke pengguna melalui **`JasperViewer`**.
    -   Kode ini dihubungkan ke *event* klik pada **Tombol "Cetak"** di *form* utama.

### 💡 Catatan Penting

> Penggunaan *library* pendukung (*.jar*) **mutlak diperlukan**, bahkan jika desain dilakukan di dalam NetBeans (dulu menggunakan *plugin* iReport). *Plugin* hanya alat desain, sementara *library* adalah mesin yang menjalankan fungsi cetak.


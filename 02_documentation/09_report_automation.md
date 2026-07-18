# Sales Performance Report — Step 9: Report Automation & Dashboard Refresh
**Proyek:** Sales Performance Report (Dealer Motor)
**Periode Data:** 13 – 19 Juli 2026 (Minggu ke-29)
**Tool:** Power Query (Excel)
**File Output:** Sales_Report_PowerQuery_Automated.xlsx

---

## Tujuan
Membuat proses pelaporan penjualan menjadi lebih efisien dengan mengurangi pekerjaan manual, mempercepat pembaruan laporan, serta memastikan proses Data Cleaning dapat dijalankan ulang secara konsisten dan akurat setiap ada data baru (mingguan) tanpa perlu mengulang seluruh proses manual dari awal.

## Input
- File raw data (`sales_july_week3_2026_RAW.xlsx`, sheet Sales Transaction)
- Seluruh langkah Data Cleaning yang sebelumnya dikerjakan secara manual di Step 4 (formula `TRIM`, `PROPER`, `SUBSTITUTE`, `IF`, `COUNTIF`, dll)

## Proses

### 1. Import Data ke Power Query
`Data → Get Data → From File → From Workbook` → pilih file sumber → pilih sheet **Sales Transaction** → klik **Transform Data** (membuka Power Query Editor).

### 2. Standarisasi Kolom Branch
| Aksi | Tools Power Query | Setara dengan Formula Excel Manual |
|---|---|---|
| Hapus spasi berlebih | Klik kanan kolom → **Transform → Trim** | `TRIM()` |
| Standarisasi kapitalisasi | Klik kanan kolom → **Transform → Capitalize Each Word** | `PROPER()` |
| Ganti singkatan/variasi penulisan | Klik kanan kolom → **Replace Values** (contoh: `Jaksel` → `Jakarta Selatan`, `Tangerang Kota` → `Tangerang`, `BEKASI` → `Bekasi`) | `SUBSTITUTE()` |

### 3. Standarisasi Kolom Date
| Aksi | Tools Power Query | Catatan |
|---|---|---|
| Translate nama bulan Indonesia | **Replace Values**: ` Juli ` → `/07/` | Diperlukan karena Power Query tidak mengenali nama bulan berbahasa Indonesia secara default |
| Konversi ke tipe Date | Klik kanan kolom → **Change Type → Date** | Baris yang formatnya belum diterjemahkan akan tampil sebagai "Error" — indikator visual langsung tanpa perlu formula `ISNUMBER` terpisah |

### 4. Penanganan Missing Values
| Kolom | Aksi |
|---|---|
| Sales Rep | **Replace Values**: `null` → `Unknown` |
| Customer Name | **Replace Values**: `null` → `Unknown` |

### 5. Penghapusan Duplicate Records
Klik kanan kolom **Transaction ID** → **Remove Duplicates**
Hasil: baris berkurang dari **348 → 341** (7 baris duplikat terhapus otomatis dalam satu langkah, tanpa filter-sort-hapus manual).

### 6. Flagging Transaksi Bernilai Nol
`Add Column → Custom Column`, dengan formula bahasa **M**:
```m
if [Total Sales] = 0 then "Batal/Refund" else "Normal"
```
Kolom baru **Status Transaksi** otomatis terbentuk.

### 7. Close & Load
`Home → Close & Load To... → Table → New Worksheet`
Hasil query dimuat sebagai tabel Excel biasa di sheet baru (di-rename menjadi **"Clean Data (Power Query)"**).

### 8. Simulasi Refresh
`Data → Refresh All` dijalankan untuk memverifikasi bahwa seluruh rangkaian langkah (Applied Steps) dapat dieksekusi ulang tanpa error.

## Perbandingan: Manual (Step 4) vs Power Query (Step 9)

| Aspek | Data Cleaning Manual (Excel Formula) | Report Automation (Power Query) |
|---|---|---|
| Waktu pengerjaan | ±1–2 jam (banyak kolom bantu, banyak formula) | ±15 menit |
| Update data periode baru | Ulang seluruh proses dari awal | Klik **Refresh All**, selesai dalam hitungan detik |
| Risiko human error | Tinggi (circular reference, salah referensi kolom akibat pergeseran posisi kolom) | Rendah — setiap langkah tersimpan sebagai "Applied Steps" yang terurut dan dapat diaudit |
| Jejak proses (audit trail) | Dicatat manual secara terpisah | Otomatis tercatat di panel **Applied Steps** pada query |
| Kebutuhan kolom bantu | Ya, banyak (Branch Clean, Date Clean, dll) | Tidak — transformasi terjadi langsung pada query, tidak menyisakan kolom bantu di data akhir |

## Temuan
- Seluruh proses cleaning yang sebelumnya memerlukan banyak kolom bantu dan berulang kali salah referensi (Step 4) berhasil direplikasi dalam satu alur kerja Power Query yang jauh lebih ringkas.
- Proses **Remove Duplicates** di Power Query menggantikan kebutuhan filter-sort-hapus manual, dan hasilnya (341 baris) konsisten dengan hasil manual sebelumnya.
- Uji simulasi **Refresh All** berhasil dijalankan tanpa error, membuktikan query siap digunakan ulang untuk periode data berikutnya.

## Output
**Semi-Automated Reporting Workflow**, terdiri dari:
- Query **"Raw Sales Transaction"** tersimpan di dalam file Excel (dapat dibuka kembali melalui `Data → Queries & Connections`)
- Sheet **"Clean Data (Power Query)"** — hasil akhir data bersih (341 baris), otomatis ter-update setiap kali di-refresh
- Prosedur refresh mingguan yang terdokumentasi (lihat bagian *Cara Refresh untuk Data Periode Berikutnya*)

## Kesimpulan
Proses Report Automation menggunakan Power Query berhasil meningkatkan efisiensi Data Cleaning secara signifikan — dari proses manual yang memakan waktu lama dan rawan kesalahan referensi kolom, menjadi satu alur kerja tersimpan (query) yang dapat dijalankan ulang hanya dengan satu klik. Workflow ini siap digunakan sebagai fondasi pelaporan mingguan yang konsisten dan mendukung kebutuhan Executive Reporting pada tahap berikutnya.

---

## Cara Refresh untuk Data Periode Berikutnya

### Konsep Dasar: Bagaimana Power Query Terhubung ke Sumber Data

Power Query **tidak** otomatis membaca file baru hanya karena nama filenya sama dan dibuka di komputer yang sama. Query yang dibuat di dalam `Sales_Report_PowerQuery_Automated.xlsx` **mengingat lokasi/path spesifik** dari file sumber yang dipilih saat setup awal (`Data → Get Data → From File → From Workbook`).

Analogi: Power Query seperti **selang air** yang tersambung ke satu keran tertentu (lokasi file sumber). Jika isi ember di keran yang sama diganti, air baru otomatis mengalir saat keran dibuka (Refresh). Namun jika embernya dipindah ke lokasi/nama file lain, selang tidak otomatis ikut tersambung — perlu disambungkan ulang secara manual.

**Konsekuensi praktis:** agar proses refresh berjalan mulus setiap minggu, file sumber baru dari ERP harus **menimpa (replace)** file lama pada **lokasi folder dan nama file yang persis sama** — bukan sekadar dibuka bersamaan di Excel.

### Langkah-Langkah Refresh Data Periode Baru

**1. Terima file baru dari ERP/Sales System**
Pastikan struktur kolom (nama sheet, nama kolom, urutan kolom) identik dengan file sebelumnya, karena setiap langkah Power Query mengacu pada nama kolom yang spesifik.

**2. Cari lokasi file sumber lama di komputer**
Buka File Explorer, temukan folder tempat file `sales_july_week3_2026_RAW.xlsx` versi lama tersimpan, dan catat lokasinya.

**3. Pastikan file lama dalam keadaan tertutup**
File sumber lama tidak boleh sedang terbuka di Excel — jika masih terbuka, proses replace/timpa file akan gagal (muncul pesan "file is open in another program").

**4. Timpa (replace) file lama dengan file baru**
- Jika file baru dari ERP sudah bernama persis sama (`sales_july_week3_2026_RAW.xlsx`): pindahkan (cut-paste) file baru ke folder file lama berada, lalu pilih **Replace/Yes** saat Windows menanyakan konfirmasi penimpaan file.
- Jika nama file baru berbeda (misal `export_20260720.xlsx`): rename terlebih dahulu menjadi nama yang persis sama seperti file lama, baru pindahkan ke folder yang sama untuk menimpa file lama.

**5. Buka file `Sales_Report_PowerQuery_Automated.xlsx`**

**6. Klik `Data → Refresh All`**
Seluruh langkah cleaning (Trim, Capitalize, Replace, Remove Duplicates, Custom Column Status Transaksi) berjalan otomatis dalam hitungan detik.

**7. Verifikasi hasil**
Sheet **"Clean Data (Power Query)"** ter-update dengan data terbaru, siap digunakan untuk Pivot Table dan Dashboard pada tahap selanjutnya.

### Jika Nama File atau Lokasi Sumber Berubah

Apabila file dari ERP tidak memungkinkan untuk selalu bernama/berlokasi sama, path sumber query dapat diperbarui manual melalui:
1. `Data → Queries & Connections`
2. Klik kanan query **"Raw Sales Transaction"** → **Data Source Settings** (atau **Edit Permissions**)
3. Arahkan ke lokasi/nama file yang baru
4. Klik `Refresh All`

**Rekomendasi operasional:** untuk meminimalkan langkah manual setiap minggu, disarankan agar sumber data dari ERP selalu diekspor dengan **nama file dan lokasi folder yang konsisten** (menimpa file periode sebelumnya), sehingga proses mingguan cukup dilakukan melalui satu langkah: **Refresh All**.

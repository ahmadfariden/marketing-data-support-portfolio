# Sales Performance Report — Step 4: Data Cleaning
**Proyek:** Sales Performance Report (Dealer Motor)
**Periode Data:** 13 – 19 Juli 2026 (Minggu ke-29)

---

## Tujuan
Memperbaiki seluruh permasalahan kualitas data yang ditemukan pada tahap Data Profiling (Step 3) agar dataset menjadi akurat, konsisten, dan siap digunakan untuk pembuatan Pivot Table dan Dashboard Sales Performance.

## Input
- Sales Transaction Data (raw)
- Data Quality Findings (hasil Data Profiling — Step 3)

## Proses & Formula yang Digunakan

Proses cleaning dikerjakan di sheet kerja terpisah (**Cleaning Sales Transaction**), dengan sheet **Raw Sales Transaction** tetap disimpan utuh sebagai arsip data mentah (bukti "sebelum").

### a. Standarisasi Nama Cabang
Menggabungkan perbaikan kapitalisasi (huruf besar/kecil), spasi berlebih, dan penyeragaman singkatan dalam satu formula:
```excel
=PROPER(TRIM(SUBSTITUTE(SUBSTITUTE(D2;"Jaksel";"Jakarta Selatan");"Tangerang Kota";"Tangerang")))
```
- `SUBSTITUTE` — mengganti singkatan/variasi penulisan menjadi nama baku
- `TRIM` — membuang spasi berlebih di awal/akhir/tengah teks
- `PROPER` — menyeragamkan kapitalisasi (huruf besar di awal kata)

**Hasil:** dari 17 nilai unik menjadi 12 nilai unik (sesuai jumlah cabang asli).

### b. Standarisasi Format Tanggal
Karena tanggal tercampur dalam 3 format (termasuk teks berbahasa Indonesia), dilakukan dalam 2 tahap:

**Tahap 1 — Normalisasi nama bulan Indonesia menjadi angka:**
```excel
=SUBSTITUTE(SUBSTITUTE(SUBSTITUTE(SUBSTITUTE(SUBSTITUTE(SUBSTITUTE(SUBSTITUTE(SUBSTITUTE(SUBSTITUTE(SUBSTITUTE(SUBSTITUTE(SUBSTITUTE(C2;" Januari ";"/01/");" Februari ";"/02/");" Maret ";"/03/");" April ";"/04/");" Mei ";"/05/");" Juni ";"/06/");" Juli ";"/07/");" Agustus ";"/08/");" September ";"/09/");" Oktober ";"/10/");" November ";"/11/");" Desember ";"/12/")
```

**Tahap 2 — Konversi ke format Date asli** (mencoba format ISO dahulu, lalu format slash):
```excel
=IFERROR(
   DATE(VALUE(LEFT(B2;4));VALUE(MID(B2;6;2));VALUE(RIGHT(B2;2)));
   DATE(VALUE(RIGHT(B2;4));VALUE(MID(B2;4;2));VALUE(LEFT(B2;2)))
)
```
Kolom hasil diformat sebagai **Date (DD/MM/YYYY)** melalui Format Cells.

**Hasil:** seluruh 348 baris berhasil dikonversi menjadi format Date asli yang konsisten dan dapat diurutkan/difilter oleh Excel.

### c. Penanganan Missing Values
```excel
=IF(E2="";"Unknown";E2)     ' Sales Rep
=IF(F2="";"Unknown";F2)     ' Customer Name
```
Baris dengan Sales Rep atau Customer Name kosong diisi label **"Unknown"**, sehingga data tetap lengkap namun sumbernya tetap dapat ditelusuri terpisah saat analisis.

### d. Penghapusan Duplicate Records
Menggunakan kolom bantu **Duplicate Check** (`=COUNTIF($A$2:$A$349;A2)`), data difilter untuk menampilkan hanya baris dengan nilai ≥2, kemudian diurutkan (Sort A–Z berdasarkan Transaction ID) agar setiap pasangan duplikat berdampingan. Dari setiap pasangan, satu baris dihapus secara manual.

**Hasil:** 7 baris duplikat dihapus → total baris berkurang dari 348 menjadi **341 baris** (dikonfirmasi dengan `=COUNTIF($A$2:$A$341;">1")` = 0).

### e. Flagging Transaksi Bernilai Nol
Alih-alih menghapus (yang berisiko menghilangkan jejak audit), transaksi dengan Total Sales = 0 diberi label status:
```excel
=IF(P2=0;"Batal/Refund";"Normal")
```
**Hasil (validasi):** `=COUNTIF(Q2:Q342;"Batal/Refund")` = **5**, sesuai temuan awal di Data Profiling.

## Temuan
- Nama cabang berhasil distandarisasi dari 17 menjadi 12 nilai unik
- Seluruh format tanggal berhasil dikonversi menjadi Date asli yang konsisten
- Missing values pada Sales Rep (12 baris) dan Customer Name (2 baris) berhasil ditangani dengan label "Unknown"
- 7 baris duplikat berhasil dihapus (348 → 341 baris)
- 5 transaksi bernilai nol berhasil diberi flag "Batal/Refund" tanpa menghapus data

## Output
**Clean Sales Data** — disimpan di sheet **Clean Sales Transaction**, terdiri dari kolom final:

| Kolom | Sumber |
|---|---|
| Transaction ID | Data asli |
| Date | Date Clean (hasil konversi) |
| Branch | Branch Clean (hasil standarisasi) |
| Sales Rep | Sales Rep Clean |
| Customer Name | Customer Name Clean |
| Product Code, Product Name, Qty, Unit Price, Discount, Total Sales | Data asli (tidak bermasalah) |
| Payment Method, Payment Status, Channel | Data asli (tidak bermasalah) |
| Status Transaksi | Normal / Batal-Refund |

## Kesimpulan
Seluruh permasalahan kualitas data yang ditemukan pada tahap Data Profiling — missing values, duplikasi, inkonsistensi format tanggal, dan inkonsistensi penulisan nama cabang — telah berhasil diperbaiki menggunakan kombinasi fungsi `TRIM`, `PROPER`, `SUBSTITUTE`, `IF`, `IFERROR`, `DATE`, dan `COUNTIF`. Dataset final (**Clean Sales Data**, 341 baris) kini akurat, konsisten, dan siap masuk ke tahap Data Validation (Step 5).

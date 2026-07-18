# Sales Performance Report — Step 5: Data Validation
**Proyek:** Sales Performance Report (Dealer Motor)
**Periode Data:** 13 – 19 Juli 2026 (Minggu ke-29)

---

## Tujuan
Memastikan dataset yang telah melalui proses Data Cleaning (Step 4) sudah akurat, lengkap, konsisten, dan sesuai dengan kebutuhan bisnis sebelum digunakan untuk analisis penjualan, pembuatan dashboard, serta laporan manajemen.

## Input
- Clean Sales Data (341 baris, sheet **Clean Sales Transaction**)
- Branch Master Data
- Product Master Data
- Target Sales Data
- Data Cleaning Report (Step 4)

## Proses & Validasi yang Dilakukan

### a. Verifikasi Ulang Missing Values
```excel
=COUNTBLANK('Clean Sales Transaction'!D:D)   ' Sales Rep
=COUNTBLANK('Clean Sales Transaction'!E:E)   ' Customer Name
```
**Hasil:** 0 sel kosong pada kedua kolom — seluruh baris yang sebelumnya kosong telah terisi label "Unknown" pada Step 4.

### b. Verifikasi Ulang Duplicate Records
```excel
=COUNTIF('Clean Sales Transaction'!A:A;">1")
```
Dicek menggunakan pendekatan yang sama seperti Step 3, namun pada sheet Clean.
**Hasil:** 0 — tidak ditemukan lagi Transaction ID yang muncul lebih dari satu kali.

### c. Verifikasi Konsistensi Format Data
- Kolom **Date**: dicek dengan `=ISNUMBER(...)` pada seluruh baris → seluruhnya TRUE (format Date asli, bukan lagi teks).
- Kolom **Branch**: dicek ulang menggunakan Pivot Table (Branch di Rows) → tepat **12 nilai unik**, sesuai jumlah cabang pada Branch Master.

### d. Validasi Hubungan Antar Dataset (Referential Integrity)
- Setiap **Product Code** pada Clean Sales Data dicocokkan terhadap **Product Master** menggunakan `VLOOKUP`/`XLOOKUP` untuk memastikan tidak ada kode produk yang tidak terdaftar.
- Setiap **Branch** pada Clean Sales Data dicocokkan terhadap **Branch Master** dengan cara yang sama.
**Hasil:** seluruh Product Code dan Branch pada Clean Sales Data memiliki padanan yang valid di data master — tidak ditemukan kode/nama yang "yatim" (orphan record).

### e. Perbandingan Total Transaksi dan Revenue dengan Data Sumber
| Metrik | Raw Data (348 baris) | Clean Data (341 baris) | Selisih |
|---|---|---|---|
| Jumlah Baris | 348 | 341 | -7 (baris duplikat yang dihapus) |
| Total Sales (Rupiah) | Rp 9.582.991.000 | Rp 9.433.489.000 | -Rp 149.502.000 (nilai dari 7 baris duplikat yang dihapus) |

Selisih total revenue **sepenuhnya dapat dijelaskan** oleh penghapusan 7 baris duplikat pada Step 4 — tidak ada data yang hilang secara tidak wajar.

### f. Pengecekan Periode Data
Seluruh 341 baris dicek menggunakan `MIN()` dan `MAX()` pada kolom Date:
```excel
=MIN('Clean Sales Transaction'!B:B)
=MAX('Clean Sales Transaction'!B:B)
```
**Hasil:** rentang tanggal 13/07/2026 – 19/07/2026, sesuai dengan periode laporan yang dituju (Minggu ke-29).

## Temuan
- Dataset sudah tidak memiliki duplicate records (terverifikasi ulang, hasil 0)
- Format tanggal dan penulisan nama cabang sudah konsisten (12 nilai unik, seluruh kolom Date bertipe Date asli)
- Seluruh transaksi memiliki referensi Branch dan Product Code yang valid terhadap data master (tidak ada orphan record)
- Total revenue Clean Data (Rp 9.433.489.000) selisihnya terhadap Raw Data sepenuhnya dapat dijelaskan oleh penghapusan duplikat
- Periode data sesuai kebutuhan laporan (13–19 Juli 2026)

## Output
**Validated Dataset:**
- Validated Sales Data (341 baris, lulus seluruh pengecekan di atas)
- Validated Branch Master Data
- Validated Product Master Data
- Validated Target Sales Data

Dokumen pendukung:
- Data Validation Report (dokumen ini)
- Data Quality Checklist:

| Checklist Item | Status |
|---|---|
| Tidak ada missing values | ✅ |
| Tidak ada duplicate records | ✅ |
| Format tanggal konsisten (Date asli) | ✅ |
| Format nama cabang konsisten (12 nilai unik) | ✅ |
| Seluruh Product Code valid terhadap Product Master | ✅ |
| Seluruh Branch valid terhadap Branch Master | ✅ |
| Total revenue terjelaskan dibanding raw data | ✅ |
| Periode data sesuai kebutuhan laporan | ✅ |

## Kesimpulan
Proses Data Validation memastikan bahwa dataset hasil cleaning telah memiliki kualitas data yang baik, akurat, dan lulus seluruh pengecekan konsistensi maupun integritas referensial. Dataset ini siap digunakan untuk tahap Data Reconciliation (Step 6) sebelum masuk ke proses analisis Pivot Table dan Dashboard Excel.

# Sales Performance Report — Step 6: Data Reconciliation
**Proyek:** Sales Performance Report (Dealer Motor)
**Periode Data:** 13 – 19 Juli 2026 (Minggu ke-29)

---

## Tujuan
Memastikan data yang telah melalui proses Data Validation (Step 5) memiliki kesesuaian dengan data sumber utama perusahaan (ERP/Sales System), sehingga angka yang digunakan dalam laporan manajemen akurat dan dapat dipercaya.

## Input
- Validated Sales Data (341 baris — Step 5)
- Raw Sales Transaction / ERP Sales Report (348 baris — Step 1)
- Target Sales Report

## Proses Rekonsiliasi

### a. Perbandingan Jumlah Transaksi
| Sumber | Jumlah Baris |
|---|---|
| Raw Data (ERP Export) | 348 |
| Validated Data (setelah cleaning) | 341 |
| Selisih | -7 |

Selisih 7 baris **sepenuhnya berasal dari penghapusan duplicate records** pada Step 4 (7 pasang transaksi kembar, 1 baris tiap pasang dihapus) — bukan kehilangan data transaksi asli.

### b. Perbandingan Total Revenue
```excel
=SUM('Raw Sales Transaction'!K:K)        ' Total Sales raw, termasuk duplikat
=SUM('Clean Sales Transaction'!K:K)      ' Total Sales clean, setelah dedup
```
| Sumber | Total Sales |
|---|---|
| Raw Data (termasuk 7 baris duplikat) | Rp 9.582.991.000 |
| Validated Data (setelah dedup) | Rp 9.433.489.000 |
| Selisih | Rp 149.502.000 |

Selisih Rp 149.502.000 **identik** dengan total nilai 7 baris duplikat yang dihapus pada Step 4 — mengonfirmasi tidak ada transaksi asli yang hilang secara tidak wajar selama proses cleaning.

### c. Perbandingan Jumlah Unit Terjual
```excel
=SUM('Raw Sales Transaction'!H:H)
=SUM('Clean Sales Transaction'!H:H)
```
| Sumber | Total Unit |
|---|---|
| Raw Data | 357 unit |
| Validated Data | 352 unit |
| Selisih | -5 unit |

Selisih 5 unit berasal dari kombinasi baris duplikat yang dihapus. Catatan: baik data raw maupun validated masih mencakup 5 transaksi berstatus "Batal/Refund" (Total Sales = 0) — transaksi ini **tidak dihapus**, hanya diberi flag, sehingga tetap tercatat dalam rekonsiliasi jumlah unit maupun baris, namun tidak berkontribusi pada nilai revenue (Rp 0).

### d. Perbandingan Performa Antar Cabang
Nilai **Target Revenue** per cabang pada sheet Target Sales dicocokkan silang dengan hasil `SUMIFS` pada Validated Data menggunakan pencocokan nama cabang (bukan posisi baris), untuk memastikan tidak ada kesalahan pemetaan:
```excel
=SUMIFS('Clean Sales Transaction'!K:K;'Clean Sales Transaction'!C:C;"Bekasi")
```
**Hasil:** seluruh 12 cabang menunjukkan kecocokan sempurna antara hasil SUMIFS berbasis nama cabang dan angka pada Pivot Table Branch Performance — tidak ditemukan cabang dengan nilai yang tidak konsisten.

### e. Investigasi Ketidaksesuaian
Tidak ditemukan ketidaksesuaian yang tidak dapat dijelaskan selama proses rekonsiliasi. Satu-satunya sumber selisih (baris, revenue, unit) adalah penghapusan duplicate records yang telah terdokumentasi pada Step 4, dan seluruh selisih tersebut telah diverifikasi bersesuaian secara matematis.

## Temuan
- Total transaksi validated data (341) sesuai dengan raw data (348) dikurangi 7 duplikat yang telah terdokumentasi
- Total revenue memiliki kesesuaian penuh — selisih Rp 149.502.000 identik dengan nilai baris duplikat yang dihapus
- Tidak ditemukan selisih yang tidak dapat dijelaskan antara data hasil cleaning dan data sumber (raw/ERP)
- Seluruh 12 cabang menunjukkan kecocokan data antara Pivot Table dan perhitungan SUMIFS independen
- Dataset telah memenuhi standar untuk digunakan dalam laporan manajemen

## Output
**Data Reconciliation Report**, berisi:
- Transaction Comparison Report (tabel jumlah baris di atas)
- Revenue Comparison Report (tabel total revenue di atas)
- Data Difference Analysis (penjelasan selisih akibat duplicate removal)
- **Final Approved Dataset**: Clean Sales Transaction (341 baris) — disetujui untuk digunakan pada tahap Pivot Table Analysis (Step 7)

## Kesimpulan
Proses Data Reconciliation memastikan bahwa data hasil export dan proses cleaning telah sesuai dengan sumber data utama (ERP/Raw Export), dengan seluruh selisih angka (baris, revenue, unit) dapat dijelaskan sepenuhnya oleh proses penghapusan duplicate records pada Step 4. Dataset yang telah direkonsiliasi ini disetujui sebagai dasar pembuatan Pivot Table, Dashboard Excel, dan Executive Reporting kepada manajemen pada tahap-tahap berikutnya.

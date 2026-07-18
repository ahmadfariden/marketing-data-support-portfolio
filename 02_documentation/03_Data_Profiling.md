# Sales Performance Report — Step 3: Data Profiling
**Proyek:** Sales Performance Report (Dealer Motor)
**Periode Data:** 13 – 19 Juli 2026 (Minggu ke-29)

---

## Tujuan
Mengidentifikasi kualitas data, memahami struktur dataset, serta menemukan permasalahan yang dapat memengaruhi akurasi analisis dan pelaporan Sales Performance.

## Input
- Sales Transaction Data (348 baris, 14 kolom)

## Proses & Formula yang Digunakan
Profiling dilakukan di sheet terpisah (**Data Profiling**) dengan mereferensi sheet **Sales Transaction**.

| Metric | Formula | Tujuan |
|---|---|---|
| Total Baris | `=COUNTA('Sales Transaction'!A:A)-1` | Menghitung jumlah baris data (dikurangi header) |
| Missing – Sales Rep | `=COUNTBLANK('Sales Transaction'!D2:D349)` | Menghitung sel kosong pada kolom Sales Rep |
| Missing – Customer Name | `=COUNTBLANK('Sales Transaction'!E2:E349)` | Menghitung sel kosong pada kolom Customer Name |
| Duplicate Records | `=COUNTIF('Sales Transaction'!O2:O349;">1")` | Menghitung baris yang Transaction ID-nya muncul lebih dari 1x |
| Transaksi Total Sales = 0 | `=COUNTIF('Sales Transaction'!K2:K349;0)` | Menghitung transaksi dengan nilai penjualan nol (indikasi batal/refund) |

Kolom bantu tambahan di sheet **Sales Transaction**:
| Kolom Bantu | Formula | Fungsi |
|---|---|---|
| Duplicate Check | `=COUNTIF($A$2:$A$349;A2)` | Menandai berapa kali suatu Transaction ID muncul (1 = unik, ≥2 = duplikat) |
| Cek Tipe Data Tanggal | `=ISNUMBER(C2)` | Mengecek apakah kolom Date sudah berupa format Date asli (TRUE) atau masih teks (FALSE) |

Konsistensi kolom **Branch** juga diperiksa secara visual menggunakan **Pivot Table** (Branch di area Rows) untuk melihat seluruh nilai unik yang tercatat.

## Temuan
| No | Temuan | Detail |
|---|---|---|
| 1 | Missing Values – Sales Rep | 12 baris kosong |
| 2 | Missing Values – Customer Name | 2 baris kosong |
| 3 | Duplicate Records | 14 baris (7 pasang transaksi kembar) |
| 4 | Transaksi Total Sales = 0 | 5 baris (indikasi transaksi batal/refund) |
| 5 | Inkonsistensi Format Tanggal | 3 format berbeda: ISO (`2026-07-14`), slash (`15/07/2026`), teks Indonesia (`15 Juli 2026`); seluruh kolom Date tersimpan sebagai teks (`ISNUMBER` = FALSE untuk semua baris) |
| 6 | Inkonsistensi Nama Cabang | 17 nilai unik muncul di Pivot Table, padahal cabang asli hanya 12. Penyebab: perbedaan kapitalisasi (`Bekasi` vs `BEKASI`) dan perbedaan penulisan/singkatan (`Jaksel` vs `Jakarta Selatan`, `Tangerang Kota` vs `Tangerang`) |

## Output
Laporan kualitas data (Data Quality Findings) berisi:
- Missing Values Report
- Duplicate Records Report
- Data Consistency Issues (format tanggal & nama cabang)
- Data Quality Findings Summary (tabel di atas)

## Kesimpulan
Ditemukan 6 kategori masalah kualitas data yang perlu diperbaiki sebelum data digunakan untuk analisis dan pembuatan Sales Performance Report: missing values pada 2 kolom, duplikasi transaksi, transaksi bernilai nol, format tanggal yang tidak seragam, dan inkonsistensi penulisan nama cabang. Seluruh temuan ini menjadi dasar pengerjaan tahap Data Cleaning (Step 4).

# Sales Performance Report — Step 2: Data Collection
**Proyek:** Sales Performance Report (Dealer Motor)
**Periode Data:** 13 – 19 Juli 2026 (Minggu ke-29)
**File Sumber:** sales_july_week3_2026_RAW.xlsx

---

## Tujuan
Mengumpulkan seluruh file data yang diperlukan untuk analisis penjualan mingguan dan memastikan data tersedia secara lengkap sebelum masuk ke tahap Data Profiling.

## Input
- Sales Transaction Data (hasil export ERP/Sales System — Step 1)
- Target Sales Data
- Branch Master Data
- Product Master Data

## Proses
- Mengumpulkan file raw export dari sistem (`sales_july_week3_2026_RAW.xlsx`)
- Memastikan periode data sesuai kebutuhan (1 minggu: 13–19 Juli 2026)
- Memastikan struktur file dapat dibuka dan dibaca
- Mengidentifikasi sheet yang akan digunakan
- Mendokumentasikan sumber & struktur tiap sheet

## Temuan
| Sheet | Jumlah Baris | Jumlah Kolom | Keterangan |
|---|---|---|---|
| Sales Transaction | 348 | 14 | Data transaksi mentah, 12 cabang |
| Target Sales | 12 | 4 | Target mingguan per cabang |
| Branch Master | 12 | 5 | Data referensi cabang |
| Product Master | 10 | 4 | Data referensi produk |

- Seluruh sheet dapat diakses tanpa kendala
- Struktur antar sheet konsisten (siap untuk tahap profiling)

## Output
Kumpulan raw dataset yang siap dilakukan Data Profiling:
- Sales Transaction Data
- Target Sales Data
- Branch Master Data
- Product Master Data

## Kesimpulan
Seluruh dataset yang diperlukan berhasil dikumpulkan dari satu file export dengan struktur multi-sheet yang jelas. Data siap digunakan pada tahap Data Profiling (Step 3) untuk pemeriksaan kualitas data.

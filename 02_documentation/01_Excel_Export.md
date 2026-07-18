# Sales Performance Report — Step 1: Excel Export
**Proyek:** Sales Performance Report (Dealer Motor)
**Periode Data:** 13 – 19 Juli 2026 (Minggu ke-29)
**File Output:** sales_july_week3_2026_RAW.xlsx
**saya sudah ubah nama filenya menjadi Marketing_Data_Support_Project.xlsx

---

## Tujuan
Mengambil data penjualan dari sistem operasional perusahaan ke dalam format Excel agar dapat digunakan untuk proses analisis dan pelaporan.

## Input
- Database penjualan
- Sistem dealer
- Sistem ERP / Sales System
- Data transaksi cabang

## Proses
- Menentukan periode data yang dibutuhkan: 1 minggu (13–19 Juli 2026, Minggu ke-29)
- Melakukan export data dari sistem (ERP/Sales System) ke dalam format Excel
- Memastikan seluruh kolom yang diperlukan ikut ter-export: Transaction ID, Date, Branch, Sales Rep, Customer Name, Product Code, Product Name, Qty, Unit Price, Discount, Total Sales, Payment Method, Payment Status, Channel
- Menyimpan file dalam format Excel (.xlsx) dengan struktur multi-sheet

## Temuan
- Data berhasil diexport dari sistem dalam satu file multi-sheet
- Dataset berisi informasi transaksi, cabang, produk, dan sales
- Terdapat 4 kategori data dalam satu file: Sales Transaction, Target Sales, Branch Master, Product Master

## Output
**Raw Excel Dataset** — `sales_july_week3_2026_RAW.xlsx`, terdiri dari 4 sheet:

| Sheet | Baris | Kolom | Keterangan |
|---|---|---|---|
| Sales Transaction | 348 | 14 | Data transaksi mentah, 12 cabang |
| Target Sales | 12 | 4 | Target mingguan per cabang |
| Branch Master | 12 | 5 | Data referensi cabang |
| Product Master | 10 | 4 | Data referensi produk |

## Kesimpulan
Data berhasil diexport dari sistem operasional dalam format Excel dengan struktur multi-sheet yang jelas, dan siap digunakan pada tahap Data Collection (Step 2).

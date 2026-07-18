# Sales Performance Report — Step 8: Dashboard Excel
**Proyek:** Sales Performance Report (Dealer Motor)
**Periode Data:** 13 – 19 Juli 2026 (Minggu ke-29)
**Sumber Data:** Sheet "Clean Sales Transaction", Pivot Table Target vs Actual, Product Performance, Sales Rep Performance (hasil Step 7)

---

## Tujuan
Menggabungkan seluruh hasil analisis Pivot Table (Step 7) ke dalam satu tampilan visual terpadu (KPI Cards + Chart) di sheet **Dashboard**, sehingga informasi performa penjualan mingguan dapat dibaca cepat dan siap dipresentasikan ke manajemen/direktur.

## Input
- Sheet **Target vs Actual** (Pivot Table + kolom Target Revenue & Achievement %)
- Sheet **Product Performance** (Pivot Table)
- Sheet **Sales Rep Performance** (Pivot Table)
- Sheet **Clean Sales Transaction** (data final bersih)

## Proses

### 1. KPI Cards
Dibuat di bagian atas sheet Dashboard, berisi 3 ringkasan angka utama. Seluruh formula menggunakan filter `Status Transaksi = "Normal"` agar transaksi Batal/Refund tidak ikut terhitung.

| KPI | Formula | Hasil |
|---|---|---|
| Total Revenue | `=SUMIFS('Clean Sales Transaction'!K:K;'Clean Sales Transaction'!Q:Q;"Normal")` | 9.433.489.000 |
| Total Unit Terjual | `=SUMIFS('Clean Sales Transaction'!H:H;'Clean Sales Transaction'!Q:Q;"Normal")` | 352 |
| Avg Achievement % | `=AVERAGE('Target vs Actual'!E4:E15)` | 233,89% |

> **Catatan penting:** Percobaan awal menggunakan `=SUM(...)` tanpa filter status menghasilkan Total Unit Terjual = 357 (selisih 5 dari hasil final), karena ikut menghitung 5 transaksi berstatus "Batal/Refund". Setelah diganti ke `SUMIFS` dengan kriteria status, hasil menjadi 352 — konsisten dengan Grand Total pada Pivot Table Product Performance.

### 2. Chart 1 — Actual vs Target Sales per Cabang
- **Sumber data:** Sheet Target vs Actual, kolom Branch, Sum of Total Sales, Target Revenue (baris Bandung s.d. Tangerang, **tanpa** baris Grand Total)
- **Tipe chart:** Clustered Column Chart
- **Catatan teknis:** Kolom Achievement % sengaja **tidak** disertakan dalam data chart karena skalanya (format persen, contoh 1,74) sangat berbeda dari skala Rupiah (ratusan juta), sehingga jika digabung akan membuat bar tidak proporsional/tidak terbaca.

### 3. Chart 2 — Product Performance (Revenue per Tipe Motor)
- **Sumber data:** Sheet Product Performance, kolom Product Name, Sum of Total Sales (baris NMAX s.d. Freego, tanpa Grand Total)
- **Tipe chart:** Clustered Column Chart
- **Catatan teknis:** Kolom Sum of Qty tidak disertakan dalam chart yang sama karena perbedaan skala drastis (satuan unit vs satuan Rupiah miliaran) menyebabkan bar Qty tidak terlihat. Data Qty tetap tersedia di tabel Pivot Table Product Performance sebagai referensi terpisah.

### 4. Chart 3 — Sales Rep Performance (Revenue per Sales)
- **Sumber data:** Sheet Sales Rep Performance, kolom Sales Rep, Sum of Total Sales (tanpa Grand Total)
- **Tipe chart:** Clustered Column Chart
- **Catatan teknis:** Sama seperti Chart 2, kolom Count of Transaction ID dikeluarkan dari chart karena perbedaan skala. Baris "Unknown" (representasi data missing value Sales Rep) tetap disertakan dalam chart untuk menjaga transparansi data, namun dapat di-exclude sesuai kebutuhan presentasi.

### Kendala Teknis Selama Pembuatan Chart
| Kendala | Penyebab | Solusi |
|---|---|---|
| Chart otomatis menjadi PivotChart dengan tombol filter menempel | Data source diambil langsung dari area Pivot Table | Salin data pivot sebagai **Values Only** ke area baru, baru buat chart dari data tersebut |
| Bar salah satu kategori (Target Revenue / Qty / Count) tidak terlihat pada chart gabungan | Perbedaan skala nilai yang signifikan antar kolom (contoh: satuan unit vs Rupiah miliaran) | Pisahkan kolom dengan skala jauh berbeda ke chart terpisah, atau gunakan Secondary Axis bila ingin tetap digabung |
| Bar "Grand Total" muncul dan merusak skala chart | Baris Grand Total ikut ter-select saat membuat chart | Pastikan area seleksi data berhenti tepat sebelum baris Grand Total |

## Output
Sheet **Dashboard** dengan struktur:
```
┌─────────────────────────────────────────┐
│  KPI Cards: Total Revenue, Total Unit,   │
│  Avg Achievement %                       │
├─────────────────────────────────────────┤
│  Chart 1: Actual vs Target per Cabang    │
├─────────────────────────────────────────┤
│  Chart 2: Product Performance            │
├─────────────────────────────────────────┤
│  Chart 3: Sales Rep Performance          │
└─────────────────────────────────────────┘
```

## Kesimpulan
Dashboard berhasil menggabungkan tiga hasil analisis Pivot Table (Target vs Actual, Product Performance, Sales Rep Performance) ke dalam satu tampilan visual yang ringkas dan siap presentasi. Insight utama yang tervisualisasi:

1. **Seluruh 12 cabang** mencapai realisasi penjualan di atas 100% target mingguan, dengan rata-rata pencapaian **233,89%**.
2. **NMAX** merupakan produk dengan kontribusi revenue terbesar, jauh di atas produk lainnya.
3. **Lukman Hakim** merupakan sales rep dengan performa tertinggi, didorong oleh volume transaksi (closing) yang konsisten.

Dashboard ini menjadi output akhir dari rangkaian proses **Data Collection → Data Profiling → Data Cleaning → Pivot Table Analysis → Dashboard Excel**, dan siap digunakan sebagai bahan laporan mingguan kepada manajemen/direktur.

---

## Ringkasan Alur Proyek End-to-End

```
Raw Sales Transaction (348 baris, 14 kolom)
        ↓  [Step 3: Data Profiling]
6 temuan masalah kualitas data
        ↓  [Step 4: Data Cleaning]
Clean Sales Transaction (341 baris, siap pakai)
        ↓  [Step 7: Pivot Table Analysis]
3 Pivot Table: Target vs Actual, Product Performance, Sales Rep Performance
        ↓  [Step 8: Dashboard Excel]
Dashboard terpadu (KPI Cards + 3 Chart) — siap presentasi
```

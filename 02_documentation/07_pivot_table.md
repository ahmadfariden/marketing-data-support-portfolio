# Sales Performance Report — Step 7: Pivot Table Analysis
**Proyek:** Sales Performance Report (Dealer Motor)
**Periode Data:** 13 – 19 Juli 2026 (Minggu ke-29)
**Sumber Data:** Sheet "Clean Sales Transaction" (341 baris, hasil Step 4: Data Cleaning)

---

## Tujuan
Mengubah data transaksi yang sudah bersih menjadi ringkasan informasi bisnis (business summary) yang siap dianalisis dan digunakan sebagai bahan pengambilan keputusan, mencakup pencapaian target per cabang, performa produk, dan performa sales rep.

## Input
- Sheet **Clean Sales Transaction** (341 baris, 14 kolom, hasil Data Cleaning)
- Sheet **Target Sales** (12 baris — target mingguan per cabang)

## Catatan Umum
Seluruh Pivot Table pada tahap ini menggunakan **Filter: Status Transaksi = "Normal"**, agar transaksi yang berstatus "Batal/Refund" (5 baris) tidak ikut terhitung dalam ringkasan performa.

---

## 1. Pivot Table — Target vs Actual (per Cabang)

### Proses
1. Insert PivotTable dari sheet Clean Sales Transaction
2. **Rows:** Branch
3. **Values:** Sum of Total Sales
4. **Filters:** Status Transaksi = "Normal"
5. Menarik Target Revenue dari sheet Target Sales menggunakan formula lookup lintas-sheet
6. Menghitung persentase pencapaian target

### Formula yang Digunakan
| Kolom | Formula | Fungsi |
|---|---|---|
| Target Revenue | `=SUMIFS('Target Sales'!D:D;'Target Sales'!A:A;A4)` | Menarik nilai target sesuai nama cabang (lookup berdasarkan nama, bukan posisi baris) |
| Achievement % | `=B4/D4` | Actual Sales dibagi Target Revenue |

Format kolom Achievement % diubah menjadi **Percentage** melalui Format Cells agar tampil sebagai `174%` alih-alih `1.743455769`.

### Temuan
| Branch | Actual Sales | Target Revenue | Achievement % |
|---|---|---|---|
| Bandung | 906.597.000 | 520.000.000 | 174,35% |
| Bekasi | 923.721.000 | 260.000.000 | 355,28% |
| Bogor | 598.845.000 | 208.000.000 | 287,91% |
| Cibubur | 800.267.000 | 468.000.000 | 171,00% |
| Cikarang | 760.218.000 | 260.000.000 | 292,39% |
| Depok | 768.832.000 | 260.000.000 | 295,70% |
| Jakarta Selatan | 918.489.000 | 468.000.000 | 196,26% |
| Jakarta Timur | 532.139.000 | 260.000.000 | 204,67% |
| Karawang | 862.042.000 | 312.000.000 | 276,30% |
| Serang | 650.659.000 | 468.000.000 | 139,03% |
| Sukabumi | 924.626.000 | 468.000.000 | 197,57% |
| Tangerang | 787.054.000 | 364.000.000 | 216,22% |
| **Grand Total** | **9.433.489.000** | – | – |

### Output
Tabel **Target vs Actual per Cabang**, siap digunakan sebagai bahan Executive Reporting.

### Kesimpulan
Seluruh 12 cabang mencatatkan pencapaian di atas 100% target mingguan, dengan **Bekasi (355%)** sebagai pencapaian tertinggi dan **Serang (139%)** sebagai pencapaian terendah — namun tetap di atas target. Hal ini mengindikasikan target yang ditetapkan untuk periode ini relatif rendah dibanding realisasi penjualan aktual.

---

## 2. Pivot Table — Product Performance

### Proses
1. Insert PivotTable dari sheet Clean Sales Transaction
2. **Rows:** Product Name
3. **Values:** Sum of Total Sales, Sum of Qty
4. **Filters:** Status Transaksi = "Normal"
5. Sort **Sum of Total Sales** dari Largest to Smallest

### Temuan
| Product Name | Sum of Total Sales | Sum of Qty |
|---|---|---|
| NMAX | 2.631.760.000 | 80 |
| Aerox | 1.811.542.000 | 62 |
| Lexi | 1.025.034.000 | 38 |
| Fazzio | 691.225.000 | 33 |
| XSR 155 | 683.880.000 | 17 |
| MX King | 652.638.000 | 27 |
| Mio | 574.938.000 | 31 |
| Grand Filano | 475.323.000 | 18 |
| Gear | 471.700.000 | 27 |
| Freego | 415.449.000 | 19 |
| **Grand Total** | **9.433.489.000** | **352** |

### Output
Tabel **Product Performance Ranking**, mencakup revenue dan volume unit terjual per tipe produk.

### Kesimpulan
- **NMAX** merupakan produk unggulan dengan revenue dan volume tertinggi (2,63 miliar, 80 unit), menjadikannya kontributor utama total penjualan.
- **XSR 155** merupakan produk kategori *high-value, low-volume* — revenue-nya (683 juta) mendekati MX King (652 juta), namun unit terjualnya paling rendah (17 unit) karena harga satuan yang tinggi (±41 juta/unit). Produk ini cocok untuk strategi niche/premium, bukan strategi volume.
- **Mio** merupakan produk *entry-level* dengan volume tinggi (31 unit) namun revenue relatif rendah, mencerminkan harga satuan yang lebih terjangkau.

---

## 3. Pivot Table — Sales Rep Performance

### Proses
1. Insert PivotTable dari sheet Clean Sales Transaction
2. **Rows:** Sales Rep
3. **Values:** Count of Transaction ID, Sum of Total Sales, Sum of Qty
4. **Filters:** Status Transaksi = "Normal"
5. Sort **Sum of Total Sales** dari Largest to Smallest

### Temuan (Top 5 & catatan khusus)
| Sales Rep | Count of Transaction ID | Sum of Total Sales | Sum of Qty |
|---|---|---|---|
| Lukman Hakim | 27 | 668.561.000 | 30 |
| Kiki Amelia | 20 | 566.792.000 | 20 |
| Rangga Saputra | 20 | 554.821.000 | 21 |
| Sari Dewi | 19 | 538.697.000 | 20 |
| Taufik Hidayat | 19 | 524.072.000 | 19 |
| ... | ... | ... | ... |
| Rudi Hartono | 9 | 261.338.000 | 10 |
| **Unknown** | 12 | 331.114.000 | 13 |
| **Grand Total** | **336** | **9.433.489.000** | **352** |

*Catatan: baris "Unknown" merepresentasikan 12 transaksi dengan data Sales Rep kosong pada data mentah (hasil Data Cleaning tahap missing value handling), dan tidak dihitung sebagai individu sales rep dalam evaluasi performa.*

### Output
Tabel **Sales Rep Performance Ranking**, mencakup jumlah transaksi (closing), total revenue, dan unit terjual per sales rep.

### Kesimpulan
**Lukman Hakim** merupakan top performer dengan jumlah transaksi tertinggi (27) yang berbanding lurus dengan total revenue tertinggi (668 juta), menunjukkan bahwa **konsistensi closing** menjadi faktor utama pencapaian, bukan semata nilai transaksi individual yang besar. Sebaliknya, **Rudi Hartono** memiliki jumlah transaksi paling sedikit (9) dan menjadi kandidat untuk evaluasi/coaching lebih lanjut.

---

## Ringkasan Step 7

| Pivot Table | Fokus Analisis | Status |
|---|---|---|
| Target vs Actual | Pencapaian target per cabang | ✅ Selesai |
| Product Performance | Produk terlaris (revenue & volume) | ✅ Selesai |
| Sales Rep Performance | Ranking performa sales individu | ✅ Selesai |

Ketiga Pivot Table di atas menjadi fondasi data untuk tahap berikutnya, yaitu **Step 8: Dashboard Excel**, di mana seluruh ringkasan ini akan divisualisasikan dalam satu tampilan terpadu (chart + KPI) untuk kebutuhan pelaporan ke manajemen/direktur.

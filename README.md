# 📊 Sales Performance Report — Marketing Data Support Project

Proyek Marketing Data Support menggunakan Microsoft Excel untuk mengolah data penjualan dealer motor dari export ERP/Sales System menjadi dashboard dan laporan eksekutif yang siap digunakan dalam meeting manajemen.

Workflow mencakup data collection, data cleaning, Power Query automation, Pivot Table analysis, dashboard development, business insight, hingga executive reporting.

**Studi Kasus:** Laporan Performa Penjualan Dealer Motor — Periode 13–19 Juli 2026 (Minggu ke-29)

---

## 🗂️ Struktur Folder

```
├── 01_Excel_Marketing_Data_Support/
│   ├── Marketing_Data_Support_Project.xlsx      # Workbook utama: raw data, cleaning, pivot table, dashboard
│   └── Sales_Report_PowerQuery_Automated.xlsx   # Workbook dengan Power Query (automated refresh)
│
├── 02_documentation/
│   ├── 01_Excel_Export.md
│   ├── 02_Data_Collection.md
│   ├── 03_Data_Profiling.md
│   ├── 04_Data_Cleaning.md
│   ├── 05_Data_Validation.md
│   ├── 06_Data_Reconciliation.md
│   ├── 07_pivot_table.md
│   ├── 08_dashboard.md
│   ├── 09_report_automation.md
│   ├── 10_insight.md
│   ├── 11_executive_reporting.md
│   ├── 12_director_meeting.md
│   ├── 13_business_decision.md
│   ├── 14_business_monitoring.md
│   └── 15_continuous_improvement.md
│
└── 03_reporting/
    ├── dashboard.png
    ├── Actual_vs_Target_Sales_per_Cabang.png
    ├── Product_Performance_Revenue_per_Tipe_Motor.png
    ├── Sales_Rep_Performance_Revenue_per_Sales.png
    ├── Executive_Summary_Sales_Performance.docx
    └── Executive_Presentation_Sales_Performance.pptx
```

---

## 🎯 Tujuan Proyek

Mensimulasikan proses kerja data support/analyst di perusahaan menengah secara menyeluruh — bukan hanya membuat chart, tetapi mendokumentasikan **seluruh siklus**: dari data kotor (missing values, duplikat, format tidak konsisten) sampai menjadi rekomendasi bisnis yang dipresentasikan ke direktur.

## 🔄 Alur Kerja (15 Tahap)

```
01 Excel Export → 02 Data Collection → 03 Data Profiling → 04 Data Cleaning
→ 05 Data Validation → 06 Data Reconciliation → 07 Pivot Table Analysis
→ 08 Dashboard Excel → 09 Report Automation (Power Query) → 10 Insight
→ 11 Executive Reporting → 12 Director Meeting & Decision Support
→ 13 Business Decision & Action Plan → 14 Business Monitoring & Performance Review
→ 15 Continuous Improvement & Reporting Optimization
```

Dokumentasi lengkap tiap tahap (tujuan, input, proses, formula yang digunakan, temuan, output, kesimpulan) tersedia di folder [`02_documentation/`](./02_documentation).

## 🛠️ Tools & Teknik yang Digunakan

| Kategori | Tools/Teknik |
|---|---|
| Data Cleaning (Manual) | Excel Formula: `TRIM`, `PROPER`, `SUBSTITUTE`, `IF`, `IFERROR`, `DATE`, `COUNTIF`, `COUNTBLANK` |
| Data Automation | Power Query (Trim, Capitalize Each Word, Replace Values, Remove Duplicates, Custom Column) |
| Analisis Data | Pivot Table (Branch Performance, Product Performance, Sales Rep Performance, Target vs Actual) |
| Visualisasi | Excel Chart (Clustered Column Chart), Excel Dashboard (KPI Cards + Chart) |
| Reporting | Microsoft Word (Executive Summary), Microsoft PowerPoint (Meeting Presentation) |

## 📌 Ringkasan Hasil Analisis

| Metrik | Nilai |
|---|---|
| Total Revenue | Rp 9.433.489.000 |
| Total Unit Terjual | 352 unit |
| Rata-rata Achievement Rate | 233,89% (seluruh 12 cabang di atas target) |
| Cabang dengan Achievement Tertinggi | Bekasi (355,3%) |
| Produk Terlaris | NMAX (27,9% dari total revenue) |
| Sales Rep Terbaik | Lukman Hakim (27 transaksi/minggu) |

Insight bisnis lengkap dan rekomendasi tersedia di [`10_insight.md`](./02_documentation/10_insight.md) dan [`11_executive_reporting.md`](./02_documentation/11_executive_reporting.md).

## 📈 Data Quality Journey

Dataset mentah (348 baris) mengandung berbagai masalah kualitas data yang umum ditemui di dunia kerja nyata — seluruhnya berhasil ditelusuri dan diperbaiki secara sistematis:

| Masalah | Ditemukan di | Diperbaiki di |
|---|---|---|
| 12 missing values (Sales Rep) | Data Profiling | Data Cleaning |
| 2 missing values (Customer Name) | Data Profiling | Data Cleaning |
| 14 baris duplikat (7 transaksi kembar) | Data Profiling | Data Cleaning |
| 3 format tanggal berbeda | Data Profiling | Data Cleaning |
| 17 variasi penulisan nama cabang (seharusnya 12) | Data Profiling | Data Cleaning |
| 5 transaksi bernilai nol | Data Profiling | Data Cleaning |

## 🖼️ Preview Dashboard

Lihat [`03_reporting/dashboard.png`](./03_reporting/dashboard.png) untuk tampilan Dashboard Excel lengkap (KPI Cards + 3 chart: Branch, Product, Sales Rep Performance).

---

## 👤 Author

**Ahmad Farid**

- Email: [ahmad.fariden@gmail.com](mailto:ahmad.fariden@gmail.com)
- LinkedIn: [linkedin.com/in/ahmadfariden](https://linkedin.com/in/ahmadfariden)
- GitHub: [github.com/ahmadfariden](https://github.com/ahmadfariden)

---

*Proyek ini dibuat sebagai bagian dari portofolio pembelajaran mandiri di bidang Data Analysis.*

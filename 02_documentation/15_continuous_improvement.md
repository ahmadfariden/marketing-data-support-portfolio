# Sales Performance Report — Step 15: Continuous Improvement & Reporting Optimization
**Proyek:** Sales Performance Report (Dealer Motor)
**Periode Data:** 13 – 19 Juli 2026 (Minggu ke-29)
**Catatan:** Berbeda dari step lain yang sebagian bersifat simulasi (karena belum ada meeting/data periode lanjutan sesungguhnya), evaluasi proses pada dokumen ini disusun berdasarkan **kendala nyata yang dialami langsung** selama pengerjaan Step 1–9 proyek ini — sehingga rekomendasinya bersifat konkret dan telah terbukti relevan.

---

## Tujuan
Melakukan evaluasi terhadap proses reporting dan meningkatkan efektivitas penyajian data agar kebutuhan manajemen dapat terpenuhi secara lebih cepat, akurat, dan relevan dengan kebutuhan bisnis.

## Input
- Management Feedback — belum tersedia secara formal (belum ada meeting aktual); evaluasi pada dokumen ini mengacu pada **Process Feedback** dari pengalaman pengerjaan langsung
- Reporting Process Evaluation (dirangkum dari Step 3–9)
- Dashboard Usage Review (Step 8)
- Business Requirements (mengacu pada SOP Data Support Workflow)

## Proses
- Meninjau kembali kendala teknis yang terjadi selama proses Data Cleaning manual (Step 4) dan Report Automation (Step 9)
- Mengevaluasi efisiensi waktu antara pendekatan manual vs otomatis
- Mengidentifikasi kebutuhan KPI tambahan yang belum tercakup pada Dashboard saat ini
- Menyusun rencana perbaikan struktur dan proses reporting untuk periode berikutnya

---

## Reporting Process Evaluation (Berdasarkan Pengalaman Nyata)

### Kendala yang Ditemukan Selama Data Cleaning Manual (Step 4)
| Kendala | Penyebab | Dampak |
|---|---|---|
| Circular reference berulang | Formula pembersih data (`PROPER`, `TRIM`, `SUBSTITUTE`) sempat ditulis di kolom yang sama dengan data sumber | Hasil formula keluar 0, perlu debugging berulang |
| Referensi kolom salah sasaran | Kolom sering bergeser posisi setelah insert/hapus kolom bantu, formula lama tidak ikut ter-update | Hasil perhitungan (SUMIFS, Duplicate Check) sempat tidak akurat sebelum diperbaiki |
| Separator formula (`,` vs `;`) | Perbedaan regional setting Excel (locale Indonesia menggunakan `;`) | Formula gagal jalan sampai disesuaikan |
| Chart otomatis menjadi PivotChart | Data chart diambil langsung dari area Pivot Table | Tombol filter ikut menempel di chart, tampilan kurang profesional untuk dashboard |
| Skala data tidak proporsional pada chart gabungan | Kolom dengan skala sangat berbeda (contoh: Rupiah miliaran vs unit puluhan) digabung dalam satu chart | Salah satu seri data tidak terlihat pada chart |

### Perbandingan Efisiensi: Manual vs Power Query
| Aspek | Data Cleaning Manual (Step 4) | Report Automation via Power Query (Step 9) |
|---|---|---|
| Waktu pengerjaan | ±1–2 jam, banyak kolom bantu | ±15 menit |
| Risiko error | Tinggi (5 jenis kendala di atas) | Rendah — tercatat otomatis di Applied Steps |
| Update periode berikutnya | Ulang dari awal | Klik Refresh All |

---

## Temuan

### Temuan 1 — KPI yang Membutuhkan Monitoring Lebih Detail
Saat ini Dashboard (Step 8) berfokus pada KPI agregat mingguan. Belum tersedia:
- Perbandingan tren **antar-minggu** (baru bisa dibangun setelah data periode ke-30 dst. tersedia, sesuai kerangka Step 14)
- KPI **rata-rata nilai transaksi per sales rep** (average transaction value), yang dapat melengkapi analisis pola "closing konsisten vs nilai transaksi besar" pada Step 10

### Temuan 2 — Kebutuhan Penyesuaian Dashboard per Stakeholder
Dashboard saat ini dirancang generik untuk seluruh audiens. Kebutuhan info berbeda antara:
- **Direktur** — cukup KPI Cards + 3 chart ringkas (sudah tersedia)
- **Manager Cabang** — membutuhkan drill-down per cabang yang belum tersedia di versi saat ini
- **Tim Sales** — membutuhkan tampilan personal (transaksi & achievement individu) yang belum tersedia

### Temuan 3 — Format Laporan Dapat Lebih Ringkas
Executive Summary (Step 11) sudah dalam format 2 halaman, namun proses penyusunan dokumentasi (Step 1–14) menghasilkan 12+ file terpisah — berpotensi disederhanakan menjadi satu portal/indeks ringkas untuk memudahkan navigasi oleh pengguna baru.

### Temuan 4 — Peluang Efisiensi Proses
Pendekatan Power Query (Step 9) terbukti secara nyata memangkas waktu pengerjaan Data Cleaning dari hitungan jam menjadi belasan menit, sekaligus mengeliminasi 5 jenis kendala teknis yang terjadi pada proses manual.

---

## Reporting Process Improvement Plan

| No | Perbaikan yang Diusulkan | Manfaat |
|---|---|---|
| 1 | Jadikan Power Query sebagai standar proses Data Cleaning sejak awal periode berikutnya (bukan hanya sebagai tahap otomatisasi belakangan) | Mengurangi waktu pengerjaan dan risiko error sejak periode pertama |
| 2 | Tambahkan kolom **Average Transaction Value** pada Pivot Table Sales Rep Performance (Step 7) | Melengkapi analisis pola performa sales rep |
| 3 | Kembangkan varian Dashboard sederhana khusus **Manager Cabang** (fokus 1 cabang) dan **Sales Rep** (fokus performa individu) | Informasi lebih relevan per level pengguna, tanpa perlu menyaring data sendiri |
| 4 | Susun 1 dokumen indeks/ringkasan yang memetakan seluruh 15 file dokumentasi proyek (Step 1–15) | Memudahkan navigasi bagi pengguna baru atau saat handover pekerjaan |
| 5 | Standarkan penamaan kolom & struktur sheet sejak Data Collection (Step 1) agar konsisten di seluruh periode, mengurangi risiko pergeseran referensi kolom seperti yang terjadi pada Step 4 | Mengurangi kendala teknis pada proses cleaning periode berikutnya |

## Output
**Continuous Improvement Report**, berisi:
- **Updated Dashboard** — rencana pengembangan varian per stakeholder (Temuan 2), menyusul pada periode berikutnya
- **Improved Reporting Template** — Power Query dijadikan standar proses sejak Data Collection (Perbaikan 1)
- **Additional KPI Monitoring** — Average Transaction Value per Sales Rep (Perbaikan 2)
- **Reporting Process Improvement Plan** — 5 poin perbaikan di atas

## Kesimpulan
Proses Continuous Improvement & Reporting Optimization pada proyek ini didasarkan pada kendala nyata yang teridentifikasi sepanjang pengerjaan Step 1–14 — bukan asumsi semata. Perbandingan langsung antara proses manual dan Power Query menunjukkan potensi efisiensi yang signifikan, sementara evaluasi kebutuhan stakeholder mengidentifikasi peluang pengembangan Dashboard yang lebih personal. Hasil evaluasi ini menjadi dasar perbaikan berkelanjutan, memastikan sistem reporting terus berkembang mengikuti kebutuhan bisnis pada periode-periode berikutnya.

---

## Penutup Siklus Proyek

Dengan selesainya Step 15, seluruh siklus **Sales Performance Report — Data Support Workflow** (Step 1 hingga Step 15) telah didokumentasikan secara lengkap:

```
Data Collection → Data Profiling → Data Cleaning → Pivot Table Analysis
→ Dashboard Excel → Report Automation (Power Query) → Insight
→ Executive Reporting → Director Meeting & Decision Support
→ Business Decision & Action Plan → Business Monitoring & Performance Review
→ Continuous Improvement & Reporting Optimization
```

Siklus ini bersifat **iteratif** — hasil Continuous Improvement (Step 15) menjadi masukan bagi Data Collection (Step 1) pada periode pelaporan berikutnya, khususnya terkait standarisasi struktur data dan adopsi Power Query sejak awal proses.

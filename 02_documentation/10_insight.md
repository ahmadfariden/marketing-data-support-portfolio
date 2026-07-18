# Sales Performance Report — Step 10: Insight
**Proyek:** Sales Performance Report (Dealer Motor)
**Periode Data:** 13 – 19 Juli 2026 (Minggu ke-29)
**Sumber Data:** Dashboard Excel, Pivot Table (Target vs Actual, Product Performance, Sales Rep Performance)

---

## Tujuan
Mengubah hasil Dashboard dan analisis penjualan menjadi insight bisnis yang dapat digunakan manajemen untuk meningkatkan performa penjualan dan mendukung pengambilan keputusan strategis.

## Reporting Focus
- Monitoring achievement sales target
- Identifikasi kontribusi & distribusi performa antar cabang
- Tracking kontribusi produk terhadap total revenue
- Evaluasi performa sales rep individu

## Input
- Sheet Dashboard (KPI Cards + 3 Chart)
- Tabel Target vs Actual (12 cabang)
- Tabel Product Performance (10 tipe produk)
- Tabel Sales Rep Performance (20 sales rep)

## Proses Analisis
- Menghitung persentase kontribusi tiap cabang terhadap total revenue
- Membandingkan achievement % tiap cabang untuk mengidentifikasi rentang performa tertinggi dan terendah
- Menghitung persentase kontribusi tiap produk terhadap total revenue dan total unit terjual
- Membandingkan proporsi revenue vs unit terjual untuk mengidentifikasi karakteristik produk (high-value vs high-volume)
- Menganalisis pola jumlah transaksi (closing) vs total revenue per sales rep

---

## Key Findings

### Finding 1 — Distribusi Kontribusi Cabang Relatif Merata
Tidak ada satu cabang yang mendominasi secara ekstrem. Empat cabang teratas (Sukabumi, Bekasi, Jakarta Selatan, Bandung) masing-masing berkontribusi pada kisaran **9,6%–9,8%** terhadap total revenue nasional, sementara cabang dengan kontribusi terendah (Jakarta Timur) tetap menyumbang **5,6%**.

| Rank | Branch | Kontribusi |
|---|---|---|
| 1 | Sukabumi | 9,8% |
| 2 | Bekasi | 9,8% |
| 3 | Jakarta Selatan | 9,7% |
| 4 | Bandung | 9,6% |
| ... | ... | ... |
| 12 | Jakarta Timur | 5,6% |

### Finding 2 — NMAX dan Aerox Menjadi Tulang Punggung Revenue
Dua tipe produk (**NMAX**: 27,9%, **Aerox**: 19,2%) bersama-sama menyumbang **47,1% dari total revenue** — hampir separuh omzet mingguan bertumpu pada dua tipe produk saja. NMAX juga menunjukkan proporsi revenue (27,9%) yang lebih tinggi dibanding proporsi unit terjualnya (22,7%), mengindikasikan kontribusi harga jual yang tinggi per unit.

### Finding 3 — Seluruh Cabang Mencapai Target Mingguan
Seluruh 12 cabang mencatatkan pencapaian **di atas 100%** target mingguan, dengan rentang **139% (Serang, terendah)** hingga **355% (Bekasi, tertinggi)**, dan rata-rata pencapaian keseluruhan **233,89%**.

### Finding 4 — Konsistensi Closing Lebih Berpengaruh daripada Nilai Transaksi Individual
**Lukman Hakim** menjadi sales rep dengan revenue tertinggi (668,5 juta), didorong oleh jumlah transaksi (closing) tertinggi (27 transaksi) — bukan oleh nilai rata-rata transaksi yang paling besar. Sebaliknya, **Rudi Hartono** mencatat jumlah transaksi paling sedikit (9 transaksi) di antara seluruh sales rep aktif.

---

## Business Impact Analysis

### Distribusi Kontribusi Cabang yang Merata
Menunjukkan bahwa performa bisnis tidak bergantung pada satu atau dua cabang saja, sehingga risiko operasional/bisnis lebih terdistribusi dan tidak rentan terhadap gangguan pada satu titik (cabang) tertentu.

### Konsentrasi Revenue pada NMAX & Aerox
Menjadi peluang sekaligus risiko — di satu sisi kedua produk ini layak menjadi prioritas stok dan promosi karena terbukti menjadi penggerak utama revenue; di sisi lain, ketergantungan yang tinggi pada dua produk berisiko menurunkan revenue signifikan apabila terjadi gangguan pasokan atau penurunan minat pasar terhadap keduanya.

### Pencapaian Target di Atas 100% pada Seluruh Cabang
Merupakan hasil positif yang layak diapresiasi, namun rentang pencapaian yang sangat tinggi (139%–355%) secara konsisten di seluruh cabang juga mengindikasikan kemungkinan **target yang ditetapkan berada di bawah kapasitas riil cabang**, sehingga target tersebut kurang optimal sebagai alat ukur performa maupun alat perencanaan sumber daya (stok, staf, dll).

### Pola Performa Sales Rep
Sales rep dengan tingkat closing tinggi (frekuensi transaksi) memberikan kontribusi revenue yang lebih signifikan dan konsisten dibanding yang mengandalkan nilai transaksi besar namun jarang. Hal ini membuka peluang replikasi teknik closing dari top performer ke sales rep dengan jumlah transaksi rendah.

---

## Recommendations

### Recommendation 1 — Pertahankan Strategi Distribusi Cabang
Distribusi kontribusi revenue yang merata sudah menjadi kondisi yang sehat; disarankan untuk mempertahankan strategi operasional saat ini di seluruh cabang tanpa perlu realokasi sumber daya besar antar-cabang.

### Recommendation 2 — Prioritaskan Stok & Promosi pada NMAX dan Aerox, Namun Jaga Diversifikasi
Alokasikan stok dan anggaran promosi lebih besar pada dua produk unggulan ini, sembari tetap menjaga ketersediaan produk lain untuk mengurangi risiko ketergantungan berlebihan pada dua tipe produk saja.

### Recommendation 3 — Apresiasi Pencapaian, Sekaligus Review Metodologi Penetapan Target
Berikan apresiasi kepada seluruh cabang atas pencapaian di atas 100% target. Secara bersamaan, direkomendasikan untuk melakukan **evaluasi terhadap metodologi penetapan target mingguan** — mengingat pencapaian yang secara konsisten sangat tinggi di seluruh cabang (rata-rata 233,89%) berpotensi menandakan target belum mencerminkan kapasitas penjualan riil, yang dapat berdampak pada akurasi perencanaan bisnis (stok, staf, target insentif) ke depannya.

### Recommendation 4 — Replikasi Teknik Closing dari Top Performer
Lakukan sesi berbagi praktik (best practice sharing) dari sales rep dengan tingkat closing tertinggi (Lukman Hakim) kepada sales rep dengan jumlah transaksi rendah (seperti Rudi Hartono), guna meningkatkan konsistensi closing di seluruh tim.

### Recommendation 5 — Tindak Lanjuti Data "Unknown" pada Sales Rep
12 transaksi (3,4% dari total data) tercatat tanpa nama sales rep yang jelas (Unknown). Disarankan menelusuri sumber data entry ini agar evaluasi performa sales rep ke depan lebih akurat dan lengkap.

---

## Expected Business Impact
- Distribusi revenue antar cabang tetap terjaga sehat dan tidak timpang
- Peningkatan efisiensi alokasi stok & promosi pada produk dengan kontribusi tertinggi
- Akurasi target mingguan yang lebih baik untuk mendukung perencanaan bisnis
- Peningkatan konsistensi closing di seluruh tim sales melalui replikasi best practice
- Kualitas data entry (khususnya kelengkapan Sales Rep) meningkat untuk mendukung evaluasi performa yang lebih akurat

## Output
Daftar insight bisnis dan rekomendasi (Key Findings, Business Impact Analysis, Recommendations) yang siap dipresentasikan kepada manajemen dan direktur pada tahap Executive Reporting (Step 11).

## Kesimpulan
Analisis menunjukkan performa penjualan mingguan yang solid dan merata di seluruh cabang, dengan NMAX dan Aerox sebagai penggerak utama revenue. Pencapaian target yang secara konsisten sangat tinggi di seluruh cabang merupakan prestasi yang layak diapresiasi, namun sekaligus menjadi sinyal penting bagi manajemen untuk meninjau kembali metodologi penetapan target agar lebih mencerminkan kapasitas penjualan riil di periode berikutnya.

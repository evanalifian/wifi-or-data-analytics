# WiFi or Data? — Data-Driven Analysis for Smarter Internet Spending

Proyek analisis data untuk menentukan apakah berlangganan Wi-Fi atau tetap menggunakan paket internet seluler lebih menguntungkan berdasarkan biaya, pola penggunaan, dan kebutuhan pengguna.

**Metode:** analisis deskriptif, analisis biaya, dan break-even analysis.

**Output:** notebook Python, visualisasi perbandingan biaya, serta rekomendasi berbasis data.

## Problem definition

**Tujuan proyek:**
Menganalisis perbandingan biaya penggunaan paket internet seluler dan Wi-Fi berdasarkan pengeluaran, kebutuhan penggunaan, jumlah pengguna, serta periode berlangganan.

**Pertanyaan analisis:**
1. Berapa rata-rata pengeluaran internet seluler per bulan?
2. Pada kondisi apa Wi-Fi menjadi lebih hemat?
3. Bagaimana jumlah pengguna memengaruhi biaya internet per orang?
4. Berapa lama waktu yang dibutuhkan agar biaya awal Wi-Fi terbayar melalui penghematan?
5. Faktor apa yang dapat mengubah rekomendasi, misalnya kebutuhan mobilitas atau kualitas koneksi?
Pertanyaan-pertanyaan ini akan menjadi panduan untuk seluruh proses analisis.

## Ekspektasi Output

1. Dataset pengeluaran internet pribadi atau hasil survei teman-teman.
2. Notebook Python berisi proses pembersihan data, analisis, dan visualisasi.
3. Dashboard yang menampilkan perbandingan biaya dan titik impas.
4. Rekomendasi berdasarkan beberapa skenario, misalnya tinggal sendiri, berbagi dengan tiga orang, atau sering berpindah tempat.
5. Opsional: aplikasi web sederhana yang menggabungkan hasil analisis dengan DSS SAW.

## Project Workflow

```bash
01

Problem definition
Menentukan masalah dan pertanyaan analisis.


02

Data collection
Mengumpulkan data pengeluaran, paket, dan pengguna.


03

Data cleaning
Memeriksa data kosong, duplikat, dan konsistensi.


04

Exploratory Data Analysis
Menganalisis pola pengeluaran dan penggunaan.


05

Cost-benefit analysis
Menghitung biaya bulanan, biaya awal, dan titik impas.


06

Visualization
Membuat grafik perbandingan dan skenario biaya.


07

Insights & recommendations
Menentukan kondisi kapan Wi-Fi atau paket seluler lebih sesuai.


08

Documentation & GitHub
Menyusun notebook, README, dan hasil proyek.
```

## Dataset yang Dibutuhkan

```bash
mobile_transactions.csv

Satu baris untuk setiap transaksi paket internet.
Kolom: date, package_name, price, quota_gb, validity_days, extra_cost


wifi_offers.csv

Satu baris untuk setiap penawaran paket Wi-Fi.
Kolom: provider, package_name, monthly_cost, installation_cost, speed_mbps, contract_months


usage_log.csv

Satu baris untuk setiap periode pencatatan penggunaan.
Kolom: date, data_used_gb, usage_hours, activity_type, connection_issue_count


scenario_inputs.csv

Satu baris untuk setiap skenario simulasi.
Kolom: scenario_id, users, months, mobile_cost, wifi_cost, installation_cost, extra_mobile_cost
```

### `mobile_transactions.csv`

File ini menyimpan riwayat pembelian paket internet seluler. Satu baris mewakili satu transaksi pembelian paket, bukan satu bulan.

Nama kolom | Tipe data | Deskripsi | Contoh |
| - | - | - | - |
date | Date | Tanggal pembelian paket internet. | 2026-10-05 |
package_name | String | Nama paket internet yang dibeli. | Paket 100 GB |
price | Integer/Float | Harga dasar paket yang dibayarkan dalam rupiah. | 100000 |
quota_gb | Float | Jumlah kuota internet yang diperoleh dari paket, dalam GB. | 100.0 |
validity_days | Integer | Masa aktif paket dalam hari. | 30 |
extra_cost | Integer/Float | Biaya tambahan yang berkaitan dengan transaksi tersebut, di luar harga dasar paket. | 10000 |

### `wifi_offers.csv`

File ini menyimpan informasi paket Wi-Fi yang tersedia di lokasi tempat tinggalmu. Satu baris mewakili satu penawaran paket dari penyedia tertentu.

Nama kolom | Tipe data | Deskripsi | Contoh |
| - | - | - | - |
provider | String | Nama perusahaan atau penyedia layanan internet. | Provider A |
package_name | String | Nama paket Wi-Fi yang ditawarkan. | Paket Home 30 Mbps |
monthly_cost | Integer/Float | Biaya berlangganan bulanan dalam rupiah. | 250000 |
installation_cost | Integer/Float | Biaya pemasangan awal dalam rupiah. | 150000 |
speed_mbps | Integer/Float | Kecepatan yang tercantum dalam penawaran, dalam Mbps. | 30 |
contract_months | Integer | Lama kontrak minimum dalam bulan. Isi 0 jika tidak ada kontrak minimum. | 12 |

### `usage_log.csv`

File ini menyimpan catatan penggunaan internet sehari-hari. Satu baris mewakili satu periode pencatatan, yang untuk versi awal proyek sebaiknya ditetapkan sebagai satu hari.

Nama kolom | Tipe data | Deskripsi | Contoh |
| - | - | - | - |
date | Date | Tanggal penggunaan internet yang dicatat .| 2026-10-05 |
data_used_gb | Float | Jumlah data internet yang terpakai pada hari tersebut, dalam GB .| 2.5 |
usage_hours | Float | Perkiraan durasi penggunaan internet pada hari tersebut, dalam jam .| 8.0 |
activity_type | String | Aktivitas utama yang menggunakan internet pada hari tersebut .| Kuliah dan coding |
connection_issue_count | Integer | Jumlah gangguan koneksi yang dialami selama periode pencatatan .| 1 |

### `scenario_inputs.csv`

File ini menyimpan parameter untuk melakukan simulasi perbandingan biaya. Satu baris mewakili satu skenario keputusan, misalnya penggunaan internet selama 6 bulan oleh dua orang.

Nama kolom | Tipe data | Deskripsi | Contoh |
| - | - | - | - |
scenario_id | String | Identitas unik untuk setiap skenario simulasi .| S001 |
users | Integer | Jumlah orang yang berbagi biaya Wi-Fi .| 3 |
months | Integer | Periode perbandingan biaya dalam bulan .| 12 |
mobile_cost | Integer/Float | Biaya internet seluler per orang per bulan yang digunakan sebagai asumsi simulasi .| 100000 |
wifi_cost | Integer/Float | Total biaya langganan Wi-Fi per bulan untuk satu koneksi rumah .| 250000 |
installation_cost | Integer/Float | Total biaya pemasangan awal Wi-Fi untuk satu koneksi .| 150000 |
extra_mobile_cost | Integer/Float | Biaya seluler tambahan per orang per bulan jika masih dibutuhkan setelah berlangganan Wi-Fi .| 20000 |
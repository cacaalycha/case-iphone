# PRD: Aplikasi Manajemen Keuangan Toko Case iPhone
**Versi:** 1.0  
**Tanggal:** 30 Juni 2026  
**Tipe:** Aplikasi Web Progressive (PWA) Mobile-First

---

## 1. Executive Summary
Aplikasi web manajemen keuangan sederhana untuk **toko case iPhone skala kecil** yang membutuhkan pencatatan pemasukan, pengeluaran, dan kasbon tanpa kompleksitas. Aplikasi dioptimalkan untuk **hp mid-low** dan **koneksi internet lambat** dengan nuansa mobile app native.

## 2. Target Pengguna & Konteks
- **Profil:** Pemilik/karyawan toko case iPhone Warung/Toko kecil (1-3 orang)
- **Perangkat:** Smartphone Android mid-low (RAM 2-4GB, storage terbatas)
- **Koneksi:** 3G/4G lambat atau sinyal tidak stabil; wifi tidak selalu tersedia
- **Literasi Teknologi:** Menengah ke bawah; tidak familiar dengan software akuntansi kompleks
- **Waktu Penggunaan:** Singkat (1-3 menit per transaksi), sering dibuka/tutup

## 3. Masalah yang Diselesaikan
1. Pencatatan keuangan masih manual (kertas/notes) sehingga rawan hilang dan sulit di recap
2. Tidak ada real-time tracking kas vs utang (kasbon)
3. Sulit menentukan apakah untung/rugi karena piutang dan kas tercampur
4. Minim struktur data; hanya ada catatan bebas tanpa summary

## 4. Goals & Objectives
- **Primary:** Pencatatan transaksi (pemasukan, pengeluaran, kasbon) dalam <30 detik
- **Secondary:** Ringkasan harian/mingguan yang mudah dibaca; export summary CSV
- **Constraint:** Tidak ada login/signup kompleks; siap pakai tanpa setup berjam-jam

## 5. Scope MVP (Fitur Minimum)
### 5.1 Fitur Inti
| Modul | Fitur | Prioritas |
|-------|-------|-----------|
| **Pemasukan** | Input cepat (nominal, sumber: penjualan case/konsumen), catatan opsional | P0 |
| **Pengeluaran** | Input cepat (nominal, kategori: modal, operasional, lainnya), catatan opsional | P0 |
| **Kasbon** | Tambah kasbon (nama, nominal, tanggal), update status lunas/belum | P0 |
| **Dashboard** | Ringkasan hari ini: pemasukan, pengeluaran, saldo kas, piutang | P0 |
| **History** | Daftar transaksi terbaru, filter by tipe/tanggal | P1 |

### 5.2 Fitur Out of Scope (Post-MVP)
- Multi pengguna/role
- Inventaris stok case
- Laporan laba rugi bulanan kompleks
- Notifikasi/reminder
- Backup cloud/Google Drive
- Pembayaran digital integration

## 6. Batasan Teknis
### 6.1 Performance
- First Load harus <2 detik pada 3G
- Ukuran total bundle: <200KB (gzip)
- Offline-first: dapat input transaksi tanpa internet, sync saat online
- No heavy framework (hindari React/Vue/Angular untuk versi awal)

### 6.2 Device
- Responsif: disain mobile-first (320px+), sesekali tampil baik di tablet sekalipun
- Hindari hover interaction; gunakan tap friendly (min 44x44px)
- Font: system-ui / sans-serif, ukuran minimal 14px body, 16px untuk input
- Warna kontras tinggi untukOutside visibility (toko sering terang)

### 6.3 Storage & Data
- LocalStorage/IndexedDB untuk data offline
- Sinkronisasi manual atau background fetch
- Export CSV untuk backup/audit

## 7. UI/UX Principles
1. **One-hand operation:** Tombol utama di bawah layar (thumb-friendly)
2. **Less is more:** Hanya tampilkan angka penting; detail disembunyikan
3. **Big buttons:** Minimal 48x48px untuk CTA
4. **Minimal text:** Label singkat, placeholder jelas
5. **Color coded:** Hijau untuk pemasukan, merah pengeluaran, kuning kasbon
6. **No ads, no login friction:** Langsung buka pakai

### 7.1 Informasi Arquitecture
```
Header: [Nama Toko] + [Tanggal Hari Ini]
─────────────────────────────────────────
Ringkasan Cepat (Cards):
  💰 Pemasukan Hari Ini     Rp 0
  💸 Pengeluaran Hari Ini   Rp 0
  🏦 Saldo Kas             Rp 0
  ⚠️  Kasbon Belum Lunas   Rp 0
─────────────────────────────────────────
Tombol Aksi Floating:
  [+ Pemasukan]  [+ Pengeluaran]  [+ Kasbon]
─────────────────────────────────────────
Tab/List History:
  [Semua] [Pemasukan] [Pengeluaran] [Kasbon]
  - 10 transaksi terbaru
─────────────────────────────────────────
Footer: [Dashboard] [History] [Export] [Info]
```

## 8. Struktur Data (JSON Schema)
```json
// Transaksi
{
  "id": "uuid",
  "type": "income|expense|debt",
  "amount": 50000,
  "category": "penjualan|modal|operasional|lainnya|kasbon_masuk|kasbon_keluar",
  "note": "jualan case clear",
  "date": "2026-06-30",
  "createdAt": "2026-06-30T11:00:00Z",
  "synced": false
}

// Kasbon (opsional bisa merge dengan transaksi type kasbon)
{
  "id": "uuid",
  "customerName": "Budi",
  "amount": 100000,
  "isPaid": false,
  "paidAt": null,
  "note": "bayar besok",
  "date": "2026-06-30",
  "createdAt": "2026-06-30T11:00:00Z"
}
```

## 9. Tech Stack Recommendation
| Layer | Pilihan | Alasan |
|-------|---------|--------|
| **Frontend** | HTML + Vanilla JS + Tailwind (CDN) | Ringan, no build step, familiar |
| **Storage** | IndexedDB via Dexie.js | Offline-first, queryable |
| **Export** | SheetJS (xlsx) atau CSV custom | Dependency kecil |
| **Deploy** | Static hosting (Vercel/Netlify/GitHub Pages) | Gratis/maintenance mudah |
| **Optional PWA** | Workbox (CDN) untuk cache | Installable seperti apk |

### Alternatif Ringan (jika ingin framework):
- **Preact +htm** (3KB) atau **Alpine.js** (10KB) untuk interaksi
- **TinyBase** untuk state management
- **Lucide icons** via CDN

## 10. Metriks Sukses
- 90% user dapat input transaksi pertama dalam 1 menit
- Use time rata-rata <2 menit per sesi
- Crash rate <1% pada hp target
- Offline coverage: 100% fitur inti bekerja tanpa internet
- Adoption: toko menggunakan >3 hari dalam seminggu pertama

## 11. Roadmap Pengembangan
| Fase | Durasi | Deliverable |
|------|--------|-------------|
| **Phase 0: Validasi** | 1 minggu | Wireframe Figma + user test dengan 2 toko |
| **Phase 1: MVP** | 3 minggu | Input 3 tipe, dashboard, history, export CSV |
| **Phase 2: Polish** | 2 minggu | PWA install, haptic feedback, dark/light mode |
| **Phase 3: Launch** | 1 minggu | Deploy static + dokumentasi 1 halaman |
| **Phase 4: Iterasi** | Berkelanjutan | Tambah kategori custom, backup QR code |

## 12. Risiko & Mitigasi
| Risiko | Dampak | Mitigasi |
|--------|--------|----------|
| Pengguna lupa backup data | High | Export CSV otomatis mingguan + fitur share |
| Browser compatibility | Medium | Target Chrome Mobile/Safari terbaru saja |
| Input salah tipe transaksi | Medium | Konfirmasi sebelum simpan; undo tombol |
| Data corrupt karena storage penuh | Low | Quota check + error message yang jelas |

## 13. Catatan Tambahan
- **Nama aplikasi:** Sementara "CatatKas" atau "CaseBook"
- **Bahasa:** Indonesia sepenuhnya
- **Karakteristik toko case iPhone:** Sering jual tambahan screen protector, charger; kategori defaults bisa disesuaikan
- **Kasbon:** Karena toko kecil, kasbon biasanya ke konsumen yang baru beli namun belum bayar; perlu kolom nama/ket untuk identifikasi

---

## Lampiran: Contoh User Flow
1. Buka aplikasi → langsung ke dashboard
2. Ketuk "+ Pengeluaran" → pilih kategori "Beli case stok" → input 250000 → simpan
3. Ketuk "+ Pemasukan" → pilih "Penjualan" → input 50000 → simpan
4. Dashboard update otomatis: Saldo turun menjadi -200000 (jika modal awal 0)
5. Ketuk tab "Kasbon" → "+ Tambah Kasbon" → nama "Andi", nominal 150000
6. Ketuk "History" → filter "Kasbon" → ketuk Andi → tandai "Lunas"
7. Ketuk "Export" → kirim CSV via WhatsApp untuk backup ke owner

---

*Dokumen ini dapat berkembang seiring feedback aktual dari pemilik toko.*

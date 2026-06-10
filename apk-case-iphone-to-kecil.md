# Perencanaan Aplikasi Kas - Toko Case iPhone Skala Kecil

## Target Pengguna
- Pemilik toko case iPhone skala kecil
- Pengguna HP mid-low end
- Internet dengan kecepatan rendah

## Kebutuhan Utama
1. **Pemasukan** - pencatatan penjualan case
2. **Pengeluaran** - pencatatan biaya operasional/toko
3. **Kasbon** - pencatatan pinjaman dengan pelunasan

## Teknologi Stack
- **Frontend**: React Native (cross-platform, performa baik di mid-low end)
- **UI Library**: React Native Paper (ringan, mudah dikustomisasi)
- **State Management**: Zustand (ringan, minimal bundle size)
- **Database**: SQLite (lokal, tidak perlu internet untuk operasi dasar)
- **Offline Support**: Redux Persist + WatermelonDB untuk sync data

## Fitur & Struktur

### Modul Utama
| Modul | Fitur |
|-------|-------|
| Dashboard | Ringkasan saldo harian, grafik sederhana (batang) |
| Pemasukan | Tambah/edit/hapus, kategori penjualan, tanggal, jumlah |
| Pengeluaran | Tambah/edit/hapus, kategori (gaji, sewa, stok, dll), tanggal, jumlah |
| Kasbon | Tambah pinjaman, catat pelunasan, status (lunas/belum) |
| Laporan | Filter per tanggal, export PDF (opsional) |

### Kategori Default
- **Pemasukan**: Penjualan case, lainnya
- **Pengeluaran**: Stok baru, sewa, listrik, internet, gaji, lainnya

## Optimisasi Mobile-Friendly
- Bundle size kecil (< 20MB)
- Minimal library eksternal
- UI sederhana dengan komponen native
- Loading skeleton untuk operasi async
- Cache gambar lokal jika diperlukan

## Optimisasi Internet Rendah
- Semua operasi data lokal (SQLite)
- Sync data opsional ke cloud (jika ada internet)
- Gambar/icon SVG bukan PNG berat
- Lazy loading komponen

## Database Schema
```sql
-- pemasukan
CREATE TABLE income (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  amount REAL NOT NULL,
  category TEXT NOT NULL,
  description TEXT,
  date TEXT NOT NULL,
  created_at TEXT DEFAULT CURRENT_TIMESTAMP
);

-- pengeluaran  
CREATE TABLE expense (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  amount REAL NOT NULL,
  category TEXT NOT NULL,
  description TEXT,
  date TEXT NOT NULL,
  created_at TEXT DEFAULT CURRENT_TIMESTAMP
);

-- kasbon
CREATE TABLE kasbon (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  amount REAL NOT NULL,
  person_name TEXT NOT NULL,
  status TEXT CHECK(status IN ('active', 'paid')) DEFAULT 'active',
  borrow_date TEXT NOT NULL,
  paid_date TEXT,
  created_at TEXT DEFAULT CURRENT_TIMESTAMP
);
```

## UI/UX Sederhana
- Tab navigation (3 tab utama)
- Floating action button untuk tambah data
- Form input maksimal 4-5 field
- List dengan swipe to delete/edit
- Tidak ada animasi berat

## Rencana Implementasi
1. Setup project React Native
2. Setup SQLite lokal
3. Buat modul kasbon (paling kompleks)
4. Buat modul pemasukan & pengeluaran
5. Buat dashboard summary
6. Testing di device low-end
7. Build APK
# Product Requirements Document (PRD)

## Aplikasi Penjualan Case iPhone Berbasis Web

---

## 1. Ikhtisar Produk

| Item | Keterangan |
|------|------------|
| **Nama Proyek** | CaseVerse - Toko Case iPhone Online |
| **Versi Dokumen** | 1.0 |
| **Tanggal** | 14 Juli 2026 |
| **Status** | Perencanaan |

**Ringkasan Singkat:**
CaseVerse adalah aplikasi web e-commerce yang menjual berbagai macam case/cover untuk seri iPhone. Aplikasi ini dirancang mobile-first dengan antarmuka aesthetic cute bernuansa putih dan burgundy, ditargetkan untuk pengguna usia 15-30 tahun yang mengaksesnya melalui smartphone kelas menengah-bawah.

---

## 2. Analisis Pengguna

### 2.1 Target Pengguna

| Aspek | Detail |
|-------|--------|
| **Usia** | 15-30 tahun |
| **Profil** | Anak remaja hingga dewasa muda pengguna iPhone |
| **Device** | Smartphone mid-low end (RAM 2-4 GB, storage terbatas) |
| **Koneksi** | Tidak selalu stabil (4G/3G/WiFi publik) |
| **Literasi Digital** | Terbiasa belanja online, aktif di media sosial |

### 2.2 User Persona

**Persona 1 - Rina (17 tahun, pelajar)**
- Ingin case iPhone yang aesthetic dengan harga terjangkau
- Sering browsing lewat HP saat istirahat sekolah
- Koneksi internet tidak selalu bagus

**Persona 2 - Dimas (24 tahun, pekerja muda)**
- Mencari case dengan proteksi bagus untuk iPhone 15 Pro
- Ingin proses checkout yang cepat dan mudah
- Sering beli online menggunakan GoPay/OVO

**Persona 3 - Admin Toko (25 tahun)**
- Mengelola stok produk, kategori, dan pesanan
- Butuh dashboard yang simpel untuk update produk harian

---

## 3. Kebutuhan Fungsional

### 3.1 Fitur Pengguna (Customer)

| No | Modul | Fitur | Deskripsi |
|----|-------|-------|-----------|
| 1 | **Katalog Produk** | Halaman utama katalog | Menampilkan daftar case iPhone dalam grid/list card dengan gambar, nama, harga, dan badge diskon (jika ada) |
| 2 | | Infinite scroll / pagination | Memuat produk secara bertahap agar tidak membebani RAM device rendah |
| 3 | **Pencarian** | Search bar | Pencarian produk berdasarkan nama/keyword dengan debouncing 300ms |
| 4 | | Search suggestion | Menampilkan rekomendasi produk saat user mengetik |
| 5 | **Filter & Sort** | Filter seri iPhone | Filter: iPhone 11, 12, 13, 14, 15, 16 series |
| 6 | | Filter kategori | Filter: Silicone, Leather, Clear, Tough, Wallet, dll. |
| 7 | | Filter harga | Rentang harga (slider atau predefined range) |
| 8 | | Urutkan | Harga terendah/tertinggi, terbaru, terlaris |
| 9 | **Detail Produk** | Halaman detail | Gambar produk (zoomable), nama, harga, deskripsi, spesifikasi, stok, rating |
| 10 | | Pilihan varian | Pilih warna/tipe untuk produk yang memiliki varian |
| 11 | | Review pengguna | Menampilkan ulasan dari pembeli sebelumnya |
| 12 | **Keranjang Belanja** | Add to cart | Menambahkan produk ke keranjang dengan pilihan jumlah |
| 13 | | Keranjang | Daftar produk di keranjang, ubah jumlah, hapus item |
| 14 | | Ringkasan harga | Subtotal, estimasi ongkir, total belanja |
| 15 | **Checkout** | Form pengiriman | Alamat pengiriman, kurir, metode pembayaran |
| 16 | | Ringkasan pesanan | Review produk, alamat, total bayar sebelum konfirmasi |
| 17 | | Multi-payment | Transfer bank, e-wallet (GoPay, OVO, Dana, QRIS) |
| 18 | **Konfirmasi Pembayaran** | Upload bukti transfer | User upload screenshot bukti pembayaran |
| 19 | | Status otomatis | Status berubah ke "Diproses" setelah admin verifikasi |
| 20 | **Riwayat Pesanan** | Daftar pesanan | Daftar semua pesanan user beserta status (Diproses, Dikirim, Selesai) |
| 21 | | Detail pesanan | Info lengkap: produk, alamat, kurir, resi, status terkini |
| 22 | **Akun Profil** | Profil user | Edit nama, email, telepon, alamat default |
| 23 | | Login / Register | Email + password, atau via Google OAuth |

### 3.2 Fitur Admin

| No | Modul | Fitur | Deskripsi |
|----|-------|-------|-----------|
| 1 | **Dashboard** | Ringkasan | Total penjualan hari ini, pesanan baru, stok menipis |
| 2 | **Kelola Produk** | CRUD produk | Tambah, edit, hapus produk dengan gambar, deskripsi, harga, stok |
| 3 | | Upload gambar | Drag & drop / pilih file, kompres otomatis |
| 4 | **Kelola Kategori** | CRUD kategori | Tambah, edit, hapus kategori produk |
| 5 | **Kelola Stok** | Update stok | Adjust stok per produk, notifikasi saat stok < ambang batas |
| 6 | **Kelola Pesanan** | Daftar pesanan | Lihat semua pesanan, filter berdasarkan status |
| 7 | | Verifikasi pembayaran | Setujui/tolak bukti pembayaran yang diupload user |
| 8 | | Update status | Ubah status: Diproses > Dikirim > Selesai |
| 9 | | Input resi | Masukkan nomor resi pengiriman |
| 10 | **Kelola User** | Daftar user | Lihat data pengguna terdaftar |

---

## 4. Kebutuhan Non-Fungsional

### 4.1 Performa

| Metrik | Target |
|--------|--------|
| **First Contentful Paint (FCP)** | < 1.5 detik |
| **Largest Contentful Paint (LCP)** | < 2.5 detik |
| **Time to Interactive (TTI)** | < 3.0 detik |
| **Total bundle size (gzipped)** | < 200 KB (initial load) |
| **Ukuran gambar per produk** | Max 200 KB (setelah kompres) |

### 4.2 Mobile & Responsif

| Kebutuhan | Detail |
|-----------|--------|
| **Mobile-first design** | Dirancang untuk layar 320px-428px terlebih dahulu |
| **Breakpoint** | Mobile: 320-767px, Tablet: 768-1023px, Desktop: 1024px+ |
| **Touch-friendly** | Tombol minimal 44x44px, area tap yang cukup |
| **Lazy loading** | Gambar dimuat saat masuk viewport |
| **Offline handling** | Tampilkan pesan yang jelas jika koneksi hilang |

### 4.3 Keamanan

| Kebutuhan | Detail |
|-----------|--------|
| **Autentikasi** | JWT token dengan refresh mechanism |
| **Otorisasi** | Role-based: Customer & Admin |
| **Input validation** | Validasi client-side & server-side |
| **Password** | Hashing dengan bcrypt |
| **File upload** | Validasi tipe file & ukuran maksimal |

### 4.4 Kompatibilitas Browser

| Browser | Versi Minimum |
|---------|---------------|
| Chrome (Android) | 90+ |
| Safari (iOS) | 14+ |
| Samsung Internet | 14+ |
| Chrome (Desktop) | 90+ |
| Firefox (Desktop) | 88+ |

---

## 5. Arsitektur & Tech Stack

### 5.1 Pilihan Teknologi

| Layer | Teknologi | Alasan |
|-------|-----------|--------|
| **Frontend** | React.js (Vite) | Cepat, modern, ekosistem besar, hot reload |
| **UI Framework** | Tailwind CSS | Utility-first, ringan, mudah customize tema |
| **State Management** | Zustand atau React Context | Ringan, cocok untuk skala menengah |
| **Backend** | Node.js + Express.js | JavaScript fullstack, cepat untuk REST API |
| **Database** | MySQL (via Sequelize/Knex) | Relational, cocok untuk data produk & pesanan |
| **Authentication** | JWT + bcrypt | Standard, aman, mudah diimplementasi |
| **File Storage** | Local / Cloudinary (free tier) | Untuk penyimpanan gambar produk |
| **Deployment** | Vercel (FE) + Render/Railway (BE) | Free tier, mudah deploy |

### 5.2 Struktur Folder (Backend)

```
server/
  config/
    database.js
  controllers/
    authController.js
    productController.js
    categoryController.js
    cartController.js
    orderController.js
    paymentController.js
    adminController.js
  middleware/
    auth.js
    role.js
    upload.js
    validation.js
  models/
    User.js
    Product.js
    Category.js
    Cart.js
    Order.js
    OrderItem.js
    Payment.js
  routes/
    authRoutes.js
    productRoutes.js
    categoryRoutes.js
    cartRoutes.js
    orderRoutes.js
    paymentRoutes.js
    adminRoutes.js
  utils/
    helpers.js
    uploadConfig.js
  app.js
  server.js
```

### 5.3 Struktur Folder (Frontend)

```
src/
  assets/
  components/
    common/
      Navbar.jsx
      Footer.jsx
      ProductCard.jsx
      SearchBar.jsx
      FilterSidebar.jsx
      Loading.jsx
      EmptyState.jsx
    cart/
      CartItem.jsx
      CartSummary.jsx
    checkout/
      ShippingForm.jsx
      PaymentMethod.jsx
      OrderSummary.jsx
  pages/
    Home.jsx
    ProductList.jsx
    ProductDetail.jsx
    Cart.jsx
    Checkout.jsx
    PaymentConfirmation.jsx
    OrderHistory.jsx
    OrderDetail.jsx
    Login.jsx
    Register.jsx
    Profile.jsx
  admin/
    Dashboard.jsx
    Products.jsx
    ProductForm.jsx
    Categories.jsx
    Orders.jsx
    Users.jsx
  hooks/
    useAuth.js
    useCart.js
    useDebounce.js
  services/
    api.js
  store/
    useStore.js
  styles/
    theme.js
  App.jsx
  main.jsx
```

---

## 6. Desain UI/UX

### 6.1 Tema Warna

| Elemen | Warna | Kode |
|--------|-------|------|
| **Primary (Burgundy)** | Burgundy | #800020 |
| **Primary Light** | Light Burgundy | #A0325C |
| **Primary Dark** | Dark Burgundy | #5C0017 |
| **Background** | Putih | #FFFFFF |
| **Surface** | Off-White | #FFF8F8 |
| **Text Primary** | Dark Gray | #2D2D2D |
| **Text Secondary** | Gray | #6B6B6B |
| **Accent** | Soft Pink | #F5D5D5 |
| **Success** | Mint Green | #4CAF50 |
| **Warning** | Amber | #FFC107 |
| **Error** | Red | #E53935 |

### 6.2 Tipografi

| Elemen | Font | Size |
|--------|------|------|
| **Heading 1** | Inter / Poppins Bold | 24-28px |
| **Heading 2** | Inter / Poppins SemiBold | 20-24px |
| **Heading 3** | Inter / Poppins Medium | 16-18px |
| **Body** | Inter / Poppins Regular | 14-16px |
| **Caption** | Inter / Poppins Regular | 12-13px |

### 6.3 Elemen UI Kunci

- **Rounded corners** pada semua card dan tombol (border-radius: 12px)
- **Shadow halus** untuk kedalaman (box-shadow ringan)
- **Ikon konsisten** menggunakan Lucide Icons atau Heroicons
- **Animasi minimal** - hover effect, loading skeleton, transisi halaman ringan
- **Whitespace cukup** - tidak terlalu padat, nyaman dibaca
- **Gambar produk** dengan aspect ratio 1:1, border-radius ringan

### 6.4 Wireframe Halaman Utama

```
+-----------------------------+
|  Home    Search   Cart User |  <- Navbar fixed
+-----------------------------+
|                             |
|   Case iPhone Trending      |  <- Hero banner (opsional)
|   Diskon hingga 30%!        |
|   [Belanja Sekarang]        |
|                             |
+-----------------------------+
|  Search: Cari case iPhone...|  <- Search bar
+-----------------------------+
|  Filter: [All] [Seri]      |  <- Filter chips
|  [Harga] [Sort: Terbaru]   |
+-----------------------------+
|  +-----+ +-----+ +-----+  |
|  |     | |     | |     |  |
|  |Case1| |Case2| |Case3|  |  <- Product grid
|  |Rp89k| |Rp69k| |Rp99k|  |     (2 kolom mobile)
|  |*4.8 | |*4.5 | |*4.9 |  |
|  +-----+ +-----+ +-----+  |
|  +-----+ +-----+ +-----+  |
|  |Case4| |Case5| |Case6|  |
|  +-----+ +-----+ +-----+  |
|                             |
|  < 1  2  3  4  5 >         |  <- Pagination
+-----------------------------+
|  Home  Search  Cart  Profile|  <- Bottom nav (mobile)
+-----------------------------+
```

---

## 7. Database Schema (ERD)

### 7.1 Struktur Tabel

#### users
| Kolom | Tipe | Keterangan |
|-------|------|------------|
| id | INT, PK, AI | ID unik user |
| name | VARCHAR(100) | Nama lengkap |
| email | VARCHAR(100), UNIQUE | Email untuk login |
| password | VARCHAR(255) | Hashed password |
| phone | VARCHAR(20) | Nomor telepon |
| address | TEXT | Alamat default |
| role | ENUM('customer', 'admin') | Role user |
| avatar | VARCHAR(255) | URL foto profil |
| created_at | TIMESTAMP | Waktu pembuatan |
| updated_at | TIMESTAMP | Waktu update terakhir |

#### categories
| Kolom | Tipe | Keterangan |
|-------|------|------------|
| id | INT, PK, AI | ID unik kategori |
| name | VARCHAR(100) | Nama kategori |
| description | TEXT | Deskripsi kategori |
| slug | VARCHAR(100), UNIQUE | Slug URL |
| created_at | TIMESTAMP | Waktu pembuatan |
| updated_at | TIMESTAMP | Waktu update terakhir |

#### products
| Kolom | Tipe | Keterangan |
|-------|------|------------|
| id | INT, PK, AI | ID unik produk |
| name | VARCHAR(200) | Nama produk |
| slug | VARCHAR(200), UNIQUE | Slug URL |
| description | TEXT | Deskripsi detail |
| price | DECIMAL(10,2) | Harga normal |
| discount_price | DECIMAL(10,2), NULL | Harga diskon |
| image_url | VARCHAR(500) | URL gambar utama |
| iphone_series | VARCHAR(50) | Seri iPhone (iPhone 15, dll) |
| stock | INT | Jumlah stok tersedia |
| category_id | INT, FK -> categories | Relasi ke kategori |
| is_active | BOOLEAN | Status aktif/tidak |
| rating | DECIMAL(2,1) | Rating rata-rata |
| sold_count | INT | Jumlah terjual |
| created_at | TIMESTAMP | Waktu pembuatan |
| updated_at | TIMESTAMP | Waktu update terakhir |

#### carts
| Kolom | Tipe | Keterangan |
|-------|------|------------|
| id | INT, PK, AI | ID unik cart item |
| user_id | INT, FK -> users | Relasi ke user |
| product_id | INT, FK -> products | Relasi ke produk |
| quantity | INT | Jumlah item |
| created_at | TIMESTAMP | Waktu pembuatan |
| updated_at | TIMESTAMP | Waktu update terakhir |

#### reviews
| Kolom | Tipe | Keterangan |
|-------|------|------------|
| id | INT, PK, AI | ID unik review |
| user_id | INT, FK -> users | Relasi ke user |
| product_id | INT, FK -> products | Relasi ke produk |
| rating | INT (1-5) | Rating bintang |
| comment | TEXT | Ulasan tulisan |
| created_at | TIMESTAMP | Waktu pembuatan |

#### orders
| Kolom | Tipe | Keterangan |
|-------|------|------------|
| id | INT, PK, AI | ID unik pesanan |
| user_id | INT, FK -> users | Relasi ke user |
| total_price | DECIMAL(12,2) | Total harga pesanan |
| shipping_address | TEXT | Alamat pengiriman |
| courier | VARCHAR(50) | Kurir (JNE, J&T, dll) |
| tracking_number | VARCHAR(100), NULL | Nomor resi |
| status | ENUM('pending','paid','processing','shipped','delivered','cancelled') | Status pesanan |
| notes | TEXT, NULL | Catatan pesanan |
| created_at | TIMESTAMP | Waktu pembuatan |
| updated_at | TIMESTAMP | Waktu update terakhir |

#### order_items
| Kolom | Tipe | Keterangan |
|-------|------|------------|
| id | INT, PK, AI | ID unik order item |
| order_id | INT, FK -> orders | Relasi ke pesanan |
| product_id | INT, FK -> products | Relasi ke produk |
| product_name | VARCHAR(200) | Nama produk (snapshot) |
| product_price | DECIMAL(10,2) | Harga saat dibeli (snapshot) |
| quantity | INT | Jumlah item |
| subtotal | DECIMAL(12,2) | Subtotal item |

#### payments
| Kolom | Tipe | Keterangan |
|-------|------|------------|
| id | INT, PK, AI | ID unik pembayaran |
| order_id | INT, FK -> orders, UNIQUE | Relasi ke pesanan |
| method | VARCHAR(50) | Metode pembayaran |
| amount | DECIMAL(12,2) | Jumlah bayar |
| proof_image_url | VARCHAR(500), NULL | URL bukti transfer |
| status | ENUM('pending','verified','rejected') | Status verifikasi |
| verified_by | INT, FK -> users, NULL | Admin yang verifikasi |
| verified_at | TIMESTAMP, NULL | Waktu verifikasi |
| created_at | TIMESTAMP | Waktu pembuatan |

### 7.2 Relasi

```
users 1:N orders
users 1:N carts
users 1:N reviews
users 1:N payments (verified_by)

categories 1:N products

products 1:N carts
products 1:N reviews
products 1:N order_items

orders 1:N order_items
orders 1:1 payments
```

---

## 8. API Endpoints

### 8.1 Autentikasi

| Method | Endpoint | Deskripsi | Auth |
|--------|----------|-----------|------|
| POST | /api/auth/register | Register user baru | No |
| POST | /api/auth/login | Login user | No |
| GET | /api/auth/me | Get data user saat ini | Yes |
| PUT | /api/auth/profile | Update profil | Yes |

### 8.2 Produk (Public)

| Method | Endpoint | Deskripsi | Auth |
|--------|----------|-----------|------|
| GET | /api/products | Get semua produk (paginated, filterable) | No |
| GET | /api/products/:slug | Get detail produk | No |
| GET | /api/products/:id/reviews | Get review produk | No |
| GET | /api/categories | Get semua kategori | No |
| GET | /api/search?q=... | Pencarian produk | No |

**Query Parameters untuk /api/products:**

```
?page=1&limit=12&category=silicone&series=iphone-15&sort=price-asc&minPrice=50000&maxPrice=200000
```

### 8.3 Keranjang Belanja

| Method | Endpoint | Deskripsi | Auth |
|--------|----------|-----------|------|
| GET | /api/cart | Get isi keranjang | Yes |
| POST | /api/cart | Tambah ke keranjang | Yes |
| PUT | /api/cart/:id | Update jumlah item | Yes |
| DELETE | /api/cart/:id | Hapus item dari keranjang | Yes |

### 8.4 Pesanan

| Method | Endpoint | Deskripsi | Auth |
|--------|----------|-----------|------|
| POST | /api/orders | Buat pesanan baru (checkout) | Yes |
| GET | /api/orders | Get riwayat pesanan user | Yes |
| GET | /api/orders/:id | Get detail pesanan | Yes |
| POST | /api/orders/:id/pay | Upload bukti pembayaran | Yes |

### 8.5 Admin

| Method | Endpoint | Deskripsi | Auth |
|--------|----------|-----------|------|
| GET | /api/admin/dashboard | Statistik dashboard | Admin |
| GET | /api/admin/products | Kelola produk | Admin |
| POST | /api/admin/products | Tambah produk | Admin |
| PUT | /api/admin/products/:id | Edit produk | Admin |
| DELETE | /api/admin/products/:id | Hapus produk | Admin |
| GET | /api/admin/categories | Kelola kategori | Admin |
| POST | /api/admin/categories | Tambah kategori | Admin |
| PUT | /api/admin/categories/:id | Edit kategori | Admin |
| DELETE | /api/admin/categories/:id | Hapus kategori | Admin |
| PUT | /api/admin/products/:id/stock | Update stok | Admin |
| GET | /api/admin/orders | Semua pesanan | Admin |
| PUT | /api/admin/orders/:id/status | Update status pesanan | Admin |
| PUT | /api/admin/orders/:id/tracking | Input no resi | Admin |
| PUT | /api/admin/payments/:id/verify | Verifikasi pembayaran | Admin |
| GET | /api/admin/users | Daftar user | Admin |

---

## 9. Alur Pengguna (User Flow)

### 9.1 Alur Belanja

```
Buka Website
    |
    v
Lihat Katalog
    |
    v
Filter / Cari Produk  ------>  Lihat Detail Produk
                                      |
                                      v
                               Pilih Varian & Jumlah
                                      |
                                      v
                               Tambah ke Keranjang
                                      |
                                      v
                               Buka Keranjang --> Review Item
                                      |
                                      v
                               Checkout --> Isi Alamat Pengiriman
                                      |
                                      v
                               Pilih Pengiriman & Metode Bayar
                                      |
                                      v
                               Konfirmasi & Bayar
                                      |
                                      v
                               Upload Bukti Pembayaran
                                      |
                                      v
                               Pesanan Tercatat (Status: Pending)
                                      |
                                      v
                               Admin Verifikasi --> Status: Paid
                                      |
                                      v
                               Admin Proses --> Status: Processing
                                      |
                                      v
                               Admin Kirim (Input Resi) --> Status: Shipped
                                      |
                                      v
                               Sampai --> Status: Delivered
                                      |
                                      v
                               Selesai (User bisa beri review)
```

### 9.2 Alur Admin

```
Login Admin
    |
    v
Dashboard (ringkasan: penjualan, pesanan baru, stok menipis)
    |
    +---> Kelola Produk (CRUD)
    |       + Tambah Produk
    |       + Edit Produk
    |       + Hapus Produk
    |
    +---> Kelola Kategori (CRUD)
    |
    +---> Kelola Stok
    |       + Update jumlah stok
    |       + Lihat produk dengan stok rendah
    |
    +---> Kelola Pesanan
    |       + Lihat daftar pesanan
    |       + Filter berdasarkan status
    |       + Verifikasi Pembayaran (Accept / Reject)
    |       + Update Status Pesanan
    |       + Input Nomor Resi
    |
    +---> Kelola User
            + Lihat daftar pengguna
```

---

## 10. Spesifikasi Detail Halaman

### 10.1 Halaman Beranda

| Elemen | Deskripsi |
|--------|-----------|
| **Hero Section** | Banner promosi (diskon/free ongkir), CTA button |
| **Kategori Populer** | Horizontal scroll chips: iPhone 11, 12, 13, 14, 15, 16 |
| **Produk Terlaris** | Grid/carousel 4-6 produk dengan badge "Terlaris" |
| **Produk Terbaru** | Grid produk terbaru yang baru ditambahkan |
| **Footer** | Info toko, link navigasi, kontak |

### 10.2 Halaman Katalog

| Elemen | Deskripsi |
|--------|-----------|
| **Search bar** | Sticky di atas, debouncing 300ms |
| **Filter chips** | Seri iPhone, kategori, range harga |
| **Sort dropdown** | Terbaru, Harga terendah/tinggi, Terlaris |
| **Product grid** | 2 kolom (mobile), 3 (tablet), 4 (desktop) |
| **Product card** | Gambar 1:1, nama, harga, badge diskon, rating bintang |
| **Pagination** | Load more atau infinite scroll |

### 10.3 Halaman Detail Produk

| Elemen | Deskripsi |
|--------|-----------|
| **Gambar** | Carousel/galeri, tap untuk zoom |
| **Info** | Nama, rating bintang + jumlah review, jumlah terjual |
| **Harga** | Harga coret (jika diskon) + harga aktual besar |
| **Varian** | Chips pilihan warna/tipe |
| **Jumlah** | Stepper tombol - / jumlah / + |
| **Tombol aksi** | "Tambah ke Keranjang" (primary), "Beli Langsung" (secondary) |
| **Tab** | Deskripsi | Spesifikasi | Reviews |
| **Review list** | Avatar, nama, rating bintang, tanggal, komentar |

### 10.4 Halaman Keranjang

| Elemen | Deskripsi |
|--------|-----------|
| **Item list** | Gambar kecil, nama produk, varian, harga satuan, stepper jumlah, subtotal per item |
| **Hapus** | Ikon trash per item + konfirmasi |
| **Ringkasan** | Subtotal semua item, total jumlah item |
| **CTA** | Tombol "Lanjut Checkout" (primary) |

### 10.5 Halaman Checkout

| Elemen | Deskripsi |
|--------|-----------|
| **Alamat** | Form: nama penerima, telepon, alamat lengkap, kota/kab, kode pos |
| **Ringkasan** | Daftar produk, harga per item, subtotal |
| **Pengiriman** | Pilihan kurir: JNE, J&T, SiCepat, GoSend + estimasi ongkir |
| **Pembayaran** | Pilihan: Transfer Bank (BCA, Mandiri, BRI), E-Wallet (GoPay, OVO, Dana), QRIS |
| **Total** | Harga subtotal + ongkir = Total bayar |
| **CTA** | Tombol "Buat Pesanan" |

### 10.6 Halaman Konfirmasi Pembayaran

| Elemen | Deskripsi |
|--------|-----------|
| **Info pesanan** | Nomor pesanan, total yang harus dibayar |
| **Instruksi** | Rekening tujuan / QR code sesuai metode yang dipilih |
| **Upload** | Area drag & drop atau klik untuk upload bukti transfer (jpg/png, max 5MB) |
| **Catatan** | "Bukti pembayaran akan diverifikasi dalam 1x24 jam" |
| **CTA** | Tombol "Kirim Bukti Pembayaran" |

### 10.7 Halaman Riwayat Pesanan

| Elemen | Deskripsi |
|--------|-----------|
| **Tab filter** | Semua, Diproses, Dikirim, Selesai |
| **Order card** | Nomor pesanan, tanggal, badge status berwarna, ringkasan item, total |
| **Detail** | Klik card untuk melihat detail lengkap (produk, alamat, kurir, resi, timeline status) |

### 10.8 Dashboard Admin

| Elemen | Deskripsi |
|--------|-----------|
| **Stat cards** | Total penjualan bulan ini, pesanan baru hari ini, produk stok rendah, total user |
| **Pesanan terbaru** | Tabel 10 pesanan terakhir dengan status |
| **Quick action** | Tombol shortcut ke verifikasi pembayaran, update stok |
| **Grafik** | Line chart penjualan mingguan (opsional, gunakan chart ringan) |

---

## 11. Daftar iPhone Series

| Seri | Models |
|------|--------|
| **iPhone 16** | iPhone 16, 16 Plus, 16 Pro, 16 Pro Max |
| **iPhone 15** | iPhone 15, 15 Plus, 15 Pro, 15 Pro Max |
| **iPhone 14** | iPhone 14, 14 Plus, 14 Pro, 14 Pro Max |
| **iPhone 13** | iPhone 13, 13 mini, 13 Pro, 13 Pro Max |
| **iPhone 12** | iPhone 12, 12 mini, 12 Pro, 12 Pro Max |
| **iPhone 11** | iPhone 11, 11 Pro, 11 Pro Max |

---

## 12. Estimasi Pengembangan

### 12.1 Fase Pengembangan

| Fase | Durasi | Scope |
|------|--------|-------|
| **Fase 1: Setup & Fondasi** | 1 minggu | Inisialisasi project, setup database & ORM, autentikasi dasar (register/login/JWT), konfigurasi CORS, folder structure |
| **Fase 2: Produk & Katalog** | 1.5 minggu | CRUD produk & kategori (admin), halaman katalog (public), filter seri/kategori/harga, search, detail produk, gambar produk |
| **Fase 3: Transaksi** | 1.5 minggu | Keranjang belanja, checkout, manajemen pesanan, upload bukti pembayaran, riwayat pesanan |
| **Fase 4: Admin Panel** | 1 minggu | Dashboard admin, CRUD kategori, kelola stok, verifikasi pembayaran, update status & resi pesanan, kelola user |
| **Fase 5: UI/UX Polish** | 0.5 minggu | Responsive fine-tuning, animasi transisi, loading skeleton, error states, empty states |
| **Fase 6: Testing & Deploy** | 0.5 minggu | Unit test, integration test, Lighthouse audit, deploy ke production |
| **Total** | **~6 minggu** | |

### 12.2 Tim Ideal

| Peran | Jumlah | Tanggung Jawab |
|-------|--------|----------------|
| Frontend Developer | 1 | Seluruh UI/UX, komponen React, state management, responsive design |
| Backend Developer | 1 | REST API, database, autentikasi, file upload, business logic |
| Fullstack Developer | 1 | Alternatif: menghandle kedua sisi jika tim terbatas |

---

## 13. Metrik Keberhasilan

| Metrik | Target | Cara Ukur |
|--------|--------|-----------|
| **Mobile Performance** | Lighthouse score >= 90 | Lighthouse audit |
| **Load Time** | < 3 detik di koneksi 3G | WebPageTest / GTmetrix |
| **Crash-Free Rate** | >= 99% sesi tanpa error | Error monitoring |
| **Conversion Rate** | >= 2% visitor ke order | Analytics |
| **Admin Task Time** | < 2 menit untuk proses 1 pesanan | Usability test |
| **Basket Abandonment** | < 50% | Analytics funnel |

---

## 14. Risiko & Mitigasi

| Risiko | Probabilitas | Dampak | Mitigasi |
|--------|-------------|--------|----------|
| Internet tidak stabil | Tinggi | Tinggi | Lazy loading, skeleton UI, caching HTTP, kompresi gambar, service worker untuk offline fallback |
| Kinerja lambat di device low-end | Sedang | Tinggi | Code splitting, tree shaking, hindari library berat, hindari animasi berat |
| Gambar produk banyak | Tinggi | Sedang | Kompresi otomatis (Sharp/ImageMagick), CDN, format WebP, lazy loading |
| Keamanan data user | Rendah | Tinggi | HTTPS, input validation (server+client), bcrypt hashing, rate limiting, helmet middleware |
| Stok tidak sinkron (race condition) | Sedang | Sedang | Optimistic locking, validasi stok di backend saat checkout, atomic update |
| Pembayaran palsu/tidak valid | Sedang | Sedang | Verifikasi manual oleh admin, validasi format bukti bayar, batasi ukuran upload |

---

## 15. Lampiran

### 15.1 Contoh Data Produk

```json
{
  "name": "Case Silky Matte iPhone 15 Pro",
  "slug": "case-silky-matte-iphone-15-pro",
  "description": "Case silikon matte premium dengan sentuhan lembut, melindungi iPhone 15 Pro Anda dari goresan dan benturan.",
  "price": 89000,
  "discount_price": 69000,
  "iphone_series": "iPhone 15",
  "stock": 150,
  "category": "Silicone",
  "rating": 4.8,
  "sold_count": 342,
  "colors": ["Burgundy", "Navy", "Sage Green", "Lilac"],
  "image_url": "/images/products/case-silky-matte-iphone15pro.jpg"
}
```

### 15.2 Contoh Status Pesanan

| Status | Keterangan | Aksi User | Aksi Admin |
|--------|------------|-----------|------------|
| **pending** | Menunggu pembayaran | Upload bukti bayar | - |
| **paid** | Pembayaran terverifikasi | Tunggu diproses | Verifikasi bukti bayar |
| **processing** | Sedang disiapkan | Tunggu dikirim | Update status |
| **shipped** | Sudah dikirim (ada resi) | Lacak pengiriman | Input nomor resi |
| **delivered** | Sampai di tujuan | Beri review | Update status |
| **cancelled** | Dibatalkan | - | Update status |

### 15.3 Contoh Respon API

**GET /api/products?page=1&limit=2&category=Silicone**

```json
{
  "success": true,
  "data": {
    "products": [
      {
        "id": 1,
        "name": "Case Silky Matte iPhone 15 Pro",
        "slug": "case-silky-matte-iphone-15-pro",
        "price": 89000,
        "discount_price": 69000,
        "image_url": "/images/products/case-silky-matte.jpg",
        "iphone_series": "iPhone 15",
        "category": { "id": 1, "name": "Silicone" },
        "rating": 4.8,
        "sold_count": 342
      }
    ],
    "pagination": {
      "currentPage": 1,
      "totalPages": 15,
      "totalProducts": 30,
      "limit": 2
    }
  }
}
```

---

*Dokumen ini merupakan acuan utama selama proses pengembangan. Setiap perubahan harus didokumentasikan dan disetujui oleh tim.*

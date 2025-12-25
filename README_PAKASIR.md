# Pakasir Pay - Sistem Pembayaran Otomatis

Website pembayaran otomatis menggunakan Pakasir dengan tampilan modern bertema Anime / Cyber / Gaming.

## 🎨 Fitur Utama

### Frontend
- ✅ **Halaman Pembayaran** - Input nominal pembayaran dengan tampilan anime/cyber
- ✅ **Quick Amount Buttons** - Pilihan nominal pembayaran cepat
- ✅ **Halaman Sukses** - Animasi sukses dengan informasi transaksi
- ✅ **Responsive Design** - Tampilan mobile & desktop yang menyesuaikan
- ✅ **Animasi Halus** - Hover effects, transitions, dan loading animations

### Admin Panel
- ✅ **Login Admin** - Autentikasi aman dengan token session
- ✅ **Dashboard** - Statistik transaksi dan ringkasan
- ✅ **Riwayat Transaksi** - Tabel lengkap semua transaksi
- ✅ **Pengaturan Pakasir** - Merchant ID & Secret
- ✅ **Pengaturan Telegram** - Bot Token & Chat ID untuk notifikasi
- ✅ **Pengaturan Admin** - Username & Password
- ✅ **Minimal Payment** - Atur minimum pembayaran

### Backend API
- ✅ **Payment Creation API** - `/api/payment/create`
- ✅ **Webhook API** - `/api/payment/webhook` (untuk update status dari Pakasir)
- ✅ **Admin Login API** - `/api/admin/login`
- ✅ **Settings API** - `/api/admin/settings`
- ✅ **Transactions API** - `/api/admin/transactions`

### Notifikasi
- ✅ **Telegram Notification** - Notifikasi otomatis saat pembayaran sukses
- ✅ **Format Pesan Rapi** - Informasi lengkap tentang transaksi

## 🚀 Cara Penggunaan

### 1. Setup Awal

#### Login Admin
1. Buka `http://localhost:3000/admin`
2. Gunakan default credentials:
   - Username: `admin`
   - Password: `admin123`

#### Konfigurasi Pakasir
1. Setelah login, masuk ke tab **Pengaturan**
2. Isi **Konfigurasi Pakasir**:
   - **Merchant ID**: Dapatkan dari dashboard Pakasir
   - **Merchant Secret**: Dapatkan dari dashboard Pakasir
   - **Redirect URL**: URL tujuan setelah pembayaran (default: success page)
   - **Minimal Pembayaran**: Minimum nominal pembayaran (default: Rp 10.000)

#### Konfigurasi Telegram (Opsional)
Untuk notifikasi ke Telegram saat pembayaran sukses:
1. Buat bot Telegram melalui @BotFather
2. Dapatkan Bot Token
3. Dapatkan Chat ID Anda (kirim pesan ke bot, lalu cek `https://api.telegram.org/bot<TOKEN>/getUpdates`)
4. Masukkan di tab **Pengaturan**:
   - **Bot Token**: Token bot Telegram Anda
   - **Chat ID**: Chat ID penerima notifikasi

### 2. Melakukan Pembayaran

1. Buka halaman utama `http://localhost:3000`
2. Masukkan nominal pembayaran
3. Klik tombol **"Bayar Sekarang"**
4. Akan di-redirect ke halaman pembayaran Pakasir
5. Lakukan pembayaran (QRIS / Transfer)
6. Setelah sukses, akan redirect ke halaman sukses

### 3. Monitoring Transaksi

1. Buka Admin Panel
2. Masuk ke tab **Transaksi**
3. Anda dapat melihat:
   - Daftar semua transaksi
   - Status transaksi (Pending, Success, Failed, Expired)
   - Detail nominal dan waktu
   - Metode pembayaran

## 📁 Struktur Proyek

```
/
├── prisma/
│   └── schema.prisma          # Database schema
├── lib/
│   └── db.ts                  # Prisma client
├── src/
│   ├── app/
│   │   ├── page.tsx           # Halaman pembayaran utama
│   │   ├── success/
│   │   │   └── page.tsx       # Halaman sukses
│   │   ├── admin/
│   │   │   ├── page.tsx       # Login admin
│   │   │   └── dashboard/
│   │   │       └── page.tsx   # Admin dashboard
│   │   └── api/
│   │       ├── payment/
│   │       │   ├── create/
│   │       │   │   └── route.ts    # Payment creation
│   │       │   └── webhook/
│   │       │       └── route.ts    # Webhook from Pakasir
│   │       ├── admin/
│   │       │   ├── login/
│   │       │   │   └── route.ts     # Admin login
│   │       │   ├── settings/
│   │       │   │   └── route.ts     # Admin settings
│   │       │   └── transactions/
│   │       │       └── route.ts     # Transaction list
│   │       └── init/
│   │           └── route.ts         # System initialization
│   ├── components/
│   │   └── ui/               # shadcn/ui components
│   └── ...
└── .env                      # Environment variables
```

## 🔐 Keamanan

- Password admin di-hash menggunakan SHA-256
- Signature verification untuk webhook Pakasir
- Sensitive data tidak ditampilkan di frontend
- Environment variables untuk configuration
- Anti-manipulasi data

## 🌐 Environment Variables

Diperlukan dalam `.env`:

```env
DATABASE_URL="file:./dev.db"
NEXT_PUBLIC_APP_URL="http://localhost:3000"
```

## 📦 Database Schema

### Transaction
- `id` - Unique identifier
- `orderId` - Order ID unik
- `amount` - Nominal pembayaran (IDR)
- `status` - Status (pending, success, failed, expired)
- `paymentMethod` - Metode pembayaran
- `paymentUrl` - URL pembayaran Pakasir
- `pakasirRef` - Reference ID dari Pakasir
- `createdAt` - Waktu dibuat
- `updatedAt` - Waktu terupdate

### AdminSettings
- `adminUsername` - Username admin
- `adminPassword` - Password admin (hashed)
- `merchantId` - Merchant ID Pakasir
- `merchantSecret` - Merchant Secret Pakasir
- `redirectUrl` - URL setelah pembayaran
- `minPayment` - Minimal pembayaran
- `telegramBotToken` - Token bot Telegram
- `telegramChatId` - Chat ID Telegram

## 🎨 Tema & Desain

- **Warna Dominan**: Ungu - Biru - Neon
- **Style**: Anime / Cyber / Gaming
- **UI Modern**: Menggunakan shadcn/ui
- **Animations**: Hover effects, transitions, loading states
- **Responsive**: Mobile-first design

## 📱 Deployment ke Vercel

1. Push kode ke repository Git
2. Connect repository ke Vercel
3. Set environment variables di Vercel:
   - `DATABASE_URL` (gunakan PostgreSQL untuk production)
4. Deploy!

**Catatan untuk Production:**
- Ganti SQLite dengan PostgreSQL
- Update database URL di Prisma
- Run `prisma migrate deploy`
- Set `NEXT_PUBLIC_APP_URL` ke domain production

## 🔧 Troubleshooting

### Login tidak berfungsi
- Pastikan database sudah di-push: `bun run db:push`
- Cek jika ada record di tabel AdminSettings

### Transaksi tidak update
- Pastikan webhook URL Pakasir benar: `{NEXT_PUBLIC_APP_URL}/api/payment/webhook`
- Cek signature verification

### Notifikasi Telegram tidak terkirim
- Verifikasi Bot Token dan Chat ID
- Pastikan bot sudah di-start (kirim /start ke bot)

## 📝 Catatan

- Website siap pakai
- Tanpa error build
- Dokumentasi lengkap
- Mudah dikembangkan
- Cocok untuk bisnis digital / top-up / donasi

## 🤝 Support

Untuk bantuan lebih lanjut, silakan cek dokumentasi Pakasir atau hubungi tim development.

---

**Dibuat dengan ❤️ untuk komunitas**

# TOUGAR | TOUR GARUT (Laravel)

Website pariwisata Garut — hasil konversi dari proyek HTML/CSS/JS "TUBES KELOMPOK DAP" ke Laravel 12.

## Cara menjalankan

Syarat: PHP 8.2+ (ekstensi `pdo_sqlite`, `mbstring`, `openssl`, `fileinfo`) dan Composer.

```bash
composer install
php artisan migrate --seed
php artisan serve
```

Buka http://localhost:8000

`.env` sudah disertakan (APP_KEY sudah terisi, database SQLite di `database/database.sqlite`).
Kalau ingin key baru: `php artisan key:generate`. Untuk MySQL, ubah `DB_*` di `.env`.

## Akun

| Peran | Username | Password | Login di |
|-------|----------|----------|----------|
| Admin | `admin` | `admin123` | `/admin/login` |
| Admin | `tougar` | `tougar2025` | `/admin/login` |
| Pengguna | daftar sendiri | — | `/register` lalu `/login` |

## Peta halaman

| URL | Route | File asal | Akses |
|-----|-------|-----------|-------|
| `/` | `landing` | `dashboard/dashboard.html` | publik |
| `/login`, `/register`, `/lupa-password` | `login`, `register`, `password.forgot` | `Login.html`, `register.html`, `lupakatasandi.html` | tamu |
| `/beranda` | `beranda` | `Beranda.html` | login |
| `/destinasi` | `destinasi` | `destinasi.html` | login |
| `/paket-wisata` | `paket` | `Paket wisata.html` | login |
| `/peta-wisata` | `peta` | `peta wisata.html` | login |
| `/laporan` | `laporan` | `Laporan.html` | login |
| `/kontak` | `kontak` | `kontak.html` | login |
| `/pembayaran` | `pembayaran` | `tugas.html` | login |
| `/admin/login`, `/admin` | `admin.login`, `admin.dashboard` | `admin/login`, `admin/beranda` | admin |

## Struktur

- `routes/web.php` — semua route
- `app/Http/Controllers` — Auth, AdminAuth, Contact, Booking
- `resources/views` — Blade (`layouts/app`, `partials/footer`, `pages/*`, `auth/*`, `admin/*`)
- `public/assets/{css,js,img}` — aset statis (nama file sudah diseragamkan huruf kecil)
- `config/paket.php` — data paket wisata (dulu variabel JS `packagesData`)
- `database/migrations` — tabel `users`, `bookings`, `contact_messages`

## Yang berubah dari versi HTML

- Login/registrasi pengguna dan admin sekarang sungguhan (database + session), bukan simulasi JavaScript/localStorage.
- Form **Kontak** menyimpan pesan ke tabel `contact_messages`.
- **Booking paket** disimpan ke tabel `bookings`; harga dihitung server dari `config/paket.php`.
- Halaman selain landing hanya bisa dibuka setelah login (hapus grup `auth` di `routes/web.php` jika tidak diinginkan).
- Panel admin masih memakai data contoh di JavaScript (`public/assets/js/admin-dashboard.js`); CRUD-nya belum tersambung ke database.
- "Lupa password" masih simulasi (belum ada pengiriman email).
- Tombol favorit (wishlist) di Beranda belum punya halaman tujuan.

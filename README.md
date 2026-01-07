Nama : Navyta Budi Yulia

NIM : 312410184

Kelas : TI.24.A2

# Project UAS Pemrograman Web 

# Aplikasi Sederhana - SISTEM INFORMASI PERPUSTAKAAN DIGITAL

## 1. Struktur Database

### Tabel : `Users`

```
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(50) UNIQUE NOT NULL,
    password VARCHAR(255) NOT NULL,
    nama VARCHAR(100) NOT NULL,
    role ENUM('admin', 'user') DEFAULT 'user',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```
### Keterangan :

- `id` : Primary key
- `username` : Username unik untuk login
- `password` : Password terenkripsi
- `nama` : Nama lengkap user
- `role` : Admin atau user
- `created_at` : Timestamp pembuatan akun

### Tabel : `buku`

```
CREATE TABLE buku (
    id INT AUTO_INCREMENT PRIMARY KEY,
    judul VARCHAR(200) NOT NULL,
    penulis VARCHAR(100),
    penerbit VARCHAR(100),
    tahun INT,
    kategori VARCHAR(50),
    stok INT DEFAULT 0,
    gambar VARCHAR(255),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);
```
### Keterangan :

- `id` : Primary key
- `judul` : judul buku
- `penulis` : Nama penulis
- `penerbit` : Nama penerbit
- `tahun` : Tahun terbit
- `lategori` : kategori buku
- `stok` : Jumlah stok tersedia
- `gambar` : Nama file gambar cover
- `created_at` : Timestamp pembuatan data
- `updated_at` : Timestamp update terakhir

### Tabel : `peminjam`

```
CREATE TABLE peminjaman (
    id INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT NOT NULL,
    buku_id INT NOT NULL,
    tanggal_pinjam DATE NOT NULL,
    tanggal_kembali DATE,
    status ENUM('dipinjam', 'dikembalikan') DEFAULT 'dipinjam',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES users(id) ON DELETE CASCADE,
    FOREIGN KEY (buku_id) REFERENCES buku(id) ON DELETE CASCADE
);
```

### Keterangan :

- `id` : Primary key
- `user_id` : Foreign key ke tabel users
- `buku_id` : foreign key ke tabel buku
- `tanggal_pinjam` : Tanggal pemiknjaman
- `tanggal_kembali` : Tanggal pengembalian (NULL jika belum dikembalikan)
- `status` : Status peminjaman
- `created_at`: Timestamp pembuatan
- `updated_at` : Timestamp update terakhir


## Struktur Folder

```
perpustakaan/
├── .htaccess                    # URL rewriting
├── index.php                    # Entry point aplikasi
│
├── config/                      # Konfigurasi
│   ├── config.php              # Konstanta & setting
│   └── database.php            # Koneksi database
│
├── core/                        # Core system
│   └── Router.php              # Routing handler
│
├── app/                         # Aplikasi utama
│   ├── controllers/            # Controllers (Business Logic)
│   │   ├── AuthController.php  # Login & logout
│   │   ├── BukuController.php  # CRUD Buku
│   │   └── PeminjamanController.php # Peminjaman
│   │
│   ├── models/                 # Models (Database Logic)
│   │   ├── User.php           # Model User
│   │   ├── Buku.php           # Model Buku
│   │   └── Peminjaman.php     # Model Peminjaman
│   │
│   └── views/                  # Views (Presentation)
│       ├── auth/
│       │   └── login.php      # Halaman login
│       ├── buku/
│       │   ├── index.php      # List buku
│       │   ├── create.php     # Form tambah buku
│       │   └── edit.php       # Form edit buku
│       └── peminjaman/
│           ├── index.php      # Peminjaman user
│           └── kelola.php     # Kelola peminjaman (admin)
│
├── public/                      # Asset publik
│   ├── css/
│   │   └── ocean.css          # Custom CSS
│   └── uploads/
│       └── buku/              # Folder upload gambar
│
└── database.sql                 # Database schema
```

## Konfigurasi Database `config/database.php`

```
private $host = 'localhost';
private $user = 'root';
private $pass = '';
private $db   = 'perpustakaan';
private $port = 3307; 
```

## Panduan Penggunaan
### Login
- Akses http://localhost/perpustakaan/
- Masukkan username dan password
- Klik "Login"

<img width="1920" height="1008" alt="Image" src="https://github.com/user-attachments/assets/c60a0ab5-991a-40b3-afe8-21a0874c9ba6" />

## SebagaI Admin
### Mengelola Buku

<img width="1920" height="1008" alt="Image" src="https://github.com/user-attachments/assets/23f41f29-801f-44a8-8aa4-06fe947d3988" />

### 1. Tambah Buku
- klik tombol "➕ Tambah Buku"
- Isi form (judul, penulis, penerbit, tahun, kategori, stok)
- Upload gambar cover (opsional)
- Klik "💾 Simpan Buku"

### 2. Edit Buku
- Klik tombol "✏️ Edit" pada buku yang ingin diubah
- Ubah data yang diperlukan
- Upload gambar baru (opsional)
- Klik "💾 Update Buku"

### 3. Hapus Buku
- Klik tombol "🗑️ Hapus" pada buku
- Konfirmasi penghapusan
- Buku dan gambarnya akan terhapus

### 4. Cari Buku
- Ketik kata kunci di kolom pencarian
- Klik "🔍 Cari"
- Sistem akan filter berdasarkan judul, penulis, atau kategori

### 5. Kelola Peminjaman
- Klik menu "🔧 Kelola Peminjaman"
- Lihat statistik peminjaman
- Lihat semua peminjaman dari semua user
- Tandai buku sudah dikembalikan jika perlu 




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

### 1. Dashboard Buku 

- Tombol "Tambah Buku" (Admin)
- Form pencarian
- Grid layout buku dengan gambar cover
- Tombol Edit & Hapus untuk setiap buku
- Pagination
- Info stok buku

<img width="1920" height="1008" alt="Image" src="https://github.com/user-attachments/assets/ecebdd55-a967-4bb3-b92e-198372084082" />

### 2. Tambah Buku
- klik tombol "Tambah Buku"
- Isi form (judul, penulis, penerbit, tahun, kategori, stok)
- Upload gambar cover (opsional)
- Klik "Simpan Buku"

<img width="1920" height="1008" alt="Image" src="https://github.com/user-attachments/assets/999a01b1-927b-4854-adb0-6340a4765d24" />

### 3. Edit Buku
- Klik tombol " Edit" pada buku yang ingin diubah
- Ubah data yang diperlukan
- Upload gambar baru (opsional)
- Klik "Update Buku"

<img width="1920" height="1008" alt="Image" src="https://github.com/user-attachments/assets/b30d7df3-2817-45db-baa4-ac5527e66eda" />

### 4. Hapus Buku
- Klik tombol "Hapus" pada buku
- Konfirmasi penghapusan
- Buku dan gambarnya akan terhapus

<img width="1920" height="1008" alt="Image" src="https://github.com/user-attachments/assets/5ab97d63-33a0-4ab5-a06b-66b42424f7c9" />

### 5. Cari Buku
- Ketik kata kunci di kolom pencarian
- Klik "Cari"
- Sistem akan filter berdasarkan judul, penulis, atau kategori

<img width="1920" height="1008" alt="Image" src="https://github.com/user-attachments/assets/cd33627e-3bf7-4e38-9b73-7d08d824e5e8" />

### 6. Kelola Peminjaman
- Klik menu "Kelola Peminjaman"
- Lihat statistik peminjaman
- Lihat semua peminjaman dari semua user
- Tandai buku sudah dikembalikan jika perlu 

## Sebagai User

<img width="1920" height="1008" alt="Image" src="https://github.com/user-attachments/assets/9db02cba-698b-41e7-b277-4f68e27b79bd" />

<img width="1920" height="1008" alt="Image" src="https://github.com/user-attachments/assets/79661ec8-bce7-4bf4-bf8c-b8cde08e5123" />


### 1. Meminjam Buku
- Browse daftar buku di halaman utama
- Cari buku yang diinginkan (opsional)
- Klik "Pinjam Buku" pada buku yang tersedia
- Konfirmasi peminjaman
- Stok akan berkurang otomatis



<img width="1920" height="1008" alt="Image" src="https://github.com/user-attachments/assets/a8d1e4d3-e22a-4441-8042-a51e0eae5ac9" />

<img width="1920" height="1008" alt="Image" src="https://github.com/user-attachments/assets/c26a8006-153a-46eb-a02f-8a961073fa34" />


### Mengembalikan Buku
- Klik menu "Peminjaman Saya"
- Lihat daftar buku yang dipinjam
- Klik "Kembalikan" pada buku yang ingin dikembalikan
- Konfirmasi pengembalian
- Stok akan bertambah otomatis

<img width="1920" height="1008" alt="Image" src="https://github.com/user-attachments/assets/e4a4d370-01b9-4650-a1e7-5075be48c765" />

### Melihat Riwayat
- Klik menu "Peminjaman Saya"
- Lihat semua riwayat peminjaman
- Status akan menunjukkan "Dipinjam" atau "Dikembalikan" 

# Prnjelasan Kode

## 1. Routing System (core/Router.php)
- Konsep: Custom router menggunakan URL rewriting dengan .htaccess

```
class Router {
    public static function run() {
        $url = $_GET['url'] ?? '';
        $url = trim($url, '/');
        
        if ($url === '') {
            $url = 'login';
        }
        
        switch ($url) {
            case 'login':
                (new AuthController())->login();
                break;
            // ... routes lainnya
        }
    }
}
```

### Penjelasan :
- Mengambil URL dari parameter GET
- Mencocokkan dengan route yang tersedia
- Memanggil controller yang sesuai
- Default route adalah 'login'

## Database Connection (config/database.php)
- Konsep: Singleton pattern untuk koneksi database

```
class Database {
    private static $instance = null;
    
    public static function getInstance() {
        if (self::$instance == null) {
            self::$instance = new Database();
        }
        return self::$instance;
    }
}
```

### Penjelasan :
- Hanya satu instance koneksi database
- Menghemat resource
- Mudah diakses dengan function helper db()

## Authentication (app/controllers/AuthController.php)
- Konsep: Login dengan password hashing dan session management

```
public function login() {
    if ($_SERVER['REQUEST_METHOD'] === 'POST') {
        $user = $userModel->login($username, $password);
        
        if ($user) {
            $_SESSION['user'] = [
                'id' => $user['id'],
                'username' => $user['username'],
                'nama' => $user['nama'],
                'role' => $user['role']
            ];
            header('Location: ' . BASE_URL . 'buku');
        }
    }
}
```

### Penjelasan :
- Cek method POST untuk submit form
- Validasi username dan password
- Simpan data user di session
- Redirect ke halaman buku jika berhasil

## 4. Password Verification (app/models/User.php)
- Konsep: Password hashing menggunakan bcrypt

```
public function login($username, $password) {
    $user = // query database
    
    if (password_verify($password, $user['password'])) {
        return $user;
    }
    return false;
}
```

### Penjelasan :
- Password di database terenkripsi dengan bcrypt
- Gunakan password_verify() untuk pencocokan
- Return user data jika cocok

## 5. CRUD Buku (app/controllers/BukuController.php)
- Konsep: Controller menangani business logic CRUD
- Create :

```
public function create() {
    if ($_SERVER['REQUEST_METHOD'] === 'POST') {
        // Handle upload gambar
        if (isset($_FILES['gambar'])) {
            $upload = $this->uploadGambar($_FILES['gambar']);
            $data['gambar'] = $upload['filename'];
        }
        
        // Insert ke database
        $bukuModel->insert($data);
    }
}
```

- Read :

```
public function index() {
    $dataBuku = $bukuModel->getPaginated($limit, $offset, $search);
    $totalPage = ceil($totalData / $limit);
    
    require __DIR__ . '/../views/buku/index.php';
}
```

- Update :

```
public function edit() {
    if ($_SERVER['REQUEST_METHOD'] === 'POST') {
        // Hapus gambar lama jika ada upload baru
        if (isset($_FILES['gambar'])) {
            unlink(UPLOAD_DIR . $buku['gambar']);
            $upload = $this->uploadGambar($_FILES['gambar']);
        }
        
        $bukuModel->update($id, $data);
    }
}
```

- Delete :

```
public function delete() {
    $bukuModel->delete($_GET['id']);
    header('Location: ' . BASE_URL . 'buku');
}
```

## 6. Upload Gambar
- Konsep: Validasi dan upload file gambar

```
private function uploadGambar($file) {
    // Validasi ukuran
    if ($file['size'] > MAX_FILE_SIZE) {
        return ['status' => false, 'message' => 'File terlalu besar'];
    }
    
    // Validasi ekstensi
    $ext = strtolower(pathinfo($file['name'], PATHINFO_EXTENSION));
    if (!in_array($ext, ALLOWED_EXT)) {
        return ['status' => false, 'message' => 'Format tidak diizinkan'];
    }
    
    // Generate nama unik
    $filename = uniqid() . '_' . time() . '.' . $ext;
    
    // Upload file
    move_uploaded_file($file['tmp_name'], UPLOAD_DIR . $filename);
}
```

### Penjelasan :
- Validasi ukuran file (max 5MB)
- Validasi ekstensi (JPG, PNG, GIF)
- Generate nama file unik untuk menghindari konflik
- Move file ke folder uploads

## 7. Pagination
- Konsep: Membagi data menjadi beberapa halaman

```
$page = isset($_GET['page']) ? (int)$_GET['page'] : 1;
$limit = 5;
$offset = ($page - 1) * $limit;

$dataBuku = $bukuModel->getPaginated($limit, $offset, $search);
$totalData = $bukuModel->countAll($search);
$totalPage = ceil($totalData / $limit);
```
### Penjelasan :
- Ambil parameter page dari URL
- Hitung offset berdasarkan page
- Query database dengan LIMIT dan OFFSET
- Hitung total halaman

## 8. Peminjaman Buku
- Konsep: Transaksi peminjaman dengan update stok otomatis
 
```
public function pinjam($user_id, $buku_id) {
    // Cek stok
    $buku = // query buku
    if ($buku['stok'] <= 0) {
        return ['status' => false, 'message' => 'Stok habis'];
    }
    
    // Cek sudah pinjam atau belum
    $cek = // query peminjaman
    if ($cek->num_rows > 0) {
        return ['status' => false, 'message' => 'Sudah meminjam'];
    }
    
    // Insert peminjaman
    // UPDATE buku SET stok = stok - 1
}
```

### Penjelasan :
- Validasi stok buku tersedia
- Cek user sudah pinjam buku yang sama atau belum
- Insert data peminjaman
- Kurangi stok buku otomatis

## 9. Pengembalian Buku
- Konsep: Update status dan tambah stok otomatis

```
public function kembalikan($peminjaman_id) {
    // Get data peminjaman
    $peminjaman = // query
    
    // Update status & tanggal kembali
    // UPDATE peminjaman SET status='dikembalikan', tanggal_kembali=NOW()
    
    // Tambah stok buku
    // UPDATE buku SET stok = stok + 1
}
```

### Penjelasan :
- Ambil data peminjaman
- Update status menjadi 'dikembalikan'
- Set tanggal pengembalian
- Tambah stok buku otomatis

## 10. Search & Filter
- Konsep: SQL LIKE query dengan multiple column

```
$sql = "SELECT * FROM buku WHERE 1=1";

if ($search !== '') {
    $search = $conn->real_escape_string($search);
    $sql .= " AND (judul LIKE '%$search%' 
              OR penulis LIKE '%$search%' 
              OR kategori LIKE '%$search%')";
}
```

### Penjelasan :
- Escape input user untuk prevent SQL injection
- LIKE query dengan wildcard %
- Search di multiple kolom (judul, penulis, kategori)



Nama : Navyta Budi Yulia

NIM : 312410184

Kelas : TI.24.A2

# Project UAS Pemrograman Web 

# Aplikasi Sederhana - SISTEM INFORMASI PERPUSTAKAAN DIGITAL

```
## Struktur Database

*Tabel : `Users`*

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

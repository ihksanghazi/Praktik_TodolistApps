# 🟦 Modul 7 Auth Guard & Logout

**🎯 Tujuan Modul**

Setelah menyelesaikan modul ini, siswa mampu:

- Memahami konsep **proteksi halaman (auth guard)**
- Membuat **middleware autentikasi sederhana**
- Melindungi halaman penting dari akses ilegal
- Membuat fitur **logout**
- Menghapus session dengan benar

## 🧠 Kenapa Halaman Perlu Diproteksi?

**Masalah Tanpa Auth Guard**

Jika tidak ada proteksi:

- User belum login bisa membuka dashboard
- User bisa langsung akses `/todolist/index.php`
- Data tidak aman

📌 Solusi:
**Auth middleware / auth guard**

## 🧠 Konsep Auth Middleware Sederhana

**Apa itu Auth Middleware?**
Auth middleware adalah **kode pengecek login** yang:

- Dijalanakan sebelum halaman ditampilkan
- Mengecek apakah user sudah login

**Prinsip Kerja**

```txt
Cek session login
    ↓
Jika belum login → redirect ke login
Jika sudah login → lanjut halaman
```

## 🧠 File `auth_check.php`

**Fungsi**

- Mengecek status login
- Digunakan di semua halaman yang dilindungi

**Buat file** `auth/auth_check.php`

```php
<?php
session_start();

if (!isset($_SESSION['login'])) {
    header("Location: ../auth/login.php");
    exit;
}
```

📌 Penjelasan:

- `session_start()` → mengaktifkan session
- `$_SESSION['login']` → penanda user sudah login
- `header()` → redirect jika belum login

## 🧠 Proteksi Halaman

**Halaman yang Wajib Diproteksi**

- Dashboard
- Todo List
- Semua halaman setelah login

## 🛠️ Proteksi Dashboard

**Edit** `dashboard/index.php`

```php
<?php
$activePage = 'dashboard';

include '../auth/auth_check.php';
include '../layouts/header.php';
include '../layouts/navbar.php';
?>
```

📌 `auth_check.php` harus dipanggil **sebelum HTML**.

## 🛠️ Proteksi Todo List

**Edit** `todolist/index.php`

```php
<?php
$activePage = 'todolist';

include '../auth/auth_check.php';
include '../config/koneksi.php';
include '../layouts/header.php';
include '../layouts/navbar.php';
?>
```

## 🧠 Logout User

**Apa itu Logout?**
Logout adalah proses:

- Menghapus session
- Mengakhiri login
- Mengembalikan user ke halaman login

## 🛠️ Membuat `logout.php`

**Buat file** `auth/logout.php`

```php
<?php
session_start();
session_destroy();
header("Location: login.php");
exit;
```

📌 Penjelasan:

- `session_destroy()` → hapus semua session
- Redirect ke halaman login

## 🛠️ Uji Auth Guard & Logout

**Uji Auth Guard**

1. Logout dari aplikasi
2. Akses langsung:
   ```bash
   http://localhost/TodoListApp/dashboard/index.php
   ```

✅ Harus diarahkan ke halaman login

**Uji Logout**

1. Login
2. Klik tombol **Logout**
3. Session hilang
4. Kembali ke halaman login

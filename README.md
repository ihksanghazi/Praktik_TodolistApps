# 🟦 Modul 4 Layout, Bootstrap & Reusable Component

**🎯 Tujuan Modul**
Setelah menyelesaikan modul ini, siswa mampu:

- Menggunakan **Bootstrap** untuk membuat UI web
- Membuat **layout konsisten** di seluruh halaman
- Menerapkan **reusable component** (header, footer, navbar)
- Mengatur **navbar active** sesuai halaman aktif
- Menambahkan **CSS custom**

## 🧠 Bootstrap Dasar

**Apa itu Bootstrap?**
Bootstrap adalah **framework CSS** yang membantu kita:

- Membuat tampilan cepat & rapi
- Menghindari styling dari nol
- Membuat layout responsif

**Komponen Bootstrap yang akan digunakan**

- Container
- Card
- Button
- Navbar
- Form
- Alert

📌 Bootstrap akan dipanggil melalui **CDN**.

## 🧠 Konsep Layout & Reusable Component

**Masalah Jika Tanpa Reusable File**

- Header ditulis berulang
- Navbar beda-beda
- Sulit maintenance

**Solusi**
Gunakan:

- header.php
- navbar.php
- footer.php

📌 Prinsip:
**Satu komponen → digunakan di banyak halaman**

## 🧠 File header.php

**Fungsi**

- Menyimpan:
  - HTML awal
  - Bootstrap CSS
  - CSS custom

**Buat file** `layouts/header.php`

```php
<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <title>Todo App</title>

    <!-- Bootstrap CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet">

    <!-- Custom CSS -->
    <link rel="stylesheet" href="../assets/css/style.css">
</head>
<body>
```

## 🧠 File footer.php

**Fungsi**

- Menutup HTML
- Memuat Bootstrap JS

**Buat file** `layouts/footer.php`

```php
    <!-- Bootstrap JS -->
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/js/bootstrap.bundle.min.js"></script>
</body>
</html>
```

## 🧠 File navbar.php

**Fungsi**

- Navigasi utama aplikasi
- Digunakan di dashboard & todolist

**Konsep Navbar Active**
Navbar akan aktif berdasarkan:

```php
$activePage
```

**Buat file** `layouts/navbar.php`

```php
<?php
if (session_status() === PHP_SESSION_NONE) {
    session_start();
}

$activePage = $activePage ?? '';
?>

<nav class="navbar navbar-expand-lg navbar-dark bg-dark px-4">
    <a class="navbar-brand" href="../dashboard/index.php">Todo App</a>

    <div class="collapse navbar-collapse">
        <ul class="navbar-nav me-auto">
            <li class="nav-item">
                <a class="nav-link <?= ($activePage === 'dashboard') ? 'active' : ''; ?>"
                   href="../dashboard/index.php">
                   Dashboard
                </a>
            </li>
            <li class="nav-item">
                <a class="nav-link <?= ($activePage === 'todolist') ? 'active' : ''; ?>"
                   href="../todolist/index.php">
                   Todo List
                </a>
            </li>
        </ul>

        <span class="navbar-text text-white me-3">
            Halo, <?= $_SESSION['name'] ?? ''; ?>
        </span>

        <a href="../auth/logout.php" class="btn btn-danger btn-sm">
            Logout
        </a>
    </div>
</nav>
```

## 🧠 Konsep include

**Apa itu** `include`?
`include` digunakan untuk:

- Memanggil file lain
- Menghindari duplikasi kode

**Contoh Penggunaan**

```php
include '../layouts/header.php';
include '../layouts/navbar.php';
include '../layouts/footer.php';
```

📌 Jika file tidak ditemukan:

- `include` → warning
- `require` → fatal error

## 🛠️ Membuat CSS Custom

**Buat file** `assets/css/style.css`

```css
body {
  background-color: #f4f6f9;
}

.card {
  border-radius: 14px;
}
```

## 🛠️ Menggunakan Layout di Halaman

**Contoh di** `dashboard/index.php`

```php
<?php
$activePage = 'dashboard';

include '../layouts/header.php';
include '../layouts/navbar.php';
?>

<div class="container mt-4">
    <div class="card shadow p-4">
        <h4>Dashboard</h4>
        <p>Selamat datang!</p>
    </div>
</div>

<?php include '../layouts/footer.php'; ?>
```

## 🛠️ Mengatur Navbar Active

**Langkah**

1. Tentukan halaman aktif:
   ```php
   $activePage = 'todolist';
   ```
2. Navbar otomatis aktif sesuai halaman

📌 Tidak perlu JavaScript

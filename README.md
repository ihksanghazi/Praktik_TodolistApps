# 🟦 Modul 8 Dashboard User

**🎯 Tujuan Modul**

Setelah menyelesaikan modul ini, siswa mampu:

- Membuat **halaman dashboard**
- Menampilkan **data user dari session**
- Menyediakan **navigasi utama aplikasi**
- Menerapkan **UX sederhana namun jelas**

## 🧠 Fungsi Dashboard

**Apa itu Dashboard?**
Dashboard adalah:

- Halaman pertama setelah login
- Pusat navigasi aplikasi
- Tempat menampilkan informasi user

📌 Dalam aplikasi TodoList, dashboard berfungsi sebagai:
“Halaman sambutan + pintu menuju fitur utama”

## 🧠 Menampilkan Data dari Session

**Data Session yang Digunakan**

Saat login [Modul 6](https://github.com/ihksanghazi/Praktik_TodolistApps/tree/Modul_6?tab=readme-ov-file#%EF%B8%8F-membuat-login_processphp), kita menyimpan:

```php
$_SESSION['name']
$_SESSION['user_id']
```

📌 Data ini bisa dipanggil di halaman mana pun selama user login.

## 🧠 UX Sederhana pada Dashboard

**Prinsip UX yang Digunakan**

- Tampilan bersih
- Informasi jelas
- Tombol aksi utama terlihat

📌 Fokus:
Jangan terlalu ramai, cukup informatif

## 🛠️ Membuat dashboard/index.php

**Buat file** `dashboard/index.php`

```php
<?php
$activePage = 'dashboard';

include '../auth/auth_check.php';
include '../layouts/header.php';
include '../layouts/navbar.php';
?>

<div class="container mt-4">
    <div class="card shadow p-4">
        <h4 class="mb-2">Dashboard</h4>

        <p class="text-muted">
            Selamat datang kembali,
            <strong><?= $_SESSION['name']; ?></strong> 👋
        </p>

        <hr>

        <p>
            Dari halaman ini, kamu bisa mengelola daftar tugas harianmu.
        </p>

        <a href="../todolist/index.php" class="btn btn-primary">
            Kelola Todo List
        </a>
    </div>
</div>

<?php include '../layouts/footer.php'; ?>
```

## 🛠️ Uji Dashboard

**Langkah**

1. Login ke aplikasi
2. Setelah login → otomatis ke dashboard
3. Pastikan:
   - Nama user tampil
   - Navbar aktif di **Dashboard**
   - Tombol menuju TodoList berfungsi

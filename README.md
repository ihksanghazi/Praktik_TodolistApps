# 🟦 Modul 5 Sistem Register User

**🎯 Tujuan Modul**

Setelah menyelesaikan modul ini, siswa mampu:

- Membuat **form pendaftaran (register)**
- Mengirim data menggunakan **method POST**
- Mengamankan password dengan **password hashing**
- Menyimpan data user ke **database MySQL**

## 🧠 Form HTML

**Apa itu Form?**
Form digunakan untuk:

- Mengambil input dari user
- Mengirim data ke server

**Komponen Form Register**

- Input nama
- Input username
- Input password
- Tombol submit

📌 Data akan dikirim menggunakan **POST** agar lebih aman.

## 🧠 Method POST

**Kenapa POST?**

- Data **tidak tampil di URL**
- Lebih aman untuk password
- Cocok untuk proses insert data

**Contoh POST**

```html
<form method="POST" action="register_process.php"></form>
```

## 🧠 Password Hashing

**Masalah Jika Password Disimpan Polos**

- Berbahaya
- Mudah dicuri
- Tidak aman

Solusi: `password_hash()`

- Mengubah password menjadi `hash`
- Tidak bisa dikembalikan ke bentuk asli

**Contoh**

```php
$password = password_hash($\_POST['password'], PASSWORD_DEFAULT);
```

## Insert Data ke Database

**Alur Register**

```txt
User isi form
    ↓
Data dikirim (POST)
    ↓
Password di-hash
    ↓
Data disimpan ke database
```

## 🛠️ Membuat `register.php`

**Buat file** `auth/register.php`

```php
<?php
session_start();
include '../layouts/header.php';
?>

<div class="d-flex justify-content-center align-items-center vh-100">
    <div class="card p-4 shadow" style="width:360px">
        <h4 class="text-center mb-3">Register</h4>

        <form action="register_process.php" method="POST">
            <input type="text" name="name" class="form-control mb-2"
                   placeholder="Nama lengkap" required>

            <input type="text" name="username" class="form-control mb-2"
                   placeholder="Username" required>

            <input type="password" name="password" class="form-control mb-3"
                   placeholder="Password" required>

            <button class="btn btn-success w-100">Daftar</button>
        </form>

        <p class="text-center mt-3 mb-0">
            Sudah punya akun?
            <a href="login.php">Login</a>
        </p>
    </div>
</div>

<?php include '../layouts/footer.php'; ?>
```

## 🛠️ Membuat `register_process.php`

**Buat file** `auth/register_process.php`

```php
<?php
include '../config/koneksi.php';

$name = $_POST['name'];
$username = $_POST['username'];
$password = password_hash($_POST['password'], PASSWORD_DEFAULT);

mysqli_query($conn, "
    INSERT INTO users (name, username, password)
    VALUES ('$name', '$username', '$password')
");

header("Location: login.php");
```

## 🛠️ Uji Register

**Langkah**

1. Buka browser
2. Akses:
   ```bash
   http://localhost/TodoListApp/auth/register.php
   ```
3. Isi form
4. Klik **Daftar**

**Cek Database**

- Buka phpMyAdmin
- Tabel `users`
- Password terlihat **hash**, bukan teks asli

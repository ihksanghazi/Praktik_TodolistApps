# 🟦 Modul 6 Sistem Login & Session

**🎯 Tujuan Modul**

Setelah menyelesaikan modul ini, siswa mampu:

- Memahami **konsep autentikasi**
- Menggunakan **session PHP**
- Membuat proses **login berhasil & gagal**
- Menampilkan **flash message error**
- Melakukan **redirect** setelah login

## 🧠 Konsep Autentikasi & Session

**Apa itu Login?**
Login adalah proses:

- Memverifikasi identitas user
- Menyimpan status login

**Apa itu Session?**
Session adalah **penyimpanan data sementara di server** selama user aktif.

📌 Session digunakan untuk:

- Menyimpan status login
- Menyimpan data user (id, nama)

## 🧠 Alur Login Aplikasi

```txt
User isi username & password
        ↓
Server cek ke database
        ↓
Jika benar → session dibuat
        ↓
Redirect ke dashboard
Jika salah → error message
```

## 🧠 Validasi User & Password

**Cek Username**

```sql
SELECT * FROM users WHERE username = ?
```

**Cek Password**
Gunakan:

```php
password_verify($password, $hash)
```

📌 Password **tidak dibandingkan langsung**.

## 🧠 Flash Message Error

**Apa itu Flash Message?**

- Pesan sementara
- Disimpan di session
- Hilang setelah ditampilkan

📌 Digunakan untuk:

- Login gagal
- Error validasi

## 🛠️ Membuat `login.php`

**Buat file** `auth/login.php`

```php
<?php
session_start();
include '../layouts/header.php';
?>

<div class="d-flex justify-content-center align-items-center vh-100">
    <div class="card p-4 shadow" style="width:360px">
        <h4 class="text-center mb-3">Login</h4>

        <!-- FLASH MESSAGE -->
        <?php if (isset($_SESSION['error'])): ?>
            <div class="alert alert-danger alert-dismissible fade show">
                <?= $_SESSION['error']; ?>
                <button type="button" class="btn-close" data-bs-dismiss="alert"></button>
            </div>
        <?php unset($_SESSION['error']); endif; ?>

        <form action="login_process.php" method="POST">
            <input type="text" name="username"
                   class="form-control mb-2"
                   placeholder="Username" required>

            <input type="password" name="password"
                   class="form-control mb-3"
                   placeholder="Password" required>

            <button class="btn btn-primary w-100">Login</button>
        </form>

        <p class="text-center mt-3 mb-0">
            Belum punya akun?
            <a href="register.php">Register</a>
        </p>
    </div>
</div>

<?php include '../layouts/footer.php'; ?>
```

## 🛠️ Membuat `login_process.php`

**Buat file** `auth/login_process.php`

```php
<?php
session_start();
include '../config/koneksi.php';

$username = $_POST['username'];
$password = $_POST['password'];

$user = mysqli_fetch_assoc(
    mysqli_query($conn, "SELECT * FROM users WHERE username='$username'")
);

if ($user && password_verify($password, $user['password'])) {

    $_SESSION['login'] = true;
    $_SESSION['user_id'] = $user['id'];
    $_SESSION['name'] = $user['name'];

    header("Location: ../dashboard/index.php");
    exit;

} else {
    $_SESSION['error'] = "Username atau password salah!";
    header("Location: login.php");
    exit;
}
```

## 🛠️ Uji Login Berhasil & Gagal

**Login Berhasil**

- Username & password benar
- Redirect ke dashboard
- Session aktif

**Login Gagal**

- Username / password salah
- Tetap di halaman login
- Muncul alert error

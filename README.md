# 🟦 Modul 9 Create & Read Todo List

**🎯 Tujuan Modul**

Setelah menyelesaikan modul ini, siswa mampu:

- Menampilkan **todo milik user yang sedang login**
- Menambahkan **todo baru ke database**
- Memahami **relasi user ↔ todo (One-to-Many)**
- Menggunakan **session untuk filter data**

## 🧠 Relasi User & Todo (Implementasi Nyata)

**Konsep Penting**

- Setiap user hanya boleh melihat todo miliknya sendiri
- Todo tidak boleh tercampur dengan user lain

**Implementasi Teknis**
Relasi ini dijalankan menggunakan:

```php
$_SESSION['user_id']
```

📌 Artinya:

- Saat user login → `user_id` disimpan di session
- Saat ambil todo → query difilter berdasarkan `user_id`

## 🧠 Query SELECT Berdasarkan User

**Masalah Jika Tanpa Filter**

```sql
SELECT * FROM todolists;
```

❌ Semua user melihat semua todo

**Solusi (WAJIB)**

```sql
SELECT * FROM todolists WHERE user_id = ?
```

## 🧠 Form Tambah Todo

**Fungsi Form**

- Mengambil input todo dari user
- Mengirim data menggunakan **POST**
- Diproses oleh `store.php`

**Field Minimal**

- `title` (isi todo)

## 🧠 INSERT Data Todo

**Alur CREATE Todo**

```txt
User isi form
     ↓
Data dikirim (POST)
     ↓
Ambil user_id dari session
     ↓
INSERT ke database
     ↓
Redirect ke halaman todo
```

## 🛠️ Menampilkan Todo (READ)

**Buat file** `todolist/index.php`

```php
<?php
$activePage = 'todolist';

include '../auth/auth_check.php';
include '../config/koneksi.php';
include '../layouts/header.php';
include '../layouts/navbar.php';

$user_id = $_SESSION['user_id'];

$todos = mysqli_query($conn, "
    SELECT * FROM todolists
    WHERE user_id = $user_id
    ORDER BY id DESC
");
?>

<div class="container mt-4">
    <div class="card shadow p-4">
        <h4 class="mb-3">Todo List</h4>

        <!-- FORM TAMBAH TODO -->
        <form action="store.php" method="POST" class="d-flex mb-4">
            <input
                type="text"
                name="title"
                class="form-control me-2"
                placeholder="Tulis todo baru..."
                required>
            <button class="btn btn-success">Tambah</button>
        </form>

        <!-- LIST TODO -->
        <?php if (mysqli_num_rows($todos) > 0): ?>
            <ul class="list-group">
                <?php while ($todo = mysqli_fetch_assoc($todos)): ?>
                    <li class="list-group-item">
                        <?= htmlspecialchars($todo['title']); ?>
                    </li>
                <?php endwhile; ?>
            </ul>
        <?php else: ?>
            <div class="alert alert-info">
                Belum ada todo. Yuk tambahkan todo pertamamu! 🚀
            </div>
        <?php endif; ?>
    </div>
</div>

<?php include '../layouts/footer.php'; ?>
```

## 🛠️ Menambah Todo (CREATE)

**Buat file** `todolist/store.php`

```php
<?php
session_start();
include '../config/koneksi.php';

$title = $_POST['title'];
$user_id = $_SESSION['user_id'];

mysqli_query($conn, "
    INSERT INTO todolists (user_id, title)
    VALUES ($user_id, '$title')
");

header("Location: index.php");
exit;
```

## 🛠️ Uji Fitur Create & Read

**Langkah Pengujian**

1. Login sebagai user A
2. Tambahkan beberapa todo
3. Logout
4. Login sebagai user B
5. Pastikan:
   - Todo user A **tidak muncul**
   - User B punya todo sendiri

✅ Jika berhasil → relasi berjalan benar

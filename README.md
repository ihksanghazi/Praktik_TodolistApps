# 🟦 Modul 3 Struktur Folder & Koneksi Database

**🎯 Tujuan Modul**
Setelah menyelesaikan modul ini, siswa mampu:

- Memahami **struktur project PHP yang rapi**
- Menjelaskan fungsi setiap folder
- Membuat **koneksi database MySQL ke PHP**
- Menguji koneksi database dengan benar

## 🧠 Konsep Struktur Folder (MVC Sederhana)

**Kenapa Struktur Folder Penting?**
Struktur folder yang baik akan:

- Membuat kode **mudah dibaca**
- Memudahkan **maintenance**
- Memisahkan **tugas setiap file**

📌 Walaupun belum full MVC, kita menerapkan **konsep pemisahan tanggung jawab**.

## 🧠 Struktur Folder Aplikasi TodoList

Struktur folder yang akan digunakan:

```txt
TodoListApp/
│
├── assets/
│   └── css/
│       └── style.css
│
├── auth/
│   ├── login.php
│   ├── login_process.php
│   ├── register.php
│   ├── register_process.php
│   ├── logout.php
│   └── auth_check.php
│
├── config/
│   └── koneksi.php
│
├── layouts/
│   ├── header.php
│   ├── footer.php
│   └── navbar.php
│
├── dashboard/
│   └── index.php
│
├── todolist/
│   ├── index.php
│   ├── store.php
│   ├── done.php
│   └── delete.php
│
└── index.php
```

## 🧠 Fungsi Setiap Folder

📁 `config`

- Menyimpan konfigurasi aplikasi
- Contoh: koneksi database

📁 `auth`

- Semua file autentikasi
- Login, register, logout, proteksi halaman

📁 `layouts`

- Komponen tampilan yang dipakai ulang
- Header, navbar, footer

📁 `dashboard`

- Halaman utama setelah login

📁 `todolist`

- Semua fitur CRUD todo

📌 Dengan struktur ini:
**1 file = 1 tanggung jawab**

## Konsep Reusable File

**Apa itu Reusable File?**
Reusable file adalah file yang:

- Ditulis **sekali**
- Digunakan **berkali-kali**

**Contoh:**

- `koneksi.php` → dipakai di banyak file
- `header.php` → dipakai di semua halaman

**Keuntungan:**

- Kode lebih singkat
- Mudah diubah
- Minim error

## 🧠 File koneksi.php

**Fungsi**
Menghubungkan aplikasi PHP dengan database MySQL.
**Isi File** `config/koneksi.php`

```php
<?php
$conn = mysqli_connect("localhost", "root", "", "todolist");

if (!$conn) {
    die("Koneksi database gagal");
}
```

**Penjelasan**

- `localhost` → server database
- `root` → username database
- `""` → password (default lokal)
- `todolist` → nama database

## 🛠️ Membuat Struktur Folder

**Langkah**

1. Masuk ke folder:

   ```bash
   htdocs/TodoListApp
   atau
   laragon/www/TodoListApp
   ```

2. Buat folder:

   ```txt
   assets
   auth
   config
   layouts
   dashboard
   todolist
   ```

3. Buat file kosong:
   - `index.php`
   - `config/koneksi.php`

## 🛠️ Membuat File Koneksi Database

**Langkah**

1. Buka `config/koneksi.php`
2. Tulis kode koneksi (di atas)
3. Simpan file

## 🛠️ Uji Koneksi Database

**Cara 1 — Uji Langsung**
Tambahkan sementara di `koneksi.php`:

```php
echo "Koneksi berhasil";
```

Akses:

```bash
http://localhost/TodoListApp/config/koneksi.php
```

Jika muncul teks → **koneksi sukses**

⚠️ Setelah tes, **hapus echo** tersebut.

**Cara 2 — Uji dari File Lain**

Buat file `test.php` di root:

```php
<?php
include 'config/koneksi.php';
echo "Database terkoneksi";
```

Akses:

```bash
http://localhost/TodoListApp/test.php
```

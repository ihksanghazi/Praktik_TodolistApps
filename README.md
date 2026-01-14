# 🟦 Modul 1 — Pengenalan Project & Setup Lingkungan

**🎯 Tujuan Modul**

Setelah mengikuti modul ini, siswa mampu:

- Memahami **gambaran besar aplikasi TodoList berbasis web**
- Menjelaskan **alur kerja aplikasi**
- Menyiapkan **environment pengembangan PHP + MySQL**
- Menjalankan aplikasi web di **localhost**

## 🧠 Apa Itu Aplikasi Web Berbasis PHP?

**Penjelasan**
Aplikasi web berbasis PHP adalah aplikasi yang:

- Berjalan di **server**
- Diakses melalui **browser**
- Menggunakan **PHP** sebagai bahasa backend
- Menggunakan **database** untuk menyimpan data

📌 Contoh aplikasi web:

- Sistem Login
- Aplikasi Kasir
- Aplikasi TodoList
- Sistem Akademik

**Kenapa PHP?**

- Mudah dipelajari
- Banyak digunakan
- Cocok untuk pemula
- Bisa langsung dijalankan di localhost

## 🧠 Studi Kasus: TodoList App

**Deskripsi Aplikasi**
Aplikasi **TodoList** adalah aplikasi untuk:

- Mencatat daftar tugas
- Menandai tugas yang sudah selesai
- Menghapus tugas
- Setiap user memiliki todo masing-masing

**Fitur Utama**

- Register
- Login
- Dashboard
- Manajemen Todo
- Logout

## 🧠 Alur Aplikasi TodoList

**Flow Aplikasi**

```txt
User membuka website
        ↓
Halaman Login
        ↓
Login berhasil
        ↓
Dashboard
        ↓
Todo List
        ↓
Logout
```

**Penjelasan Singkat**

- **Login** → Autentikasi user
- **Dashboard** → Halaman utama setelah login
- **Todo List** → CRUD data todo
- **Logout** → Keluar dari sistem

## 🧠 Pengenalan Teknologi yang Digunakan

**1️⃣ PHP Native**

- PHP tanpa framework
- Fokus ke logika dasar
- Cocok untuk memahami konsep backend

**2️⃣ MySQL**

- Database untuk menyimpan:
  - Data user
  - Data todo
- Diakses menggunakan PHP

3️⃣ Bootstrap

- Framework CSS
- Membuat tampilan:
  - Lebih rapi
  - Responsif
  - Modern

## 🧠 Tools yang Digunakan

**Tools Wajib**

- **XAMPP / Laragon**
  - Apache (Web Server)
  - MySQL (Database)
- **Browser**
  - Chrome / Firefox
- **Code Editor**
  - VS Code (disarankan)

📌 Catatan:
Disarankan menggunakan **Laragon** karena ringan dan cepat.

## 🛠️ Menjalankan Web Server

**Langkah (Laragon)**

1. Buka **Laragon**
2. Klik **Start All**
3. Pastikan:
   - Apache: ✅ Running
   - MySQL: ✅ Running

**Cek di Browser**
Buka:

```txt
http://localhost
```

Jika muncul halaman Laragon/XAMPP → **berhasil**

## 🛠️ Membuat Folder Project

**Langkah**

1. Masuk ke folder:

   ```txt
   laragon/www/
   ```

   atau

   ```txt
   xampp/htdocs/
   ```

2. Buat folder baru:

   ```txt
   TodoListApp
   ```

3. Masuk ke folder tersebut

## 🛠️ Mengakses Project di Browser

**Langkah**

1. Buka browser
2. Akses:
   ```txt
   http://localhost/TodoListApp
   ```

Jika belum ada file:

- Akan tampil halaman kosong / error directory
- Ini **normal** pada tahap awal

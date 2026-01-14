# 🟦 Modul 2 — Database & Relasi One-to-Many

**🎯 Tujuan Modul**

Setelah menyelesaikan modul ini, siswa mampu:

- Memahami **konsep database relasional**
- Menjelaskan fungsi tabel `users` dan `todolists`
- Menerapkan **relasi One-to-Many**
- Menggunakan **Foreign Key** dengan benar
- Menyiapkan database untuk aplikasi TodoList

## 🧠 Konsep Database

**Apa itu Database?**
Database adalah tempat untuk **menyimpan data secara terstruktur**, sehingga:

- Data mudah dicari
- Data aman
- Data bisa diolah oleh aplikasi

📌 Dalam aplikasi TodoList, database digunakan untuk menyimpan:

- Data user (akun)
- Data todo (daftar tugas)

## 🧠 Tabel users

**Fungsi Tabel** `users`
Tabel `users` menyimpan data akun pengguna.

**Kolom pada tabel** `users`
| Kolom | Fungsi |
| ---------- | ---------------------------- |
| id | Primary Key (identitas user) |
| name | Nama lengkap user |
| username | Username untuk login |
| password | Password (terenkripsi) |
| created_at | Waktu pendaftaran |

**📌 Catatan penting**
`id` bersifat **unik** dan akan digunakan oleh tabel lain.

## 🧠 Tabel todolists

**Fungsi Tabel** `todolists`
Menyimpan daftar todo milik user.

**Kolom pada tabel** `todolists`
| Kolom | Fungsi |
| ---------- | ---------------------- |
| id | Primary Key todo |
| user_id | Relasi ke tabel users |
| title | Isi todo |
| is_done | Status selesai / belum |
| created_at | Waktu pembuatan |

## 🧠 Relasi One-to-Many

**Konsep Relasi**
**One-to-Many** berarti:
Satu data di tabel A bisa memiliki banyak data di tabel B

**Pada Aplikasi TodoList**

```txt
1 user → banyak todo
```

Artinya:

- 1 user bisa punya 10 todo
- 1 todo **hanya milik 1 user**

## 🧠 Foreign Key & ON DELETE CASCADE

**Apa itu Foreign Key?**
Foreign Key adalah **kolom penghubung** antar tabel.
Pada kasus ini:

- `todolists.user_id` → `users.id`

**Fungsi** `ON DELETE CASCADE`

Jika:

- User dihapus
  Maka:
- Semua todo milik user tersebut **ikut terhapus otomatis**

📌 Ini mencegah **orphan data**

## 🛠️ Membuat Database todolist

**Langkah**

1. Buka **phpMyAdmin**
2. Klik menu **SQL**
3. Jalankan perintah:
   ```sql
   CREATE DATABASE IF NOT EXISTS todolist;
   USE todolist;
   ```

✅ Jika berhasil, database `todolist` akan muncul di sidebar kiri.

## 🛠️ Membuat Tabel users

Jalankan SQL berikut:

```sql
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    username VARCHAR(50) NOT NULL UNIQUE,
    password VARCHAR(255) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

**Penjelasan Singkat**

- `AUTO_INCREMENT` → id otomatis bertambah
- `UNIQUE` → username tidak boleh sama
- `VARCHAR(255)` → aman untuk hash password

## 🛠️ Membuat Tabel `todolists` + Relasi

Jalankan SQL berikut:

```sql
CREATE TABLE todolists (
    id INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT NOT NULL,
    title VARCHAR(150) NOT NULL,
    is_done BOOLEAN DEFAULT 0,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,

    CONSTRAINT fk_user_todo
        FOREIGN KEY (user_id)
        REFERENCES users(id)
        ON DELETE CASCADE
);
```

**Penjelasan Penting**

- `user_id` → penghubung ke tabel users
- `FOREIGN` KEY → membuat relasi
- `ON DELETE CASCADE` → hapus otomatis data todo

## 🛠️ Cek Relasi di phpMyAdmin

Langkah

1. Klik tabel `todolists`
2. Masuk tab **Structure**
3. Scroll ke bagian **Relation View**
4. Pastikan:
   - `user_id` terhubung ke `users.id`

Jika terlihat relasi → **berhasil**

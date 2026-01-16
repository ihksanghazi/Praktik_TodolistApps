# 🟦 Modul 11 Delete Todo & Finalisasi Aplikasi

**🎯 Tujuan Modul**

Setelah menyelesaikan modul ini, siswa mampu:

- Menghapus data todo dengan benar
- Memahami **risiko operasi DELETE**
- Menggunakan **konfirmasi sebelum hapus**
- Melakukan **testing end-to-end**
- Menyelesaikan aplikasi TodoList Web secara utuh 🎉

## 🧠 Konsep DELETE pada Database

**Apa itu DELETE?**
DELETE digunakan untuk:

- Menghapus data secara **permanen**
- Data **tidak bisa dikembalikan**

**Contoh**

```sql
DELETE FROM todolists WHERE id = 10;
```

📌 **Peringatan Penting**
DELETE tanpa `WHERE` bisa menghapus **SEMUA DATA**.

## 🧠 Risiko DELETE & Solusinya

**Risiko**

- Salah klik
- Data penting terhapus
- Tidak ada undo

**Solusi UX**

- Konfirmasi sebelum hapus
- Pesan peringatan jelas

## 🛠️ Membuat `delete.php`

**Buat file** `todolist/delete.php`

```php
<?php
include '../config/koneksi.php';

$id = $_GET['id'];

mysqli_query($conn, "
    DELETE FROM todolists
    WHERE id = $id
");

header("Location: index.php");
exit;
```

📌 `id` memastikan hanya **1 todo** yang terhapus.

## 🛠️ Konfirmasi Hapus (JavaScript)

**Edit** `todolist/index.php`
Tambahkan tombol hapus:

```php
<?php if (!$todo['is_done']): ?>
    <a
        href="done.php?id=<?= $todo['id']; ?>"
        class="btn btn-sm btn-warning"
        title="Tandai selesai">
        ✔
    </a>
<?php endif; ?>

// letakkan kode dibawah ini

<a href="delete.php?id=<?= $todo['id']; ?>"
   class="btn btn-sm btn-danger"
   onclick="return confirm('Hapus todo ini?')"
   title="Hapus">
   ✖
</a>
```

📌 Jika user klik **Cancel**, proses DELETE dibatalkan.

## 🛠️ Uji Fitur Delete

**Langkah**

1. Tambahkan beberapa todo
2. Klik tombol hapus
3. Pilih:
   - **Cancel** → todo tetap ada
   - **OK** → todo terhapus

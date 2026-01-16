# 🟦 Modul 10 Update Status Todo (Done)

**🎯 Tujuan Modul**

Setelah menyelesaikan modul ini, siswa mampu:

- Mengubah status todo menjadi **selesai**
- Memahami **query UPDATE**
- Menggunakan **parameter** `id`
- Memberikan **feedback visual** pada todo yang selesai

## 🧠 Konsep UPDATE pada Database

**Apa itu UPDATE?**
UPDATE digunakan untuk:

- Mengubah data yang sudah ada
- Bukan menambah data baru

**Contoh Kasus**
Mengubah status todo:

```txt
Belum selesai → Selesai
```

## 🧠 Status is_done

**Fungsi Kolom** `is_done`
| Nilai | Arti |
| ----- | ------------- |
| 0 | Belum selesai |
| 1 | Selesai |

📌 Status ini yang akan kita ubah menggunakan UPDATE.

## 🧠 Parameter id

**Kenapa Pakai** `id`?

- Setiap todo punya `id` unik
- UPDATE harus tepat sasaran

Contoh:

```php
?id=5
```

📌 Artinya: ubah todo dengan `id = 5`.

## 🧠 UX: Feedback Visual

**Kenapa Perlu Feedback Visual?**
User perlu tahu:

- Todo sudah selesai
- Tidak perlu ditebak

**Solusi**

- Todo dicoret
- Warna abu-abu

## Tombol “Tandai Selesai”

**Edit** `todolist/index.php`

```php
<?= htmlspecialchars($todo['title']); ?>
// letakkan kodenya dibawah htmlspecialchars
<div>
    <?php if (!$todo['is_done']): ?>
        <a
            href="done.php?id=<?= $todo['id']; ?>"
            class="btn btn-sm btn-warning"
            title="Tandai selesai">
            ✔
        </a>
    <?php endif; ?>
</div>
```

📌 Tombol ini akan mengirim `id` todo ke `done.php`.

## 🛠️ Membuat done.php

**Buat file** `todolist/done.php`

```php
<?php
include '../config/koneksi.php';

$id = $_GET['id'];

mysqli_query($conn, "
    UPDATE todolists
    SET is_done = 1
    WHERE id = $id
");

header("Location: index.php");
exit;
```

## 🛠️ Styling Todo Selesai

**Tambahkan kode ini di** `assets/css/style.css`

```css
.todo-done {
  text-decoration: line-through;
  color: gray;
}
```

## 🛠️ Terapkan Styling di List Todo

**Edit bagian list di** `todolist/index.php`

Bungkus `htmlspecialchars` dengan tag `span` beserta attributnya:

```php
<span class="<?= $todo['is_done'] ? 'todo-done' : ''; ?>">
    <?= htmlspecialchars($todo['title']); ?>
</span>
```

📌 Jika `is_done = 1`, class `todo-done` akan aktif.

## 🛠️ Uji Update Status Todo

**Langkah**

1. Tambahkan beberapa todo
2. Klik tombol ✔
3. Pastikan:
   - Todo dicoret
   - Data di database berubah (`is_done = 1`)

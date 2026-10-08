# Jawaban Refleksi - Check Yourself (Lab 04)

> Dokumen ini berisi jawaban refleksi untuk persiapan evaluasi dan *review* AFL 1.

---

### 1. A Text inside a Row overflows. Which part of "constraints go down, sizes go up, parent sets position" was violated, and by which widget?

**Jawaban:**
Bagian **"constraints go down"** dilanggar oleh **`Row`**. `Row` memberikan batasan lebar horizontal tak terbatas (*unbounded width*) kepada *child*-nya, sehingga `Text` mengukur dirinya sendiri tanpa batas hingga melebihi lebar layar.

---

### 2. Why is adding `width: 150` to the text the wrong fix, even if the stripes disappear?

**Jawaban:**
Menggunakan nilai *hard-coded* seperti `width: 150` hanya menyembunyikan masalah sementara dan memindahkan bug ke ukuran layar lain. Saat aplikasi dibuka di layar yang lebih kecil (misalnya 320 dp) atau saat pengguna memperbesar ukuran teks sistem (*accessibility font*), garis *overflow* akan muncul kembali.

---

### 3. You fixed the landscape overflow by wrapping everything in a `SingleChildScrollView` and setting `shrinkWrap: true` on the list. Which test fails, and why does it matter once the data comes from an API?

**Jawaban:**
Tes ke-7 (**500 items — built lazily, scrolled hard**) akan gagal. `shrinkWrap: true` memaksa `ListView` membuat seluruh 500 *widget* sekaligus di memori saat pertama kali dimuat (*eager building*). Ketika data diambil dari API dalam jumlah besar, hal ini akan memicu *lag* parah, menghabiskan RAM, hingga menyebabkan aplikasi *crash*.

---

### 4. Why does the tablet layout use `LayoutBuilder` rather than `MediaQuery.sizeOf(context)`?

**Jawaban:**
`LayoutBuilder` mengukur area batas (*constraints*) yang benar-benar tersedia untuk *widget* tersebut di dalam hierarki UI, sedangkan `MediaQuery.sizeOf(context)` selalu mengambil ukuran total dari seluruh layar perangkat. Menggunakan `LayoutBuilder` membuat *widget* tetap adaptif jika kelak ditempatkan di dalam *split-screen*, panel samping (*sidebar*), atau *dialog*.

---

### 5. The empty-data crash was not a layout error. Why does it belong in a layout lab anyway?

**Jawaban:**
Tampilan *empty state* adalah bagian tak terpisahkan dari tata letak yang tahan banting (*unbreakable layout*). Sebuah tata letak responsif tidak hanya harus bertahan pada perbedaan ukuran layar, tetapi juga harus mampu menangani seluruh kondisi batas data—mulai dari 0 item hingga 500 item—tanpa merusak struktur UI atau memicu *crash*.
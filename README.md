## Pertanyaan dan Penjelasan Desain

Berikut adalah penjelasan untuk beberapa keputusan teknis yang diambil selama pengembangan.

### a. Keputusan `grid-cols` dan `gap` di Tiap Breakpoint

Tata letak galeri foto dirancang dengan pendekatan **mobile-first** untuk memberikan pengalaman pengguna terbaik di semua ukuran layar.

* **Mobile (Default): `grid-cols-2` dan `gap-1`**
    Di layar kecil, saya memilih **2 kolom** (`grid-cols-2`). Ini adalah kompromi yang baik antara menampilkan beberapa gambar sekaligus dan menjaga ukuran tiap gambar agar tetap jelas terlihat. Menggunakan 1 kolom akan memakan terlalu banyak ruang vertikal, sementara 3 kolom akan membuat gambar terlalu kecil. **`gap-1`** (jarak yang sangat kecil) dipilih untuk menciptakan efek galeri yang padat dan modern.

* **Tablet & Desktop (`sm:grid-cols-3` dan `sm:gap-4`)**
    Begitu layar mencapai breakpoint `sm` (640px), tata letak berubah menjadi **3 kolom** (`sm:grid-cols-3`). Ini memanfaatkan ruang horizontal yang lebih luas, memungkinkan pengguna melihat lebih banyak konten secara sekilas. Jarak antar gambar juga diperbesar menjadi **`gap-4`** untuk memberikan "ruang bernapas" pada desain, membuatnya terlihat lebih rapi dan tidak sesak di layar yang lebih besar.

### b. Pemanfaatan Utility Responsive untuk Layout Mobile

Saya memanfaatkan utility responsive Tailwind untuk mengatasi masalah tata letak di bagian profil.

* **Masalah di Mobile**: Di layar besar, foto profil dan info (username, bio, statistik) idealnya berdampingan. Jika tata letak ini dipaksakan di mobile, konten akan menjadi sangat sempit dan sulit dibaca.

* **Solusi dengan Pendekatan Mobile-First**:
    1.  **Desain Awal untuk Mobile**: Struktur HTML dibuat agar secara *default* sudah optimal untuk mobile. Kontainer utama profil (`<section>`) diberi kelas `flex flex-wrap`. Masing-masing `div` untuk gambar dan info diberi lebar penuh (`w-full`). Ini secara otomatis membuat mereka tersusun **vertikal (atas-bawah)**. Saya juga menambahkan `justify-center` agar foto profil berada di tengah.

    2.  **Adaptasi untuk Layar Besar**: Untuk layar yang lebih besar (`sm:` dan seterusnya), saya menambahkan kelas berawalan `sm:` untuk mengubah tata letak. `div` untuk gambar diubah menjadi `sm:w-1/3` dan `div` untuk info menjadi `sm:w-2/3`. Ini membuat mereka menjadi **berdampingan (kiri-kanan)**.

Dengan cara ini, layout sudah benar di mobile sejak awal, dan kita hanya menambahkan "penyesuaian" untuk layar yang lebih besar.

### c. Trade-off: Utility Classes vs. Komponen CSS

Keputusan antara menggunakan banyak utility class langsung di HTML atau membuat komponen CSS sendiri adalah inti dari filosofi Tailwind.

* **Menggunakan Banyak Utility Classes (Cara Tailwind)**
    * **Kelebihan**: Kecepatan prototyping sangat tinggi, perubahan terisolasi, dan ukuran file CSS final sangat kecil.
    * **Kekurangan**: HTML bisa terlihat "kotor" atau berantakan, dan untuk elemen berulang (misal: tombol), kita harus menulis ulang rangkaian kelas yang sama.

* **Membuat Komponen CSS Sendiri (Cara Tradisional/@apply)**
    * **Kelebihan**: HTML terlihat lebih bersih dan semantik (misal: `<button class="btn-primary">`), dan komponen mudah digunakan kembali.
    * **Kekurangan**: File CSS bisa membengkak, butuh disiplin penamaan yang ketat (seperti BEM), dan memperlambat alur kerja karena harus bolak-balik antara file HTML dan CSS.

**Kesimpulan Trade-off**: Saya memilih pendekatan **utility-first** untuk proyek ini karena kecepatan dan kemudahan dalam membangun desain yang spesifik tanpa perlu membuat file CSS kustom.

# Pemograman-web-uts
# Eksperimen Keamanan Web: SQL Injection Bypass

Project ini dibuat untuk memenuhi tugas **UTS Mata Kuliah Pemrograman Web** (2026).

## Data Mahasiswa
* **Nama:** Den Fahmi Satria
* **NIM:** 312410523[cite: 1]
* **Kelas:** I241E[cite: 1]

## Deskripsi Project
Project ini adalah simulasi sistem login sederhana menggunakan PHP Native untuk mendemonstrasikan kerentanan keamanan **SQL Injection** dan cara mitigasinya menggunakan **Prepared Statements**[cite: 1].

## Isi Repository
* `index.php`: File utama yang berisi form login dan logika autentikasi (Mode Vulnerable & Mode Secure)[cite: 1].
* `db_uts.sql`: Struktur database dan data contoh untuk menjalankan eksperimen.

## Cara Menjalankan Eksperimen
1. Import file `db_uts.sql` ke phpMyAdmin kamu.
2. Letakkan file `index.php` di dalam folder `htdocs/uts_fahmi`.
3. Akses melalui browser di `localhost/uts_fahmi`.
4. Cobalah login menggunakan teknik bypass yang ditemukan selama eksperimen:
   - Input: `admin' #` atau `' OR 1=1 #`[cite: 1].

## Kesimpulan Eksperimen
Eksperimen ini membuktikan bahwa penggabungan input user secara langsung ke dalam query SQL sangat berbahaya karena dapat dimanipulasi menggunakan karakter komentar (`#` atau `-- `) untuk melewati validasi password[cite: 1]. Solusi terbaik adalah selalu menggunakan *Prepared Statements*.

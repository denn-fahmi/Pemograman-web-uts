# Pemograman-web-uts
# Eksperimen Keamanan Web: SQL Injection Bypass

Project ini dibuat untuk memenuhi tugas **UTS Mata Kuliah Pemrograman Web** (2026). <p>

* **Nama:** Den Fahmi Satria
* **NIM:** 312410523
* **Kelas:** I241E

## Deskripsi Project
Project ini adalah simulasi sistem login sederhana menggunakan PHP Native untuk mendemonstrasikan kerentanan keamanan **SQL Injection** dan cara mitigasinya menggunakan **Prepared Statements**.

## Isi Repository
* `index.php`: File utama yang berisi form login dan logika autentikasi (Mode Vulnerable & Mode Secure).
```
// CONTOH KODE YANG SUDAH DIMITIGASI TOTAL
if (isset($_POST['login'])) {
    $username = $_POST['username'];
    $password = $_POST['password'];

    try {
        // Menggunakan Prepared Statements (Mode B)
        $stmt = $conn->prepare("SELECT password FROM users WHERE username = ?");
        $stmt->bind_param("s", $username);
        $stmt->execute();
        $result = $stmt->get_result();

        if ($user = $result->fetch_assoc()) {
            // Verifikasi password yang sudah di-hash
            if (password_verify($password, $user['password'])) {
                $message = "Login Sukses!";
            } else {
                $message = "Password Salah!";
            }
        } else {
            $message = "User tidak ditemukan!";
        }
    } catch (Exception $e) {
        // Menampilkan pesan umum tanpa membocorkan info server
        $message = "Terjadi kesalahan pada sistem. Silakan coba lagi.";
    }
}
```
* `db_uts.sql`: code untuk database.
```
CREATE TABLE users (
    id INT PRIMARY KEY AUTO_INCREMENT,
    username VARCHAR(50),
    password VARCHAR(50)
);

INSERT INTO users (username, password) VALUES ('admin', 'rahasia123');
## Cara Menjalankan Eksperimen
1. `db_uts.sql` ke phpMyAdmin.
2. Letakkan file `index.php` di dalam folder `htdocs/uts_fahmi`.
3. Akses melalui browser di `localhost/uts_fahmi`.
4. Cobalah login menggunakan teknik bypass yang ditemukan selama eksperimen:
   - Input: `admin' #` atau `' OR 1=1 #`.
```
## Kesimpulan Eksperimen
Eksperimen ini membuktikan bahwa penggabungan input user secara langsung ke dalam query SQL sangat berbahaya karena dapat dimanipulasi menggunakan karakter komentar (`#` atau `-- `) untuk melewati validasi password. Solusi terbaik adalah selalu menggunakan *Prepared Statements*.

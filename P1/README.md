# Implementasi Kriptografi AES-128 untuk Pengamanan File Berbasis Web (Studi Kasus: SMP Yapipa)

![License](https://img.shields.io/badge/license-MIT-blue.svg)
![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)

Repositori ini berisi kode sumber untuk aplikasi pengamanan file soal ujian sekolah berbasis web menggunakan algoritme **Advanced Encryption Standard (AES) 128-bit**. Studi kasus dilakukan untuk meningkatkan keamanan data dan mencegah kebocoran dokumen konfidensial di SMP Yapipa.

## 📌 Latar Belakang
Proses digitalisasi dokumen soal ujian sekolah memiliki risiko tinggi terhadap kebocoran data dan akses ilegal jika hanya disimpan dalam folder biasa. Dokumen-dokumen ini bersifat rahasia dan konfidensial. Sistem ini dirancang untuk memberikan lapisan keamanan yang kuat namun tetap ringan saat dijalankan di server sekolah.

## 🔒 Fitur Utama
* **Sistem Autentikasi:** Log-in pengguna untuk membatasi hak akses.
* **Enkripsi & Dekripsi:** Mengamankan file saat di-upload dan mengembalikan file ke format asli saat di-download menggunakan kunci simetris AES-128 (10 putaran transformasi).
* **Multi-format Support:** Mendukung berbagai format dokumen sekolah seperti `PDF`, `XLS`, `DOC`, dan `TXT`.
* **Manajemen File:** Antarmuka berbasis web yang ramah pengguna, dapat diakses langsung melalui browser.

## 🚀 Performa & Analisis Keamanan
Berdasarkan hasil pengujian sistem pada file berukuran di bawah 3MB:
* **Rata-rata Waktu Enkripsi:** 1,31 detik
* **Rata-rata Waktu Dekripsi:** 1,55 detik
* **Integritas Data:** File yang diproses dijamin tidak rusak setelah didekripsi.
* **Keamanan Kunci:** Perlindungan maksimal yang mengharuskan kecocokan kunci 100% untuk membuka *ciphertext*.

## 🛠️ Teknologi yang Digunakan
* **Web Environment:** PHP / JavaScript (Sesuaikan dengan stack asli proyekmu)
* **Database:** MySQL / phpMyAdmin (Sesuaikan dengan stack asli proyekmu)
* **Algoritme Kriptografi:** AES-128 (Symmetric Key)

## 👥 Anggota Kelompok (Kelompok 4)
* Kris Ardani (2402059)
* Rizqi Mubarok (2402071)
* Shinta Qurrota Aini (2402074)

---
*Catatan: Proyek ini dikembangkan berdasarkan penelitian/jurnal oleh Isra Priambudi & Mufti (Teknologi Informasi, Universitas Budi Luhur).*

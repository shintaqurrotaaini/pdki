# 🌐 Debian 12 Remote Access Configuration: Telnet & SSH

Proyek ini mendokumentasikan langkah-langkah instalasi, kustomisasi port, serta analisis keamanan layanan *Remote Access* menggunakan protokol **Telnet Server** dan **SSH Server** di lingkungan sistem operasi **Debian 12 (Bookworm)** melalui VM Oracle VirtualBox.

Dokumen ini juga merangkum berbagai kendala teknis jaringan yang sering ditemui pada Debian modern beserta solusi pemecahannya.

---

## 🛠️ Alat dan Bahan
- **Host OS:** Windows 10/11
- **Guest OS:** Debian 12 Server (CLI)
- **Hypervisor:** Oracle VM VirtualBox
- **Remote Client:** PuTTY

---

## 🚀 Langkah Implementasi & Konfigurasi

### 1. Konfigurasi Jaringan (Bridged Mode)
Untuk menghubungkan Host (Windows) dan Guest (Debian), pastikan Network Adapter di VirtualBox diubah dari **NAT** menjadi **Bridged Adapter** yang mengarah ke kartu jaringan Wi-Fi/Ethernet aktif.

Minta alokasi IP Address baru ke DHCP Server lokal:
```bash
dhclient -v enp0s3

Verifikasi IP Address yang didapatkan:
ip a
Pastikan mendapatkan IP valid satu segmen dengan Host (Contoh: 10.232.10.129).2.

2. Instalasi Telnet Server (Standalone)
Karena manajemen Debian 12 sangat ketat terhadap paket superserver lama openbsd-inetd (sering mengalami blank config dan Connection refused), maka digunakan paket standalone telnetd-ssl:
# Hapus total paket inetd jika terlanjur macet
apt-get remove --purge telnetd openbsd-inetd -y

# Instalasi Telnet Standalone
apt-get install telnetd-ssl -y
Uji coba koneksi lokal:Bashtelnet localhost

3. Pembuatan User BaruBuat user biasa non-root untuk pengujian hak akses remote client:
Bashadduser user1
adduser user2

4. Instalasi & Kustomisasi Port SSH ServerInstalasi layanan OpenSSH Server:
apt-get install openssh-server -y
Buka konfigurasi utama untuk mengubah port default 22 menjadi port kustom 354, serta memberikan izin login root:
nano /etc/ssh/sshd_config
Tambahkan/sesuaikan baris berikut di dalam file:
Port 354
PermitRootLogin yes
Restart layanan SSH untuk menerapkan konfigurasi baru:
systemctl restart ssh

💻 Pengujian Jarak Jauh (Remote Client)
Menggunakan PuTTY (Windows)
1. Buka aplikasi PuTTY
2. Masukkan IP Address Debian Server (cth: 10.232.10.129).
3. Ubah kolom Port menjadi 354.
4. Pilih Connection type: SSH.
5. Klik Open, terima Security Alert, lalu login menggunakan user1.

🔍 Analisis & Pembuktian Sistem
Untuk memverifikasi koneksi aktif dari pihak luar yang sedang meremote server, jalankan perintah berikut di terminal utama Debian:who
Contoh Output:
root     tty1         Jun 23 10:41
user1    pts/0        Jun 23 11:16 (10.232.10.130)
tty1: Sesi administrator (root) yang sedang aktif secara lokal di VirtualBox.
pts/0: Sesi remote (user1) yang berhasil masuk via SSH menggunakan PuTTY dari IP komputer Windows (10.232.10.130).

📝 Kesimpulan Security
Meskipun Telnet berhasil diimplementasikan, protokol ini tidak direkomendasikan untuk jaringan publik karena mengirimkan kredensial dalam bentuk plaintext. Penggunaan SSH dengan teknik Port Switching (mengubah port default) memberikan proteksi enkripsi yang jauh lebih aman dari serangan brute force otomatis.

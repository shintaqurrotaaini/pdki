# 🛡️ Implementasi IDS Suricata pada Linux Debian 11

[![Suricata](https://img.shields.io/badge/IDS%2FIPS-Suricata-orange?style=flat-for-the-badge)](https://suricata.io/)
[![OS](https://img.shields.io/badge/OS-Debian%2011-blue?style=flat-for-the-badge&logo=debian)](https://www.debian.org/)
[![Environment](https://img.shields.io/badge/Environment-VirtualBox-vienna?style=flat-for-the-badge&logo=virtualbox)](https://www.virtualbox.org/)

Proyek ini mendokumentasikan langkah-langkah implementasi **Intrusion Detection System (IDS)** menggunakan **Suricata** pada lingkungan jaringan virtual terisolasi (*Internal Network*). Sistem dikonfigurasi untuk mendeteksi aktivitas mencurigakan seperti serangan **ICMP (Ping)** dan **TCP SYN Port Scanning**.

---

## 🗺️ Topologi Jaringan Virtual

Praktikum ini melibatkan dua buah *Virtual Machine* (VM) Linux Debian yang terhubung dalam satu segmen jaringan internal rahasia:

| Nama VM | Peran | Alamat IP (Statis) | Interface | Mode VirtualBox |
| :--- | :--- | :--- | :--- | :--- |
| **Debian 1** | Target Server / IDS | `192.168.10.1/24` | `enp0s3` | Internal Network (`intnet`) + *Allow All* |
| **Debian 2** | Attacker / Penyerang | `192.168.10.2/24` | `enp0s3` | Internal Network (`intnet`) + *Allow All* |

> ⚠️ **Penting:** *Promiscuous Mode* pada pengaturan Network VirtualBox wajib diatur ke **Allow All** agar Suricata dapat mengendus paket data secara transparan tanpa filternya di layer hardware.

---

## 🛠️ Langkah Konfigurasi (Debian 1 - IDS Server)

### 1. Registrasi Aturan Kustom
Buka konfigurasi utama Suricata:
```bash
sudo nano /etc/suricata/suricata.yaml

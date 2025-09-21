# Basic Firewall with iptables

Halo!👋 Gua bagas dan ini small project gue buat nunjukin cara buat **firewall sederhana** di Linux menggunakan **iptables**.  

Analogi gampang: firewall itu kayak **satpam rumah** yang cek siapa yang boleh masuk, siapa yang nggak.

---

## 🎯 Tujuan
- Membuat firewall dasar di Linux.  
- Membatasi port yang boleh diakses.  
- Tes menggunakan Nmap untuk buktiin rules bekerja(host Windows sebagai scanner) 
---

## Tools
- Kali Linux (target)
- Windows (Scanner/testing)
- `iptables` (di Kali) 
- `nmap` (di Windows)

---

## Step-by-step

1. **Update sistem & cek iptables**
```bash
sudo apt update && sudo apt upgrade -y
sudo iptables -V
```
2. **Set default policy → block semua incoming**
```bash
sudo iptables -P INPUT DROP
sudo iptables -P FORWARD DROP
sudo iptables -P OUTPUT ACCEPT
```
3. **Nmap BEFORE (dari Windows host)**
```bash
nmap -sT 192.168.56.104
```
<p align="center">
  <img src="images/iptables-after.png" alt="iptables after" width="700">
</p> 
4. **Buka akses SSH (biar nggak ngelock diri sendiri)**
```bash
sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT
```
5.**Buka HTTP & HTTPS (untuk web server)**
```bash
sudo iptables -A INPUT -p tcp --dport 80 -j ACCEPT
sudo iptables -A INPUT -p tcp --dport 443 -j ACCEPT
```
6.**Nmap AFTER (dari Windows host)**
```bash
nmap -sT 192.168.56.104
```
7.**Save rules supaya tetap ada setelah reboot**
```bash
sudo apt install iptables-persistent -y
sudo iptables-save > /etc/iptables/rules.v4
```
Intinya: gue nge-set firewall dasar: semua incoming diblok kecuali port penting (SSH & HTTP). Setelah diterapkan, scanner dari host (Windows) nggak bisa menemukan port FTP lagi — bukti firewall bekerja. Simple tapi efektif untuk baseline security.

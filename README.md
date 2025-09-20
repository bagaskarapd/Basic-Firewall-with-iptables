# Basic Firewall with iptables

Halo!👋 Gua bagas dan ini small project gue buat nunjukin cara buat **firewall sederhana** di Linux menggunakan **iptables**.  

Analogi gampang: firewall itu kayak **satpam rumah** yang cek siapa yang boleh masuk, siapa yang nggak.

---

## 🎯 Tujuan
- Membuat firewall dasar di Linux.  
- Membatasi port yang boleh diakses.  
- Tes menggunakan Nmap untuk buktiin rules bekerja.  
---

## Tools
- Kali Linux
- `iptables`  
- `nmap` untuk testing

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
3.**Buka akses SSH (biar nggak ngelock diri sendiri)**
```bash
sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT
```
4.**Buka HTTP & HTTPS (untuk web server)**
```bash
sudo iptables -A INPUT -p tcp --dport 80 -j ACCEPT
sudo iptables -A INPUT -p tcp --dport 443 -j ACCEPT
```
5.**Save rules supaya tetap ada setelah reboot**
```bash
sudo apt install iptables-persistent -y
sudo iptables-save > /etc/iptables/rules.v4
```
6.**Tes pake Nmap**
```bash
nmap -sT <IP_SERVER>
```

# Basic Firewall with iptables

Halo!👋 Gua bagas dan ini small project gue buat nunjukin cara buat **firewall sederhana** di Linux menggunakan **iptables**.  

Analogi gampang: firewall itu kayak **satpam rumah** — dia cek siapa yang boleh masuk, siapa yang nggak.

---

## 🎯 Tujuan
- Membuat firewall dasar di Linux.  
- Membatasi port yang boleh diakses.  
- Tes menggunakan Nmap untuk buktiin rules bekerja.  
---

## Tools
- Linux (Ubuntu)  
- `iptables`  
- `nmap` untuk testing

---

## Step-by-step

1. **Update sistem & cek iptables**
```bash
sudo apt update && sudo apt upgrade -y
sudo iptables -V

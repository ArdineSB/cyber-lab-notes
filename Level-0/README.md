# Level 0 – TCP 3-Way Handshake (step-by-step for absolute beginners)

**Date**  : 29 September 2025  
**Lab**   : Home-lab (VirtualBox – NO cable needed)  
**Attacker** : Parrot OS VM (192.168.56.101)  
**Target**  : Metasploitable 2 VM (192.168.56.102)

---

## A. What you will do (big picture)
1. Install two virtual computers inside your laptop.  
2. Make them talk to each other without internet.  
3. Scan one computer with **nmap**.  
4. Watch the first “hand-shake” of every TCP connection in **Wireshark**.  
5. Save the proof → upload to GitHub → show off.

---

## B. Prepare your Windows host (10 minutes)
1. Download & install **VirtualBox** (next-next finish).  
2. Download:
   - Parrot OS ISO (≈ 2 GB)  
   - Metasploitable 2 zip (≈ 800 MB) – extract → you get `Metasploitable.vmdk`  
3. Create a folder `D:\Labs\` (any drive) to keep files tidy.

---

## C. Build a “private street” inside your laptop
VirtualBox → File → Preferences → Network → Host-Only → **+** (add).  
Leave everything default → OK.  
Now you have a private road named `192.168.56.x` that only VMs can use.

---

## D. Create the TARGET (Metasploitable)
VirtualBox → New:
- Name: `Metasploitable`  
- Type: Linux → Ubuntu 64-bit  
- RAM: **512 MB** (lightweight)  
- Hard-disk: **Use existing** → choose `Metasploitable.vmdk`  
Settings → Network → Adapter 1 → **Host-Only** → OK.

---

## E. Create the ATTACKER (Parrot OS)
VirtualBox → New:
- Name: `ParrotOS`  
- Type: Linux → Ubuntu 64-bit  
- RAM: **4096 MB** (4 GB)  
- Hard-disk: **Create new** → 20 GB, VDI, **Dynamically allocated**  
Settings → Storage → Empty → choose Parrot ISO  
Settings → Network → Adapter 1 → **Host-Only** → OK.

Start Parrot VM → install (choose language, username, password) → reboot → login.

---

## F. Check IP addresses (both VMs)
Metasploitable login: `msfadmin` / `msfadmin`  
Type:  
```
ifconfig
```  
Look for `inet addr:192.168.56.???` (example `192.168.56.102`)  

Parrot OS open terminal:  
```
ip a
```  
You should see `192.168.56.101`  

Test “can they talk?”  
In Parrot:
```
ping 192.168.56.102
```
Stop with `Ctrl+C` when you see replies.

---

## G. Run nmap (port scanner)
Still in Parrot terminal:
```
nmap 192.168.56.102
```
Wait → you will see a list of open ports.  
Save the result:
```
nmap 192.168.56.102 > level0-nmap.txt
```

---

## H. Capture the 3-way handshake with Wireshark
1. Open Wireshark (Applications → Sniffing & Spoofing → Wireshark).  
2. Click the green **▶** on interface `enp0s3` → starts capturing.  
3. **While capture is running**, open a **new terminal** and repeat:
   ```
   nmap 192.168.56.102
   ```
4. Back to Wireshark → click red **■** to stop.  
5. Type `tcp` in the display filter box → press Enter.  
6. Find **three packets in a row** that show:  
   ```
   [SYN]  →  [SYN, ACK]  →  [ACK]
   ```
7. Screenshot that part → save as `syn-handshake.png`.  
8. Save the whole capture: File → Save As → `level0.pcapng`.

---

## I. Evidence files
| Evidence | File |
|----------|------|
| nmap result | [`level0-nmap.txt`](level0-nmap.txt) |
| handshake screenshot | [`syn-handshake.png`](syn-handshake.png) |
| raw capture | [`level0.pcapng`](level0.pcapng) |

---

## J. What I learned
- I can build a mini-network inside my laptop without extra hardware.  
- Every TCP connection starts with a “hello” sequence (3-way handshake).  
- I can save proof of my work and put it on GitHub for portfolio.

---

## K. Next
Level 1 – Build a firewall + IDS with **pfSense** and **Suricata**.

Back to [root README](../README.md)

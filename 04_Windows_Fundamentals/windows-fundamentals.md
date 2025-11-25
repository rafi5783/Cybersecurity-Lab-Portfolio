# Windows Fundamentals

## 1. Introduction
While Linux powers much of the server world, Windows remains the dominant OS for corporate endpoints and Active Directory environments. A strong grasp of Windows internals is critical for both offensive (Red Team) and defensive (Blue Team) security operations. This module explores the core architecture, management interfaces, and security controls of the Windows operating system.

---

## 2. File System & Permissions (NTFS)
Unlike the Linux "Everything is a file" philosophy, Windows uses a drive-letter system (C:\, D:\) and relies heavily on the **New Technology File System (NTFS)**.

### The Structure
* **Roots:** Physical drives are assigned letters. `C:\` is traditionally the system drive.
* **User Profiles:** Located in `C:\Users\`. Contains individual user settings, `AppData` (hidden config files), and Documents.
* **System Files:** `C:\Windows\System32` houses core OS files. **Note:** On 64-bit systems, `System32` contains 64-bit files, while `SysWOW64` contains 32-bit files (a common point of confusion).

### Permissions (DACLs & SACLs)
Windows permissions are more granular than Linux `rwx`.
* **DACL (Discretionary Access Control List):** Determines *who* can access a file and *what* they can do (Read, Write, Execute, Modify, Full Control).
* **SACL (System Access Control List):** Used for auditing access (logging who touched a file).
* **Inheritance:** Files usually inherit permissions from their parent folder.
* **Tooling:**
    * GUI: Right-click -> Properties -> Security.
    * CLI: `icacls` (The Windows equivalent of `chmod`).

> **Security Note:** NTFS supports **Alternate Data Streams (ADS)**. This allows a file to hide data "behind" it without changing the file size. Hackers often use ADS to hide malicious code.

---

## 3. The Windows Registry
The Registry is a hierarchical database that stores low-level settings for the OS and applications. It is effectively the "blueprint" of the system.

### Structure
The Registry is organized into **Hives** (top-level folders), Keys (sub-folders), and Values (data).
* **HKLM (HKEY_LOCAL_MACHINE):** Settings for the local computer (boot config, installed software). Critical for forensics.
* **HKCU (HKEY_CURRENT_USER):** Settings specific to the currently logged-in user.
* **HKCR (HKEY_CLASSES_ROOT):** File association information (what program opens .pdf?).

### Security Context
Malware frequently targets the registry to achieve **Persistence** (starting automatically when the computer turns on).
* **Common Attack Path:** `HKLM\Software\Microsoft\Windows\CurrentVersion\Run`

---

## 4. Processes and Services
Understanding what is running on the system is the first step in identifying a compromise.

### Processes
An instance of an executable program.
* **Task Manager:** The basic tool to view CPU/RAM usage.
* **Process Hierarchy:** Processes can spawn "Child Processes." A Word document spawning a PowerShell terminal is a major red flag.

### Services
Programs that run in the background without user interaction (similar to Linux Daemons).
* **SCM (Service Control Manager):** Manages starting/stopping services.
* **Tooling:** `services.msc` or `Get-Service` (PowerShell).
* **Svchost.exe:** You will see many of these. They are "host" processes for DLL-based services. If one `svchost.exe` crashes, it doesn't take down the whole system.

---

## 5. Monitoring & Logging (Event Viewer)
Windows has a robust logging system centralized in the **Event Viewer**.

* **Application Logs:** Errors or events from installed software.
* **System Logs:** OS-level events (driver failures, reboot times).
* **Security Logs:** The most critical for security. Tracks logins, privilege escalation, and file access.

### Critical Event IDs to Watch
* **4624:** Successful Logon.
* **4625:** Failed Logon (Multiple rapid failures indicate Brute Force).
* **4720:** A user account was created.

---

## 6. Command Line & PowerShell
Modern Windows administration relies on two command-line interfaces.

### CMD (Command Prompt)
The legacy CLI. Useful for quick, basic tasks.
* `dir`: List files.
* `ipconfig`: Network details.
* `net user`: Manage users.
* `whoami`: Display current user context.

### PowerShell
A powerful, object-oriented scripting language and shell. It is the industry standard for Windows automation.
* **Verb-Noun Syntax:** Commands are structured as Action-Object (e.g., `Get-Process`, `New-Item`, `Set-Content`).
* **Piping:** Like Linux, you can pipe outputs, but in PowerShell, you pipe *objects*, not just text.
* **Execution Policy:** A safety feature that determines if scripts can run. (Often bypassed by attackers using `-ExecutionPolicy Bypass`).

```powershell
# Example: Check for a specific process and get its ID
Get-Process | Where-Object {$_.Name -eq "notepad"} | Select-Object Id, Path

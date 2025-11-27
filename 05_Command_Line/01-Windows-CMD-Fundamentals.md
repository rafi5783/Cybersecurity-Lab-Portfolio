# Windows Command Line (CMD) Fundamentals

## 1. System Information
Basic commands to understand the host machine.
* `whoami`: Displays the current logged-in user.
* `hostname`: Prints the computer name.
* `systeminfo`: Detailed configuration (OS version, RAM, Hotfixes).
* `ver`: Displays the Windows version.

## 2. File System Navigation
* `dir`: Lists files in the current directory.
    * `dir /a`: View hidden files.
    * `dir /s`: List files in subdirectories (recursive).
* `cd <folder>`: Change directory.
    * `cd ..`: Go back one folder.
    * `cd \`: Go to the root of the drive (C:\).
* `tree`: Visualizes the directory structure.

## 3. File Manipulation
* `type file.txt`: Displays the contents of a file (similar to `cat` in Linux).
* `copy source.txt dest.txt`: Copies a file.
* `move source.txt dest.txt`: Moves or renames a file.
* `del file.txt`: Deletes a file.
* `mkdir folder_name`: Creates a new folder.
* `rmdir folder_name`: Deletes a folder (must be empty).

## 4. Networking Utilities
* `ipconfig`: Shows IP address, Subnet Mask, and Gateway.
    * `ipconfig /all`: Shows full details including MAC address and DNS.
* `ping <ip>`: Tests connectivity to a target.
* `tracert <ip>`: Traces the path (hops) packets take to reach a destination.
* `netstat`: Displays active network connections.
    * `netstat -a`: Show all active ports.
    * `netstat -b`: Show which application is using the port (requires Admin).
    * `netstat -n`: Display addresses and port numbers numerically.
    * `netstat -ano`: Useful for matching a port to a Process ID (PID).
* `nslookup <domain>`: Query DNS records for a domain.

## 5. User & Group Management
* `net user`: Lists all users on the computer.
* `net user <username>`: Displays info about a specific user.
* `net user <username> <password> /add`: Adds a new user.
* `net localgroup`: Lists all groups (e.g., Administrators).
* `net localgroup Administrators <username> /add`: Adds a user to the admin group.

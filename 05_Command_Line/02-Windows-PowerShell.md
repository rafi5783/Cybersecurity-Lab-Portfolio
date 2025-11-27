# Windows PowerShell Essentials

## 1. Core Concepts
PowerShell uses a **Verb-Noun** syntax (e.g., `Get-Help`).
* **Cmdlet**: A lightweight command used in the PowerShell environment.
* **Pipeline (`|`)**: Passes the output of one command as input to another.

## 2. Discovery & Help (Crucial)
* `Get-Help <cmdlet>`: Basic help.
    * `Get-Help <cmdlet> -Examples`: Shows how to actually use the command.
    * `Get-Help <cmdlet> -Full`: Shows detailed documentation.
* `Get-Command`: Lists all available cmdlets.
    * `Get-Command *service*`: Finds commands containing the word "service".
* `Get-Alias`: Lists shortcuts (e.g., `ls` is an alias for `Get-ChildItem`).

## 3. File & Navigation (The "Get" equivalents)
* `Get-ChildItem` (or `ls`, `dir`): Lists files.
    * `Get-ChildItem -Path C:\ -Recurse`: Lists files recursively.
    * `Get-ChildItem -Hidden`: Shows hidden files.
* `Set-Location` (or `cd`): Changes the directory.
* `Get-Content` (or `cat`, `type`): Reads a file.
* `Get-FileHash <file> -Algorithm MD5`: Checks file integrity.

## 4. System Administration
* `Get-Process`: Lists running processes.
* `Get-Service`: Lists status of services.
* `Get-LocalUser`: Lists local users.
* `Get-NetIPConfiguration`: The PowerShell version of `ipconfig`.
* `Get-NetTCPConnection`: The PowerShell version of `netstat`.

## 5. Filtering and Objects (The Power of `|`)
PowerShell passes **Objects**, not just text.
* **Select-Object**: Picks specific properties.
    * `Get-Process | Select-Object Id, Name`
* **Where-Object**: Filters results based on criteria.
    * `Get-Service | Where-Object -Property Status -eq 'Running'`
    * `Get-ChildItem | Where-Object -Property Length -gt 100` (Files larger than 100 bytes).
* **Sort-Object**: Sorts the output.
    * `Get-Process | Sort-Object CPU -Descending` (Finds high CPU usage).

## 6. Operators Cheat Sheet
* `-eq`: Equal to
* `-ne`: Not equal to
* `-gt`: Greater than
* `-lt`: Less than
* `-contains`: Checks if a collection contains a value.

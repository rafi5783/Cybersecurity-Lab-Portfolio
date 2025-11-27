# Linux Shell (Bash) Fundamentals

## 1. Navigation & Listing
* `pwd`: Print Working Directory (Where am I?).
* `cd`: Change Directory.
    * `cd ~`: Home directory.
    * `cd /`: Root directory.
* `ls`: List files.
    * `ls -l`: Long listing (shows permissions, owner, size).
    * `ls -a`: Show hidden files (starting with `.`).
    * `ls -la`: Combine both.

## 2. File Operations
* `touch file`: Creates an empty file.
* `cat file`: Displays content.
* `mkdir folder`: Creates a directory.
* `cp source dest`: Copies file.
* `mv source dest`: Moves or renames file.
* `rm file`: Removes a file.
* `rm -r folder`: Removes a folder recursively.
* `nano file`: Opens a text editor.

## 3. Search & Filters
* `grep "text" file`: Searches for a string inside a file.
* `find . -name "filename"`: Searches for a file by name.
* `find . -type f -name "*.txt"`: Finds all text files.
* `wc -l file`: Counts the number of lines in a file.

## 4. Shell Operators (Redirection)
* `>`: Overwrite (Output to file).
    * `echo "Hello" > file.txt` (Replaces content).
* `>>`: Append.
    * `echo "World" >> file.txt` (Adds to the end).
* `|` (Pipe): Use output of one command as input for another.
    * `cat access.log | grep "Error"`

## 5. Permissions & Users
* `whoami`: Shows current user.
* `sudo`: Run command as Superuser (Root).
* `su <user>`: Switch user.
* `chmod`: Change file permissions.
    * `chmod +x script.sh`: Make executable.
    * `chmod 777 file`: Read/Write/Execute for everyone (Dangerous).
* `chown user:group file`: Change file ownership.

## 6. Common Directories

* `/etc`: System configuration files.
* `/var`: Variable data (logs, websites).
* `/root`: Home directory for the root user.
* `/tmp`: Temporary files (deleted on reboot).
* `/bin`: Essential user binaries (commands).

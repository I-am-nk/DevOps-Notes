# Linux and Shell Scripting Basics

**Operating System (OS):** System software that manages computer hardware, software resources, and provides services for computer programs. It acts as an intermediary between users and the computer hardware.

**Linux:** Linux is a free, open-source, and secure operating system. It contains different types of distributions and is fast, which is why most companies use Linux as their OS in DevOps.

## 1. Kernel (Core of the OS)
The Kernel is the heart of the Linux operating system. It is responsible for managing system resources such as CPU, memory, and devices.

## 2. System Libraries
System libraries provide essential functions that programs use to communicate with the kernel without direct interaction.

---

## Summary Table

| Component        | Function                                 |
|------------------|------------------------------------------|
| Kernel           | Manages hardware resources and system operations. |
| System Libraries | Provides essential functions for applications.    |
| Compilers        | Converts high-level code into machine code.      |
| User Programs    | Applications for users (e.g., browsers, editors).|
| System Software  | OS tools, utilities, and device drivers.         |

---

## What is Shell Scripting?

A shell script is a file containing a sequence of commands written in a shell programming language to automate tasks in Linux. Instead of executing commands one by one in the terminal, a shell script can run them all at once.

- `man <command>`: Provides detailed information about the command.  
  Example: `man ls`

- `history`: Shows the history of commands used.  
  Example: `history`

- To run Linux in Windows CMD, use:  
  Example: `wsl`

---

## Basic & Daily Use Linux Commands

| Command          | Description                               | Example                      |
|------------------|-------------------------------------------|------------------------------|
| pwd              | Shows the current directory path           | pwd                          |
| ls               | Lists files & directories                  | ls                           |
| ls -l            | Detailed list (permissions, owner, size, date) | ls -l                    |
| ls -ltr          | List files sorted by modification time (oldest first) | ls -ltr             |
| ls -a            | Shows hidden files (starting with .)       | ls -a                        |
| cd <dir>         | Changes directory                          | cd /home/user                |
| cd ..            | Moves up one directory                     | cd ..                        |
| mkdir <dir>      | Creates a directory                        | mkdir my_folder              |
| rmdir <dir>      | Deletes an empty directory                 | rmdir my_folder              |
| rm -r <dir>      | Deletes a directory with files             | rm -r my_folder              |
| cp <src> <dest>  | Copies files                               | cp file1.txt backup/         |
| mv <src> <dest>  | Moves/Renames files                        | mv file1.txt newfile.txt     |
| find / -name file.txt | Searches for a file                  | find /home -name "*.log"     |
| touch <file>     | Creates the file                           | touch file.txt               |

---

## 📄 File Viewing & Editing

| Command               | Description                       | Example                |
|-----------------------|-----------------------------------|------------------------|
| cat <file>            | Displays file content              | cat file.txt           |
| tac <file>            | Displays file in reverse order     | tac file.txt           |
| less <file>           | Opens a file for scrolling         | less file.txt          |
| head -n <num> <file>  | Shows first n lines of a file      | head -5 file.txt       |
| tail -n <num> <file>  | Shows last n lines of a file       | tail -10 file.txt      |
| tail -f <file>        | Live updates of a file (useful for logs) | tail -f /var/log/syslog |
| nano <file>           | Opens file in Nano editor          | nano file.txt          |
| vim <file>            | Opens file in Vim editor           | vim file.txt           |
| touch <file>          | Creates the file                   | touch file.txt         |

---

## 🔍 Searching & Filtering

| Command                | Description                         | Example                  |
|------------------------|-------------------------------------|--------------------------|
| grep "text" <file>     | Finds text in a file                | grep "error" logs.txt    |
| grep -i "text" <file>  | Case-insensitive search             | grep -i "warning" logs.txt|
| grep -r "text" <dir>   | Searches recursively in a directory | grep -r "failed" /var/log/|
| awk '{print $1}' <file>| Extracts first column from a file   | awk '{print $2}' data.txt|
| sed 's/old/new/g' <file>| Replaces text in a file            | sed 's/error/fixed/g' logs.txt|
| sort <file>            | Sorts a file alphabetically         | sort names.txt           |
| uniq <file>            | Removes duplicate lines             | uniq data.txt            |

---

## 🔧 Process & System Monitoring

| Command         | Description                           | Example                  |
|-----------------|---------------------------------------|--------------------------|
| ps aux          | Shows all running processes           | ps aux                   |
| top             | Displays real-time CPU & memory usage | top                      |
| htop            | Enhanced process viewer (install with sudo apt install htop) | htop   |
| kill <PID>      | Stops a process by PID                | kill 1234                |
| kill -9 <PID>   | Force kills a process                 | kill -9 1234             |
| pkill <name>    | Kills a process by name               | pkill firefox            |
| free -m         | Shows free & used RAM in MB           | free -m                  |
| df -h           | Shows disk usage (human-readable)     | df -h                    |
| du -sh <dir>    | Checks size of a directory            | du -sh /var/log          |

---

## 🖧 Networking Commands

| Command        | Description                      | Example                      |
|----------------|----------------------------------|------------------------------|
| ip a           | Shows IP addresses               | ip a                         |
| hostname -I    | Displays system's IP address     | hostname -I                  |
| ping <host>    | Checks network connectivity      | ping google.com              |
| curl <URL>     | Fetches website content          | curl https://example.com     |
| wget <URL>     | Downloads a file                 | wget https://example.com/file.zip |
| netstat -tulnp | Shows open ports & listening services | netstat -tulnp             |

---

## 👤 User & Permission Management

| Command                | Description                         | Example                     |
|------------------------|-------------------------------------|-----------------------------|
| whoami                 | Shows current user                  | whoami                      |
| id                     | Displays user ID & group info       | id                          |
| sudo <command>         | Runs command as root                | sudo apt update             |
| chmod 755 <file>       | Sets permissions (rwxr-xr-x)        | chmod 644 file.txt          |
| chown user:group <file>| Changes ownership                   | chown john:developers script.sh|

---

## 🕒 Scheduling & Automation

| Command      | Description                  | Example           |
|--------------|------------------------------|-------------------|
| crontab -e   | Edits cron jobs (automated tasks) | crontab -e   |
| crontab -l   | Lists scheduled cron jobs         | crontab -l   |
| at 14:30     | Schedules a task at 2:30 PM       | at 14:30      |
| sleep <seconds> | Pauses script execution        | sleep 10       |

---

## 🔥 Important Shortcuts

| Shortcut | Description                 |
|----------|-----------------------------|
| Ctrl + C | Kills the running command   |
| Ctrl + Z | Suspends (pauses) a process |
| Ctrl + D | Closes the terminal         |
| Ctrl + L | Clears the screen           |
| !!       | Repeats the last command    |
| !xyz     | Runs the last command starting with xyz |

---

## Notes

- For creating any executable shell scripting file, a few things need to be followed:
  1. Create the file with a name ending with `.bash` (e.g., `demo.bash`). The `.bash` extension is used to execute the file's content.
  2. After that, give permission to that file using the command `chmod 777` (this means the owner, group, and others can read, write, and execute that file).
  3. `./demo.sh` is used to execute the file.
  4. `./` is used to execute the file.
  5. The pipe `|` command is used to pass the output of the first command to the second command.

---

## Linux File Permissions

In Linux, file permissions are represented using three-digit octal numbers (e.g., 755, 644). Each digit represents a set of permissions for:
- Owner (User)
- Group
- Others

Each permission has a numeric value:
- Read (`r`) = 4
- Write (`w`) = 2
- Execute (`x`) = 1

The sum of these values determines the permission level.

| Octal Number | Permission | Meaning                               |
|--------------|------------|---------------------------------------|
| 0            | ---        | No permissions                        |
| 1            | --x        | Execute only                          |
| 2            | -w-        | Write only                            |
| 3            | -wx        | Write and Execute (2+1=3)              |
| 4            | r--        | Read only                             |
| 5            | r-x        | Read and Execute (4+1=5)              |
| 6            | rw-        | Read and Write (4+2=6)                |
| 7            | rwx        | Read, Write, and Execute (4+2+1=7)    |

---

## Linux File System Hierarchy

<img width="1600" height="2121" alt="image" src="https://github.com/user-attachments/assets/48b0073d-accc-4839-995a-f58e2675c85f" />


---

## NGINX: How NGINX Works from Start to Finish

<img width="1260" height="1789" alt="image" src="https://github.com/user-attachments/assets/8d2c682f-679e-4fa6-a0cf-67ec23a238ca" />


---


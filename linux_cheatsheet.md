# Linux Command Cheat Sheet (MCS-022 / IGNOU BCA)

---

## 1. Navigation & Basic Info

| Command | Description | Example |
|---|---|---|
| `pwd` | Print current working directory | `pwd` → `/home/vivekvro` |
| `ls` | List files/directories | `ls` |
| `ls -l` | Long listing (permissions, owner, size) | `ls -l` |
| `ls -a` | Show hidden files (start with `.`) | `ls -a` |
| `ls -la` | Combine long + hidden | `ls -la` |
| `cd` | Change directory | `cd folder_1` |
| `cd ..` | Move up one level | `cd ..` |
| `cd ~` or `cd` | Go to home directory | `cd` |
| `cd /path` | Absolute path navigation | `cd /home/vivekvro/folder_1` |
| `whoami` | Show current logged-in user | `whoami` |
| `who` | Show who is logged into the system | `who` |
| `uname -a` | Show kernel/system info | `uname -a` |
| `date` | Show current date/time | `date` |
| `cal` | Show calendar | `cal` |
| `clear` | Clear terminal screen | `clear` |
| `history` | Show command history | `history` |
| `man command` | Show manual/help for a command | `man ls` |

---

## 2. File & Directory Management

| Command | Description | Example |
|---|---|---|
| `mkdir` | Create directory | `mkdir folder_1` |
| `mkdir -p` | Create nested directories at once | `mkdir -p a/b/c` |
| `rmdir` | Remove **empty** directory | `rmdir folder_1` |
| `rm` | Remove file | `rm self.txt` |
| `rm -r` | Remove directory and contents recursively | `rm -r folder_1` |
| `rm -f` | Force remove without prompt | `rm -f self.txt` |
| `rm -rf` | Force remove directory + contents (careful!) | `rm -rf old_folder` |
| `touch` | Create empty file / update timestamp | `touch self.txt` |
| `cp` | Copy file | `cp self.txt folder_2/` |
| `cp -r` | Copy directory recursively | `cp -r folder_1 folder_2` |
| `cp -i` | Prompt before overwrite | `cp -i self.txt folder_2/` |
| `mv` | Move or rename file | `mv self.txt folder_2/` |
| `mv oldname newname` | Rename (same directory) | `mv old.txt new.txt` |
| `find` | Search for files | `find / -name "self.txt"` |
| `locate` | Fast file search (uses database) | `locate self.txt` |
| `file` | Identify file type | `file self.txt` |

---

## 3. Viewing File Content

| Command | Description | Example |
|---|---|---|
| `cat` | Display entire file at once | `cat self.txt` |
| `cat -n` | Display with line numbers | `cat -n self.txt` |
| `cat file1 file2 > file3` | Concatenate files | `cat a.txt b.txt > c.txt` |
| `more` | View page-by-page, **forward only** | `more self.txt` |
| `less` | View page-by-page, forward **and** backward | `less self.txt` |
| `head` | Show first 10 lines (default) | `head self.txt` |
| `head -n 5` | Show first 5 lines | `head -n 5 self.txt` |
| `tail` | Show last 10 lines (default) | `tail self.txt` |
| `tail -n 5` | Show last 5 lines | `tail -n 5 self.txt` |
| `tail -f` | Live-follow a growing file (e.g. logs) | `tail -f logfile.txt` |
| `wc` | Word/line/char count | `wc self.txt` |
| `wc -l` | Count lines only | `wc -l self.txt` |

---

## 4. Redirection & Pipes

| Symbol/Command | Description | Example |
|---|---|---|
| `>` | Redirect output, **overwrite** file | `ls > list.txt` |
| `>>` | Redirect output, **append** to file | `echo "hi" >> list.txt` |
| `<` | Redirect input from file | `sort < names.txt` |
| `\|` | Pipe: send output of one command as input to another | `ls -l \| more` |
| `2>` | Redirect error output | `command 2> errors.txt` |

⚠️ **Exam trap:** `>` truncates the target file *immediately*, even if the command itself fails.

---

## 5. Permissions & Ownership

| Command | Description | Example |
|---|---|---|
| `ls -l` | View permissions (`-rwxr-xr-x`) | `ls -l self.txt` |
| `chmod 755 file` | Set permissions numerically | `chmod 755 self.txt` |
| `chmod u+x file` | Add execute for owner | `chmod u+x self.txt` |
| `chmod g-w file` | Remove write for group | `chmod g-w self.txt` |
| `chmod o=r file` | Set others to exactly read | `chmod o=r self.txt` |
| `chmod a+r file` | Add read for all (u+g+o) | `chmod a+r self.txt` |
| `chown user file` | Change owner | `sudo chown rahul self.txt` |
| `chown user:group file` | Change owner and group | `sudo chown rahul:staff self.txt` |
| `chgrp group file` | Change group only | `sudo chgrp staff self.txt` |
| `umask` | Show default permission mask | `umask` |

**Numeric values:** r=4, w=2, x=1 → add per category (owner, group, others).
Example: `rwxr-xr--` = 7 5 4 = **754**

---

## 6. User & Group Management

| Command | Description | Example |
|---|---|---|
| `useradd -m name` | Create user with home directory | `sudo useradd -m rahul` |
| `passwd name` | Set/change password | `sudo passwd rahul` |
| `usermod -aG group name` | Add user to a group (append, not replace) | `sudo usermod -aG sudo rahul` |
| `usermod -l new old` | Rename user | `sudo usermod -l raj rahul` |
| `usermod -L name` | Lock account | `sudo usermod -L rahul` |
| `userdel name` | Delete user | `sudo userdel rahul` |
| `userdel -r name` | Delete user + home directory | `sudo userdel -r rahul` |
| `groupadd name` | Create group | `sudo groupadd staff` |
| `groupdel name` | Delete group | `sudo groupdel staff` |
| `gpasswd -a user group` | Add user to group | `sudo gpasswd -a rahul staff` |
| `gpasswd -d user group` | Remove user from group | `sudo gpasswd -d rahul staff` |
| `su - name` | Switch user (full environment) | `su - rahul` |
| `id name` | Show UID/GID/groups | `id rahul` |
| `groups name` | Show group memberships | `groups rahul` |
| `visudo` | Safely edit sudoers file | `sudo visudo` |
| `cat /etc/passwd` | List all users | `cat /etc/passwd` |
| `cat /etc/group` | List all groups | `cat /etc/group` |

---

## 7. Process Management

| Command | Description | Example |
|---|---|---|
| `ps` | List current user's processes | `ps` |
| `ps -ef` | List all processes, full detail | `ps -ef` |
| `top` | Live resource/process monitor | `top` |
| `kill PID` | Terminate process by ID | `kill 1234` |
| `kill -9 PID` | Force kill | `kill -9 1234` |
| `bg` | Resume job in background | `bg %1` |
| `fg` | Bring job to foreground | `fg %1` |
| `jobs` | List background jobs | `jobs` |
| `nice` | Start process with priority | `nice -n 10 command` |
| `renice` | Change priority of running process | `renice 5 -p 1234` |
| `nohup` | Keep process running after logout | `nohup command &` |
| `&` | Run command in background | `sleep 100 &` |

---

## 8. Text Processing & Filters

| Command | Description | Example |
|---|---|---|
| `grep` | Search text pattern in file | `grep "Linux" self.txt` |
| `grep -i` | Case-insensitive search | `grep -i "linux" self.txt` |
| `grep -c` | Count matching lines | `grep -c "Linux" self.txt` |
| `grep -v` | Show non-matching lines | `grep -v "Linux" self.txt` |
| `sort` | Sort lines alphabetically | `sort names.txt` |
| `sort -r` | Sort in reverse | `sort -r names.txt` |
| `sort -n` | Sort numerically | `sort -n numbers.txt` |
| `uniq` | Remove adjacent duplicate lines | `sort file.txt \| uniq` |
| `cut` | Extract columns/fields | `cut -d ":" -f1 /etc/passwd` |
| `paste` | Merge lines of files side by side | `paste a.txt b.txt` |
| `sed` | Stream editor (find & replace) | `sed 's/old/new/' self.txt` |
| `awk` | Pattern scanning & processing | `awk '{print $1}' self.txt` |
| `tr` | Translate/replace characters | `tr 'a-z' 'A-Z' < self.txt` |

---

## 9. Compression & Archiving

| Command | Description | Example |
|---|---|---|
| `tar -cvf` | Create archive | `tar -cvf archive.tar folder_1` |
| `tar -xvf` | Extract archive | `tar -xvf archive.tar` |
| `tar -czvf` | Create compressed (gzip) archive | `tar -czvf archive.tar.gz folder_1` |
| `tar -xzvf` | Extract .tar.gz archive | `tar -xzvf archive.tar.gz` |
| `gzip` | Compress a file (.gz) | `gzip self.txt` |
| `gunzip` | Decompress .gz file | `gunzip self.txt.gz` |
| `zip` | Create .zip archive | `zip archive.zip self.txt` |
| `unzip` | Extract .zip archive | `unzip archive.zip` |

---

## 10. Networking Commands

| Command | Description | Example |
|---|---|---|
| `ping` | Test connectivity to a host | `ping google.com` |
| `ifconfig` / `ip addr` | Show network interface info | `ip addr` |
| `netstat` | Show network connections | `netstat -tuln` |
| `ssh` | Remote login to another machine | `ssh user@192.168.1.5` |
| `scp` | Securely copy files between machines | `scp file.txt user@host:/path` |
| `wget` | Download file from URL | `wget https://example.com/file.zip` |
| `hostname` | Show system's hostname | `hostname` |

---

## 11. vi Editor Essentials

| Action | Key(s) | Notes |
|---|---|---|
| Enter Insert mode | `i` | Start typing text |
| Exit to Normal mode | `Esc` | Needed before `:` commands |
| Save | `:w` | Write without quitting |
| Save and quit | `:wq` or `ZZ` | Most common exit |
| Quit without saving | `:q` | Only if no changes |
| Force quit, discard changes | `:q!` | Discards edits |
| Delete a line | `dd` | In Normal mode |
| Copy (yank) a line | `yy` | In Normal mode |
| Paste | `p` | After yy or dd |
| Search | `/pattern` | Forward search |

---

## 12. Shell Scripting Basics

```bash
#!/bin/bash
# Variable assignment (no spaces around =)
name="Vivek"
echo "Hello, $name"

# Command-line arguments
echo "First arg: $1"
echo "Total args: $#"

# If-else
if [ $1 -gt 10 ]
then
    echo "Greater than 10"
else
    echo "10 or less"
fi

# For loop
for i in 1 2 3
do
    echo "Number: $i"
done

# While loop
count=1
while [ $count -le 5 ]
do
    echo $count
    count=$((count+1))
done
```

**Run a script:**
```
chmod +x script.sh
./script.sh
```

---

## 13. Quick Exam-Favorite Concepts

- **Absolute path**: starts with `/` (from root) — e.g. `/home/vivekvro/self.txt`
- **Relative path**: no leading `/` (from current location) — e.g. `folder_1/self.txt`
- **Hard link vs Soft link**: hard link shares the same inode as original; soft link (`ln -s`) is a pointer/shortcut and can cross file systems
- **`more` vs `less`**: `more` scrolls forward only; `less` scrolls both directions and opens large files faster
- **`cp` vs `mv`**: `cp` duplicates (original stays); `mv` relocates/renames (original gone from source)
- **`>` vs `>>`**: `>` overwrites; `>>` appends
- **File permission bits**: r=4, w=2, x=1; three categories = owner (u), group (g), others (o)

---

*Compiled for MCS-022 (IGNOU BCA) exam preparation.*

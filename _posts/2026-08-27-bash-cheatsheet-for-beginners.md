---
title: "Learning Bash Felt Like Learning a New Language — Because It Is One"
date: 2026-08-27
categories: [Linux & SQL]
tags: [bash, linux, cheatsheet, command line]
excerpt: "My beginner's Bash cheatsheet: navigation, files, searching, piping, users, and permissions."
---

A few weeks into the program, I hit a wall I didn't expect: the command line.

Not a technical wall, exactly. More like the feeling of moving to a new country and realizing "please" and "thank you" only get you so far.

## It's Not Intuitive. That's the Point.

Here's the thing nobody tells you upfront: Bash isn't unintuitive because you're bad at it. It's unintuitive because it *is* a language — its own syntax, its own grammar, its own very unforgiving rules about spacing, flags, and punctuation. One extra character in the wrong place, and the whole thing refuses to understand you, the same way a misplaced accent mark can change the entire meaning of a word in Portuguese.

I've actually learned three real languages in my life. Bash is the first one that talks back with error messages instead of a confused look.

## So I Did What I Always Do: I Started Taking Notes

This is where the cheatsheet came from — not as a formal study tool, but as survival. Every time I looked up a command, used it wrong, fixed it, and finally got the output I wanted, I wrote it down. Command, what it does, an example, and repeat.

The basics came first and felt almost like small talk: `pwd` to figure out where I even was, `cd` to move around, `ls -la` when I wanted to see everything, including the hidden files nobody warns you exist. Then it got a little more like real conversation — `grep` to actually search inside files instead of scrolling forever, and piping one command into another with `|`, which was the first moment Bash stopped feeling like isolated vocabulary and started feeling like actual sentences.

On that note, this blog post is a cheatsheet for all beginners learning a new language.

---

## The Cheatsheet

### 1. File System Navigation & Identity

| Command | What It Does |
|---|---|
| `cd reports` | Navigates to a subdirectory named `reports` |
| `cd /home/analyst/reports` | Navigates using an absolute file path |
| `cd ..` | Navigates up one level to the parent directory |
| `pwd` | Prints the full path of the current working directory (e.g., `/home/analyst`) |
| `whoami` | Returns the username of the current logged-in user |
| `ls` | Displays files and directories in the current working directory |
| `ls /path/to/dir` | Displays contents of a specified target directory |
| `ls -a` | Displays all files, including hidden files (those starting with `.`) |
| `ls -l` | Displays detailed long-listing format (permissions, owner, group, size, last modified) |
| `ls -la` | Long-listing format for **all** files, including hidden ones |

### 2. Directory & File System Management

| Command | What It Does |
|---|---|
| `mkdir network` | Creates a directory named `network` in the current location |
| `mkdir /home/analyst/logs/network` | Creates a directory using an absolute path |
| `rmdir` | Removes an empty directory (errors if it contains files) |
| `touch permissions.txt` | Creates a new, empty file |
| `rm permissions.txt` | Permanently deletes a file |
| `mv permissions.txt /home/analyst/logs` | Moves a file to another directory |
| `mv permissions.txt perm.txt` | Renames a file in place |
| `cp permissions.txt /home/analyst/logs` | Copies a file to a new location, keeping the original |

### 3. Reading File Contents

| Command | What It Does |
|---|---|
| `cat updates.txt` | Displays the entire content of a file in the terminal |
| `head updates.txt` | Displays the beginning of a file (defaults to first 10 lines) |
| `head -n 5 updates.txt` | Displays only the first 5 lines |
| `tail updates.txt` | Displays the end of a file (defaults to last 10 lines) |
| `tail -n 5 updates.txt` | Displays only the last 5 lines |
| `less updates.txt` | Displays content one page at a time, with scrolling |

### 4. Searching & Content Filtering

| Command | What It Does |
|---|---|
| `find /home/analyst/projects` | Searches all files starting at a given directory |
| `find /home/analyst/projects -name "*log*"` | Case-sensitive search using a wildcard pattern |
| `find /home/analyst/projects -iname "*log*"` | Case-*insensitive* search using a wildcard pattern |
| `find /home/analyst/projects -mtime -3` | Finds files modified within the past 3 days |
| `find /home/analyst/projects -mmin -15` | Finds files modified within the past 15 minutes |
| `grep OS updates.txt` | Searches a file and returns matching lines |

**grep flags:** `-i` (ignore case) · `-v` (invert match) · `-r` / `-R` (recursive search) · `-n` (show line numbers) · `-c` (count matches) · `-w` (exact whole word match)

### 5. Output Redirection & Piping

| Symbol | What It Does |
|---|---|
| `>` | Redirects output to a file, **overwriting** existing content (creates the file if missing) |
| `>>` | **Appends** output to the end of a file without overwriting (creates the file if missing) |
| `\|` | Sends the output of one command as input to another — e.g. `ls /home/analyst/reports \| grep users` |

### 6. Text Editing (nano)

| Command | What It Does |
|---|---|
| `nano permissions.txt` | Opens or creates a file in the command-line text editor |
| `CTRL + O` | Saves file changes |
| `CTRL + X` | Exits the editor |
| `CTRL + K` | Cuts the current line of text |
| `CTRL + U` | Pastes (uncuts) text |
| `CTRL + W` | Searches for text in the file |

### 7. User Authentication & System Administration (sudo)

**Core concepts:**
- **Authentication** — verifying a user's identity to grant appropriate access
- **Root User (Superuser)** — has full elevated privileges to modify the system and run any command
- **sudo** ("Super-User Do") — temporarily grants elevated privileges to users authorized in the sudoers file; direct root login is discouraged due to security risk and lack of audit tracking
- **Principle of Least Privilege** — users should only be granted the minimal access their role requires

**useradd (create accounts):**

| Command | What It Does |
|---|---|
| `sudo useradd fgarcia` | Adds a new user account to the system |
| `sudo useradd -g security fgarcia` | Sets the user's primary default group (`-g`) |
| `sudo useradd -G finance,admin fgarcia` | Adds the user to supplemental groups (`-G`) |

**usermod (modify existing accounts):**

| Command | What It Does |
|---|---|
| `sudo usermod -g executive fgarcia` | Changes a user's primary group |
| `sudo usermod -G <group> fgarcia` | Replaces all existing supplemental groups |
| `sudo usermod -a -G marketing fgarcia` | **Appends** a supplemental group without removing existing ones |
| `sudo usermod -d /home/garcia_f fgarcia` | Changes the user's home directory |
| `sudo usermod -l garcia_f fgarcia` | Changes the user's login name |
| `sudo usermod -L fgarcia` | **Locks** an account to prevent logins |

**userdel & groupdel (delete accounts/groups):**

| Command | What It Does |
|---|---|
| `sudo userdel fgarcia` | Deletes a user account, keeping their home directory |
| `sudo userdel -r fgarcia` | Deletes a user account **and** their home directory/files |
| `sudo groupdel accounting` | Deletes a group from the system |

### 8. Managing Ownership & File Permissions

**Changing ownership (chown):**

| Command | What It Does |
|---|---|
| `sudo chown fgarcia access.txt` | Changes the user owner of a file |
| `sudo chown :security access.txt` | Changes the group owner (note the colon prefix) |
| `sudo chown fgarcia:security access.txt` | Changes user and group owner at the same time |

**Reading a permission string** (e.g. `drwxrwxrwx`):

| Position | Example | Meaning |
|---|---|---|
| 1st | **d**rwxrwxrwx | File type — `d` = directory, `-` = regular file |
| 2nd–4th | d**rwx**rwxrwx | User (owner) read / write / execute |
| 5th–7th | drwx**rwx**rwx | Group read / write / execute |
| 8th–10th | drwxrwx**rwx** | Other (everyone else) read / write / execute |

- **Read (r):** view file contents, or list directory contents
- **Write (w):** modify a file, or create/delete files inside a directory
- **Execute (x):** run a file as a program/script, or `cd` into a directory

**Modifying permissions (chmod):**

| Command | What It Does |
|---|---|
| `chmod u+rwx,g+rwx,o+rwx login_sessions.txt` | Adds (`+`) read, write, execute for user, group, and other |
| `chmod g-rw bonuses.txt` | Removes (`-`) read and write from group |
| `chmod u=r,g=r,o=r login_sessions.txt` | Sets (`=`) exact read-only permissions |

**chmod shorthand:** Owners — `u` (user) · `g` (group) · `o` (other) · `a` (all) · Operators — `+` (add) · `-` (remove) · `=` (set exact) · Permissions — `r` (read) · `w` (write) · `x` (execute)

### 9. Command Help & System Manuals

| Command | What It Does |
|---|---|
| `man chown` | Displays detailed documentation ("man pages") for a command |
| `whatis nano` | Displays a one-line summary description of a command |
| `apropos password` | Searches manual page descriptions for a keyword when you don't know the exact command |
| `apropos -a graph editor` | Returns commands matching **both** search strings |

---

Still building the list. Still making typos. Still keeping notes.

## These commands cover most daily operations in Linux

### 1. System Information
```bash
uname -a  # Shows all system information (kernel name, version, machine hardware, etc.)
uname -r  # Displays the kernel release version
uname -m  # Shows the machine hardware name (e.g., x86_64)

hostname        # Shows the current hostname
hostname --all-ip-addresses     # Displays all network addresses of the host

uptime  # Displays uptime, number of users, and load averages

df -h  # Shows disk usage in human-readable format (e.g., GB, MB)
df -i  # Displays inode usage instead of block usage

free -h  # Shows memory usage in human-readable format (RAM and swap)

# Displays real-time system processes and resource usage
top   # Basic process viewer or Displays real-time system processes and resource usage
# Press `q` to quit.
# Press `k` to kill a process (you'll be prompted for the PID).
# Press `h` for help.
# Press 'r' to renice
htop  # Interactive process viewer (requires installation)
# Press `F9` to kill a process.
# Press `F10` to quit
# Navigation in htop:
# F6 - sort by column
# k - kill process
# / - search

lsb_release -a  # Shows distribution details (e.g., Ubuntu, Debian)

date        # Shows current date and time

#  Displays logged-in users
who  # Shows who is logged in
w    # Shows who is logged in and what they are doing
whoami      # Display current username

ps aux  #  Displays information Lists all running processes
ps -ef  # Displays information Another format to list processes
ps -u username # Shows processes for a specific user
ps -C process_name # Shows processes by name (e.g., `ps -C bash`)

lsblk  # Displays block devices in a tree format (e.g., disks, partitions)
```

### 2. Navigation
```bash
pwd  # Shows the full path of the current directory

# Changes the current directory
cd /path/to/directory  # Navigates to a specific directory
cd ..                 # Moves up one directory level
cd ~                  # Navigates to the home directory
cd -                  # Switches to the previous directory

#  Lists files and directories
ls          # Lists files and directories in the current directory
ls -l       # Displays detailed list (permissions, size, etc.)
ls -a       # Shows hidden files (those starting with a dot)
ls -lh      # Human-readable file sizes
ls /path    # Lists contents of a specific directory

# Displays directory structure in a tree format
tree        # Shows directory tree (requires installation)
tree -L 2   # Limits depth to 2 levels

# Quickly finds files by name (uses a database)
locate filename  # Searches for files (requires `updatedb` to update the database)

# Shows the full path of a command.
which ls  # Displays the path of the `ls` command

# Locates the binary, source, and manual pages for a command
whereis ls  # Shows locations of `ls` binary, source, and man pages

# Estimates file and directory space usage
du -sh /path  # Shows total size of a directory in human-readable format
du -ah        # Displays sizes of all files and directories

# Displays detailed information about a file or directory.
stat filename  # Shows file size, permissions, access times, etc.

# Determines the type of a file.
file filename  # Displays file type (e.g., text, binary, directory)
```

### 3. File Management

```bash
touch filename  # Creates an empty file or updates its timestamp

mkdir dirname        # Creates a directory
mkdir -p dir1/dir2   # Creates nested directories (parent directories if they don't exist)

rmdir dirname  # Deletes an empty directory

rm filename        # Deletes a file
rm -r dirname      # Recursively deletes a directory and its contents
rm -f filename     # Forces deletion without confirmation
rm -i filename     # Prompts for confirmation before deletion

cp file1 file2        # Copies file1 to file2
cp -r dir1 dir2       # Recursively copies a directory
cp -v file1 file2     # Verbose mode (shows what is being copied)
cp -i file1 file2     # Prompts before overwriting

mv file1 file2        # Renames file1 to file2
mv file1 /path/dir    # Moves file1 to /path/dir
mv -i file1 file2     # Prompts before overwriting

ln -s target linkname  # Creates a symbolic (soft) link
ln target linkname     # Creates a hard link

more filename  # Displays file content one page at a time
less filename  # Allows scrolling up and down (more advanced than `more`)

chmod 755 filename  # Sets permissions to rwxr-xr-x
chmod +x filename   # Makes the file executable
chmod -R 755 dir    # Recursively changes permissions for a directory

chown user:group filename  # Changes owner and group of a file
chown -R user:group dir    # Recursively changes ownership for a directory

tar -cvf archive.tar dir/  # Creates a tar archive
tar -xvf archive.tar       # Extracts a tar archive
tar -czvf archive.tar.gz dir/  # Creates a compressed tar archive (gzip)
tar -xzvf archive.tar.gz   # Extracts a compressed tar archive (gzip)

gzip filename       # Compresses a file (creates filename.gz)
gunzip filename.gz  # Decompresses a file

```

### 4. File Viewing & Editing
```bash
# Simple text editor
nano file.txt             
# Common commands:
# Ctrl + O - Save
# Ctrl + X - Exit
# Ctrl + W - Search

# Advanced text editor
vim file.txt              
# Common modes:
# i - Insert mode
# Esc - Command mode
# :w - Save
# :q - Quit
# :wq - Save and quit

cat filename        # Displays file content
cat file1 file2     # Concatenates and displays multiple files
cat > filename      # Creates a new file and writes input to it (Ctrl+D to save)
cat file1 >> file2  # Appends file1 content to file2

head filename       # Displays the first 10 lines
head -n 20 filename # Displays the first 20 lines

tail filename       # Displays the last 10 lines
tail -n 20 filename # Displays the last 20 lines
tail -f filename    # Follows the file in real-time (useful for logs)
```

### 5. File Searching
```bash

# Searches for files and directories.
find /path -mtime -7         # Finds files modified in the last 7 days
# Find Command
find /path -name "*.txt"  # Find all .txt files
# Example: find /home -name "*.jpg"

find . -type d           # Find only directories
find . -type f           # Find only files

find . -size +100M      # Find files larger than 100MB

# Grep Command
grep "pattern" file     # Search for pattern in file
# Example: grep "error" log.txt

grep -i "pattern" file  # Case-insensitive search
grep -r "pattern" dir   # Recursive search in directory
grep -v "pattern" file  # Show lines NOT matching pattern
grep -n "pattern" file  # Show line numbers

# Practical Examples:
# Find all PHP files containing "function"
find . -name "*.php" -exec grep -l "function" {} \;

# Search for IP addresses in log files
grep -E '[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}' log.txt

# Find large files modified in last 24 hours
find / -type f -size +100M -mtime -1
```

### 6. Process Management
```bash
pstree  # Shows processes in a hierarchical tree structure

command &  # Runs the command in the background

jobs  # Shows all background jobs

# Brings a background job to the foreground
fg %1  # Brings job number 1 to the foreground

# Resumes a stopped background job
bg %1  # Resumes job number 1 in the background

ctrl+z                 # Suspend current process

# Runs a command that will continue running even after logging out
nohup command &  # Runs the command in the background and ignores hangup signals

# Sends a signal to a process (default is SIGTERM, which terminates the process)
kill PID          # Terminates the process with the specified PID
kill -9 PID       # Forcefully kills the process (SIGKILL)
kill -l           # Lists all available signals
killall process_name # Kills all processes with the specified name

pkill process_name  # Kills processes by name
pkill -u username   # Kills processes owned by a specific user

xkill  # Click on the window of the application you want to kill

nice -n 10 command  # Starts a command with a niceness of 10 (lower priority)

# Changes the priority of an already running process
renice 5 -p PID  # Changes the niceness of the process with the specified PID to 5
renice -n 10 -u username # Changes the niceness of all processes owned by a user

# Reports virtual memory statistics
vmstat 1  # Displays system performance statistics every 1 second

# Reports CPU and I/O statistics.
iostat 1  # Displays CPU and I/O statistics every 1 second

# Lists open files and the processes using them
lsof              # Lists all open files
lsof -u username  # Lists files opened by a specific user
lsof -i :80       # Lists processes using port 80

# Traces system calls and signals of a process
strace command  # Traces system calls of a command
strace -p PID   # Attaches to a running process and traces its system calls

# Finds the PID of a process by name
pgrep process_name  # Displays the PID of the process
```

### 7. Package Management
```bash
# Debian/Ubuntu (apt)
apt update                # Update package database
apt upgrade               # Upgrade installed packages
apt install package_name  # Install package
apt remove package_name   # Remove package
apt search keyword        # Search for package
apt list --installed     # List installed packages

# Red Hat/CentOS (yum)
yum update               # Update packages
yum install package_name # Install package
yum remove package_name  # Remove package
yum search keyword       # Search for package

# Package Information
dpkg -l                 # List installed packages (Debian)
rpm -qa                 # List installed packages (Red Hat)
```

### 8. Network
```bash
# Connectivity Testing
ping hostname           # Test network connectivity
ping -c 4 google.com    # Ping 4 times only

# Network Configuration
ifconfig                # Show/configure network interfaces
ip addr                 # Modern replacement for ifconfig
ip route               # Show routing table

# Network Monitoring
netstat -tuln          # Show active network connections
# -t: TCP ports
# -u: UDP ports
# -l: listening ports
# -n: show numbers instead of names

# Remote Access
ssh user@hostname       # Connect to remote host
scp file user@host:/path # Secure copy file to remote host
```

### 9. User Management
```bash
# User Administration
useradd username       # Create new user
usermod -aG group user # Add user to group
userdel username       # Delete user

# Password Management
passwd username        # Change password
passwd -l username     # Lock user account
passwd -u username     # Unlock user account

# User Information
who                    # Show who is logged in
w                      # Show who is logged in and what they're doing
id username            # Show user ID and group info
groups username        # Show user's groups

# Privilege Escalation
su username            # Switch user
sudo command           # Execute as superuser
sudo -i               # Get root shell
```

### 10. Text Processing
```bash
# Basic Text Processing
sort file.txt          # Sort lines alphabetically
sort -n file.txt       # Sort numerically
sort -r file.txt       # Sort in reverse

uniq file.txt          # Remove adjacent duplicate lines
sort file.txt | uniq   # Remove all duplicates (must sort first)

# Counting
wc file.txt            # Count lines, words, characters
wc -l file.txt         # Count lines only

# Text Manipulation
cut -d: -f1 file.txt   # Cut first field using : delimiter
tr 'a-z' 'A-Z'         # Convert lowercase to uppercase

# Advanced Text Processing
sed 's/old/new/' file  # Replace first occurrence
sed 's/old/new/g' file # Replace all occurrences

awk '{print $1}' file  # Print first column
awk -F',' '{print $1,$3}' file # Use comma delimiter

# Practical Examples
# Count unique IP addresses in log file
cat access.log | cut -d' ' -f1 | sort | uniq -c | sort -nr

# Extract emails from text file
grep -E -o '\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,6}\b' file.txt

# Sum numbers in a column
awk '{sum += $1} END {print sum}' numbers.txt
```
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
rmdir dir*  # Deletes all directories with name 'dir'

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

chmod 755 filename  # Sets permissions to rwxr-xr-x (r = read) (w = write) (x = execute)
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

echo string > newfile # The specified string is placed in a new file
echo string >> existingfile # The specified string is appended to the end of an already existing file
echo $variable # The contents of the specified environment variable are displayed

head filename       # Displays the first 10 lines
head -n 20 filename # Displays the first 20 lines

tail filename       # Displays the last 10 lines
tail -n 20 filename # Displays the last 20 lines
tail -f filename    # Follows the file in real-time (useful for logs)

# Viewing Compressed Files
zcat compressed-file.txt.gz # To view a compressed file
zless somefile.gz # To page through a compressed file
zmore somefile.gz # To page through a compressed file
zgrep -i less somefile.gz # To search inside a compressed file
zdiff file1.txt.gz file2.txt.gz # 	To compare two compressed files

cat filename        # Displays file content
cat file1 file2     # Concatenates and displays multiple files
cat > filename      # Creates a new file and writes input to it (Ctrl+D to save)
cat file1 >> file2  # Appends file1 content to file2
cat file1 file2	# Concatenate multiple files and display the output; i.e. the entire content of the first file is followed by that of the second file
cat file1 file2 > newfile # 	Combine multiple files and save the output into a new file
cat file >> existingfile # Append a file to the end of an existing file
cat > file  # Any subsequent lines typed will go into the file, until CTRL-D is typed
cat >> file # Any subsequent lines are appended to the file, until CTRL-D is typed
cat << EOF > myfile # The string used to show the beginning and end of the process need not be EOF. It could be STOP or any other string not used in the content itself

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
ls g???? # List files with names starting with g and containing five letters
ls mk* # List files whose names begin with mk and end with any characters.
ls g[a-n]??? # List files having five letter names starting with g and second character between a-n.
ls g[!a-m]??? # List five letter names starting with g and not having the second character between a-m.
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

# Groups
sudo /usr/sbin/groupadd groupname # add new group
sudo /usr/sbin/groupdel groupname # remove group
sudo /usr/sbin/usermod -a -G groupname username # Adding a user to an already existing group

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
sort <filename>          # Sort lines alphabetically
sort -n <filename>       # Sort numerically
sort -r <filename>       # Sort in reverse order
cat file1 file2 | sort # Combine the two files, then sort the lines and display the output on the terminal
sort -k 3 <filename> # Sort the lines by the 3rd field on each line instead of the beginning

uniq <filename>          # Remove adjacent duplicate lines
sort <filename> | uniq   # Remove all duplicates (must sort first)

paste -d, file1 file2 # Combine lines from multiple files

# Counting
wc <filename>            # Count lines, words, characters
wc -l <filename>         # Count lines only

# Text Manipulation
cut -d: -f1 <filename>   # Cut first field using : delimiter
tr 'a-z' 'A-Z'         # Convert lowercase to uppercase

# Advanced Text Processing
sed 's/old/new/' file  # Replace first occurrence
sed 's/old/new/g' file # Replace all occurrences

# Sum numbers in a column
awk '{sum += $1} END {print sum}' numbers.txt
awk '{print $1}' file  # Print first column
awk -F',' '{print $1,$3}' file # Use comma delimiter

# Practical Examples
# Count unique IP addresses in log file
cat access.log | cut -d' ' -f1 | sort | uniq -c | sort -nr

# Extract emails from text file
grep -E -o '\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,6}\b' file.txt
grep [pattern] <filename> # Search for a pattern in a file and print all matching lines
grep -v [pattern] <filename> # 	Print all lines that do not match the pattern
grep [0-9] <filename> # Print the lines that contain the numbers 0 through 9
grep -C 3 [pattern] <filename> # Print context of lines (specified number of lines above and below the pattern) for matching the pattern. Here, the number of lines is specified as 3

strings book1.xls | grep my_string # TO search my_string in file book1.xls:
```

### 11. Networking Configuration and Tools

```bash
ping google.com # Check the status of the remote host

route –n or ip route # Show current routing table
route add -net address or ip route add # Add static route
route del -net address or ip route add # Delete static route

traceroute google.com # Print the route taken by the packet to reach the network host

scp <localfile> <user@remotesystem>:/home/user/ # Copy a local file to a remote system
```

### 12. The Bash Shell and Basic Scripting

`bash -x <filename>` Turns on debugging
`bash +x <filename>` Turns off debugging

- `#`	Used to add a comment, except when used as \#, or as #! when starting a script
- `\`	Used at the end of a line to indicate continuation on to the next line, or to indicate that the next character is to be interpreted literally, as in \$
- `;`	Used to interpret what follows as a new command to be executed after completion of the current command
- `$`	Indicates what follows is an environment variable
- `>`	Redirect output
- `>>`	Append output
- `<`	Redirect input
- `|`	Used to pipe the result into the next command
- `$0`	Script name
- `$1`	First parameter
- `$2, $3, etc.`	Second, third parameter, etc.
- `$*`	All parameters
- `$#`	Number of arguments
- `function_name () {}` Functions
- The if Statement
```
if [ <condition> ] ; then
    <statements>
elif [ <condition> ] ; then
    <statements> 
else
    <statements>
fi
```
- `-e` file	Checks if the file exists
- `-d` file	Checks if the file is a directory
- `-f` file	Checks if the file is a regular file (i.e., not a symbolic link, device node, directory, etc.)
- `-s` file	Checks if the file is of non-zero size
- `-g` file	Checks if the file has sgid set
- `-u` file	Checks if the file has suid set
- `-r` file	Checks if the file is readable
- `-w` file	Checks if the file is writable
- `-x` file	Checks if the file is executable
- `&&`	`AND`	The action will be performed only if both the conditions evaluate to true
- `||`	`OR`	The action will be performed if any one of the conditions evaluate to true
- `!`	`NOT`	The action will be performed only if the condition evaluates to false
- `-eq`	Equal to
- `-ne`	Not equal to
- `-gt`	Greater than
- `-lt`	Less than
- `-ge`	Greater than or equal to
- `-le`	Less than or equal t
- `[[ string1 > string2 ]]`	Compares the sorting order of string1 and string2
- `[[ string1 == string2 ]]`	Compares the characters in string1 with the characters in string2
- `myLen1=${#string1}`	Saves the length of string1 in the variable myLen1
- `${string#*.}` Extract all characters in a string after a dot (.)
- The case statement
  ```
  case <expression> in
     <pattern1>) <execute commands>;;
     <pattern2>) <execute commands>;;
     * )       <execute some default commands or nothing> 
     ;;
  esac
  ```
- The for loop
  ```
  for <variable-name> in <list>
  do
    <execute commands>
  done
  ```
- The while loop or condition is true
  ```
  while [ <condition> ] 
  do
    <execute commands>
  done
  ```
- The until loop or condition is false
  ```
  until [ <condition> ] 
  do
    <execute commands>
  done
  ```
- `stdin`	Standard Input, by default the keyboard/terminal for programs run from the command line	`0`
- `stdout`	Standard output, by default the screen for programs run from the command line	`1`
- `stderr`	Standard error, where output error messages are shown or saved; by default, the same as stdout	`2`
- `TEMP=$(mktemp /tmp/tempfile.XXXXXXXX)`	To create a temporary file
- `TEMPDIR=$(mktemp -d /tmp/tempdir.XXXXXXXX)`	To create a temporary directory
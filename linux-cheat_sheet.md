# Linux Commands and Their Uses

## Basic Commands
- **`ls`**: Lists files and directories in the current directory.
  - `ls -l`: Lists files in long format.
  - `ls -a`: Lists all files including hidden files.
- **`cd`**: Changes the current directory.
  - `cd /path/to/directory`: Navigates to the specified directory.
  - `cd ..`: Moves up one directory level.
- **`pwd`**: Prints the current working directory.
- **`mkdir`**: Creates a new directory.
  - `mkdir directory_name`: Creates a directory with the specified name.
- **`rmdir`**: Removes an empty directory.
  - `rmdir directory_name`: Removes the specified empty directory.
- **`rm`**: Removes files or directories.
  - `rm file_name`: Deletes the specified file.
  - `rm -r directory_name`: Recursively deletes the specified directory and its contents.
- **`cp`**: Copies files or directories.
  - `cp source_file destination_file`: Copies the source file to the destination file.
  - `cp -r source_directory destination_directory`: Recursively copies a directory and its contents.
- **`mv`**: Moves or renames files or directories.
  - `mv old_name new_name`: Renames or moves a file or directory.
- **`touch`**: Creates an empty file or updates the timestamp of an existing file.
  - `touch file_name`: Creates an empty file with the specified name.

## File Viewing and Editing
- **`cat`**: Concatenates and displays file content.
  - `cat file_name`: Displays the content of the specified file.
- **`more`**: Views file content one screen at a time.
  - `more file_name`: Displays the content of the specified file one screen at a time.
- **`less`**: Similar to `more` but allows backward movement in the file as well.
  - `less file_name`: Displays the content of the specified file with backward movement.
- **`head`**: Displays the first few lines of a file.
  - `head file_name`: Displays the first 10 lines of the specified file.
  - `head -n 20 file_name`: Displays the first 20 lines.
- **`tail`**: Displays the last few lines of a file.
  - `tail file_name`: Displays the last 10 lines of the specified file.
  - `tail -n 20 file_name`: Displays the last 20 lines.
- **`nano`**: A simple text editor in the terminal.
  - `nano file_name`: Opens the specified file in nano for editing.
- **`vi`** or **`vim`**: A powerful text editor.
  - `vi file_name`: Opens the specified file in vi or vim for editing.

## File Permissions and Ownership
- **`chmod`**: Changes file permissions.
  - `chmod 755 file_name`: Sets the specified permissions (owner can read/write/execute, others can read/execute).
- **`chown`**: Changes file ownership.
  - `chown user:group file_name`: Changes the owner and group of the specified file.
- **`chgrp`**: Changes the group ownership of a file.
  - `chgrp group_name file_name`: Changes the group ownership of the specified file.

## System Information
- **`uname`**: Displays system information.
  - `uname -a`: Displays all system information.
- **`top`**: Displays real-time system information and process statistics.
- **`ps`**: Displays currently running processes.
  - `ps aux`: Shows detailed information about all running processes.
- **`df`**: Displays disk space usage.
  - `df -h`: Shows disk space usage in a human-readable format.
- **`du`**: Displays directory space usage.
  - `du -h directory_name`: Shows directory space usage in a human-readable format.
- **`free`**: Displays memory usage.
  - `free -h`: Shows memory usage in a human-readable format.
- **`uptime`**: Displays how long the system has been running.

## Networking
- **`ping`**: Checks connectivity to a network host.
  - `ping hostname_or_ip`: Sends ICMP ECHO_REQUEST packets to network hosts.
- **`ifconfig`**: Configures network interfaces.
- **`wget`**: Downloads files from the web.
  - `wget url`: Downloads a file from the specified URL.
- **`curl`**: Transfers data from or to a server.
  - `curl url`: Retrieves data from the specified URL.

## Package Management
- **`apt-get`** (Debian/Ubuntu): Installs, upgrades, or removes packages.
  - `apt-get update`: Updates the package list.
  - `apt-get install package_name`: Installs the specified package.
  - `apt-get upgrade`: Upgrades all installed packages.
- **`yum`** (Red Hat/CentOS): Installs, upgrades, or removes packages.
  - `yum update`: Updates the package list.
  - `yum install package_name`: Installs the specified package.
  - `yum upgrade`: Upgrades all installed packages.

## Disk Management
- **`mount`**: Mounts a file system.
  - `mount device directory`: Mounts a device to a directory.
- **`umount`**: Unmounts a file system.
  - `umount directory`: Unmounts the file system from the directory.
- **`fdisk`**: Disk partitioning tool.
  - `fdisk /dev/sda`: Manages partitions on the specified disk.

## Searching and Finding Files
- **`find`**: Searches for files in a directory hierarchy.
  - `find /path -name file_name`: Finds files by name.
- **`grep`**: Searches for patterns within files.
  - `grep 'pattern' file_name`: Searches for a pattern in the specified file.
- **`locate`**: Finds files by name.
  - `locate file_name`: Locates files by name using a pre-built database.

## Archiving and Compression
- **`tar`**: Archives files.
  - `tar -cvf archive_name.tar directory_name`: Creates an archive from the specified directory.
  - `tar -xvf archive_name.tar`: Extracts an archive.
- **`gzip`**: Compresses files.
  - `gzip file_name`: Compresses the specified file.
- **`gunzip`**: Decompresses files.
  - `gunzip file_name.gz`: Decompresses the specified file.
- **`zip`**: Compresses files.
  - `zip archive_name.zip file_name`: Compresses the specified file into a ZIP archive.
- **`unzip`**: Decompresses files.
  - `unzip archive_name.zip`: Extracts the specified ZIP archive.

## User Management
- **`useradd`**: Adds a new user.
  - `useradd user_name`: Creates a new user.
- **`passwd`**: Changes a user's password.
  - `passwd user_name`: Changes the password for the specified user.
- **`usermod`**: Modifies a user account.
  - `usermod -aG group_name user_name`: Adds a user to a group.
- **`userdel`**: Deletes a user.
  - `userdel user_name`: Deletes the specified user

- **`df`**: Displays disk space usage.
  - `df -h`: Shows disk space usage in a human-readable format.
- **`du`**: Displays directory space usage.
  - `du -sh directory_name`: Shows the total size of the specified directory.
- **`mount`**: Mounts a file system.
  - `mount device directory`: Mounts a device to a directory.
- **`umount`**: Unmounts a file system.
  - `umount directory`: Unmounts the file system from the directory.
- **`fsck`**: Checks and repairs a Linux file system.
  - `fsck device`: Checks and repairs the specified device.

## Miscellaneous
- **`echo`**: Prints text to the terminal.
  - `echo "Hello, World!"`: Prints "Hello, World!" to the terminal.
- **`date`**: Displays or sets the system date and time.
  - `date`: Displays the current date and time.
- **`whoami`**: Displays the current user.
- **`man`**: Displays the manual for a command.
  - `man ls`: Displays the manual for the `ls` command.
- **`history`**: Displays the command history.
- **`alias`**: Creates a shortcut for a command.
  - `alias ll='ls -l'`: Creates an alias `ll` for `ls -l`

- **`crontab`**: Edits the cron table to schedule tasks.
  - `crontab -e`: Edits the current user's cron jobs.
  - `crontab -l`: Lists the current user's cron jobs.
- **`at`**: Schedules a one-time task to run at a specified time.
  - `at now + 1 hour`: Schedules a task to run in one hour.
- **`nohup`**: Runs a command immune to hangups, with output to a non-tty.
  - `nohup command &`: Runs the command, allowing it to continue running in the background after logging out.
- **`alias`**: Creates a shortcut for a command.
  - `alias ll='ls -l'`: Creates an alias `ll` for `ls -l`.
- **`df`**: Displays disk space usage.
  - `df -h`: Shows disk space usage in a human-readable format.
- **`du`**: Displays directory space usage.
  - `du -sh directory_name`: Shows the total size of the specified directory.
- **`uptime`**: Displays how long the system has been running.
- **`dmesg`**: Prints the kernel ring buffer messages.
  - `dmesg | less`: Views kernel messages one page at a time.
- **`history`**: Displays the command history.
  - `history`: Shows the list of commands entered.
  - `!n`: Repeats the `n`th command from history.



  ## Process Management
- **`kill`**: Sends a signal to a process.
  - `kill PID`: Sends the default `SIGTERM` signal to the specified process.
  - `kill -9 PID`: Sends the `SIGKILL` signal to forcefully terminate the process.
- **`pkill`**: Sends a signal to processes by name.
  - `pkill process_name`: Sends the default `SIGTERM` signal to processes with the specified name.
- **`bg`**: Resumes a suspended job in the background.
  - `bg %1`: Resumes job number 1 in the background.
- **`fg`**: Brings a job to the foreground.
  - `fg %1`: Brings job number 1 to the foreground.
- **`jobs`**: Lists current jobs.
  - `jobs`: Displays the status of jobs in the current session.

## Networking
- **`netstat`**: Displays network connections, routing tables, interface statistics, masquerade connections, and multicast memberships.
  - `netstat -tuln`: Shows all listening ports.
- **`ss`**: Another utility to investigate sockets.
  - `ss -tuln`: Displays listening TCP and UDP ports.
- **`traceroute`**: Traces the route packets take to a network host.
  - `traceroute hostname_or_ip`: Traces the route to the specified host.
- **`dig`**: Queries DNS name servers.
  - `dig domain`: Retrieves DNS information for the specified domain.
- **`nslookup`**: Queries DNS and retrieves information about domain names and IP addresses.
  - `nslookup domain`: Looks up DNS information for the specified domain.
- **`iptables`**: Configures the Linux kernel firewall.
  - `iptables -L`: Lists current firewall rules.

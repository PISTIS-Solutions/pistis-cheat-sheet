### INTRODUCTION:

If you're looking for a rapid review of SSH commands or beginning your journey with SSH, there's nothing quite like having a convenient guide on hand. Sorting through the multitude of SSH or OpenSSH commands can be daunting, especially when determining their relevance to your specific task at hand. SSH is indispensable for network administrators and anyone requiring access to remote computers and servers.

Excitingly, we've compiled a concise and straightforward SSH cheat sheet designed for both novice and seasoned users. This resource encompasses fundamental SSH commands, configurations, and options, as well as guidance on remote server administration, advanced SSH operations, and tunneling techniques. Additionally, it provides insights into utilizing a router and Wireshark for capturing web traffic on a remote host.


### What Is SSH?

SSH, abbreviated for "Secure Shell" or "Secure Socket Shell," stands as a network protocol facilitating secure access to network services across unsecured networks. It encompasses a suite of utilities, including:

- `ssh-keygen`: utilized for generating new authentication key pairs for SSH;
- SCP (Secure Copy Protocol): employed for transferring files between network hosts;
- SFTP (Secure File Transfer Protocol): employed for transmitting and receiving files securely. It serves as an SSH-protected alternative to FTP (File Transfer Protocol), having supplanted FTP and FTPS (FTP Secure) as the preferred means for internet file sharing.

By default, an SSH server listens for connections on the standard Transmission Control Protocol (TCP) port 22. However, applications may opt to listen for SSH connections on alternative ports.

SSH empowers users to securely administer remote systems and applications. This encompasses tasks such as remotely logging into another computer over a network, executing commands, and transferring files between computers. Moreover, SSH boasts advanced functionality, enabling the establishment of secure tunnels for remotely executing other application protocols.


### Basic SSH Commands

Here are some essential SSH commands. Try to memorize as many as possible.



| COMMAND | DESCRIPTION |
| ----------- | ----------- |
| ssh | Connect to a remote server |
| ssh david@pistis | Connect to the device pistis on the default SSH port 22 as user david |
| ssh david@pistis -p 3344 | Connect to the device pistis on a specific port 3344 as user david |
| ssh -i /path/file.pem admin@192.168.1.1 | Connect to root@192.168.1.1 via the key file /path/file.pem as user admin |
| ssh root@192.168.2.2 'ls -l' | Execute remote command ls -l on 192.168.2.2 as user root |
| $ ssh user@192.168.3.3 bash < script.sh | Invoke the script script.sh in the current working directory spawning the SSH session to 192.168.3.3 as user user |
| ssh friend@Best.local "tar cvzf - ~/ffmpeg" > output.tgz | Compress the ~/ffmpeg directory and download it from a server Best.local as user friend |
| ssh-keygen | Generate SSH keys (follow the prompts) |
| ssh-keygen -F [ip/hostname] | Search for some IP address or hostname from ~/.ssh/known_hosts (logged-in host) |
| ssh-keygen -R [ip/hostname] | Remove some IP address or hostname from ~/.ssh/known_hosts (logged-in host) |
| ssh-keygen -f ~/.ssh/filename | Specify file name |
| ssh-keygen -y -f private.key > public.pub | Generate public key from private key |
| ssh-keygen -c -f ~/.ssh/id_rsa | Change the comment of the key file ~/.ssh/id_rsa |
| ssh-keygen -p -f ~/.ssh/id_rsa | Change passphrase of private key ~/.ssh/id_rsa |
| ssh-keygen -t rsa -b 4096 -C "my@email.com" | Generate an RSA 4096-bit key with “my@email.com” as a comment: -t: Type of key (rsa, ed25519, dsa, ecdsa); -b: The number of bits in the key; -C: Provides a new comment |
| scp | Copy files securely between servers |
| scp user@server:/folder/file.ext dest/ | Copy from remote to local destination dest/ |
| scp dest/file.ext user@server:/folder | Copy from local to remote |
| scp user1@server1:/file.ext user2@server2:/folder | Copy between two different servers |
| scp user@server:/folder/* . | Copies from a server folder to the current folder on the local machine |
| scp -r | Recursively copy entire directories |
| scp -r user@server:/folder dest/ | Copy the entire folder to the local destination dest/ |
| scp user@server:/folder/* dest/ | Copy all files from a folder to the local destination dest/ |
| scp -C | Option to compress data |
| scp -v | Option to print verbose info |
| scp -p | Option to preserve the last modification timestamps of the transferred files |
| scp -P 8080 | Option to connect to remote host port 8080 |
| scp -B | Option for batch mode and prevent you from entering passwords or passphrases |
| sftp | Securely transfer files between servers |
| sftp -p | Option to preserve the last modification timestamps of the transferred files |
| sftp -P 8080 | Option to connect to remote host port 8080 |
| sftp -r | Recursively copy entire directories when uploading and downloading. SFTP doesn’t follow symbolic links encountered in the tree traversal. |

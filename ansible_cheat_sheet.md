# ANSIBLE CHEAT SHEET
<br />

## WHAT IS ANSIBLE
Ansible is a continuous deployment and 
configuration tool which provides large productivity 
gains to a wide variety of automation challenges. It is an open source engine that automates deployment, 
orchestration, cloud provisioning and other tools. It uses a playbook to describe jobs and uses YAML which is human readable.

<br />

## HOW DOES IT WORK?
```markdown
• Connects nodes and pushes small programs called modules to them 
and are removed when they are done.
• The management node controls whole execution of the playbook. 
• The inventory file provides the list of hosts where the modules need 
to be run. 
• The management node does an ‘ssh’ connection and executes the 
modules and installs the software
```
<br />

## ENVIRONMENT SETUP, SSH KEY GENERATION AND ANSIBLE INSTALLATION
### Environment Setup
```markdown
Types of machines:
    • Control machine : manages other machines
    • Remote machine: controlled by other machines
Multiple remote systems can be handled by one machine.
    • Remote machine managing is done by ansible by default.
    • Ansible doesn’t leave any software running on them. Therefore there is no need of an upgrade when moving to a newer version.
```

### SSH Key Generation
Ansible uses SSH to communicate between the nodes.
```markdown
#Setting Up SSH Command 
$ sudo apt-get install openssh-server
#Generating SSH Key
$ ssh-keygen 
#Copy the SSH Key on the Hosts 
$ ssh-copy-id hostname 
#Check the SSH Connection
$ ssh <nodeName>
```


### Install Ansible 
To install Ansible in Debian Linux, follow the following steps:

```markdown
Add Ansible repository
$ sudo apt-add-repository ppa:ansible/ansible 
#Run the update command
$ sudo apt-get update 
#Install Ansible package
$ sudo apt-get install ansible 
#Check Ansible Version
$ ansible –version
```

<br />

## INVENTORY FILES & HOSTS PATTERNS

Ansible’s inventory lists all the platforms you want to automate across. Ansible can at a single instance work on multiple hosts in the
infrastructure

### Setup & Hosts Connection
Follow the below steps to set hosts and then check their connection.

```markdown
#Set up hosts by editing the hosts' file in the Ansible directory
$ sudo nano /etc/ansible/hosts 
#To check the connection to hosts
#First change the directory to /etc/Ansible
$ cd /etc/ansible 
#To check whether Ansible is connecting to hosts, use ping command
$ ansible –m ping <hosts> 
#To check on servers individually
$ ansible -m ping server name 
#To check a particular server group
$ ansible -m ping servergroupname
```

### Ansible Hosts Pattern
| | |
| ---------- | ---------- |
| a | b | 
| all | All hosts in inventory |
| * | All hosts in inventory |
| ungrouped | All hosts in inventory not appearing within a group |
| 10.0.0.* | All hosts with an IP starting 10.0.0.* |
| webservers | The group webservers |
| webservers:!moscow | Only hosts in webservers, not also in group moscow |
| webservers:&moscow | Only hosts in the group’s webservers and moscow |

### Example Inventory File
The below is an example inventory file, which you can refer to understand the various parameters.
| | |
| ----------- | ---------- |
| ungrouped.example.com | #An ungrouped host |
| [webservers] | #A group called webservers |
| beta.example.com ansible_host = 10.0.0.5 | #ssh to 10.0.0.5 |
| github.example.com ansible_ssh_user = abc | #ssh as user abc |
| [clouds] 
cloud.example.com fileuser = alice | #fileuser is a host variable |
| [moscow] 
| beta.example.com | #Host (DNS will resolve) |
| telecom.example.com | #Host(DNS will resolve) |
| [dev1:children] | #dev1 is a group containing |
| webservers | #All hosts in group webservers |
| clouds | #All hosts in group clouds |
<br />

## ADHOC COMMANDS
Ad-Hoc commands are quick commands which are used to perform the actions, that won’t be saved for later.

### Parallelism & Shell Commands
```markdown
#To set up SSH agent
`$ ssh-agent bash $ ssh-add ~/.ssh/id_rsa`
#To use SSH with a password instead of keys, you can use --ask-pass (-K)
$ ansible europe -a "/sbin/reboot" -f 20 
#To run /usr/bin/ansible from a user account, not the root
$ ansible europe -a "/usr/bin/foo" -u username 
#To run commands through privilege escalation and not through user account
$ ansible europe -a "/usr/bin/foo" -u username --become [--ask-become-pass] 
#If you are using password less method then use --ask-become-pass (-K) to interactively get the password to be use 
#You can become a user, other than root by using --become-user
$ ansible europe -a "/usr/bin/foo" -u username --become --become-user otheruser [--ask-become-pass]
```

### Host Connection
```markdown
#Check connectivity of hosts 
$ ansible <group> -m ping
#Rebooting hosts 
$ ansible <group> -a “/bin/reboot”
#Check host system’s info 
$ ansible<group> -m steup | less
```

### File Transfer
```markdown
#Transfer a file directly to many servers
$ ansible europe -m copy -a "src=/etc/hosts dest=/tmp/hosts" 
#To change the ownership and permissions on files
$ ansible webservers -m file -a "dest=/srv/foo/a.txt mode=600" $ ansible webservers -m file -a "dest=/srv/foo/b.txt 
mode=600 owner=example group=example" 
#To create directories
$ ansible webservers -m file -a "dest=/path/to/c mode=755 owner=example group=example state=directory“
#To delete directories (recursively) and delete files
$ ansible webservers -m file -a "dest=/path/to/c state=absent
```

### Managing User
```markdown
#Create new user
$ ansible<group> -m user -a “name=ansible 
password= <encrypted password>”
#Deleting user
$ ansible<group> -m user -a “name=ansible 
state- absent”
```

### Manage Packages
```markdown
#To ensure that a package is installed, but doesn’t get updated
$ ansible webservers -m apt -a "name=acme state=present" 
#To ensure that a package is installed to a specific version
$ ansible webservers -m apt -a "name=acme-1.5 state=present" 
#To ensure that a package at the latest version
$ ansible webservers -m apt -a "name=acme state=latest" 
#To ensure that a package is not installed
$ ansible webservers -m apt -a "name=acme state=absent
```

### Manage Services
```markdown
#To ensure a service is started on all web servers
$ ansible webservers -m service -a "name=httpd
state=started" 
#To restart a service on all web servers
$ ansible webservers -m service -a "name=httpd
state=restarted" 
#To ensure a service is stopped
$ ansible webservers -m service -a "name=httpd
state=stopped
```

### Deploying From Source Control
```markdown
#GitRep:https://foo.example.org/repo.git #Destination:/src/myapp
$ ansible webservers -m git -a "repo=https://foo.example.org/repo.git dest=/src/myapp version=HEAD"
```
<br />

## PLAYBOOK
It is the place where all YAML files are stored. A playbook can have more than one plays. Plays map the instructions defined against a particular host.

### Playbook and YAML
A YAML mapping entry is a key and a value
`parameter: value`

A YAML sequence entry is an itemized list and each element has to be written in a new line
```markdown
- foo
- bar
- baz
```

A mapping entry can contain a sequence
OS:
```markdown
Distro:
 - Fedora
 - RHEL
 - Debian
 - Slackware
 ```

Sequence items can contain mappings
```markdown
 - Linux: Fedora
 - BSD: NetBSD
 ```

 Boolean terms are also used in YAML

Tags of YAML:
```markdown
1. Name: name of the playbook
2. Hosts: specifies the lists of hosts. Tasks can be on the same machine or a different one.
3. Vars: defines the variables which you can use
4. Tasks: it is the list of actions that need to be performed. A task is always linked to a module.
```

### Playbook structure
|  |  |
| ----------- | ---------- |
| ---  | YAML files start with three dashes |
| - name: “My play” | Use the name mapping to name your play |
| &ensp; hosts: all | Indent, and define which hosts the play runs on. List target hosts in etc/ansible/hosts |
| &ensp; tasks: | Open a tasks mapping, which will contain a sequence |
| &ensp; - name: | “My task” Give the task a name with the name mapping |
| &ensp;&ensp; some_module: | Import a module as a new mapping containing a sequence of parameters. Find required and optional parameters in the module’s documentation. |
| &ensp;&ensp;&ensp;&ensp;path: ‘/example/’ | Parameters are usually mappings using the command option as the key and an argument as the value. |
| &ensp; - name: “My other task” | A play may contain more than one task |
| &ensp;&ensp; other_module: | A task usually imports a module |
| &ensp;&ensp; foo: ‘bar’ |

### Sample Playbook
```markdown
#Every YAML file starts with ---
---
- hosts: webservers 
  vars: http_port: 80 
  max_clients: 200 
  remote_user: root 
 tasks: 
 -name: ensure apache is at the latest version 
     apt: name=httpd state=latest 
 -name: write the apache config file 
    template: src=/srv/httpd.j2 dest=/etc/httpd.conf
  notify: -
   -restart apache 
  -name: ensure apache is running (and enable it at boot)
   service: name=httpd state=started enabled=yes 
handlers: 
  -name: restart apache 
  service: name=httpd state=restarted
```

### Writing Playbooks
#Generate the SSH Key and connect hosts to control
machine before writing and running playbooks.

#Create a Playbook
```markdown
$ vi <name of your file>.yml
```
#To write the playbook refer to the snapshot [here](https://www.edureka.co/blog/ansible-tutorial/#hands_on).

#Run the playbook
```markdown
$ ansible-playbook <name of your file>.yml
```

<br />

## VARIABLES
```markdown
• Same as using variables in programming languages
    Ex: - hosts : <your hosts> 
    • tomcat_port : 8080
    • Here tomcat_port is assigned to 8080
• Keywords used:
    • Block- ansible syntax to execute a block
    • Name- name of the block
    • Action- the code that is to be executed
    • Register- registers the output 
    • Always- states that below word will be run
    • Msg- displays the message 
• Exception handling:
    • Similar to any other programming language
    • Keywords : rescue and always 
    • The code is written in block
    • It goes to the rescue phase and gets executed 
    if the command in the block fails.
    • Thereby block is the same as “try block “, 
    catch block is like “ rescue” and always 
    performs the same function as we know.
```

<br />

## TROUBLESHOOTING
```markdown
 Common strategies to debug playbooks are 
    • Debug and register 
    • Use verbosity (verbosity level)
• Playbook issues: 
    • Quoting
    • Indentation
• Some drawbacks are:
    • OS restrictions: is OS dependent so code on one OS will 
    not work for another
    • Once playbook is running, adding of hosts is not possible
    • Error reporting is mediocre.
```
# User and group management
## Prerequisites
- Successful SSH access
- Ubuntu server running
- Basic Linux command line


## Introduction
Linux is a multi-user operating system where multiple people can create user accounts for their personal purposes. Every user will have their own permissions, access controls and privileges which are determined by the organization or the root user.
The root user has unrestricted access to the system and any changes made by the root user are allowed and is also one reason why it is recommended to use a user profile for daily tasks as even one small mistake can change the system and cause potential issues which might affect the system as a whole.


## Objective
To create a dedicated user for administrative purposes and organize permissions using groups
Grant sudo privileges to the user and reduce the dependence upon the default Ubuntu user.


## Background
- Linux Users  
Every person or service runs as a user and has their own unique ID. Each user has their own home directory and user ID while the process has a PID. 
- Groups  
A group is a collection of users to maintain user privleges and control the environment as a whole. It simplifies permission management as it assigns the privileges to a group and anyone in it, automatically has those privileges. Users can belong to multiple groups too.
- Sudo  
It is used to execute commands with elevated privileges and is controlled through the sudo group. Anyone within the sudo group has access to sudo privileges. It is safer than logging in directly as the root as it allows authorized users to execute administration level commands without logging in as the root so that no critical infrastructure of the system is messed up.
- Root user  
This is the highest privileged account. Unrestricted access to the system. It's UID is 0. It has unrestricted control over the system and is often a best practice to avoid using it for daily administration.
- Home Directory  
This is the personal workspace for every user created and it stores the user configuration and also contains the .ssh directory
- File Ownership  
```text
Owner
↓
Group
↓
Others
```
Owner is the creator of the file or the one who owns it.
Group is the collection of users within the same group as the owner.
Others are other users outside of the groups in which the owner is present.
All of these different user accounts have different levels of permissions.
r - read(4)
w - write(2)
x - execute(1)
A file with only read and write access for owner and group would have the following permission
rw-rw---- and corresponds to 660
- UID  
Unique numeric identifier for identifying each user in the system and specific to that user. Root always has an ID = 0. Regular users have a non-zero UID.


## Implementation
```text
Create user
↓
Set password
↓
Create home directory
↓
Copy authorized_keys
↓
Set ownership
↓
Add user to sudo group
↓
Verify login
```


## Commands Used
```bash
 sudo adduser devops

 sudo usermod -aG sudo devops

 id devops

 groups devops

 ls -la /home/devops

 sudo chown -R devops:devops /home/devops/.ssh
 
 sudo chmod 700 /home/devops/.ssh
 sudo chmod 600 /home/devops/.ssh/authorized_keys
```


## Verification
```text
Login as new user
↓
whoami
↓
groups
↓
sudo command successful
```


## Lessons Learned
- Linux users  and groups
- Principle of Least Privilege
- sudo administration
- Home directory structure
- File ownership and permissions
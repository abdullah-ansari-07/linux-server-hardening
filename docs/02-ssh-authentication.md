SSH Authentication
# Prerequisites
- Completed EC2 setup
- Running Ubuntu EC2 instance
- Downloaded .pem private key

# Introduction
SSH (Secure Shell) is a cryptographic network protocol for secure communication, remote shell services, command executions and other secure network services between two computers.
It was designed to replace Telnet and make it secure.
Devices can be connected and administered over the network by securing an encrypted connection over the network for purposes specific to the user.

# Objective
To use the .pem containing the private key to SSH into our AWS EC2 instance through our device's command line terminal.
No passwords are to be used and identity to be verified only through SSH Key Authentication

# Background
- SSH  
SSH stands for Secure Shell. It is a protocol for remote administration and encrypted communication between 2 devices over a network.
SSH replaces insecure protocols like Telnet which sent packets of confidential data and secrets over the network in plain text and was very much prone to attackers gaining access to it and reading confidential data mostly through Man-in-the-middle attacks.
- Client and Server  
The SSH Client, I, initiated a connection through the command line which sent a request to the SSH server (sshd) which checks the incoming request and verifies the authenticity of the connection request before accepting the connection. Our local machine is the client while the EC2 instance is the server.
- SSH Daemon  
The SSH Daemon (sshd) deals with all the background services of the SSh. It listens on port 22 for any incoming SSH connections, performs authentication and starts the user's shell session.
- Key Pair Authentication  
Creating an SSH key generates 2 keys, one public which is stored in AWS EC2 instance and one private key, which is stored in our local device. During SSH key authentication, the server generates a random challenge for the private key present in our system which signs it and sends the signed copy back to public key which verifies the authenticity of the challenge solved and the signature attached. 
- Authorized_keys  
This file contains the public key stored in the AWS EC2 instance. It is located inside ~/.ssh in the server and is used during authentication.
- Port 22
    - Default SSH port
    - Listened to by sshd
    - Used for secure remote administration

# Implementation
The following sequence was used to establish the initial SSH connection.
```text
Locate .pem
↓
chmod 400
↓
ssh -i key.pem ubuntu@public-ip
↓
Host authenticity
↓
Accept fingerprint
↓
Login successful
```

chmod 400 gives read permission for the owner only and gives no access to others in the group or other external groups. This is done to ensure security and data privacy.

# Commands Used
```bash
 chmod 400 key.pem
 
 ssh -i key.pem ubuntu@<public-ip>
 
 exit
```

# Verification
```text
Successful login
↓
Ubuntu MOTD displayed
↓
Shell prompt appeared
↓
whoami
↓
hostname
```
# SSH Key Authentication Visualised
```text
Local Machine
(private key)
        │
        │ SSH
        ▼
Internet
        │
        ▼
EC2 Instance
(authorized_keys)
        │
        ▼
Authentication Successful
```

# Lessons Learned
- SSH into a remote server from local machine
- Challenge response authentication concept
- Public and Private SSH Keys
- Importance of file permissions (chmod)
- Host fingerprint verification
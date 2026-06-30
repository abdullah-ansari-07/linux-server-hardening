SSH Hardening
# Prerequisite
- Successful SSH authentication
- Dedicated administrative user created
- Sudo privileges

# Introduction
SSH is secure by default as it encrypts the data over the network so that only authorized personnel can access it.
Although SSH is secure by default, additional hardening reduces the attack surface. Even though it is protected, it still is open to others and is important to prevent unauthorized access.

# Objective
To secure the SSH service further by disabling unnecessary authentication methods. This will help restrict who can login. It also helps reduce brute-force attack opportunities.

# Background
- SSH Configuration file  
This is the main SSH server configuration file and is stored in `/etc/ssh/sshd_config`. This file is read by sshd for configuration and any changes to this require service restart/reload.
- Password Authentication  
This is the concept of using a username and password for authentication which is also best susceptible to brute-force attacks. This is disabled in favour of key authentication.
- Public Key Authentication  
It uses cryptographic key pair and is far more secure than password authentication. It is enabled by default when the SSH key pair is generated.
- Root Login  
This is the highest privileged account in the system and is a high-value attack target. It is usually disabled for security purposes. 
```bash
PermitRootLogin no
```
- Principle of Least Privilege  
The idea of giving users only the least amount of privilege which is necessary to accomplish their specific tasks.
- Attack Surface  
It is the collection of all possible entry points from where an attacker could try to gain access or compromise a system. Reducing unnecessary services or authentication methods reduces the attack surface.

# Implementation
```text
Open sshd_config
↓
Create backup
↓
Edit configuration
↓
Disable password authentication
↓
Disable root login
↓
Save configuration
↓
Test configuration
↓
Restart SSH
↓
Verify connection
```
Testing the configuration before restarting the SSH service is an important factor as it helps prevent configuration errors from locking administrations out of the server.

# Configuration Changes

| Setting | Before | After | Reason |
| ------- | ------ | ----- | ------ |
| PasswordAuthentication | yes | no | Reduce attack-surface | 
| PubkeyAuthentication | yes | yes | Keep SSH key authentication enabled |
| PermitRootLogin | yes (or default) | no | Prevent direct root logins |

# Commands Used
```bash
 sudo cp /etc/ssh/sshd_config /etc/ssh/sshd_config.bak
 
 sudo nano /etc/ssh/sshd_config
 
 sudo sshd -t
 
 sudo systemctl restart ssh
 
 sudo systemctl status ssh
```

# Verification
```text
Configuration test passed
↓
SSH service restarted
↓
Reconnect successful
↓
Password login rejected
↓
SSH key login successful
```
# Lessons Learned
- SSH server configuration
- SSH configuration testing
- Passwordless authentication
- Principle of Least Privilege
- Safe service restart procedure
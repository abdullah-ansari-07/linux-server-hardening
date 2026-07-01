# Automatic System Updates
## Prerequisites
- Ubuntu server running
- Internet connectivity
- Administrative user with sudo privileges


## Introduction
Software vulnerabilities are regularly discovered everywhere, even in the most secure systems, there are vulnerabilities which are waiting to be exploited by hackers. Security patches fix these vulnerabilities to secure the software and automatic updates make sure the security patch is updated whenever there is an update. This reduces the time the software remains vulnerable. Ubuntu provides unattended-upgrades for this purpose.


## Objective
Setting up automatic security updates in order to keep the system patched and up-to-date with security fixes. It helps reduce manual maintenance and improves long-term security.


## Background
- Package Manager(APT)  
APT stands for Advanced Package Tools, a package manager which install, update and manage softwares in the system. They also help resolve dependencies.
Update and upgrade are the most frequently used apt commands.  
    - apt update  
    Only updates the local package index about the upgrades available
    - apt upgrade  
    Does the actual system upgrade to the latest available version
- Repositories
These are the official software repositories provided by Ubuntu where the new upgrades are released and stored for all the systems to check and upgrade.
- Security Updates
These are regular upgrades released to fix security issues and mostly contain bug fixes, vulnerability patches, stability improvements and cover other security concerns. The linux server is configured to have automatic security updates.
- unattended-upgrades
This is a built-in package in Ubuntu which installs security updates automatically and runs without any user intervention

- Why Automatic Updates?
Automatic updates reduce exposure to known vulnerabilities and protect the system as sometimes the administrator might forget to update the system or the servers may be running continuously. Automatic updates makes sure the system stays up-to-date.


## Implementation
```text
Install unattended-upgrades
        ↓
Enable automatic updates
        ↓
Configure update settings
        ↓
Enable periodic execution
        ↓
Verify configuration
```


## Commands Used
```bash
 sudo apt update
 
 sudo apt install unattended-upgrades

 sudo dpkg-reconfigure unattended-upgrades

 sudo nano /etc/apt/apt.conf.d/20auto-upgrades

 sudo nano /etc/apt/apt.conf.d/50unattended-upgrades

 sudo unattended-upgrade --dry-run --debug
```


## Configuration Changes
| File                                        | Purpose                              |
| ------------------------------------------- | ------------------------------------ |
| `/etc/apt/apt.conf.d/20auto-upgrades`       | Enable periodic updates              |
| `/etc/apt/apt.conf.d/50unattended-upgrades` | Configure automatic security updates |


## Verification
```text
Package installed
↓
Configuration enabled
↓
Dry run successful
↓
No configuration errors
```


## Lessons Learned
- Ubuntu package management
- APT repositories
- Security patch management
- Automatic system maintenance
- Importance of regular updates
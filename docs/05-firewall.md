# Firewall
## Prerequisites
- Ubuntu server running
- SSH configured
- Administrative user with sudo privileges


## Introduction
Firewall is one of the most important defensive layers in securing a network. It controls network traffic to and from the server. Network traffic should not have access to all the services in the server and must be restricted.
Default-deny secures the server at a higher level than default-allow as it does not allow access without the necessary permissions.
UFW - Uncomplicated Firewall simplifies the Linux firewall management 


## Objectives
The main objective here is to configure the firewall to allow only required services and block all other incoming traffic. Setting up the firewall also reduces the attack surface, which is the ultimate goal.


## Background
- Firewall  
It is a network security layer which filters incoming and outgoing traffic in the network. It also manages connections on the network by allowing or blocking the connections over the network.
- UFW  
It stands for Uncomplicated Firewall and is a command-line utility which acts as the Front-end for iptables/nftables in the network. It simplifies the firewall management in Linux. UFW is the default firewall manager for Ubuntu.
- Default Policies  
By default, all incoming traffic is blocked and all outgoing traffic is allowed. This is because there could be attackers who want to attack the system and gain access for malicious purposes while outgoing traffic is allowed because it is initiated by processes already running on the system.
- Rules
Rules are the basic permissions in Linux and are of the following kind:
1. allow  - allows the connection
2. deny   - blocks the connection
3. reject - blocks the connection and notify the sender
4. limit  - rate limits the repeated connection attempts
- Port 22
SSH uses TCP port 22. It must remain open before enabling the firewall because the firewall rules are not configured yet and can block us out of the server as well. Incorrect firewall rules may prevent further SSH access to the server.


## Implementation
```text
Check UFW status
↓
Allow OpenSSH
↓
Enable firewall
↓
Verify status
↓
Confirm SSH remains accessible
```
Check the status of UFW and allow OpenSSH before enabling firewall as not doing so will block the administrator from accessing the server via SSH.


## Commands Used
```bash
 sudo ufw status

 sudo ufw allow OpenSSH

 sudo ufw enable

 sudo ufw status verbose
```


## Firewall Rules
| Rule     | Action | Reason                               |
| -------- | ------ | ------------------------------------ |
| OpenSSH  | Allow  | Maintain remote administration       |
| Incoming | Deny   | Block unsolicited traffic            |
| Outgoing | Allow  | Permit normal outbound communication |


## Verification
```text
Firewall active
↓
OpenSSH allowed
↓
Default incoming policy = deny
↓
SSH session remained connected
```


## Lessons Learned
- Linux firewall concepts
- Default-deny security model
- UFW rule management
- Importance of allowing SSH before enabling UFW
- Network attack surface reduction
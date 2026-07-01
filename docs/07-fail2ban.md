# Fail2Ban
## Prerequisites
- Ubuntu server running
- SSH configured
- UFW Firewall enabled
- Administrative user with sudo privileges


## Introduction
Authentication services are constantly targetted by brute-force attacks. Password authentication is particularly vulnerable to such attacks. Fail2Ban monitors the log files and temporarily bans IP addresses which have suspicious activity on the network. Fail2Ban adds another layer of defense behind the firewall. It strengthens the security of the server.


## Objective
To detect repeated failed SSH login attempts and automatically ban IP addresses that exhibit suspicious behaviour. It helps reduce brute-force attacks and increases server security.


## Background
- Fail2Ban
Fail2Ban is an intrusion prevention tool which monitors log files and detects suspicious behaviour. It then temporarily bans the suspicious IP address from accessing the network for the configured ban time.
- Brute-Force Attack
This is a type of security threat where the attacker takes repeated attempts to guess usernames or passwords in a password authentication system of software/system/server.
- Jail
Jail is a configuration section which combines filter, log file and action and enhances security. It specifies what services to protect, which logs to monitor, how to recognise malicious behaviour, and what actions to take when such behaviour is detected.
Example Jail
```bash
[sshd]
enabled = true
port = ssh
filter = sshd
logpath = /var/log/auth.log
maxretry = 5
findtime = 10m
bantime = 1h
```
- Filter
A filter defines which log entries are considered suspicious based on predefined patterns.
- Actions
```text
Ban IP
↓
iptables/UFW rule
↓
Temporary block
```
- Authentication Logs
Fail2Ban watches `/var/log/auth.log` checks for SSH authentication failures and applies the configured rules when matching log entries are detected.
- Ban Parameters
    - bantime  - How long an IP remains banned
    - findtime - Time window between multiple failed attempts
    - maxretry - maximum failed attempts in the given time frame


## Implementation
```text
Install Fail2Ban
        ↓
Copy jail.conf → jail.local
        ↓
Enable SSH jail
        ↓
Configure ban settings
        ↓
Start service
        ↓
Verify status
```


## Configuration Changes
| Setting  | Value | Purpose                 |
| -------- | ----- | ----------------------- |
| enabled  | true  | Enable SSH protection   |
| bantime  | 10m   | Ban duration            |
| findtime | 10m   | Observation window      |
| maxretry | 5     | Allowed failed attempts |


## Commands Used
```bash
 sudo apt install fail2ban

 sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local

 sudo nano /etc/fail2ban/jail.local

 sudo systemctl restart fail2ban

 sudo systemctl status fail2ban

 sudo fail2ban-client status

 sudo journalctl -u fail2ban

 sudo fail2ban-client -d
 ```


 ## Troubleshooting
One issue I encountered was Fail2Ban failed to start after configuration and I had to investigate the issue
- Commands to investigate
```bash
 systemctl status fail2ban

 journalctl -u fail2ban

 fail2ban-client -d
```
- Root cause
I found a duplicate `[sshd]` section in the `jail.local` file which was causing a configuration  parsing conflict and the program quit.
- Resolution
Removed the duplicate section and restarted Fail2Ban and then verified that it started successfully.
Configuration files should contain unique section names only.
- Debugging walk-through
```text
Service failed
    ↓
Read logs
    ↓
Identify duplicate [sshd]
    ↓
Fix configuration
    ↓
Restart service
    ↓
Verify
```


## Verification
```text
Fail2Ban service running
↓
SSH jail active
↓
Configuration loaded
↓
No startup errors
```


## Lessons Learned
- Fail2Ban configuration
- Intrusion prevention
- SSH brute-force protection
- Reading Linux logs
- Debugging system services
- Importance of configuration validation
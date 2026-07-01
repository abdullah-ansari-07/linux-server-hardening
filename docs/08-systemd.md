# Systemd
## Prerequisites
- Ubuntu server running
- Administrative user with sudo privileges
- Basic understanding of Linux services


## Introduction
Linux runs many background services which need to be managed, started, stopped, and monitored. systemd is Ubuntu's initialization and service management system. It also provides centralized logging through journald.


## Objectives
To manage Linux services, understand service states, inspect system logs, and troubleshoot service failures.


## Background
- systemd  
An init system is the first process that starts after the Linux kernel finishes booting. It initializes the rest of the operating system.
The service manager controls the background services (called daemons). It manages, starts, stops, restarts, reloads, enables, disables and checks service processes in the system.
- Service  
A service is a background process that performs a specific task without user interaction. Ex: sshd, fail2ban, cron
- Daemon
A daemon is a background process that waits for events or requests and provides a service when required. Ex: sshd
- Socket Activation
systemd listens on network sockets and services start only when a connection arrives. This reduces unnecessary resource usage. Modern Ubuntu commonly uses socket activation for OpenSSH.
- journalctl
Reads logs collected by systemd-journald
```bash
 journalctl

 journalctl -u
 
 journalctl --since

 journalctl -b

 journalctl -p
 ```
- Service states
Shows the current state of each service currently
active - service is running
inactive - service is not running
failed - service failed to start
enabled - service enabled(starts automatically during system boot)
disabled - service disabled(service does not automatically start during boot)


## Implementation
```text
View service status
        ↓
Start service
        ↓
Restart service
        ↓
Check logs
        ↓
Investigate failures
        ↓
Verify service
```


## Commands Used
```bash
 systemctl status ssh

 systemctl status fail2ban

 systemctl start

 systemctl stop

 systemctl restart

 systemctl reload

 systemctl is-active

 systemctl is-enabled

 systemctl show

 systemctl cat

 systemctl list-dependencies

 journalctl -u ssh

 journalctl -u fail2ban

 journalctl --since "1 hour ago"

 journalctl -b

 journalctl -p err
```


## Service Management Commands
| Command      | Purpose                                                  |
| ------------ | -------------------------------------------------------- |
| `start`      | Start a service                                          |
| `stop`       | Stop a service                                           |
| `restart`    | Restart a service                                        |
| `reload`     | Reload configuration without full restart (if supported) |
| `status`     | View service status                                      |
| `is-active`  | Check if running                                         |
| `is-enabled` | Check if the service starts on boot                      |


## Logging Commands
| Command              | Purpose                    |
| -------------------- | -------------------------- |
| `journalctl`         | View all logs              |
| `journalctl -u`      | Logs for one service       |
| `journalctl --since` | Logs from a specified time |
| `journalctl -b`      | Logs from current boot     |
| `journalctl -p err`  | Error messages only        |


## Verification
```text
Services running
↓
Logs accessible
↓
Failed service identified
↓
Service restarted successfully
```


## Lessons Learned
- Linux service management
- systemd architecture
- Daemon concepts
- Socket activation
- System log analysis
- Service troubleshooting
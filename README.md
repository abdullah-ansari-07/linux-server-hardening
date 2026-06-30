# linux-server-hardening
A hands-on Linux server hardening project on AWS EC2

# Table of Contents
- Introduction
- Architecture
- Security Features
- Repository Structure
- Project Highlights
- Skills Demonstrated


# Introduction
I built a hardened Ubuntu server hosted by Amazon Web Services using the EC2 service. I hardened it by using multiple layers of security.
The end result was a secure Ubuntu server with a defense-in-depth security model.
The purpose of this project was to understand Linux systems, learn Linux commands, get introduced to the basics of securing a system and applying it to a real live-hosted EC2 instance.

# Project Status
Completed.

# Architecture
Incoming traffic reaches the server through the following security layers:
```text
Internet
    │
    ▼
AWS Security Group
    │
    ▼
UFW Firewall
    │
    ▼
Fail2Ban
    │
    ▼
SSH Daemon
    │
    ▼
Public Key Authentication
    │
    ▼
Linux User
```
The AWS Security Group, UFW Firewall, Fail2ban monitor and Public Key Authentication provide the multiple layers for the defense in depth feature


# Security Features
AWS Security Group - Provided by AWS for security and controls which network traffic is allowed to reach the instance.
UFW Firewall is designed to simplify management of iptables firewall rules which helps allow or block network traffic on Linux.
Fail2ban monitor monitors the authentication logs. It follows the preset rules and conditions and blocks an IP if the activity is deemed suspicious or the activity is falls in the grey region of it's rules.
Public Key Authentication only allows access to systems with the respective private key.

# Repository Structure
The following is the structure of this repository:
linux-server-hardening
│
├── README.md
│
├── docs
│   ├── screenshots
│   ├── diagrams
│   └── notes
│
└── LICENSE


# Key Accomplishments
- Users were created and added to Groups and also included in the sudo group for sudo permissions.
- Setting up defense-in-depth for higher security features
- The system was also set for auto-upgrades for the security feature so that it gets updated without needing manual updates
- The concept of SSH, Daemon, Socket Activation, log checking were easily understood through the hands-on application.

# Skills Demonstrated
- Linux Administration
- AWS EC2
- SSH Key Authentication
- Firewall Configuration
- Fail2ban
- Systemd
- Linux Troubleshooting

# Technologies Used
- Ubuntu 26.04 LTS
- AWS EC2
- OpenSSH
- UFW
- Fail2Ban
- systemd
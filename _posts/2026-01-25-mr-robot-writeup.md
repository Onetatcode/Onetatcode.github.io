---
title: "TryHackMe: Mr. Robot CTF Writeup"
date: 2026-01-25 15:30:00 +0500
categories: [CTF, TryHackMe]
tags: [mr-robot, linux, wordpress, nmap, privesc, medium]
---

# TryHackMe Writeup: Mr. Robot CTF
**Difficulty:** Medium | **Platform:** TryHackMe | **Date:** January 2025

## 1. Executive Summary
This report details the exploitation of the "Mr. Robot" Capture The Flag (CTF) room on TryHackMe. The objective was to locate three hidden flags (keys) by enumerating the target, exploiting a web application vulnerability to gain initial access, and performing privilege escalation to reach the root user.

## 2. Reconnaissance & Enumeration

### 2.1. Network Scanning
We began by connecting to the TryHackMe network via OpenVPN and deploying the target machine. Initial port scanning was performed using **Nmap** to identify running services.

**Command:**
bash
nmap -sV -sC -oA nmap_output [Target_IP]

Results: The scan identified three open ports:

22/tcp (SSH): Closed

80/tcp (HTTP): Apache httpd

443/tcp (SSL/HTTP): Apache httpd
![Nmap Scan Results](/assets/img/r-robot/nmap.png)

### 2.2. Web Directory Enumeration
To identify hidden directories and files, we utilized Gobuster against the target web server using the directory-list-2.3-small.txt wordlist.

Command:

Bash
gobuster dir -u http://[hostname] -w /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt -t 100 -q -o gobuster_output.txt
Findings: Gobuster revealed several critical paths, including /login, /wp-login, /admin, /license, and /robots.

![Gobuster Scan Results](/assets/img/r-robot/gobuster.png)

## 3. Web Exploitation & Initial Access
### 3.1. Retrieving Key 1
Upon inspecting the /robots.txt file manually, two interesting entries were discovered: fsocity.dic and key-1-of-3.txt.

![Robot-text](/assets/img/r-robot/robots-txt.png)

By navigating to http://[Target_IP]/key-1-of-3.txt, we successfully retrieved the first flag.

Key 1: 0734****************************

![First Flag](/assets/img/r-robot/f1.png)

We also downloaded the dictionary file fsocity.dic using curl for later use in password cracking.

Bash
curl http://[Target_IP]/fsocity.dic > dictionary.txt

![Nmap Scan Results](/assets/img/r-robot/dict.png)

### 3.2. Credential Harvesting
Navigating to the /license page revealed a base64 encoded string: ZWxsaW90OkVSMjgtMDY1Mgo=.

![Nmap Scan Results](/assets/img/r-robot/dict-inspect.png)

Using CyberChef, we decoded this string to reveal valid credentials:

User: elliot

Password: ER28-0652

![Nmap Scan Results](/assets/img/r-robot/cyberchef.png)

### 3.3. WordPress Exploitation
With the credentials elliot:ER28-0652, we successfully logged into the WordPress dashboard at /wp-login.php.

![Nmap Scan Results](/assets/img/r-robot/dashboard.png)

As an administrator, we navigated to Appearance > Editor and selected the 404.php template. We replaced the existing code with a PHP reverse shell (e.g., PentestMonkey), configured with our local IP and listening port.

We started a Netcat listener on our attack machine:

![Nmap Scan Results](/assets/img/r-robot/netcat.png)

Bash
nc -lvnp 4444
By visiting the 404 page, the payload executed, granting us a reverse shell as the daemon user.

![Nmap Scan Results](/assets/img/r-robot/netcat-shell.png)

## 4. Privilege Escalation
### 4.1. Shell Stabilization
To interact with the system more effectively, we upgraded the shell using Python:

Bash
python -c 'import pty; pty.spawn("/bin/sh")'

### 4.2. Horizontal Escalation (daemon -> robot)

![Nmap Scan Results](/assets/img/r-robot/daemon.png)

We discovered a password hash file in /home/robot named password.raw-md5 containing the hash c3fcd3d76192e4007dfb496cca67e13b.

We cracked this hash using John the Ripper and the rockyou.txt wordlist:

Bash
john --format=raw-md5 --wordlist=/usr/share/wordlists/rockyou.txt secret
Cracked Password: abcdefghijklmnopqrstuvwxyz

Using these credentials, we switched users to robot and retrieved the second flag. Key 2: 822c****************************

![Nmap Scan Results](/assets/img/r-robot/f2.png)

### 4.3. Vertical Escalation (robot -> root)
To escalate to root, we searched for files with the SUID bit set using the following command:

Bash
find / -perm -4000 2>/dev/null
The output revealed that Nmap had the SUID bit set. Older versions of Nmap allow for an interactive mode that can spawn a shell. Since the binary runs with SUID permissions, the spawned shell inherits root privileges.

Exploit Commands:

Bash
nmap --interactive
nmap> !sh
# whoami
### root
With root access secured, we retrieved the final flag. Key 3: 0478****************************

## Conclusion
This room provided excellent practice in web enumeration and SUID privilege escalation. The combination of WordPress vulnerability assessment and Linux permission abuse makes it a classic challenge for sharpening Blue and Red team skills.

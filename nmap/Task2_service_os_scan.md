# Day 2 – Service & OS Detection Scan

Date: 2025-08-17
Attacker Machine: Kali Linux VM
Target Machine: Metasploitable VM
Target IP: 192.186.0.128
Objective: Perform a basic SYN scan to identify open ports and services.

## Command Used

nmap -sV 192.168.0.128
nmap -O 192.168.0.128
nmap -A 192.168.0.128

## Results
Initial results showed that metaspolit vm was unreachable. Rebooted both metasploit and kali vm. Issue corrected.

PORT     STATE SERVICE
21/tcp → FTP (vsftpd 2.3.4, anonymous login allowed)

22/tcp → SSH (OpenSSH 4.7p1)

23/tcp → Telnet (Linux telnetd)

25/tcp → SMTP (Postfix, SSLv2 enabled)

53/tcp → DNS (BIND 9.4.2)

80/tcp → HTTP (Apache 2.2.8, Ubuntu)

111/tcp → rpcbind + NFS

139, 445/tcp → SMB (Samba 3.0.20-Debian)

3306/tcp → MySQL 5.0.51a

5432/tcp → PostgreSQL 8.3.x

5900/tcp → VNC (protocol 3.3)

6667/tcp → IRC (UnrealIRCd 3.2.8.1)

8180/tcp → Apache Tomcat 5.5

Many more (see full scan output in /scans/day02_full.txt)

RACEROUTE
HOP RTT     ADDRESS
1   1.40 ms 192.168.0.128

Other information redacted for safety concerns. Information did include type of operating system, 



## Takeaways
-sV → probes services on open ports to detect versions (ex: Apache 2.4.7, OpenSSH 7.2p2).

-O → attempts OS fingerprinting by comparing network responses to known OS signatures.

-A → “Aggressive scan” that combines:

-sV (service/version)

-O (OS detection)

Traceroute

NSE (Nmap Scripting Engine) default scripts

FTP allows anonymous login → potential credential harvesting or file retrieval.

SMTP supports VRFY command → can enumerate valid users.

SSLv2 enabled → known to be insecure & deprecated.

Multiple databases exposed directly to the network (MySQL, PostgreSQL) → potential SQL injection or default credentials.

Samba (SMB) with message signing disabled → susceptible to man-in-the-middle attacks.

IRC service running → old backdoor vectors.

A Metasploitable-specific bindshell detected on port 1524 → intentional vulnerability.


## Lessons Learned

What services and versions are running, not just the ports.

OS detection gives me a good guess at the target’s operating system (sometimes accurate, sometimes not).

Aggressive scans are powerful, but loud and detectable.

This helps me plan attack paths (e.g., if I see Apache 2.4.7, I can look up CVEs for that version).

This scan revealed a wide attack surface with outdated services.

## Next steps:

Test FTP anonymous login (list/download files).

Attempt SMB enumeration (null sessions, shares, users).

Explore web services (Apache on port 80, Tomcat on port 8180).

Document vulnerable SSL/crypto settings.

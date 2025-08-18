# Nmap Basic Scan – Metasploitable VM

**Date:** 2025-08-17  
**Attacker Machine:** Kali Linux VM  
**Target Machine:** Metasploitable VM  
**Target IP:** 192.186.0.128  
**Objective:** Perform a basic SYN scan to identify open ports and services.
---

## Command Used
nmap/zenmap
nmap -sS -Pn 192.168.0.128

Results
PORT     STATE SERVICE

21/tcp   open  ftp

22/tcp   open  ssh

23/tcp   open  telnet

80/tcp   open  http

139/tcp  open  netbios-ssn

445/tcp  open  microsoft-ds

3306/tcp open  mysql

## Takeaways
1) SYN scan (-sS) is faster and stealthier than a TCP connect scan.
2) -Pn ensures the scan still runs even if ICMP (ping) is blocked.
3) Multiple services are exposed → each could be a future attack vector

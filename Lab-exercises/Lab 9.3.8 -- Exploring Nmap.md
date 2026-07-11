# Lab 9.3.8 -- Exploring Nmap

## Overview
*(Written last — final summary of what the lab covered and what was demonstrated.)*

---

## Background

Network reconnaissance is usually the first stage of an intrusion. The attacker starts by using Nmap to enumerate the network for open ports, services and live hosts,
in order to determine the attack surface. This technique is documented in MITRE ATT&CK as T1595 — Active Scanning and T1046 — Network Service Discovery. Nmap is an open-source tool for scanning networks 
by sending packets to target systems and examining their responses to determine service identity, port availability, and in some cases, the operating system. Nmap is also 
a valuable tool for defenders to perform authorized scans in order to identify unintentionally exposed ports to close or restrict them, minimizing the attack surface.

---
## Environment & Tools

| Component       | Details |
|-----------------|---------|
| Operating System | CyberOps Workstation VM (Arch Linux) |
| Primary Tool(s) | Nmap 7.80 (flags: -A, -T4) |
| Networking Details | VM IP (10.0.2.15), local network (10.0.2.0/24), external host (scanme.nmap.org), default gateway (10.0.2.2) |

---

## Procedure Summary

Learning about the purpose of Nmap can be done by executing the `man nmap` command in a terminal. The command returns information from its purpose, network exploration, to examples like `nmap -A -T4`, where `-A` is a flag enabling OS detection, version detection, script scanning and traceroute, combined with `-T4` to speed up scan execution. The first scan was performed on localhost, revealing three open ports: port 21 for FTP version 2.0.8, port 22 for SSH version 8.9, and port 23 for telnet, identified as Linux telnetd. Localhost port 21 for FTP allows anonymous FTP login, raising security concerns. Running the ip address command revealed the VM's IP address (10.0.2.15/24), and zeroing the last octet produced the network address 10.0.2.0/24, which was then used to scan the subnet. The scan performed to `10.0.2.0/24` displayed the same three open ports from localhost (`10.0.2.15`) as well as one more port from the default gateway (`10.0.2.2`) running on the network with an open port 631 for IPP version CUPS 2.4. Lastly, a scan was run on a remote host named scanme.nmap.org, revealing one host up and running on Linux with eight open ports and a filtered one. 

---

## Key Findings



---

## Security Implications
*(Analysis of what the findings mean from a defensive and offensive perspective — dual-use nature of the tool, exposure risks from findings like anonymous FTP or Telnet if present, and reference to MITRE ATT&CK T1046 — Network Service Discovery, plus T1590 — Gather Victim Network Information if relevant to the remote scan step.)*

## References

- CyberOps Associate -- Lab 9.3.8 Exploring nmap

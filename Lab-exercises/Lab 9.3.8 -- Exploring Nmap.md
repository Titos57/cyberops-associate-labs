# Lab 9.3.8 -- Exploring Nmap

## Overview
*(Written last — final summary of what the lab covered and what was demonstrated.)*

## Background
*(Why port/service scanning matters in a security context, what Nmap is, and the operational scenario this lab simulates — reconnaissance phase of an attack, or the equivalent defensive discovery activity.)*

## Environment & Tools
*(CyberOps Workstation VM details — hostname secOps, user analyst — Nmap version used, target hosts/scope: localhost, local subnet, scanme.nmap.org.)*

## Procedure Summary
*(Full narrated walkthrough — not just restating steps, but explaining what each scan was doing and why. This should cover, in order:
1. Using `man nmap` to establish what Nmap is and its purpose
2. Locating and interpreting Example 1 in the man page (the `-A -T4` example scan)
3. Scanning localhost with `nmap -A -T4 localhost`
4. Identifying the VM's IP/subnet via `ip address`
5. Scanning the local subnet with `nmap -A -T4 <network>/<prefix>`
6. Scanning the remote host `scanme.nmap.org` with `nmap -A -T4`
Each step should reference actual output values once you have run it, not placeholders.)*

## Key Findings
*(Concrete, value-based observations — e.g., specific ports, services, and versions identified on each target; hosts discovered on the LAN; open vs. filtered port differences between local and remote scans.)*

## Security Implications
*(Analysis of what the findings mean from a defensive and offensive perspective — dual-use nature of the tool, exposure risks from findings like anonymous FTP or Telnet if present, and reference to MITRE ATT&CK T1046 — Network Service Discovery, plus T1590 — Gather Victim Network Information if relevant to the remote scan step.)*

## Reflection (optional)
*(Your own analysis of how Nmap serves both defenders and threat actors, tied to what you actually observed rather than generic statements.)*

## References
*(Cisco NetAcad lab document, Nmap official documentation, MITRE ATT&CK technique pages cited above.)*

# Lab 3.3.11 -- Using Windows PowerShell

> **Course:** Cisco CyberOps Associate  
> **Module:** 3 — Windows Operating System  
> **Platform:** Windows 10 Home
> **Lab Type:** Hands-On  
> **Completed:** June 2026 
> **Author:** Christos Panopoulos — University of Peloponnese, 
CS & Telecommunications

---

## Overview

[2–3 sentences. Written last. What the lab covers, what tools were 
used, and why it matters to security. Never start with "In this 
lab..."]

---

## Background

[1–2 paragraphs. The security concept this lab demonstrates. Why it 
matters to defenders and attackers. No copying from Cisco text. 
Reference relevant frameworks or principles where appropriate.]

---

## Environment & Tools

| Component          | Details |
|--------------------|---------|
| Operating System   |         |
| Primary Tool(s)    |         |
| Supporting Tool(s) |         |
| Key Concepts       |         |

---

## Procedure Summary

### Part 1 — Accessing PowerShell

[How PowerShell was launched alongside Command Prompt. 
One short paragraph.]

*Screenshot: `01-powershell-and-cmd.png`*

### Part 2 — Command Prompt and PowerShell Commands

[What commands were run in both shells. What the comparison 
revealed about compatibility between the two environments.]

*Screenshot: `02-dir-comparison.png`*

### Part 3 — Exploring Cmdlets

[What Get-Alias dir revealed about how PowerShell aliases 
traditional commands to its own cmdlet structure. What the 
verb-noun cmdlet naming convention means in practice.]

*Screenshot: `03-get-alias-dir.png`*

### Part 4 — Exploring Netstat Using PowerShell

[What netstat -r revealed about the routing table and IPv4 
gateway. What netstat -abno showed about active TCP connections 
and associated processes. How a specific PID was correlated to 
a process in Task Manager. Why elevated privileges were required 
for the -b flag.]

*Screenshot: `04-netstat-abno.png`*
*Screenshot: `05-pid-task-manager.png`*

### Part 5 — Emptying the Recycle Bin Using PowerShell

[What the clear-recyclebin cmdlet demonstrated about PowerShell 
automating tasks that would otherwise require GUI interaction.]

*Screenshot: `06-clear-recyclebin.png`*

---

## Key Findings

[3–5 sentences. Specific observations from your actual output — 
your IPv4 gateway, the PID you selected and what process it 
mapped to, what the alias revealed, what the routing table 
showed. No vague statements.]

---

## References

- Cisco NetAcad — CyberOps Associate, Lab 3.3.11: 
  Using Windows PowerShell

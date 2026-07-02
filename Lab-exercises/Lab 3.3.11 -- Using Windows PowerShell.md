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

Launching both PowerShell and Command Prompt side by side reveals one immediate difference. 
PowerShell prefixes the prompt with `PS` before the path location, while Command Prompt displays
the path alone. Testing commands against both of them at the same time can reveal the capabilities
that each one offers.

### Part 2 — Command Prompt and PowerShell Commands

Executing the `dir` command without any flags on both PowerShell and Command Prompt produced identical outputs of 13
directories. However, Command Prompt reveals two additional entries, `.` and `..`, representing the current and parent directories that PowerShell did not.
Other commands like `ping`, `cd` and `ipconfig` respond identically in both.

### Part 3 — Exploring Cmdlets

PowerShell applies aliases to widely known and used commands to make the transition
easier. An example of such aliases is the `dir` command, executing `Get-Alias dir`
shows the command that `dir` actually relates to in PowerShell's cmdlet `Get-ChildItem`.
PowerShell uses a verb to describe the action and a noun to represent the exact target 
of the action.

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

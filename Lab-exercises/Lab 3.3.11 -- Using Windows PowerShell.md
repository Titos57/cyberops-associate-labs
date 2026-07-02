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

![dir command](../Lab-screenshots/PowerShell/dir%20comparison%20.png)

### Part 3 — Exploring Cmdlets

PowerShell applies aliases to widely known and used commands to make the transition
easier. An example of such aliases is the `dir` command, executing `Get-Alias dir`
shows the command that `dir` actually relates to in PowerShell's cmdlet `Get-ChildItem`.
PowerShell uses a verb to describe the action and a noun to represent the exact target 
of the action.

![Get alias dir command](../Lab-screenshots/PowerShell/Get-Alias%20dir%20command.png)

### Part 4 — Exploring Netstat Using PowerShell

Before using the `netstat` command, check the available flags to
maximize information gained by executing the `netstat -h` command. Running the `netstat -r` command 
produces a routing table of the local machine's IP and IPv4 Gateway (192.168.1.1) among other
useful information. However, in some cases launching PowerShell as administrator is required 
before executing `netstat` commands. For example, the `netstat -abno` command requires administrator
access to execute, as it provides all the UDP and TCP active connections on the machine. 
Investigating the process with PID 10384 through Task Manager reveals the svchost.exe process.
Accessing the properties page of svchost.exe reveals more details such as the executable path, the 
process description and the version, amongst others.

![netstat -h command](../Lab-screenshots/PowerShell/netstat%20-h.png)
![netstat -r command](../Lab-screenshots/PowerShell/netstat%20-r.png)
![netstat -abno command](../Lab-screenshots/PowerShell/netstat%20-abno.png)
![PID Task Manager -r command](../Lab-screenshots/PowerShell/PID%20task%20manager.png)

### Part 5 — Emptying the Recycle Bin Using PowerShell

A simple command following the verb-noun type that was mentioned is
`clear-recyclebin`, which clears the contents inside the machines
recycle bin.

![recyclebin command](../Lab-screenshots/PowerShell/recycle%20bin%20cleanup%20command.png)

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

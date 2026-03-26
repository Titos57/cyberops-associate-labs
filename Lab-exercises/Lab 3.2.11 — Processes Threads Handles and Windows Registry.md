# Lab 3.2.11 — Exploring Processes, Threads, Handles, 
and Windows Registry

**Course:** Cisco CyberOps Associate
**Module:** 3.2.11
**Date:** March 2026
**Author:** Christos Panopoulos
**Tool Used:** Windows Sysinternals Process Explorer, 
Registry Editor

---

## Objective
Use Process Explorer to analyze processes, threads, 
and handles, and use the Windows Registry to modify 
application behavior.

---

## Part 1 — Exploring Processes

### Active Process Identification


[text + screenshot Find_process_window.jpg]

### Killing the Browser Process
[text + screenshot chrome killed]

### Command Prompt Process Tree
[text + screenshot cmd.exe with conhost.exe]

### Ping Process Observation
[text + screenshot ping running]

### VirusTotal Analysis
[text + screenshots VirusTotal_Analysis.jpg 
and after_conhost_exe_scan.jpg]

### Killing the Parent Process
[text + screenshot cmd killed]

---

## Part 2 — Threads and Handles

### Threads
[text + screenshot threads tab]

### Handles
[text + screenshot handles view]

---

## Part 3 — Windows Registry

### EulaAccepted Key — Initial Value
[text + screenshot value = 1]

### Registry Value Modification
[text + screenshots value = 0 and EULA reappeared]

---

## Key Observations
[3-4 sentences]

---

## References
- [Windows Sysinternals Process Explorer](https://learn.microsoft.com/en-us/sysinternals/downloads/process-explorer)
- [Windows Registry Documentation](https://learn.microsoft.com/en-us/windows/win32/sysinfo/registry)
- [VirusTotal](https://www.virustotal.com)
```

---

## Security Audit vs Portfolio Documentation

These are fundamentally different in purpose, audience and format.

**What you are doing now — Portfolio Documentation** is written for a recruiter or hiring manager who has never seen your work. The goal is to demonstrate that you understand what you are doing and why it matters. It includes explanations, observations, security implications, and key takeaways. The tone is educational and reflective. You are proving competence.

**A Security Audit** is a formal professional document written for a client or management team after assessing a real system. It assumes the reader already understands security concepts. It focuses purely on findings, evidence, risk ratings, and recommendations. There is no explanation of what lsass.exe is — the reader already knows. The tone is formal, precise, and liability-aware. Every finding is rated by severity — Critical, High, Medium, Low. Remediation steps are specific and time-bound.

A real security audit report looks like this:
```
Finding: Unpatched CVE-2026-21509 on workstation WS-042
Severity: Critical
Evidence: Process Explorer screenshot showing version 
          10.0.19041.6807
Risk: Remote code execution via spear-phishing attachment
Recommendation: Apply Microsoft emergency patch within 
                24 hours

# Lab 3.2.11 — Exploring Processes, Threads, Handles, and Windows Registry

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
To find a specific process, click the Find Window's Process button at the top and drag it to the
process window you want to locate, and the process gets highlighted. The  process in that case is
chrome.exe, and all of the child processes below. A lot of processes are running
simultaneously, this is because of Chrome's multi-process architecture, where every tab, extension
and plugin run as a separate process for security reasons.

![Active Process Identification](../Lab-screenshots/procexp.exe/Find_process_window.jpg)


### Killing a Process
Upon killing the parent chrome.exe process, every Chrome connection is terminated simultaneously,
including all the child processes that depend on it, as shown by the red highlight in Process Explorer.
This is an important forensics concept — terminating a parent process cascades through all its 
children.

![Killing a Process](../Lab-screenshots/procexp.exe/kill_process%20.jpg)

### Command Prompt Tree
By using the Find Window's Process tool to locate the Command Prompt, identified as cmd.exe, it is
clear that cmd.exe is the parent process with conhost.exe as the child process. However is important
to mention that cmd.exe is a child of explorer.exe - the Windows shell responsible for launching 
user applications.

![Command Prompt child](../Lab-screenshots/procexp.exe/after%20conhost.exe%20scan.jpg)

### Ping Command Observation
While running a command, such as ping, on the command prompt process, we observe that a new child
process is now shown, called PING.exe. This test shows how parent processes spawn child 
processes based on the actions they need to perform, while Process Explorer helps us
visualize these changes in real time. Once the ping is completed, PING.EXE disappears 
from the process tree.

![Ping command on CMD](../Lab-screenshots/procexp.exe/ping_command.jpg)

### VirtualTotal analysis - conhost.exe
By right-clicking on the conhost.exe process and selecting Check VirtualTotal, a score is shown
0/72 - meaning no security vendors flagged the file as dangerous/malicious. When the score is
clicked, we get redirected to the VirtualTotal page showing results in detail.

While reviewing other processes on the VirusTotal column, it is interesting to observe the Process
Lively.Watchdog.exe with 1/72 - flagged by one vendor as malicious. This demonstrates the practical
value of VirusTotal, as running it against all the running processes could locate a possibly
malicious process that went undetected up until then.

![VirusTotal analysis result](../Lab-screenshots/procexp.exe/VirusTotal%20Analysis.jpg)
![Possible Malicious process](../Lab-screenshots/procexp.exe/after%20conhost.exe%20scan.jpg)

### Killing cmd.exe 
As demonstrated before, upon killing the cmd.exe process, conhost.exe is also simultaneously 
terminated, showing the hierarchical nature of Windows process management.

![Killing cmd.exe](../Lab-screenshots/procexp.exe/kill_process_cmd.exe.jpg)

## Part 2 - Threads & Handles

### Part 2.1 - Threads






















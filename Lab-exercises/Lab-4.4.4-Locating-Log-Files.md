# Lab 4.4.4 — Locating Log Files

**Course:** Cisco CyberOps Associate  
**Category:** Practical / Hands-On  
**Platform:** CyberOps Workstation Virtual Machine (Linux)  
**Date Completed:** April 2026

---

## Objective


---

## Part 1: Log File Overview

### Step 1: Web Server Log File Example
There are different formats of log files based on the service or process. However, 
log files cover five main pieces of information: Timestamp, Type of event,
PID, Client IP, and Description. 

By using the `cat` command to print the `/var/log/logstash-tutorial.log` file in the 
terminal, an analyst can identify that web server log files are displayed.
Web server log files, like Apache and nginx, record HTTP requests, with the format starting with
the client's IP, timestamp, HTTP request, protocol version, response code, and 
size of response. An analyst monitoring those logs would look for unusual IP
addresses making many requests, requests on unusual hours, and large response sizes
indicating data exfiltration.

![logstash-tutorial.log](../

---

### Step 2: Operating System Log File Example
Using the `more` command to display the `/var/log/syslog` log files offers a clearer
way to read log files, as each one is on its own line.
The syslog file stores the OS events of the kernel, service start and stop events, and 
network interface events. OS event files also follow a format of timestamp, hostname,
service name, and description. As an analyst, monitoring system logs can reveal malware disabling 
critical services and unusual network interface state changes.

![/var/log/syslog](../

---

## Part 2: Locating Log Files in Unknown Systems

### Step 1: Reading Documentation with man nginx



---

### Step 2: Verifying nginx is Running





---

### Step 3: Locating nginx Configuration File








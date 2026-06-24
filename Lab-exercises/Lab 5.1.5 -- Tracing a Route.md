# Lab 5.1.5 — Tracing a Route

> **Course:** Cisco CyberOps Associate
> **Module:** 5 — Network Communications
> **Platform:** CyberOps Workstation VM (Arch Linux)
> **Lab Type:** Hands-On
> **Completed:** 06-2026
> **Author:** Christos Panopoulos

---

## Overview

The lab demonstrates the amount of information anyone can find with utilities 
such as `ping` and `traceroute` about a network's reachability, IP and hostnames. For an 
attacker reconnaissance with tools is a fundamental step and mitigating the access to 
sensitive information from these tools as a Blue Team is of extreme importance.


---

## Environment & Tools

| Component       | Details |
|-----------------|---------|
| Operating System | CyberOps Workstation VM (Arch Linux) |
| Primary Tool(s) | ping - traceroute |
| Supporting Tool(s) | https://gsuite.tools/traceroute |
| Key Protocols | ICMP, IP |
---

## Part 1 — Verifying Network Connectivity Using Ping

Network connectivity to www.cisco.com was verified by using the `ping` utility. The `ping` output identified
the Fully Qualified Domain Name (FQDN) **e2867.dsca.akamaiedge.net** and the IP address **2.16.188.101** of the targeted host.
Four pings were sent and all of them received a response, indicating 0% of packet loss, with an average of
**3016ms** for the packets to cross the network. The RTT results can be found in the last line of the 
output, where it recorded a minimum of **11.455ms** and a maximum of **16.904ms** with a mdev of **1.976ms** indicating
consistent latency through the four pings. This confirms the reachability and stability of the host.

![Ping Output](../Lab-screenshots/Traceroute/ping%20traceroute.png)

---

## Part 2 — Tracing a Route to a Remote Server

### 2a — Traceroute to www.cisco.com

Performing a `traceroute` utility to www.cisco.com discloses the path packets follow to reach the target host.
Only 6 hops responded with an ICMP response out of the maximum 64 hops. After hop 6, the routers seem to be configured to 
suppress the ICMP Time Exceeded response as indicated by the *** entries. Hop 1 and 2 are gateways, one from the VM and 
the second from the house network towards the ISP network. After the response of hop 5, hop 6 jumps to a new IP range as 
indicated by the latency spike from 9ms to 105ms, probably moving away from Greece's ISP infrastructure to an international one.
Interesting to notice is the latency difference on hop 6 alone, it seems to reduce its latency by each path attempt from 105ms 
all the way down to 16ms, finding a better path to reach the IP each time.

![Cisco trace Output](../Lab-screenshots/Traceroute/cisco%20traceroute.png)

### 2b — Traceroute to an RIR Target

Investigating the path to www.afrinic.net with the `traceroute` utility reveals 15 hops to the target host with significantly 
higher latency compared to the www.cisco.com trace from 19ms to 300ms. Hop 1 and 2 are the gateways from the VM and home network towards the ISP
infrastructure. At hop 6, the latency reaches 102ms, indicating an international network, after jumping to 205ms in just one 
hop to 7. From hops 8 to 14, the Mauritius network is reached with an average RTT of 300ms. Interesting to note is hop 15, where 
the trace receives !X, meaning a firewall actively blocks the traceroute packets as a security measure.

![Afrinic trace Output](../Lab-screenshots/Traceroute/Afrinic%20traceroute.png)

---

## Part 3 — Web-Based Visual Traceroute

Tracing `www.github.com` through `https://gsuite.tools/traceroute` offers a visual representation of the locations that a traceroute 
follows to reach the target host. The trace received responses from 7 hops out of the maximum 30. This time, the trace started from 
London instead of Greece, as the utility wasn't run locally. First 5 hops have extremely low latency tracing through UpCloud's internal
network. After hop 5, a clear spike is displayed as the trace jumps to Frankfurt's network in Germany and later on hop 7, reaching the 
GitHub infrastructure, where the ICMP stops sending any responses.

![Web Page Output](../Lab-screenshots/Traceroute/Web%20Page%20Traceroute.png)

---

## Key Findings

Performing a `ping` utility to www.cisco.com confirmed the reachability of the host and offered the FQDN (e2867.dsca.akamaiedge.net) and IP address (2.16.188.101) of it.
With that information, a `traceroute` utility was executed, revealing a latency spike from 9ms to 105ms, indicating the trace is moving
away from Greece's ISP infrastructure to an international network, after which ICMP responses are blocked as a security precaution. The
www.afrinic.net trace however had a significantly higher latency of 300ms and a firewall started blocking the ICMP responses at hop 15 instead of 6 on the cisco trace.
In the end, performing a trace through `https://gsuite.tools/traceroute` offered a visual trace through the geographical map locations showing the trace originated
from London instead of Greece as the trace wasn't executed locally.

---

## Security Implications

Traceroute is just one of the many utilities that an attacker can use to gather a victim's network information by identifying the hostnames, IP ranges and even approximate location
of a host. As documented on ***MITRE ATT&CK*** T1590 - Gather Victim Network Information, mitigating such techniques cannot be easily done. The only way a Blue Team can reduce 
information of the network structure to an attacker is by focusing on minimizing the sensitive data available to external sources. A measure to limit an attacker's 
information as shown by Cisco and Afrinic is by setting up the firewall to block ICMP responses. As a SOC analyst, much of such reconnaissance is frequently observed, emphasizing the 
importance of having a router baseline documentation to be able to spot any inconsistencies like traffic hijacking.

---

### References

- MITRE ATT&CK — T1590: Gather Victim Network Information  
  https://attack.mitre.org/techniques/T1590/



# Lab 5.1.5 — Tracing a Route

> **Course:** Cisco CyberOps Associate
> **Module:** 5 — Network Communications
> **Platform:** CyberOps Workstation VM (Arch Linux)
> **Lab Type:** Hands-On
> **Completed:** 06-2026
> **Author:** Christos Panopoulos

---

## Overview



---

## Environment & Tools

| Component       | Details |
|-----------------|---------|
| Operating System | CyberOps Workstation VM (Arch Linux) |
| Primary Tool(s) | ping - traceroute |
| Supporting Tool(s) | https://gsuite.tools/traceroute |

---

## Part 1 — Verifying Network Connectivity Using Ping

Network connectivity to www.cisco.com was verified by using the `ping` utility. The `ping` output identified
the Fully Qualified Domain Name (FQDN) **e2867.dsca.akamaiedge.net** and the IP address **2.16.188.101** of the targeted host.
Four pings were sent and all of them received a response, indicating 0% of packet loss, with an average of
**3016ms** for the packets to cross the network. The RTT results can be found in the last line of the 
output, where it recorded a minimum of **11.455ms** and a maximum of **16.904ms** with a mdev of **1.976ms** indicating
consistent latency through the four pings. This confirms the reachability and stability of the host.

![Ping Output](../Lab-screenshots/

---

## Part 2 — Tracing a Route to a Remote Server

### 2a — Traceroute to www.cisco.com

[Paste your real traceroute output. Then write an analytical paragraph:
walk through the hops — what does each one reveal? Identify the gateway,
ISP infrastructure, and destination. Note any interesting hostnames.]

### 2b — Traceroute to an RIR Target

[Which RIR did you choose and why? Paste your output.
How does this path compare to the Cisco trace? Note hop count differences,
latency changes, any unresponsive hops (* * *), and what that tells you.]

---

## Part 3 — Web-Based Visual Traceroute

[What site did you trace? What did the visual tool show that the terminal
did not? Describe the geographic hop distribution. Screenshot goes here.
Answer the lab reflection question in analytical paragraph form — not as Q&A.]

---

## Key Findings

[4–5 sentences, each one a specific, factual observation from your actual output.
No vague statements. Every finding must reference a concrete value or observation.]

---

## Security Implications

[2–3 paragraphs connecting what you did to real security work.
Think: what would an attacker learn from your traceroute output?
What would a SOC analyst use this technique for?
Reference at least one MITRE ATT&CK technique by ID and name.]

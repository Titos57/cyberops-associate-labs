# Lab 5.3.7 -- Introduction to Wireshark

> **Course:** Cisco CyberOps Associate 
**Module:** 5 — Network Protocols 
**Platform:** CyberOps Workstation VM
**Lab Type:** Hands-On
**Completed:** June 2026
**Author:** Christos Panopoulos — University of Peloponnese, CS & Telecommunications

---

## Overview

[Written last]

---

## Background

[Explain what Wireshark is and its role as a packet analyzer for network troubleshooting and security analysis, and briefly introduce the Mininet-simulated topology (R1, S1, H1–H4) used to generate traffic for capture.]

---

## Environment & Tools

| Component        | Details                                      |
| ----------------- | --------------------------------------------- |
| Operating System  | CyberOps Workstation VM (Arch Linux, hostname secOps) |
| Primary Tool(s)   | Mininet, Wireshark, ping                      |
| Key Concepts      | Packet encapsulation, ICMP, ARP, MAC/IP addressing |

---

## Procedure Summary

### Part 1 — Mininet Topology Setup

Before launching Wireshark and capturing traffic, the virtual network is initialized by running the `cyberops_topo.py` script, which configures four hosts, a switch, and a router. A terminal is opened on H1 using `xterm H1`, and on H2 using `xterm H2`. Running `ip address` in each terminal returns the IPv4 and MAC address of the corresponding interface, a step required to correlate captured frames back to the originating and receiving host. H1-eth0 is configured with an IPv4 address of `10.0.0.11/24` and a MAC address of `86:29:54:5c:57:b0`. H2-eth0 is configured with an IPv4 address of `10.0.0.12/24` and a MAC address of `62:a4:02:f3:f7:2a`.

### Part 2 — Local LAN Capture (H1 to H2)

[Condensed summary: starting Wireshark on H1-eth0, running `ping -c 5 10.0.0.12`, applying the icmp filter, and examining the Ethernet II source/destination MAC addresses against recorded values.]

### Part 3 — Remote LAN Capture (H1 to H4)

[Condensed summary: recording H4-eth0, R1-eth1, and R1-eth2 addresses, starting a new capture on H1, running `ping -c 5 172.16.0.40`, and examining the destination IP/MAC addresses returned in the capture.]

---

## Key Findings

[Must include, using actual recorded values: whether the local-LAN capture confirmed source/destination MAC addresses matching H1 and H2 directly; and the key finding from the remote-LAN capture — that the destination MAC address resolved to R1-eth1 rather than H4's own MAC address, since ARP resolves the default gateway for traffic destined off-subnet, with the IP header still carrying H4's address end-to-end.]

---

## References

- Cisco NetAcad — CyberOps Associate, Lab 5.3.7: Introduction to Wireshark

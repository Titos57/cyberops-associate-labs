# Lab 5.3.7 -- Introduction to Wireshark

> **Course:** Cisco CyberOps Associate 
> **Module:** 5 — Network Protocols 
> **Platform:** CyberOps Workstation VM
> **Lab Type:** Hands-On
> **Completed:** June 2026
> **Author:** Christos Panopoulos — University of Peloponnese, CS & Telecommunications

---

## Overview

ICMP traffic was captured and analyzed using Wireshark within a Mininet-simulated topology, comparing packet behavior between two hosts on the same local subnet and between a local host and a remote host reached through a router. Hosts on the same subnet communicate directly with each other, as the source and destination MAC addresses correspond to the two communicating hosts. Hosts on remote subnets communicate through a router, with the destination MAC address changing at every hop while the IP address remains the same throughout the exchange. This lab demonstrates how MAC values change hop-by-hop while IP addresses remain intact.

---

## Background

Wireshark is a protocol analyzer used by security professionals to capture, decode, and examine traffic moving through a network interface, supporting network troubleshooting, protocol analysis, and traffic-based investigation. This lab uses a Mininet-simulated topology consisting of four hosts (H1–H4), a switch (S1), and a router (R1), configured across two subnets, to generate controlled ICMP traffic for capture and analysis. Examining this traffic demonstrates how data is encapsulated within Ethernet and IP headers, and how that encapsulation changes as traffic crosses from a local subnet to a remote one through a router.

---

## Environment & Tools

| Component        | Details                                      |
| ----------------- | --------------------------------------------- |
| Operating System  | CyberOps Workstation VM |
| Primary Tool(s)   | Mininet, Wireshark, ping |
| Key Concepts      | Packet encapsulation, ICMP, MAC/IP addressing |

---

## Procedure Summary

### Part 1 — Mininet Topology Setup

Before launching Wireshark and capturing traffic, the virtual network is initialized by running the `cyberops_topo.py` script, which configures four hosts, a switch, and a router. A terminal is opened on H1 using `xterm H1`, and on H2 using `xterm H2`. Running `ip address` in each terminal returns the IPv4 and MAC address of the corresponding interface, a step required to correlate captured frames back to the originating and receiving host. H1-eth0 is configured with an IPv4 address of `10.0.0.11/24` and a MAC address of `86:29:54:5c:57:b0`. H2-eth0 is configured with an IPv4 address of `10.0.0.12/24` and a MAC address of `62:a4:02:f3:f7:2a`.

### Part 2 — Local LAN Capture (H1 to H2)

Capturing traffic between H1 and H2 begins with launching Wireshark using the `wireshark &` command and selecting the H1-eth0 interface. The `ping -c 5 10.0.0.12` command is then executed to send five ICMP echo requests to H2. Wireshark captured a range of traffic, since the ping command generates ICMP protocol messages. By applying `icmp` in the Filter field, the ping requests and replies are isolated for examination. For the ping request frame, the Ethernet II section in the middle panel confirms a source MAC address of `86:29:54:5c:57:b0` and a destination MAC address of `62:a4:02:f3:f7:2a`, matching the addresses previously recorded for H1-eth0 and H2-eth0.

### Part 3 — Remote LAN Capture (H1 to H4)

Communicating with a remote host requires an additional step, since traffic must pass through a router when the source and destination reside on different subnets. R1-eth1 is configured with an IPv4 address of `10.0.0.1/24`, serving as the default gateway for the `10.0.0.0/24` subnet containing H1 and H2, and a MAC address of `c6:c4:76:dd:1f:03`. R1-eth2 is configured with an IPv4 address of `172.16.0.1/12`, serving as the default gateway for the `172.16.0.0/12` subnet containing H4, and a MAC address of `56:83:fe:51:22:a2`. H4 is configured with an IPv4 address of `172.16.0.40/12` and a MAC address of `2e:73:af:d6:b8:ef`. Launching Wireshark from the H1 terminal and executing `ping -c 5 172.16.0.40` generates ICMP echo request and reply messages captured by Wireshark. Examining the captured frame, the destination MAC address matches R1-eth1 `(c6:c4:76:dd:1f:03)` rather than H4's own MAC address, while the destination IP address in the IP header still shows `172.16.0.40`, confirming that H1 forwards the frame to the router as the next hop while the packet's ultimate destination remains H4.

---

## Key Findings

On a local subnet, captured frames contain the source and destination MAC addresses of the two hosts directly, since the two hosts share the same subnet. However, when communicating with a remote subnet the destination MAC address corresponds to the router's interface(`c6:c4:76:dd:1f:03`) rather than the H4(`2e:73:af:d6:b8:ef`) host, which is the destination. On remote communications, MAC addresses change from hop to hop, while IP addresses stay the same throughout.

---

## References

- Cisco NetAcad — CyberOps Associate, Lab 5.3.7: Introduction to Wireshark

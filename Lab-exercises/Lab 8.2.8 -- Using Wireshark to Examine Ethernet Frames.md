# Lab 8.2.8 -- Using Wireshark to Examine Ethernet Frames

>**Author:** Christos Panopoulos
>**Environment:** Cisco CyberOps Workstation VM — Mininet topology (R1, S1, H1–H4)

---

## Overview
*(Written last — high-level summary of what was done and what it demonstrates)*

---

## Background



---

## Environment & Tools

*(VM details, Wireshark version if visible, Mininet topology diagram/description, host IPs/MACs recorded from `ip address` and `netstat -r`)*

[Screenshot: H3 `ip address` and `netstat -r` output]

---

## Procedure Summary (Full, Narrated)

Logging into the CyberOps VM and launching the network simulation script provides the testing network to start capturing traffic.
The procedure started by executing `ip address` at the H3 terminal to note the IPv4 address (`10.0.0.13`), the IPv6 address (`fe80::6448:45ff:fef4:c012`)
and the MAC address (`66:48:45:f4:c0:12`), while `netstat -r` revealed the default gateway to be `10.0.0.1`. Running `arp -n` to view the ARP table did not reveal any entries, as a result executing
`arp -d <ip>` was not required. After opening Wireshark with `wireshark &` and choosing the H3-eth0 interface, traffic capture began on the interface.
Executing `ping -c 5 10.0.0.1` (pinging the default gateway 5 times) revealed five Echo requests from the H3 host and five Echo replies from the default gateway (router) acknowledging the requests.
The Ethernet II section of the Packet Details pane showed the source H3 MAC address (`66:48:45:f4:c0:12`), the destination default gateway MAC address (`ca:fd:1b:5f:ea:3e`), and the Frame Type code `0x0800` (IPv4).

A new Wireshark capture was started on the same interface, targeting a host on another network. This was achieved by changing the IP address of the ping command to the H4 IP address instead of the default gateway. Five more Echo requests were sent from H3 (`10.0.0.13`)
to H4 with `ping -c 5 172.16.0.40`. The source MAC address of H3 (`66:48:45:f4:c0:12`) remained the same as expected and the destination MAC address remained 
the same as that of the default gateway (`ca:fd:1b:5f:ea:3e`). This occurred because H3 is on a different network from H4 and the requests are sent to the default gateway to handle routing.

[Screenshot: ARP cache clear — `arp -n` before/after `arp -d`]
[Screenshot: Wireshark capture filtered on icmp — local ping to gateway]
[Screenshot: Ethernet II frame details pane — local ping]
[Screenshot: Wireshark capture — ping to H4 (routed)]
[Screenshot: Ethernet II frame details pane — routed ping]

---

## Key Findings

*(Concrete values only — actual MAC addresses, OUI values, frame types (0x0800 / 0x0806), IP addresses recorded from both captures. State explicitly: destination MAC stayed the same/changed between local and routed ping while destination IP changed — with the real recorded values.)*

---

## Security Implications

*(Connect to real concepts: why ARP resolution matters for on-path attacks/ARP spoofing, why MAC addresses don't traverse routers (relevant to network segmentation and lateral movement detection), relevance of frame-level visibility to SOC packet analysis/IDS. MITRE ATT&CK: T1040 – Network Sniffing, and optionally T1557 – Adversary-in-the-Middle if you want to extend into ARP spoofing implications.)*

---

## References

- Cisco Networking Academy, *CyberOps Associate v1.0/1.1 — Lab: Using Wireshark to Examine Ethernet Frames*
- Wireshark documentation (if cited)

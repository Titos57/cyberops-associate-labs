# Lab 8.2.8 -- Using Wireshark to Examine Ethernet Frames

>**Author:** Christos Panopoulos
>**Environment:** Cisco CyberOps Workstation VM — Mininet topology (R1, S1, H1–H4)

---

## Overview
*(Written last — high-level summary of what was done and what it demonstrates)*

---

## Background

The Ethernet II frame is the Layer 2 encapsulation structure used to deliver data across a local network, and includes the source and destination MAC addresses, the preamble responsible for letting the receiving hardware detect the start of the frame, the FCS that makes sure there are no errors during transmission, as well as the frame type and the data field that includes the payload. ARP protocol is commonly used by the source device to associate an IP address with the MAC address of the destination device. On a local network, the frame's source and destination MAC addresses directly represent the two communicating hosts. While communicating to a remote network, layer 2 addressing changes on each hop.

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

Inspecting the Packet Details pane on Wireshark can provide unique insight. The Ethernet II section of the Packet Details pane displays the destination, source, and frame type fields. The Frame type on ICMP messages is 0x0800, confirming IPv4 encapsulation. However, in the case of ARP messages, this code would be 0x0806, indicating ARP traffic. Vendor identification is also possible from looking up the first 6 hex digits of any host MAC address, providing information about the device sending or receiving the traffic.

When H3 pinged its default gateway (same subnet, 10.0.0.0/24), the frame's source and destination MAC addresses directly represented the two communicating hosts. However, on remote hosts that is not the case. When H3 pinged H4, the destination IP address changed to H4's IP address, but the destination MAC address remained as the gateway's. As observed from H3's perspective, layer 2 addressing (MAC address) is hop-by-hop, while layer 3 addressing (IP address) remains the same end-to-end.

Before constructing the frame of a packet, the source device checks its ARP table for the MAC address of the IP address the packet is meant to be sent to. If the ARP table does not contain the MAC address of the specific IP, the ARP protocol sends an ARP request to all devices to locate the MAC address of the IP. After a reply is received with the MAC address, the frame is fully constructed and sent. 

---

## Security Implications

Whenever a device does not have the MAC address of the device trying to communicate, it sends an ARP request. ARP requests do not contain any authentication process. As a result, an attacker could send ARP replies to intercept future traffic. This process is called ARP spoofing and corresponds to MITRE ATT&CK sub-technique T1557.002 (ARP Cache Poisoning).

By inspecting traffic on Wireshark, an analyst can detect a MAC address vendor that does not match the expected vendor for a device, therefore providing an opportunity to flag the device for further investigation. This technique can be used by attackers as well, providing an attacker with MAC/IP mapping of the network or even intercepting unencrypted traffic. This is called Network Sniffing, referred to in MITRE ATT&CK under T1040.

Vendor identification via the MAC OUI, such as H3's OUI (`66:48:45`), which identifies the NIC vendor, can support rogue device detection by flagging a MAC address whose vendor does not match expected devices on the network.

Knowledge of how traffic is routed through a network (MAC address hop-by-hop, IP address static end-to-end) is essential to accurately track the steps an attacker took and what devices routed the specific traffic.

---

## References

- Cisco Networking Academy, *CyberOps Associate v1.0/1.1 — Lab: Using Wireshark to Examine Ethernet Frames*
- Wireshark documentation (if cited)

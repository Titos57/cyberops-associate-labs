# Lab 9.2.6 — Using Wireshark to Observe the TCP 3-Way Handshake

>**Author:** Christos Panopoulos
>**Course:** Cisco CyberOps Associate
>**Date:** July 2026

## Overview

The TCP three-way handshake was captured by tcpdump and redirected into a `pcap` file to be analyzed. The analysis was performed on both Wireshark and tcpdump, confirming the handshake progression of SYN->SYN-ACK->ACK and proving that packet analysis results are tool-independent. Having knowledge of the regular traffic behavior on a network, like the TCP handshake, is essential for detection of anomalies.

---

## Background

When applications use the TCP protocol, they require all the data to be reliably transmitted, as every segment is important. TCP achieves that reliability by establishing a stateful communication with the destination server before transmitting. The TCP three-way handshake is the process of establishing communication with the destination, which happens in three stages. First, the client starts by sending a SYN request to the server. The server receives the request and responds with its own SYN request and an acknowledgement message, ACK (SYN-ACK). Finally, the client responds with an ACK message to establish the communication stream. After establishing the communication, data can be transmitted between the client and server reliably. As a defender, knowing the correct handshake process can help spot anomalies during a handshake, like SYN floods or an incomplete handshake. 

---

## Environment & Tools

| Component       | Details |
|-----------------|---------|
| Operating System | CyberOps Workstation VM (Arch Linux) |
| Primary Tool(s) | Wireshark, Firefox, tcpdump, Mininet(R1, S1, H1, H4) |
| Key Concepts    | TCP Handshake |

---

## Procedure Summary

Web pages use the TCP protocol as information needs to be reliably transmitted. Using the provided topology (R1, S1, H1, H4), a web server is launched on H4 host with `/home/analyst/lab.support.files/scripts/reg_server_start.sh`. Tcpdump is executed on the H1 host to capture the TCP traffic when H1 navigates to `172.16.0.40` via Firefox to generate traffic on H4's web server. The TCP traffic captured on tcpdump is opened in Wireshark and filtered with `tcp` to isolate the relevant frames and inspect them through the Packet Details pane. 

Expanding the Transmission Control Protocol pane on the first SYN message from client to server reveals the Source Port 51542 and the Destination Port 80, which the server is listening to.
The SYN flag is set to 1, indicating the start of the connection and the sequence number is set to 0. The second frame sent by the server contains the SYN-ACK flags set to 1, with the destination and source port reversed and a sequence number of 0, while the acknowledgement number is 1. The final ACK flag is sent by the client with the sequence number incrementing to 1 and the acknowledgement number remaining at 1. 
Tcpdump was also used to inspect the traffic. An interesting distinction between Wireshark and tcpdump is that tcpdump represents the SYN flag as S and the ACK flag as a period (.).

---

## Key Findings

Wireshark and tcpdump, despite having different representations of data present the same handshake, demonstrating that on a packet-level, results remain tool-independent.

The underlying handshake follows a strict format of flags and sequences. The SYN->SYN-ACK->ACK progression where each frame is set as:
- Frame 1 (SYN): seq=0
- Frame 2 (SYN-ACK): seq=0, ack=1
- Frame 3 (ACK): seq=1, ack=1

The Source Port 51542 is dynamically chosen from a range (49152-65535) of ports before a client attempts to communicate with a server, where the port number of the server is based on the service running on it. In this case, the HTTP service is listening on port number 80.

---

## References

-CyberOps Associate, Using Wireshark to Observe the TCP 3-Way Handshake Using Wireshark to Observe the TCP 3-Way Handshake

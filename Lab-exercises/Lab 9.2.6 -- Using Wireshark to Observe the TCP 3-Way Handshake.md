# Lab 9.2.6 — Using Wireshark to Observe the TCP 3-Way Handshake

>**Author:** Christos Panopoulos
>**Course:** Cisco CyberOps Associate
>**Date:** July 2026

## Overview
[Written last]

---

## Background

When applications use the TCP protocol, they require all the data to be reliably transmitted, as every segment is important. TCP achieves that reliability by establishing a stateful communication with the destination server before transmitting. The TCP three-way handshake is the process of establishing communication with the destination, which happens in three stages. First, the client starts by sending a SYN request to the server, the server receives the request and responds with its own SYN request and an acknowledgement message ACK (SYN-ACK). Finally, the client responds with an ACK message to establish the communication stream. After establishing the communication, data can be transmitted between the client and server reliably. As a defender, knowing the correct handshake process can help spot anomalies during a handshake, like SYN floods or an incomplete process. 

---

## Environment & Tools

---

## Procedure Summary

---

## Key Findings

---

## References

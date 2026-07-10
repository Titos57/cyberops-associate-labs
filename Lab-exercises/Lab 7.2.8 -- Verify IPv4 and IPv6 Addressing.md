# Lab 7.2.8 -- Verify IPv4 and IPv6 Addressing

>**Author:** Christos Panopoulos
>**Course:** Cisco CyberOps Associate
>**Environment:** Cisco Packet Tracer

---

## Overview

Using the provided topology of three routers and two hosts on Packet Tracer and running commands like `ping` and `tracert` provided equivalent results regardless of whether IPv4 or IPv6 addressing was used.
The `ipconfig /all` command provided the information to perform the dual-stack tests. The successful execution of the commands indicates the proper configuration of both the hosts and routers, as well as the consistent path routing regardless of IP version.

---

## Environment & Tools

- Cisco Packet Tracer
- Devices in topology: R1, R2, R3, PC1, PC2
- Addressing scheme in use: dual-stack IPv4 and IPv6
- Commands used: `ipconfig /all`, `ping`, `tracert`

---

## Procedure Summary

Launching Packet Tracer with the topology given(R1, R2, R3, PC1, PC2) and executing `ipconfig /all` on both PC1 and PC2 command prompts displays information about the two hosts.
PC1 has an IPv4 address of `10.10.1.100` and an IPv6 address of `2001:DB8:1:1::A/64`, with a subnet mask of `255.255.255.224` and an IPv4 default gateway of `10.10.1.97` and IPv6 `FE80::1`.
PC2 has an IPv4 address of `10.10.1.20` and an IPv6 address of `2001:DB8:1:4::A/64`, with a subnet mask of `255.255.255.240` and an IPv4 default gateway of `10.10.1.17` and IPv6 `FE80::3`. Attempting to `ping`
both hosts from one another with IPv4 and IPv6 addresses was successful, showing they are configured correctly with 4 packets received and 0% Loss on all 4 pings. 
Sending ICMP messages with `tracert` from both hosts revealed the same IP addresses starting from PC2, the first hop is `10.10.1.17`(R3), the second hop is `10.10.1.9`(R2), the third hop is `10.10.1.6`(R1) and 
finally reaching PC1 at `10.10.1.100`. By tracing with IPv6 addresses this time, the result follows the same path starting from `2001:DB8:1:4::1`(R3), then `2001:DB8:1:3::1`(R2), the third hop is `2001:DB8:1:2::2`(R1)
and the final hop is PC1 with `2001:DB8:1:1::A` IPv6 address.

![ipconfig + ping](../Lab-screenshots/Packet%20Tracer/ipconfig%20%2B%20ping.png)
![IPv4 tracert](../Lab-screenshots/Packet%20Tracer/IPv4%20tracert.png)

---

## References

- Cisco Networking Academy, *Packet Tracer - Verify IPv4 and IPv6 Addressing*, CyberOps Associate course materials, 2020.

---

# 🛠️ Networking Tools Operational Guide

This document outlines the standard Command Line Interface (CLI) tools used for network troubleshooting and initial reconnaissance.

## 1. Ping (ICMP)
Uses the **Internet Control Message Protocol** to check if a host is reachable.
* **Syntax:** `ping <target_ip>`
* **Security Note:** Many Windows firewalls block ICMP Echo Requests by default. A failed ping does *not* always mean the host is offline.
* **Linux Flag:** `ping -c 4 <ip>` (Sends only 4 packets).

## 2. Traceroute / Tracert
Maps the path data takes to reach its destination, showing every router (hop) along the way.
* **Syntax (Linux):** `traceroute <target_ip>`
* **Syntax (Windows):** `tracert <target_ip>`
* **Use Case:** Identifying network bottlenecks or visualizing the path traffic takes through the internet.

## 3. Telnet (Banner Grabbing)
While Telnet is insecure for remote management, it is excellent for **Banner Grabbing**—connecting to a port to see what version of software is running.
* **Syntax:** `telnet <ip> <port>`
* **Example:** `telnet 192.168.1.10 80`
* **Output:** Might reveal `Apache/2.4.41 (Ubuntu)`, giving the attacker specific version info to look for CVEs.

## 4. ARP (Address Resolution Protocol)
Displays the mapping between IP addresses (Layer 3) and MAC addresses (Layer 2).
* **Syntax:** `arp -a`
* **Security Note:** Used to detect **ARP Poisoning** attacks where an attacker associates their MAC address with the gateway IP.

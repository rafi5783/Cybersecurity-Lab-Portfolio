# 🦈 Tcpdump: The Basics

This room explores the fundamental usage of the powerful command-line network packet analyzer, **tcpdump**.

---

## 💻 Task 1: Introduction

**tcpdump** is a command-line utility for capturing and analyzing network traffic. It is widely used by network administrators and security professionals for debugging network issues, monitoring traffic, and analyzing security incidents.

It operates by capturing packets that pass over a network interface and displaying them based on specified criteria.

**Key Features:**
* **Packet Capture:** Sniffs and captures packets in real-time.
* **Protocol Analysis:** Decodes various network protocols (TCP, UDP, ICMP, etc.).
* **Filtering:** Allows for complex filtering of captured traffic.
* **Saving Output:** Can save captured packets to a file for later analysis (using tools like Wireshark).

---

## ⚙️ Task 2: Basic Packet Capture

To start capturing packets, you simply execute the `tcpdump` command. The basic syntax is:

```bash
tcpdump [options]
Option,Description
-i <interface>,"Specifies the network interface to listen on (e.g., eth0, lo)."
-n,Don't resolve hostnames (show IP addresses instead).
-nn,Don't resolve hostnames or port names (show IP addresses and port numbers).
"-v, -vv, -vvv",Increase the verbosity of the output.
-c <count>,Stop after capturing <count> number of packets.
-s <snaplen>,"Set the snap-length (packet size) to capture, often set to 0 for full packet capture."
-w <file>,Write the raw packet data to a specified file (for later analysis).
-r <file>,Read packets from a specified file (created with -w).


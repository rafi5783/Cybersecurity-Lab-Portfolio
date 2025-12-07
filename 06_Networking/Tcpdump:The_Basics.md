# 🦈 Tcpdump: The Basics

## 💻 Introduction

**tcpdump** is a command-line utility for capturing and analyzing network traffic. It is widely used by network administrators and security professionals for debugging network issues, monitoring traffic, and analyzing security incidents.

It operates by capturing packets that pass over a network interface and displaying them based on specified criteria.

**Key Features:**
* **Packet Capture:** Sniffs and captures packets in real-time.
* **Protocol Analysis:** Decodes various network protocols (TCP, UDP, ICMP, etc.).
* **Filtering:** Allows for complex filtering of captured traffic.
* **Saving Output:** Can save captured packets to a file for later analysis (using tools like Wireshark).

---

## ⚙️ Basic Packet Capture

To start capturing packets, you simply execute the `tcpdump` command. The basic syntax is:


Option,Description
-i <interface>,"Specifies the network interface to listen on (e.g., eth0, lo)."
-n,Don't resolve hostnames (show IP addresses instead).
-nn,Don't resolve hostnames or port names (show IP addresses and port numbers).
"-v, -vv, -vvv",Increase the verbosity of the output.
-c <count>,Stop after capturing <count> number of packets.
-s <snaplen>,"Set the snap-length (packet size) to capture, often set to 0 for full packet capture."
-w <file>,Write the raw packet data to a specified file (for later analysis).
-r <file>,Read packets from a specified file (created with -w).

## 🔍 Filtering Expressions
Filtering is the most powerful feature of Tcpdump. It allows you to isolate specific traffic rather than being overwhelmed by all network noise.Host FilteringFilter traffic coming from or going to a specific IP address.Bash# Capture traffic involving a specific host
tcpdump host 192.168.1.5

# Capture traffic ONLY from a source IP
tcpdump src host 192.168.1.5

# Capture traffic ONLY to a destination IP
tcpdump dst host 192.168.1.5
Port FilteringFilter traffic on specific ports (e.g., Web or SSH traffic).Bash# Capture traffic on port 80 (HTTP)
tcpdump port 80

# Capture traffic on destination port 443 (HTTPS)
tcpdump dst port 443
Protocol FilteringYou can filter by protocol name directly.Bash# Capture only ICMP (Ping) packets
tcpdump icmp

# Capture only UDP traffic
tcpdump udp

## 🧠 Advanced Filtering (Logical Operators)
You can combine multiple filters using logical operators to create precise queries.

Operator,Keyword,Description
AND,"and, &&",Both conditions must be true.
OR,"or, `",
NOT,"not, !",The condition must be false.

# Examples:

# Capture traffic from 192.168.1.5 AND destination port 80
tcpdump src host 192.168.1.5 and dst port 80

# Capture DNS (port 53) OR HTTP (port 80) traffic
tcpdump port 53 or port 80

# Capture all traffic EXCEPT SSH (port 22)
tcpdump not port 22

## 🔬 Bitwise & Flag Filtering
For advanced analysis, you can filter based on TCP flags (SYN, ACK, RST, FIN). This is useful for detecting port scans or connection issues.

# Syntax: tcp[tcpflags] == tcp-<flag>

# Capture only TCP SYN packets (Connection Requests)
tcpdump 'tcp[tcpflags] == tcp-syn'

# Capture TCP RST packets (Connection Resets)
tcpdump 'tcp[tcpflags] == tcp-rst'

# Capture packets with the ACK flag set
tcpdump 'tcp[tcpflags] & tcp-ack != 0'

## 📝 Conclusion
Tcpdump is an essential tool for any security analyst. While Wireshark provides a graphical interface, Tcpdump is lightweight, scriptable, and available on almost every Linux system by default.

# Cheatsheet Summary:

Listen: tcpdump -i eth0

Write to file: tcpdump -w capture.pcap

Read from file: tcpdump -r capture.pcap

No Name Resolution: tcpdump -n

Filter: tcpdump host 10.10.10.1 and port 80

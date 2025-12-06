# Wireshark: The Basics

## Introduction

**Wireshark** is the industry-standard, open-source network protocol analyzer. It is used essentially to "microscope" network traffic, allowing you to see what is happening on your network at a microscopic level.

### Key Concepts
* **Packet Sniffing:** Wireshark captures (sniffs) packets as they traverse a network interface (like Ethernet or Wi-Fi). It captures traffic in real-time and displays it in a human-readable format.
* **Promiscuous Mode:** By default, network cards only listen to traffic addressed to them. Wireshark often uses "promiscuous mode" to capture *all* traffic on the wire, regardless of the destination.
* **PCAP (Packet Capture):** This is the file format used to save captured data. `.pcap` or `.pcapng` files contain a recording of network traffic that can be analyzed offline later.
* **Use Cases:**
    * **Network Troubleshooting:** Finding latency issues, dropped packets, or misconfigurations.
    * **Security Analysis:** Identifying malicious traffic, malware beaconing, or unauthorized data exfiltration.
    * **Education:** Learning how protocols (HTTP, TCP, DNS) work under the hood.

> **Note:** Packet capturing can view sensitive data (passwords, emails) if the traffic is unencrypted. Always ensure you have authorization before capturing traffic on a network you do not own.

---

## Tool Overview

When you open Wireshark and load a capture file, the interface is divided into three primary distinct panes. Understanding these is crucial for analysis.

### 1. The Packet List Pane (Top)
This displays a summary of each captured packet.
* **Columns:** Typically shows `No.` (Packet Number), `Time`, `Source`, `Destination`, `Protocol`, `Length`, and `Info`.
* **Color Coding:** Wireshark uses colors to help you identify traffic types quickly (e.g., Green for TCP, Light Blue for UDP, Black for errors).

### 2. The Packet Details Pane (Middle)
This provides a hierarchical view of the selected packet, breaking it down by protocol layers (OSI Model).
* **Frame:** Physical layer details (bits on the wire).
* **Ethernet II:** Data Link layer (MAC addresses).
* **Internet Protocol (IP):** Network layer (IP addresses).
* **Transmission Control Protocol (TCP) / UDP:** Transport layer (Ports).
* **Application Layer:** The actual data (HTTP, DNS, SSH).

### 3. The Packet Bytes Pane (Bottom)
This shows the raw data of the packet in **Hexadecimal** (left side) and **ASCII** (right side). When you click a field in the "Details" pane, the corresponding bytes are highlighted here.

### Toolbar Basics
* **Blue Shark Fin:** Start capturing.
* **Red Square:** Stop capturing.
* **Green Fin:** Restart capturing.
* **Magnifying Glass:** Find packets (search).

---

## Packet Dissection

Packet dissection is the process of translating raw binary data into human-readable fields. Wireshark uses "dissectors" to understand thousands of different protocols.

### Dissecting the OSI Layers
To analyze a packet, you expand the "trees" in the **Packet Details Pane**:

1.  **Layer 1 (Physical):** Expand the **Frame** line. This shows the arrival time, interface ID, and total frame length.
2.  **Layer 2 (Data Link):** Expand **Ethernet II**. Here you verify the **Source MAC** and **Destination MAC**.
3.  **Layer 3 (Network):** Expand **Internet Protocol Version 4/6**. This allows you to verify the **Source IP** and **Destination IP** and the Time-to-Live (TTL).
4.  **Layer 4 (Transport):** Expand **TCP** or **UDP**. This reveals **Source Port**, **Destination Port**, Sequence Numbers, and Flags (SYN, ACK, FIN).
5.  **Layer 7 (Application):** Expand protocols like **HTTP**. This reveals the method (GET/POST), User-Agent, and requested URI.

---

## Packet Navigation

In large capture files (which can contain millions of packets), navigating efficiently is a required skill.

### Go To Packet
If you know the specific packet number you need to analyze:
* Use the shortcut `Ctrl + G`.
* Enter the Packet Number to jump directly to it.

### Find Packets
To search for specific data inside a packet:
* Use `Ctrl + F` to open the search bar.
* **Display Filter:** Search by protocol query.
* **String:** Search for text (e.g., "password" or "admin") inside the packet bytes.
* **Hex Value:** Search for a specific hex signature.

### Marking and Comments
* **Mark/Unmark:** `Ctrl + M`. This highlights a packet in black, useful for bookmarking interesting packets while scrolling.
* **Packet Comments:** You can right-click a packet and add a comment to leave notes for yourself or other analysts.

---

## Packet Filtering

Filtering is the most powerful feature of Wireshark. It allows you to ignore the noise and focus on specific traffic. There are two types: **Capture Filters** (set before capturing) and **Display Filters** (applied after capturing).

### Common Display Filters
Type these into the bar at the top and press **Enter** (or the blue arrow).

* **Filter by Protocol:**
    * `tcp`, `udp`, `dns`, `http`, `icmp`
* **Filter by IP:**
    * `ip.addr == 192.168.1.1` (Shows traffic to OR from this IP)
    * `ip.src == 192.168.1.1` (Shows traffic ONLY from this IP)
    * `ip.dst == 192.168.1.1` (Shows traffic ONLY to this IP)
* **Filter by Port:**
    * `tcp.port == 80`
    * `udp.port == 53`
* **Logical Operators:**
    * `&&` (AND): `ip.src == 10.10.10.1 && tcp.port == 443`
    * `||` (OR): `dns || http`
    * `!` (NOT): `!arp` (Exclude all ARP traffic)

### Following Streams
To see the full reconstruction of a conversation (e.g., a web page loading or a login attempt):
1.  Right-click a TCP packet.
2.  Select **Follow** > **TCP Stream**.
3.  This opens a new window showing the data payload purely as text, with client data in **Red** and server data in **Blue**.

---

## Conclusion

Wireshark is an indispensable tool for any IT or Cybersecurity professional. It bridges the gap between abstract networking theory and the reality of what is actually moving across the wire.

**Summary of Skills Learned:**
* **Interface:** Navigating the three main panes.
* **Dissection:** Translating bits into protocol layers.
* **Navigation:** Using search and "Go To" to move through large files.
* **Filtering:** Using query syntax to isolate specific events.

Mastering these basics provides the foundation for advanced tasks like malware analysis, network forensics, and performance tuning.

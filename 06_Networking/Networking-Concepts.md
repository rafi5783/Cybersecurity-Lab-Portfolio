# Networking Concepts Summary

## 1. The OSI Model (Open Systems Interconnection)
A conceptual framework developed by ISO to describe how network communications occur. It consists of seven layers (1 being the bottom, 7 being the top).


### Layer Breakdown
* **Layer 1: Physical Layer**
    * **Function:** Deals with physical connections and transmission of binary digits (0s and 1s).
    * **Media:** Electrical (Ethernet), Optical (Fiber), Wireless (WiFi 2.4/5/6 GHz).
* **Layer 2: Data Link Layer**
    * **Function:** Enables node-to-node transfer on the same **network segment**. Handles physical addressing.
    * **Addressing:** **MAC Address** (Media Access Control). 6 bytes, hexadecimal. First 3 bytes = Vendor ID.
    * **Unit:** Frame.
    * **Protocols:** Ethernet (802.3), WiFi (802.11).
* **Layer 3: Network Layer**
    * **Function:** Inter-network communication (sending data between *different* networks). Handles **logical addressing** and **routing** (finding the best path).
    * **Unit:** Packet.
    * **Protocols:** IP (IPv4/IPv6), ICMP, IPSec.
* **Layer 4: Transport Layer**
    * **Function:** End-to-end communication between specific applications on hosts. Handles flow control, segmentation, and error correction.
    * **Protocols:** TCP (Reliable), UDP (Fast).
* **Layer 5: Session Layer**
    * **Function:** Establishing, maintaining, and synchronizing sessions between applications.
    * **Protocols:** NFS, RPC.
* **Layer 6: Presentation Layer**
    * **Function:** Data translation, encryption, compression, and character encoding. Ensures the application layer can understand the data.
    * **Examples:** ASCII, Unicode, JPEG, PNG, MIME (for email attachments).
* **Layer 7: Application Layer**
    * **Function:** Provides network services directly to end-user applications (browsers, email clients).
    * **Protocols:** HTTP, FTP, DNS, SMTP, POP3, IMAP.



<img width="900" height="450" alt="image" src="https://github.com/user-attachments/assets/73d85e2d-8a6f-4539-9c2e-bf44b3430f29" />



---

## 2. The TCP/IP Model
A practical, implemented model developed by the DoD (Department of Defense). Designed for survivability and dynamic routing. It maps to the OSI model but groups layers differently.

### Layer Mapping (Top to Bottom)
1.  **Application Layer:** Combines OSI Layers 5, 6, and 7. (HTTP, FTP, SSH, etc.).
2.  **Transport Layer:** Maps to OSI Layer 4. (TCP, UDP).
3.  **Internet Layer:** Maps to OSI Layer 3. (IP, ICMP).
4.  **Link Layer:** Maps to OSI Layer 2 (and often Layer 1 in 5-layer models).



<img width="1280" height="960" alt="image" src="https://github.com/user-attachments/assets/f7167adc-f55b-4ab1-a0c4-6b09889807a7" />



---

## 3. IP Addressing (Internet Protocol)
An identifier for a host on a network, functioning like a postal address.

### IPv4 Structure
* **Format:** 32 bits divided into four octets (e.g., `192.168.0.1`).
* **Range:** Each octet is 0–255.
* **Special Addresses:**
    * **Network Address:** The first address in a range (e.g., `.0`). Identifies the subnet.
    * **Broadcast Address:** The last address in a range (e.g., `.255`). Targets all hosts on that subnet.

### Subnet Masks
* Used to divide the IP into Network bits and Host bits.
* **CIDR Notation:** `/24` (e.g., `255.255.255.0`) means the first 24 bits are the network, remaining 8 bits are for hosts.

### Command Line Tools
* **Windows:** `ipconfig`
* **Linux:** `ifconfig` or `ip a s` (ip address show).

### Private vs. Public Addresses
* **Public IP:** Routable on the internet; unique worldwide.
* **Private IP:** Used within local networks (LAN); cannot be routed on the internet without NAT (Network Address Translation). Defined in **RFC 1918**.

**Private Ranges:**
* `10.0.0.0` - `10.255.255.255` (/8)
* `172.16.0.0` - `172.31.255.255` (/12)
* `192.168.0.0` - `192.168.255.255` (/16)

---

## 4. Routing and Transport Protocols

### Routing
* **Role:** Routers operate at **Layer 3**. They inspect the destination IP and forward the packet to the next best router (hop) until it reaches the destination.

### UDP (User Datagram Protocol)
* **Type:** Connectionless (Fire and forget).
* **Features:** Unreliable (no delivery confirmation), no ordering, lower overhead, faster speed.
* **Use Case:** Streaming, DNS, gaming.
* **Analogy:** Standard mail without tracking.

### TCP (Transmission Control Protocol)
* **Type:** Connection-oriented.
* **Features:** Reliable delivery, error checking, sequencing (ordering of packets).
* **Connection Process:** **Three-Way Handshake**.
    1.  **SYN:** Client sends synchronization request with initial sequence number.
    2.  **SYN-ACK:** Server acknowledges and sends its own sequence number.
    3.  **ACK:** Client acknowledges the server's response.



<img width="1280" height="640" alt="image" src="https://github.com/user-attachments/assets/e8c17302-e55b-47f2-872b-5099bf3e120e" />



### Ports
Used to identify specific *processes* or services on a host. Range: 0–65535.
* IP identifies the *device*; Port identifies the *application*.

---

## 5. Encapsulation
The process where each layer adds a header (and sometimes a trailer) to the data received from the layer above before passing it down.

**The Flow (Top to Bottom):**
1.  **Application:** User data is created.
2.  **Transport:** Adds TCP/UDP header $\rightarrow$ Becomes a **Segment** or **Datagram**.
3.  **Network:** Adds IP header (Source/Dest IP) $\rightarrow$ Becomes a **Packet**.
4.  **Data Link:** Adds MAC header and trailer $\rightarrow$ Becomes a **Frame**.
5.  **Physical:** Transmits bits via wire/wireless.

*Decapsulation* is the reverse process happening at the receiving end.



---

## 6. Telnet
* **Protocol:** TELNET (Teletype Network).
* **Function:** Allows remote terminal connection to issue text commands.
* **Security:** Sends data in cleartext (insecure compared to SSH).
* **Testing Usage:** Can be used to manually connect to any TCP port to test services.
    * **Port 7 (Echo):** Echoes back input.
    * **Port 13 (Daytime):** Returns date/time.
    * **Port 80 (HTTP):** Can manually send `GET / HTTP/1.1` request to retrieve web pages.

# 🏗️ The OSI Model Reference

Understanding the OSI model is critical for identifying where attacks happen (e.g., Layer 7 DDoS vs. Layer 3 Spoofing).

| Layer | Name | Function | Security Relevance |
| :--- | :--- | :--- | :--- |
| **7** | **Application** | User interaction (HTTP, FTP) | Web Attacks (SQLi, XSS) happen here. |
| **6** | **Presentation** | Data formatting/encryption | SSL/TLS encryption occurs here. |
| **5** | **Session** | Establishes connections | Session Hijacking vulnerabilities. |
| **4** | **Transport** | Data transfer (TCP/UDP) | Port Scanning and Firewall filtering. |
| **3** | **Network** | Routing (IP Addresses) | IP Spoofing and Router ACLs. |
| **2** | **Data Link** | Physical addressing (MAC) | ARP Spoofing and MAC filtering. |
| **1** | **Physical** | Cables and electrical signals | Wiretapping and physical security. |

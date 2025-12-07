# Networking Core Protocols

This module explores the fundamental protocols that power the internet and local networks. Understanding these core protocols is essential for network analysis, troubleshooting, and cybersecurity operations.

---


## DNS: Remembering Addresses

**Domain Name System (DNS)** acts as the phonebook of the internet. It translates human-readable domain names (like `google.com`) into machine-readable IP addresses (like `142.250.190.46`).

* **Default Port:** 53 (UDP/TCP)
* **Key Function:** Resolution of Hostnames to IP addresses.
* **Record Types:**
    * **A Record:** IPv4 Address.
    * **AAAA Record:** IPv6 Address.
    * **CNAME:** Canonical Name (Alias).
    * **MX:** Mail Exchange (Email servers).
    * **TXT:** Text records (often used for verification like SPF/DKIM).

---

## WHOIS

**WHOIS** is a query and response protocol that is widely used for querying databases that store the registered users or assignees of an Internet resource, such as a domain name, an IP address block, or an autonomous system.

* **Default Port:** 43 (TCP)
* **Key Function:** Identify domain ownership and registration details.
* **Information Retrieved:**
    * Registrar information.
    * Registrant contact details (Name, Organization, Email).
    * Registration and Expiration dates.
    * Name Servers.

*Note: Due to GDPR and privacy protection, much of this information is often redacted in public queries.*

---

## HTTP(S): Accessing the Web

**HyperText Transfer Protocol (HTTP)** and its secure version **(HTTPS)** are the foundation of data communication for the World Wide Web.

### HTTP
* **Default Port:** 80
* **Function:** Transmits data in cleartext (unencrypted).
* **Structure:** Client sends a request -> Server sends a response.

### HTTPS (Secure)
* **Default Port:** 443
* **Function:** Transmits data encrypted via TLS (Transport Layer Security) or SSL (Secure Sockets Layer).
* **Importance:** Prevents Man-in-the-Middle (MitM) attacks and eavesdropping.

**Common Status Codes:**
* **200 OK:** Request succeeded.
* **404 Not Found:** Resource does not exist.
* **403 Forbidden:** Access denied.
* **500 Internal Server Error:** Server-side issue.

---

## FTP: Transferring Files

**File Transfer Protocol (FTP)** is a standard network protocol used for the transfer of computer files between a client and server on a computer network.

* **Default Ports:**
    * **Port 21:** Command/Control channel (sending commands like LIST, RETR).
    * **Port 20:** Data channel (actual file transfer).
* **Security Warning:** Standard FTP sends usernames and passwords in cleartext. It is recommended to use **SFTP** (SSH File Transfer Protocol) or **FTPS** (FTP over SSL) for secure transfers.

---

## SMTP: Sending Email

**Simple Mail Transfer Protocol (SMTP)** is the standard protocol for *sending* emails across the Internet.

* **Default Ports:**
    * **25:** Default for relaying (often blocked by ISPs to prevent spam).
    * **587:** Modern standard for secure submission (uses STARTTLS).
    * **465:** Legacy secure port (SMTPS).
* **Function:** Handles the sending of mail from a client to a mail server, or between mail servers. It is strictly a "push" protocol.

---

## POP3: Receiving Email

**Post Office Protocol version 3 (POP3)** is an older standard used by local email clients to retrieve emails from a remote server over a TCP/IP connection.

* **Default Port:** 110 (Unencrypted) / 995 (SSL/TLS).
* **Key Characteristic:** Download and Delete.
    * By default, POP3 downloads email to the local device and deletes it from the server.
    * It is not ideal for users who access email from multiple devices (e.g., phone and laptop), as the email only exists on the device that downloaded it first.

---

## IMAP: Synchronizing Email

**Internet Message Access Protocol (IMAP)** is the modern standard for email retrieval and storage.

* **Default Port:** 143 (Unencrypted) / 993 (SSL/TLS).
* **Key Characteristic:** Synchronization.
    * Emails are stored on the server.
    * The client synchronizes with the server, viewing a copy of the messages.
    * Actions (read, delete, move) performed on one device are reflected on all other devices accessing that account.

---

## Conclusion

Networking protocols are the vocabulary of the internet.
* **DNS** locates the destination.
* **HTTP/S** delivers the content.
* **FTP** moves the files.
* **SMTP, POP3, and IMAP** handle communication via email.


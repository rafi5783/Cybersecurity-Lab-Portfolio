# 🌐 Web Fundamentals & Security Basics

## 1. How the Web Works
The World Wide Web (WWW) acts as an information retrieval service built on top of the Internet. It relies on the **Client-Server** model.
- **Client:** The browser (Chrome, Firefox, curl) that requests data.
- **Server:** The computer hosting the website/application that sends data back.

### The Request-Response Cycle
1. **User** types a URL.
2. **DNS** resolves the domain to an IP address.
3. **Browser** sends an HTTP Request to that IP.
4. **Server** processes it and sends an HTTP Response (HTML, JSON, etc.).
5. **Browser** renders the response for the user.

---

## 2. DNS (Domain Name System)
DNS is the "Phonebook of the Internet." It translates human-readable domain names into machine-readable IP addresses.

| Record Type | Description | Example |
| :--- | :--- | :--- |
| **A Record** | Maps a domain to an IPv4 address. | `google.com` -> `142.250.190.46` |
| **AAAA Record** | Maps a domain to an IPv6 address. | `google.com` -> `2001:4860::` |
| **CNAME** | "Canonical Name" (Alias). Maps one domain to another. | `www.example.com` -> `example.com` |
| **TXT Record** | Text notes. Often used for verification (SPF, DKIM). | `v=spf1 include:_spf.google.com ~all` |

> **Security Note:** Attackers often use **DNS Spoofing** or **Poisoning** to redirect users to fake websites by corrupting this resolution process.

---

## 3. HTTP (HyperText Transfer Protocol)
HTTP is the protocol used for communicating on the web. It is a stateless protocol, meaning each request is independent.

### Common HTTP Methods (Verbs)
* **GET:** Retrieve data (e.g., viewing a page). *Parameters are visible in the URL.*
* **POST:** Submit data (e.g., logging in). *Data is hidden in the body.*
* **PUT:** Update or replace a resource.
* **DELETE:** Remove a resource.



### HTTP Status Codes
These codes tell the client the result of their request.

* **2xx (Success):**
    * `200 OK`: Request succeeded.
* **3xx (Redirection):**
    * `301 Moved Permanently`: The page has moved to a new URL.
    * `302 Found`: Temporary redirect.
* **4xx (Client Error):**
    * `400 Bad Request`: Server couldn't understand the request.
    * `401 Unauthorized`: You need to log in.
    * `403 Forbidden`: You are logged in but don't have permission.
    * `404 Not Found`: The resource doesn't exist.
* **5xx (Server Error):**
    * `500 Internal Server Error`: The server crashed or had a code error.
    * `503 Service Unavailable`: Server is overloaded or down.

---

## 4. Headers & Cookies
Headers provide "metadata" about the request or response.

### Key Headers
* **User-Agent:** Tells the server what browser/OS you are using.
* **Content-Type:** Tells the client what file type is being sent (e.g., `text/html`, `application/json`).
* **Host:** The specific domain name being requested (crucial for virtual hosting).

### Cookies
Because HTTP is stateless, servers use **Cookies** to remember who you are.
1. You log in.
2. Server sends a `Set-Cookie: session_id=xyz` header.
3. Your browser saves this and sends `Cookie: session_id=xyz` with every subsequent request.

> **Security Note:** If an attacker steals your **Session Cookie**, they can impersonate you without your password (Session Hijacking).

---

## 5. Web Vulnerabilities (The "Big 3" Basics)

### A. SQL Injection (SQLi)
Occurs when user input is dangerously concatenated directly into a database query.
* **Attack:** `' OR 1=1 --`
* **Result:** Bypasses login or dumps the database.

### B. Cross-Site Scripting (XSS)
Occurs when an application includes untrusted data in a web page without validation.
* **Attack:** `<script>alert('Hacked')</script>`
* **Result:** Steals cookies, redirects users, or defaces websites.

### C. IDOR (Insecure Direct Object Reference)
Occurs when an application exposes a reference to an internal object (like a file or database key) without checking permissions.
* **Attack:** Changing `user_id=100` to `user_id=101` in the URL.
* **Result:** Viewing another user's private profile.

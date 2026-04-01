# Phase 1 — Foundations (Days 1–60)

> Build the base. You cannot find security bugs in systems you don't understand.

---

## Week 1 — How the Internet Works (Days 1–7)

### Day 1 — HTTP Basics
**What to learn:** HTTP methods (GET, POST, PUT, DELETE, PATCH), status codes, request/response structure
- 📖 [MDN HTTP Overview](https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview)
- 🎥 [HTTP Crash Course — Traversy Media](https://www.youtube.com/watch?v=iYM2zFP3Zn0)
- 🎥 [HTTP Full Course — freeCodeCamp](https://www.youtube.com/watch?v=2JYT5f2isg4)
- ✅ Task: Use browser DevTools → Network tab → visit any site → read the raw HTTP request/response

### Day 2 — HTTP Headers and Cookies
**What to learn:** Common headers (Content-Type, Authorization, Cookie, X-Forwarded-For), how cookies work, Set-Cookie flags (HttpOnly, Secure, SameSite)
- 📖 [MDN HTTP Headers](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers)
- 📖 [OWASP Secure Cookie Guide](https://owasp.org/www-chapter-london/assets/slides/OWASPLondon20171130_Cookie_Security_Myths_Misconceptions_David_Johansson.pdf)
- ✅ Task: Open DevTools → Application → Cookies → find a site's cookies and read their flags

### Day 3 — HTTPS and TLS
**What to learn:** How TLS handshake works, certificates, what HTTPS protects (and what it doesn't)
- 📖 [Cloudflare — What is TLS?](https://www.cloudflare.com/learning/ssl/transport-layer-security-tls/)
- 🎥 [TLS Explained Simply — ByteByteGo](https://www.youtube.com/watch?v=AlE5X1NlHgg)
- ✅ Task: Visit a site in browser → click the padlock → read the certificate details

### Day 4 — DNS
**What to learn:** DNS records (A, AAAA, CNAME, MX, TXT, NS), how DNS resolution works, why it matters for recon
- 📖 [Cloudflare — What is DNS?](https://www.cloudflare.com/learning/dns/what-is-dns/)
- 🎥 [DNS Explained — Computerphile](https://www.youtube.com/watch?v=72snZctFFtA)
- ✅ Task: Run `nslookup google.com` and `dig google.com ANY` in terminal

### Day 5 — Sessions and Authentication Basics
**What to learn:** Session tokens vs JWTs, how login works, why session IDs matter, stateless vs stateful
- 📖 [OWASP Session Management](https://cheatsheetseries.owasp.org/cheatsheets/Session_Management_Cheat_Sheet.html)
- 🎥 [Session vs Token Auth — Web Dev Simplified](https://www.youtube.com/watch?v=UBUNrFtufWo)
- ✅ Task: Login to a site → inspect the session cookie → what happens when you delete it?

### Day 6 — Same-Origin Policy and CORS
**What to learn:** What SOP is, why it exists, what CORS allows, how misconfigs cause vulnerabilities
- 📖 [MDN Same-Origin Policy](https://developer.mozilla.org/en-US/docs/Web/Security/Same-origin_policy)
- 📖 [PortSwigger CORS Guide](https://portswigger.net/web-security/cors)
- ✅ Task: Read the PortSwigger CORS intro page fully

### Day 7 — Wrap Up + Review
- ✅ Revisit Days 1–6 topics you found confusing
- ✅ Lab: [TryHackMe — HTTP in Detail](https://tryhackme.com/room/httpindetail) (free room)

---

## Week 2 — Linux for Security (Days 8–14)

### Day 8 — Linux File System
**What to learn:** `/etc`, `/var/log`, `/home`, `/tmp`, `/proc` — what lives where and why it matters for security
- 🎥 [Linux File System Explained — DorianDotSlash](https://www.youtube.com/watch?v=HbgzrKJvDg8)
- ✅ Task: Explore your system — `ls -la /etc`, `cat /etc/passwd`, `ls /var/log`

### Day 9 — Linux Permissions
**What to learn:** chmod, chown, SUID/SGID bits, sticky bit, how privilege escalation exploits bad permissions
- 📖 [Linux Permissions Guide](https://linuxhandbook.com/linux-file-permissions/)
- 🎥 [Linux Permissions — TCM Security](https://www.youtube.com/watch?v=I4EWvMFj37g)
- ✅ Task: Find SUID binaries: `find / -perm -4000 2>/dev/null`

### Day 10 — Essential Linux Commands
**What to learn:** `grep`, `find`, `curl`, `wget`, `netstat`/`ss`, `ps`, `awk`, `sed`, piping
- 📖 [Linux Command Cheatsheet](https://cheatography.com/davechild/cheat-sheets/linux-command-line/)
- ✅ Task: OverTheWire Bandit — [Levels 0–5](https://overthewire.org/wargames/bandit/)

### Day 11 — Bash Scripting Basics
**What to learn:** Variables, loops, conditionals, functions — enough to automate recon tasks
- 🎥 [Bash Scripting Tutorial — freeCodeCamp](https://www.youtube.com/watch?v=tK9Oc6AEnR4)
- ✅ Task: Write a bash script that pings a list of IPs and logs which ones respond

### Day 12 — Networking Commands
**What to learn:** `nmap`, `curl`, `netcat`, `traceroute`, `whois`, `ping`
- 🎥 [Nmap Tutorial — NetworkChuck](https://www.youtube.com/watch?v=4t4kBkMsDbQ)
- ✅ Task: Run `nmap -sV -sC localhost` and understand the output

### Day 13 — Log Analysis
**What to learn:** Reading `/var/log/auth.log`, `/var/log/apache2/access.log`, what attackers leave behind
- 📖 [OWASP Log Files Guide](https://owasp.org/www-community/controls/Log_Files)
- ✅ Task: Install Apache locally, visit a URL, read the access.log entry

### Day 14 — OverTheWire Practice
- ✅ Complete OverTheWire Bandit [Levels 6–15](https://overthewire.org/wargames/bandit/)
- ✅ Lab: [TryHackMe — Linux Fundamentals Part 1](https://tryhackme.com/room/linuxfundamentalspart1) (free)

---

## Week 3 — Networking Fundamentals (Days 15–21)

### Day 15 — OSI Model
**What to learn:** 7 layers, what happens at each layer, where attacks happen
- 🎥 [OSI Model Explained — Practical Networking](https://www.youtube.com/watch?v=LkolbURrtTs)
- ✅ Task: Map common attacks (XSS, SQLi, ARP spoofing) to their OSI layer

### Day 16 — TCP/IP and Ports
**What to learn:** TCP 3-way handshake, common ports (80, 443, 22, 21, 3306, 8080), UDP vs TCP
- 📖 [Cloudflare — What is TCP?](https://www.cloudflare.com/learning/ddos/glossary/tcp-ip/)
- 🎥 [TCP vs UDP — Practical Networking](https://www.youtube.com/watch?v=qqRYkcta6IE)
- ✅ Task: Use Wireshark — capture a TCP handshake to any website

### Day 17 — Proxies and Intercepting Traffic
**What to learn:** What a proxy is, how Burp Suite sits between browser and server, setting up FoxyProxy
- 🎥 [Burp Suite Setup — TechRaj](https://www.youtube.com/watch?v=G3hpAeoZ4ek)
- ✅ Task: Install Burp Suite Community Edition + FoxyProxy browser extension. Intercept one HTTP request.

### Day 18 — VPNs and Anonymity Basics
**What to learn:** How VPNs work, why bug hunters use them, what they hide and what they don't
- 📖 [Cloudflare — What is a VPN?](https://www.cloudflare.com/learning/access-management/what-is-a-vpn/)
- ✅ Task: Read about how HackerOne handles IP logging in their disclosure policy

### Day 19 — Firewalls and WAFs
**What to learn:** Network firewall vs WAF, how WAFs block attacks, common WAF bypass techniques
- 📖 [OWASP WAF Bypass Techniques](https://owasp.org/www-community/attacks/SQL_Injection_Bypassing_WAF)
- 🎥 [What is a WAF — Computerphile](https://www.youtube.com/watch?v=p8CQcF_9280)

### Day 20 — Wireshark Basics
**What to learn:** Capture filters, display filters, reading HTTP/HTTPS traffic
- 🎥 [Wireshark Full Tutorial — David Bombal](https://www.youtube.com/watch?v=lb1Dw0elw0Q)
- ✅ Task: Capture HTTP traffic to an HTTP (not HTTPS) site — find the request in Wireshark

### Day 21 — Review + Lab
- ✅ [TryHackMe — Pre-Security Path](https://tryhackme.com/path/outline/presecurity) — complete remaining rooms

---

## Week 4 — OWASP Top 10 Overview (Days 22–30)

### Day 22 — What is OWASP
- 📖 [OWASP Top 10 Official](https://owasp.org/www-project-top-ten/)
- 🎥 [OWASP Top 10 Explained — Simply Learn](https://www.youtube.com/watch?v=rWHvp7rUka8)
- ✅ Task: Read the full OWASP Top 10 2021 list. Take one note per category.

### Day 23 — A01: Broken Access Control
- 📖 [OWASP A01 Broken Access Control](https://owasp.org/Top10/A01_2021-Broken_Access_Control/)
- 🎥 [Broken Access Control — Rana Khalil](https://www.youtube.com/watch?v=FpnmHvxcaio)
- ✅ Task: PortSwigger — [Access Control Labs Intro](https://portswigger.net/web-security/access-control)

### Day 24 — A02: Cryptographic Failures
- 📖 [OWASP A02](https://owasp.org/Top10/A02_2021-Cryptographic_Failures/)
- ✅ Task: Find a real CVE where weak encryption caused a breach. Write 3 sentences about it.

### Day 25 — A03: Injection
- 📖 [OWASP A03 Injection](https://owasp.org/Top10/A03_2021-Injection/)
- 🎥 [SQL Injection Explained — PwnFunction](https://www.youtube.com/watch?v=ciNHn38EyRc)
- ✅ Task: Try first SQLi on [PortSwigger Lab](https://portswigger.net/web-security/sql-injection/lab-retrieve-hidden-data)

### Day 26 — A04 & A05: Insecure Design + Security Misconfiguration
- 📖 [OWASP A04](https://owasp.org/Top10/A04_2021-Insecure_Design/) | [OWASP A05](https://owasp.org/Top10/A05_2021-Security_Misconfiguration/)
- ✅ Task: Find 3 examples of security misconfiguration in public CVE databases

### Day 27 — A06 & A07: Vulnerable Components + Auth Failures
- 📖 [OWASP A06](https://owasp.org/Top10/A06_2021-Vulnerable_and_Outdated_Components/) | [OWASP A07](https://owasp.org/Top10/A07_2021-Identification_and_Authentication_Failures/)
- ✅ Task: Check if any npm or pip package you use has a known CVE using [Snyk Advisor](https://snyk.io/advisor/)

### Day 28 — A08, A09, A10
- 📖 [A08 — Software/Data Integrity](https://owasp.org/Top10/A08_2021-Software_and_Data_Integrity_Failures/)
- 📖 [A09 — Logging Failures](https://owasp.org/Top10/A09_2021-Security_Logging_and_Monitoring_Failures/)
- 📖 [A10 — SSRF](https://owasp.org/Top10/A10_2021-Server-Side_Request_Forgery_%28SSRF%29/)

### Day 29 — DVWA Setup
- ✅ Install DVWA using Docker: `docker run --rm -it -p 80:80 vulnerables/web-dvwa`
- 🎥 [DVWA Setup Guide — HackerSploit](https://www.youtube.com/watch?v=ht9840D2tkE)
- ✅ Complete DVWA Brute Force (Low security)

### Day 30 — DVWA Practice
- ✅ Complete DVWA: Command Injection, File Inclusion, XSS Reflected (all Low)
- ✅ [TryHackMe — OWASP Top 10 Room](https://tryhackme.com/room/owasptop10) (free)

---

## Week 5–6 — Web Technologies for Security (Days 31–45)

### Day 31 — HTML and the DOM
**What to learn:** DOM structure, how JavaScript interacts with DOM — essential for XSS understanding
- 🎥 [HTML Crash Course — Traversy Media](https://www.youtube.com/watch?v=UB1O30fR-EE)
- ✅ Task: Open DevTools Console → type `document.cookie` — what do you see?

### Day 32 — JavaScript Basics for Security
**What to learn:** How JS runs in browser, `fetch()`, `XMLHttpRequest`, event handlers — for XSS payloads
- 🎥 [JavaScript for Hackers — TomNomNom](https://www.youtube.com/watch?v=FTeE3OrTNoA)
- ✅ Task: Write a JS payload that creates an alert and reads `document.cookie`

### Day 33 — Web Application Architecture
**What to learn:** Frontend vs backend, APIs, databases, how data flows — what an attacker can reach
- 🎥 [Web App Architecture — Traversy Media](https://www.youtube.com/watch?v=ysEN5RaKOlA)

### Day 34 — REST APIs for Pentesters
**What to learn:** Endpoints, verbs, JSON, authentication headers — how to probe an API manually
- 📖 [REST API Security Guide — OWASP](https://owasp.org/www-project-api-security/)
- ✅ Task: Use [reqres.in](https://reqres.in) — send GET/POST/PUT requests with Postman or curl

### Day 35 — SQL Basics for Pentesters
**What to learn:** SELECT, WHERE, UNION, comments (`--`, `#`), blind queries — the SQL you need for SQLi
- 🎥 [SQL for Hackers — Rana Khalil](https://www.youtube.com/watch?v=1nJqWMh5bq0)
- ✅ Task: Install SQLite locally — practice UNION queries

### Days 36–38 — Using Burp Suite
- 🎥 [Burp Suite For Beginners — PortSwigger](https://www.youtube.com/watch?v=Ov9bfgdcBkk)
- 🎥 [Burp Suite Full Course — TechRaj](https://www.youtube.com/watch?v=G3hpAeoZ4ek)
- ✅ Task: Intercept, modify, and forward 10 different HTTP requests using Burp Repeater

### Days 39–42 — Postman for API Testing
- 🎥 [Postman Beginner Tutorial — Telequality](https://www.youtube.com/watch?v=VywxIQ2ZXw4)
- ✅ Task: Import a public API collection → test every endpoint → find one that behaves unexpectedly

### Days 43–45 — Review and Lab Sprint
- ✅ [TryHackMe — Burp Suite Basics](https://tryhackme.com/room/burpsuitebasics)
- ✅ [TryHackMe — Burp Suite Repeater](https://tryhackme.com/room/burpsuiterepeater)
- ✅ Complete DVWA all Low-security challenges

---

## Week 7–9 — Security Fundamentals (Days 46–60)

### Days 46–48 — Cryptography Basics
**What to learn:** Symmetric vs asymmetric encryption, hashing (MD5, SHA), password hashing (bcrypt, Argon2), base64
- 🎥 [Cryptography Crash Course — Computerphile](https://www.youtube.com/watch?v=AQDCe585Lnc)
- ✅ Task: Decode a base64 string. Crack an MD5 hash using [crackstation.net](https://crackstation.net)

### Days 49–51 — Authentication Mechanisms
**What to learn:** Password auth, MFA, OAuth flows, API keys, JWT — how each can fail
- 📖 [OWASP Authentication Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Authentication_Cheat_Sheet.html)
- 🎥 [JWT Explained — Fireship](https://www.youtube.com/watch?v=7Q17ubqLfaM)

### Days 52–54 — Secure Development Concepts
**What to learn:** Input validation, output encoding, parameterized queries, principle of least privilege
- 📖 [OWASP Secure Coding Practices](https://owasp.org/www-project-secure-coding-practices-quick-reference-guide/)

### Days 55–57 — Common Vulnerability Types Overview
**What to learn:** Map every OWASP Top 10 category to a real CVE — understand impact
- ✅ Task: Search [NVD NIST](https://nvd.nist.gov/) for one CVE per OWASP category. Read the description.

### Days 58–60 — Phase 1 Review and Checkpoint
- ✅ [TryHackMe — Web Fundamentals Path](https://tryhackme.com/path/outline/web) — complete remaining rooms
- ✅ Write a one-page summary of everything you learned in Phase 1
- ✅ Earn: [ISC2 CC Free Certificate](https://www.isc2.org/certifications/cc) — study and register (exam is free in 2024)

---

*Next: [Phase 2 — Web Security](./phase-2-web-security.md)*

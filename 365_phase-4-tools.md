# Phase 4 — Tools Deep Dive (Days 191–240)

> Tools don't find bugs — pentesters do. But knowing your tools deeply saves hours on every engagement.

---

## Burp Suite Pro (Days 191–205)

### Day 191 — Burp Suite Architecture
**What to learn:** Proxy, Target, Repeater, Intruder, Scanner, Decoder, Comparer — what each is for
- 🎥 [Burp Suite Full Course — PortSwigger Official](https://www.youtube.com/watch?v=Ov9bfgdcBkk)
- 🎥 [Burp Suite Masterclass — TCM Security](https://www.youtube.com/watch?v=G3hpAeoZ4ek)
- ✅ Task: Map out what you use each Burp tool for — make a personal cheatsheet

### Day 192 — Burp Repeater Mastery
- ✅ Task: Take 10 different API requests — modify each in Repeater — observe what changes in the response

### Day 193 — Burp Intruder
**What to learn:** Attack types (Sniper, Battering Ram, Pitchfork, Cluster Bomb), payload sets, grep match
- 🎥 [Burp Intruder — TechRaj](https://www.youtube.com/watch?v=3xheC9-QCPM)
- ✅ Task: Run Intruder username enumeration against DVWA brute force

### Day 194 — Burp Scanner (Active + Passive)
- ✅ Task: Crawl DVWA with Burp Scanner → understand every finding it reports → verify manually

### Day 195 — Burp Extensions
**Essential extensions to install:**
- Logger++ — advanced request logging
- Autorize — access control testing (IDOR)
- ParamMiner — discover hidden parameters
- Active Scan++ — enhanced scanning
- JWT Editor — JWT manipulation
- InQL — GraphQL testing
- Turbo Intruder — fast fuzzing
- 🎥 [Best Burp Extensions — NahamSec](https://www.youtube.com/watch?v=iyl8iurQJDU)

### Day 196 — Autorize — IDOR Testing at Scale
- 🎥 [Autorize Tutorial — NahamSec](https://www.youtube.com/watch?v=3K1-a7dnA60)
- ✅ Task: Setup Autorize with 2 different user sessions → browse crAPI → catch IDOR findings automatically

### Day 197 — ParamMiner — Hidden Parameter Discovery
- ✅ Task: Run ParamMiner against DVWA → find any hidden parameters → test each for vulnerabilities

### Day 198 — Turbo Intruder
- 🎥 [Turbo Intruder Tutorial — James Kettle (PortSwigger)](https://www.youtube.com/watch?v=qQECyR0OOhw)
- ✅ Task: Use Turbo Intruder to send 1000 requests in parallel — observe race condition behavior

### Days 199–205 — Burp Workflow Practice
- ✅ Complete [TryHackMe — Burp Suite Pro](https://tryhackme.com/room/burpsuitepro)
- ✅ Full pentest of DVWA using only Burp Suite — document every finding

---

## Nmap (Days 206–212)

### Day 206 — Nmap Fundamentals
- 🎥 [Nmap Full Course — NetworkChuck](https://www.youtube.com/watch?v=4t4kBkMsDbQ)
- 🎥 [Nmap Tutorial — HackerSploit](https://www.youtube.com/watch?v=5MTZdN9TEO4)
- ✅ Task: `nmap -sV -sC -O -T4 scanme.nmap.org` — understand every line of output

### Day 207 — Nmap Scan Types
**What to learn:** TCP SYN (-sS), TCP Connect (-sT), UDP (-sU), stealth scanning, timing templates
```bash
nmap -sS target       # Stealth SYN scan
nmap -sV target       # Service version detection
nmap -sC target       # Default scripts
nmap -O target        # OS detection
nmap -p- target       # All 65535 ports
nmap -A target        # Aggressive (all of above)
nmap -T4 target       # Faster timing
```

### Day 208 — Nmap Scripting Engine (NSE)
- 📖 [NSE Documentation](https://nmap.org/book/nse.html)
- ✅ Task: `nmap --script=http-headers target` and `nmap --script=vuln target` — read all output

### Day 209 — Web Recon with Nmap
```bash
nmap -p 80,443,8080,8443 --script=http-title,http-methods,http-headers target
```
- ✅ Task: Find all HTTP services on your local network with Nmap

### Days 210–212 — Nmap Practice
- ✅ [TryHackMe — Nmap Room](https://tryhackme.com/room/furthernmap)
- ✅ [TryHackMe — Nmap Advanced](https://tryhackme.com/room/nmap04)

---

## ffuf — Content Discovery and Fuzzing (Days 213–218)

### Day 213 — ffuf Basics
- 🎥 [ffuf Tutorial — NahamSec](https://www.youtube.com/watch?v=iLFkxAmwXF0)
- 📖 [ffuf GitHub](https://github.com/ffuf/ffuf)
- ✅ Install: `go install github.com/ffuf/ffuf/v2@latest`

### Day 214 — Directory and File Discovery
```bash
ffuf -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt \
     -u http://target.com/FUZZ \
     -fc 404 -t 50
```
- ✅ Wordlists: [SecLists](https://github.com/danielmiessler/SecLists) — download and bookmark

### Day 215 — Parameter Fuzzing
```bash
# Discover hidden GET parameters
ffuf -w params.txt -u http://target.com/page?FUZZ=test -fc 404

# POST body fuzzing
ffuf -w payloads.txt -u http://target.com/login \
     -X POST -d "username=admin&password=FUZZ" \
     -H "Content-Type: application/x-www-form-urlencoded"
```

### Day 216 — VHost Discovery
```bash
ffuf -w subdomains.txt -u http://target.com \
     -H "Host: FUZZ.target.com" -fc 404
```

### Day 217 — API Endpoint Fuzzing
```bash
ffuf -w /path/to/api-endpoints.txt \
     -u http://target.com/api/v1/FUZZ \
     -H "Authorization: Bearer TOKEN" -fc 404,403
```

### Day 218 — ffuf Practice
- ✅ Use ffuf on DVWA — find hidden directories and files
- ✅ [TryHackMe — Content Discovery Room](https://tryhackme.com/room/contentdiscovery)

---

## SQLmap (Days 219–224)

### Day 219 — SQLmap Fundamentals
- 🎥 [SQLmap Full Tutorial — HackerSploit](https://www.youtube.com/watch?v=nVj8MUKkzQk)
- ✅ Basic usage: `sqlmap -u "http://target.com/page?id=1" --dbs`

### Day 220 — SQLmap with Burp Requests
```bash
# Save a request from Burp as request.txt
sqlmap -r request.txt --dbs --level=3 --risk=2
```

### Day 221 — SQLmap Tamper Scripts
**What to learn:** WAF bypass using tamper scripts (space2comment, between, randomcase)
```bash
sqlmap -u "http://target.com/?id=1" --tamper=space2comment,between --dbs
```

### Day 222 — SQLmap for API Testing
```bash
sqlmap -u "http://target.com/api/users/1" \
       -H "Authorization: Bearer TOKEN" \
       -H "Content-Type: application/json" \
       --dbs
```

### Days 223–224 — SQLmap Practice
- ✅ Run SQLmap against DVWA (all difficulty levels)
- ✅ Task: Find a SQLmap tamper script that bypasses basic WAF on DVWA Medium

---

## Wireshark and Network Analysis (Days 225–230)

### Day 225 — Wireshark for Web Traffic
- 🎥 [Wireshark Full Course — David Bombal](https://www.youtube.com/watch?v=lb1Dw0elw0Q)
- ✅ Filter: `http.request` — capture and read HTTP traffic

### Day 226 — Analyzing HTTPS Traffic
**What to learn:** SSL stripping, certificate pinning, SSLKEYLOGFILE for HTTPS inspection
- ✅ Task: Set `SSLKEYLOGFILE` environment variable → capture HTTPS in Wireshark → read decrypted traffic

### Day 227 — Finding Credentials in Packet Captures
- ✅ Task: Download a sample PCAP from [Wireshark Wiki Samples](https://wiki.wireshark.org/SampleCaptures) → find credentials in cleartext

### Days 228–230 — Wireshark Practice
- ✅ [TryHackMe — Wireshark The Basics](https://tryhackme.com/room/wiresharkthebasics)
- ✅ [TryHackMe — Wireshark Traffic Analysis](https://tryhackme.com/room/wiresharktrafficanalysis)

---

## Other Essential Tools (Days 231–240)

### Day 231 — Nikto
```bash
nikto -h http://target.com -port 80,443 -ssl
```
- ✅ Task: Run Nikto against DVWA — understand what it finds vs what it misses

### Day 232 — Subfinder + Amass (Subdomain Enumeration)
```bash
subfinder -d target.com -o subdomains.txt
amass enum -d target.com
```
- 🎥 [Subdomain Enumeration — NahamSec](https://www.youtube.com/watch?v=U32z4aEHTg0)

### Day 233 — httpx — Probing Subdomains
```bash
cat subdomains.txt | httpx -status-code -title -tech-detect
```

### Day 234 — gau + waybackurls — Historical URLs
```bash
gau target.com | grep "\.js$"
waybackurls target.com | grep "api"
```

### Day 235 — Nuclei — Template-Based Scanning
- 📖 [Nuclei GitHub](https://github.com/projectdiscovery/nuclei)
- 🎥 [Nuclei Tutorial — STÖK](https://www.youtube.com/watch?v=amihlWTtkMA)
- ✅ Task: `nuclei -u http://target.com -t cves/ -severity critical,high`

### Days 236–240 — Full Toolchain Practice
- ✅ Build a recon script that chains: subfinder → httpx → gau → ffuf → nuclei
- ✅ Test entire toolchain against a HackTheBox machine or TryHackMe room
- 📜 Earn: [TCM Security — Practical Ethical Hacking](https://academy.tcm-sec.com/p/practical-ethical-hacking-the-complete-course) certificate (paid — ~$30, worth it)

---

*Next: [Phase 5 — DevSecOps](./phase-5-devsecops.md)*

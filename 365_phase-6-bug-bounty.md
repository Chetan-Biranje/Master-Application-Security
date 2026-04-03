# Phase 6 — Bug Bounty (Days 291–335)

> Bug bounty isn't just hacking — it's structured research, good communication, and knowing what to look for in 30 minutes before moving on.

---

## Bug Bounty Foundations (Days 291–300)

### Day 291 — How Bug Bounty Platforms Work
- 📖 [HackerOne Platform Overview](https://docs.hackerone.com/hackers.html)
- 📖 [Bugcrowd Getting Started](https://www.bugcrowd.com/hackers/faqs/)
- 📖 [Intigriti Hacker Guide](https://blog.intigriti.com/hackademy/how-to-get-started-with-bug-bounty/)
- ✅ Task: Create accounts on HackerOne, Bugcrowd, and Intigriti

### Day 292 — Reading Program Policies Correctly
**What to learn:** Scope (in-scope vs out-of-scope), asset types, exclusions, safe harbor language, response SLAs
- ✅ Task: Pick 3 programs — read their full policy — list 5 in-scope assets for each
- ⚠️ Rule: If it's not explicitly in scope, it's out of scope. Testing out-of-scope assets can get you banned or prosecuted.

### Day 293 — Choosing Your First Program
**Good first programs for beginners:**
- Programs with wide scope (wildcards like `*.target.com`)
- Programs with public bug reports (learn from others)
- Programs marked "beginner-friendly" on HackerOne
- 🎥 [How to Pick Bug Bounty Programs — InsiderPhD](https://www.youtube.com/watch?v=8t0-x7R59hA)
- 🎥 [Bug Bounty Program Selection — NahamSec](https://www.youtube.com/watch?v=o4QRl8y1ctQ)

### Day 294 — Understanding CVSS and Severity
- 📖 [CVSS v3.1 Calculator](https://www.first.org/cvss/calculator/3.1)
- 📖 [HackerOne Severity Ratings](https://docs.hackerone.com/hackers/severity-ratings.html)
- ✅ Task: Take 5 bug reports from HackerOne Disclosed — calculate CVSS score yourself — compare to what was assigned

### Day 295 — Recon Mindset
**What you're looking for:**
- Entry points (login, registration, file upload, search, API)
- User roles (what can admin do that user can't?)
- Data flows (where does user input go?)
- Trust boundaries (what talks to what?)
- 🎥 [Bug Bounty Recon Methodology — STÖK](https://www.youtube.com/watch?v=uKAKEj2YQac)

### Day 296 — Manual vs Automated Testing
**Rule:** Always start manual. Understand the app. Then automate the boring parts.
- 🎥 [Manual vs Automated Recon — NahamSec](https://www.youtube.com/watch?v=p-JiLCXZJ0c)

### Day 297 — Reading Bug Bounty Reports
- 📖 [HackerOne Hacktivity — Public Reports](https://hackerone.com/hacktivity)
- ✅ Task: Read 20 disclosed reports across different vuln types. For each note: the endpoint, the payload, the impact, how they found it.

### Day 298 — Report Writing That Gets Paid
**A good report has:**
1. Vulnerability title (vuln type + impact, e.g. "IDOR allows access to other users' orders")
2. Severity + CVSS score
3. Affected endpoint (URL, method, parameters)
4. Step-by-step reproduction steps (numbered)
5. Proof of concept (screenshots or video)
6. Impact (what can an attacker actually do?)
7. Remediation recommendation
- 🎥 [Writing Bug Bounty Reports — InsiderPhD](https://www.youtube.com/watch?v=GgkMOBgFER0)

### Day 299 — Report Writing Practice
- ✅ Pick one vulnerability you found in PortSwigger labs or crAPI
- ✅ Write a full professional report as if submitting to HackerOne
- ✅ Get it reviewed — post in bug bounty Discord communities

### Day 300 — Bug Bounty Communities
- [HackerOne Discord](https://discord.gg/hackerone)
- [NahamSec Discord](https://discord.gg/nahamsec)
- [Bug Bounty Hunter Forum](https://forum.bugbountyhunter.com/)
- [Reddit r/bugbounty](https://www.reddit.com/r/bugbounty/)
- [Bugcrowd Discord](https://discord.gg/bugcrowd)

---

## Recon Methodology (Days 301–315)

### Day 301 — Passive Recon
**What to learn:** OSINT without touching the target — Google dorking, Shodan, Censys, LinkedIn, job postings
```bash
# Google dorks
site:target.com filetype:pdf
site:target.com inurl:admin
site:target.com ext:env OR ext:config
"target.com" "api_key" site:github.com
```
- 🎥 [Passive Recon — TCM Security](https://www.youtube.com/watch?v=qDym7-_JTtY)

### Day 302 — Subdomain Enumeration
```bash
# Passive (no direct contact with target)
subfinder -d target.com -o subs.txt
amass enum -passive -d target.com -o subs-amass.txt
assetfinder --subs-only target.com >> subs.txt

# Check which are alive
cat subs.txt | sort -u | httpx -status-code -title -o alive.txt
```
- 🎥 [Subdomain Enumeration Masterclass — NahamSec](https://www.youtube.com/watch?v=U32z4aEHTg0)

### Day 303 — JavaScript File Analysis
**What to learn:** Finding API endpoints, secrets, hardcoded URLs in JS files
```bash
# Download and search JS files
gau target.com | grep "\.js$" | httpx -status-code | grep "200" | awk '{print $1}' | \
  xargs -I{} sh -c 'curl -s {} | grep -E "api_key|secret|password|token|endpoint"'
```
- 🎥 [JS Analysis for Bug Bounty — TomNomNom](https://www.youtube.com/watch?v=FTeE3OrTNoA)
- ✅ Tool: [LinkFinder](https://github.com/GerbenJavado/LinkFinder)

### Day 304 — API Endpoint Discovery
```bash
# From JS files
python3 linkfinder.py -i https://target.com -d -o cli

# From Wayback Machine
waybackurls target.com | grep "api" | sort -u

# From GAU
gau target.com | grep "/api/" | sort -u
```

### Day 305 — Port Scanning in Scope
```bash
# Only scan if explicitly in scope
nmap -iL alive.txt -p 80,443,8080,8443,8888,9000,3000 --open -oN portscan.txt
```

### Day 306 — Technology Fingerprinting
```bash
# What tech stack is the target running?
httpx -l alive.txt -tech-detect -status-code -title

# Wappalyzer browser extension — detect frameworks instantly
```

### Day 307 — Google Dorking
```bash
site:target.com ext:log
site:target.com ext:sql
site:target.com inurl:"/admin/"
site:target.com "index of" "backup"
site:target.com filetype:env
inurl:"/api/swagger" site:target.com
```

### Day 308 — Shodan and Censys
```bash
# Shodan (free account)
org:"Target Company" http.title:"Login"
ssl:"target.com" port:443

# Censys — find all target IPs/domains
```
- 📖 [Shodan Tutorial](https://www.shodan.io/explore)

### Day 309 — GitHub Recon
```bash
# Search GitHub for secrets
"target.com" "api_key" language:javascript
"target.com" password site:github.com
"target.com" "secret" extension:env
```
- ✅ Tool: [Gitrob](https://github.com/michenriksen/gitrob) or [TruffleHog](https://github.com/trufflesecurity/trufflehog)

### Day 310 — Nuclei for Recon
```bash
# Run nuclei templates on alive subdomains
nuclei -l alive.txt -t exposures/ -t misconfiguration/ -severity high,critical
```

### Days 311–315 — Full Recon Automation
- ✅ Write a bash script that does the full recon pipeline:
  1. subfinder → amass → deduplicate
  2. httpx → filter alive
  3. gau → find JS files → LinkFinder
  4. nuclei → scan for known misconfigs
  5. Output: `target_recon_YYYYMMDD.txt`
- 🎥 [Recon Automation — NahamSec Live](https://www.youtube.com/watch?v=pBACM1FnBBg)

---

## Testing Methodology (Days 316–327)

### Day 316 — Your First Bug Bounty Session (1 hour structure)
```
0:00–0:10  Read program scope + previous reports
0:10–0:25  Passive recon (subdomains, JS, Wayback)
0:25–0:45  Manual browsing — understand the app
0:45–1:00  Test highest-impact areas (auth, IDOR, API)
```

### Day 317 — IDOR Hunting Methodology
1. Find every place a user ID / object ID appears in a request
2. Create two test accounts
3. Switch session → test if Account A can access Account B's data
4. Try GUIDs, hashed IDs, sequential IDs, encoded values
- 🎥 [IDOR Hunting — NahamSec](https://www.youtube.com/watch?v=3K1-a7dnA60)

### Day 318 — Authentication Testing Checklist
- [ ] Username enumeration (different error messages)
- [ ] Password brute force (is there rate limiting?)
- [ ] Password reset (predictable token? host header injection?)
- [ ] Remember me token (long lived? predictable?)
- [ ] OAuth state parameter (CSRF possible?)
- [ ] JWT (alg:none? weak secret? expired token accepted?)

### Day 319 — API Testing Checklist
- [ ] All HTTP verbs (GET, POST, PUT, DELETE, PATCH, OPTIONS)
- [ ] All versions (v1, v2, v3 — do old versions have weaker controls?)
- [ ] Authentication bypass (no token, invalid token, expired token)
- [ ] Mass assignment (send extra fields in POST/PUT)
- [ ] BOLA (change object IDs)
- [ ] Excessive data exposure (response contains more than needed)
- [ ] Rate limiting (is there any?)

### Days 320–327 — Live Practice on Bug Bounty Programs
- ✅ Pick one program with a web app in scope
- ✅ Spend 1 hour per day on one specific vulnerability class per day
- ✅ Document all findings — even if N/A or informational
- ✅ Submit your first report (even if low severity)
- 🎥 [Bug Bounty Live Hacking — NahamSec](https://www.youtube.com/watch?v=y0-cIucCfts)

---

## From N/A to Valid (Days 328–335)

### Day 328 — Why Reports Get Closed as N/A
- Out of scope endpoint
- Self-XSS (no victim interaction needed? Not a bug)
- No security impact demonstrated
- Duplicate
- Known/accepted risk
- 🎥 [Why Your Reports Get Closed — InsiderPhD](https://www.youtube.com/watch?v=8K-FzPMW3G8)

### Day 329 — Impact Demonstration
**Rule:** Without a clear, realistic attack scenario — you don't have a bug, you have an observation.
- ✅ For every finding: write one sentence of who is attacked, how, and what data/action is compromised

### Days 330–335 — Review, Submit, Iterate
- ✅ Read 50 more disclosed reports across HackerOne
- ✅ Note the writing patterns of reports that got HIGH or CRITICAL ratings
- 📜 Earn: [HackerOne Hacker101 CTF Certificate](https://www.hacker101.com/ctf)
- ✅ Goal: Submit at least 3 reports by Day 335

---

*Next: [Phase 7 — Advanced](365_phase-7-advanced.md)*

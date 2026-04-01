# Phase 7 — Advanced + Career (Days 336–365)

> You've built the foundation. Now sharpen the edge.

---

## Threat Modeling (Days 336–343)

### Day 336 — What is Threat Modeling
**What to learn:** Why threat modeling exists, STRIDE vs PASTA vs LINDDUN, when to apply it
- 📖 [OWASP Threat Modeling](https://owasp.org/www-community/Threat_Modeling)
- 🎥 [Threat Modeling Explained — Adam Shostack](https://www.youtube.com/watch?v=GqmQg-cszw4)

### Day 337 — STRIDE Framework
| Threat | Example | Control |
|---|---|---|
| **S**poofing | Logging in as another user | Strong authentication |
| **T**ampering | Modifying data in transit | HTTPS + integrity checks |
| **R**epudiation | Denying an action | Audit logging |
| **I**nformation Disclosure | Data leaks via error messages | Error handling |
| **D**enial of Service | Flooding a login endpoint | Rate limiting |
| **E**levation of Privilege | Regular user accessing admin | RBAC + least privilege |

- 🎥 [STRIDE Threat Modeling — TechWorld with Nana](https://www.youtube.com/watch?v=GqmQg-cszw4)
- ✅ Task: Take your `secure-rbac-api` project — draw a data flow diagram — apply STRIDE to every component

### Day 338 — Data Flow Diagrams (DFD)
- ✅ Tool: [OWASP Threat Dragon](https://threatdragon.github.io/) — free, online DFD tool
- ✅ Task: Model the login flow of any app using Threat Dragon — identify 3 threats

### Days 339–343 — Threat Model a Real System
- ✅ Pick one of your projects (secure-rbac-api or api-security-toolkit)
- ✅ Create a full threat model document:
  1. System description
  2. Data flow diagram
  3. STRIDE analysis per component
  4. Risk rating for each threat
  5. Mitigations

---

## Secure Code Review (Days 344–352)

### Day 344 — Secure Code Review Methodology
**The approach:**
1. Get the codebase — understand the tech stack
2. Map the attack surface (entry points, auth, data handling)
3. Search for dangerous functions (`eval`, `exec`, `query`, `innerHTML`)
4. Follow data flow from input to output
5. Check business logic

- 🎥 [Secure Code Review — Rana Khalil](https://www.youtube.com/watch?v=rAwxFw25x3E)
- 📖 [OWASP Code Review Guide](https://owasp.org/www-project-code-review-guide/)

### Day 345 — What to Look for in Python
```python
# DANGEROUS — command injection
os.system(user_input)
subprocess.call(user_input, shell=True)
eval(user_input)

# DANGEROUS — SQLi
cursor.execute("SELECT * FROM users WHERE id = " + user_id)

# DANGEROUS — hardcoded secrets
API_KEY = "sk-abc123"

# SAFE — parameterized
cursor.execute("SELECT * FROM users WHERE id = ?", (user_id,))
```

### Day 346 — What to Look for in JavaScript/Node.js
```javascript
// DANGEROUS — XSS
element.innerHTML = userInput;
document.write(userInput);

// DANGEROUS — command injection
exec(userInput)
eval(userInput)

// DANGEROUS — SQLi (raw query)
db.query(`SELECT * FROM users WHERE id = ${userId}`)

// SAFE
db.query('SELECT * FROM users WHERE id = ?', [userId])
```

### Day 347 — DVNA Code Review
- ✅ [DVNA Source Code](https://github.com/appsecco/dvna) — clone it
- ✅ Find all vulnerability instances manually by reading code — no running the app
- ✅ Compare your findings to the DVNA documentation

### Days 348–352 — Code Review Practice
- ✅ [PentesterLab Code Review](https://pentesterlab.com/exercises) — free exercises
- 🎥 [Finding Bugs in Open Source — LiveOverflow](https://www.youtube.com/watch?v=v85_cH-0Ck0)
- ✅ Task: Review any small open source project on GitHub — submit a responsible disclosure if you find something

---

## OWASP ASVS — Security Verification Standard (Days 353–357)

### Day 353 — What is OWASP ASVS
**What to learn:** ASVS is a checklist for verifying a web app's security — Level 1, 2, 3 requirements
- 📖 [OWASP ASVS 4.0](https://owasp.org/www-project-application-security-verification-standard/)
- 🎥 [ASVS Explained — OWASP](https://www.youtube.com/watch?v=HFmGKy2Mbos)

### Day 354 — Applying ASVS to Your Projects
- ✅ Download the ASVS Excel/CSV checklist from the OWASP site
- ✅ Run Level 1 checks against your `secure-rbac-api` project
- ✅ Document which requirements pass and which fail

### Days 355–357 — Writing an ASVS Report
- ✅ Produce a short ASVS Level 1 verification report for one of your projects
- ✅ Include: requirement ID, pass/fail, evidence, remediation for failures

---

## Career and Portfolio (Days 358–365)

### Day 358 — Building Your Security Portfolio
**What to include:**
- GitHub with real, working projects (not tutorials, your own builds)
- Bug bounty profile (even informational reports show activity)
- A technical blog or writeups (even one good writeup beats ten empty repos)
- CTF profile on HackTheBox or TryHackMe

### Day 359 — Writing Security Writeups
**Writeup structure:**
1. Challenge/vulnerability name
2. What you found and where
3. How you tested it (tools, steps)
4. What the impact was
5. How to fix it
- ✅ Write one writeup for a PortSwigger Expert lab you completed
- 📝 Publish on [Medium](https://medium.com), [HashNode](https://hashnode.com), or your GitHub Pages

### Day 360 — LinkedIn and GitHub Optimization
- ✅ LinkedIn: Add all roles, 15+ valid findings, ASVS/STRIDE, SAST/DAST experience
- ✅ GitHub: Pin 4 repos, all have complete READMEs, no empty repos
- ✅ GitHub profile README: Stats, tools, current learning
- 🎥 [GitHub Profile README — Catalin Pit](https://www.youtube.com/watch?v=ECuqb5Tv9qI)

### Day 361 — Certifications to Target Next
| Cert | Cost | Difficulty | Worth It? |
|---|---|---|---|
| eWPT (eLearnSecurity) | ~$200 | Medium | ✅ Yes — practical web pentesting |
| BSCP (PortSwigger) | ~$99 | Hard | ✅ Yes — respected, hard to fake |
| OSCP (Offensive Security) | ~$1499 | Hard | ✅ Yes — gold standard |
| CEH | ~$500 | Easy | ❌ Theory-heavy, not respected by industry |
| CompTIA Security+ | ~$400 | Easy | ✅ OK for corporate/compliance roles |
| TCM PNPT | ~$400 | Medium | ✅ Yes — practical, affordable |

### Day 362 — Interview Preparation
**Common AppSec interview questions:**
- Explain IDOR and how you would prevent it
- How does CSRF work — what are the defenses?
- What is the difference between authentication and authorization?
- How would you find XSS in a codebase?
- Walk me through how you would pentest a REST API
- What is STRIDE? Apply it to a login page.
- What is the difference between SAST and DAST?

### Day 363 — HackerOne Profile Polish
- ✅ Complete your HackerOne profile (bio, skills, reputation)
- ✅ Submit at least 5 total reports by now
- ✅ Your `h1` profile should reflect your GitHub work

### Day 364 — Your Security Mindset
**What separates good security engineers from average ones:**
- They ask "what can go wrong?" before writing code
- They read CVEs, not just checklists
- They understand how things work before trying to break them
- They write clear, impact-focused reports
- They fix things, not just find them

### Day 365 — You Are Not Done
Security is a continuous field. Day 365 is not graduation — it's the beginning of consistent practice.

**What to do after Day 365:**
- Continue bug bounty — aim for 1 submission per week
- Read one security research blog per week (PortSwigger Research, Google Project Zero)
- Study for BSCP or eWPT
- Contribute to OWASP projects
- Write writeups for every significant finding

---

## 🏆 Final Certificates to Earn

| Certificate | Platform | Cost | Link |
|---|---|---|---|
| Hacker101 CTF Certificate | HackerOne / Hacker101 | Free | [Link](https://www.hacker101.com/ctf) |
| PortSwigger All Labs Badge | PortSwigger Academy | Free | [Link](https://portswigger.net/web-security/all-labs) |
| TryHackMe Jr Penetration Tester | TryHackMe | Free | [Link](https://tryhackme.com/path/outline/jrpentester) |
| TryHackMe SOC Level 1 | TryHackMe | Free | [Link](https://tryhackme.com/path/outline/soclevel1) |
| ISC2 Certified in Cybersecurity | ISC2 | Free | [Link](https://www.isc2.org/certifications/cc) |
| Google Cybersecurity Certificate | Coursera (audit) | Free | [Link](https://www.coursera.org/professional-certificates/google-cybersecurity) |
| BSCP | PortSwigger | ~$99 | [Link](https://portswigger.net/web-security/certification) |

---

*Built by [Chetan Biranje](https://github.com/mr-Shadex) · Application Security Engineer · Pune, India*

# Phase 2 — Web Security (Days 61–130)

> Learn how web vulnerabilities actually work — from theory to hands-on exploitation and remediation.

---

## XSS — Cross-Site Scripting (Days 61–75)

### Day 61 — XSS Theory
**What to learn:** What XSS is, why browsers execute attacker-controlled scripts, impact (cookie theft, keylogging, phishing)
- 📖 [PortSwigger XSS Theory](https://portswigger.net/web-security/cross-site-scripting)
- 🎥 [XSS Explained — PwnFunction](https://www.youtube.com/watch?v=EoaDgUgS6QA)
- 🎥 [XSS Full Course — Rana Khalil](https://www.youtube.com/playlist?list=PLuyTk2_mYISId4_l9YET7Gv29cHcNguq-)

### Day 62 — Reflected XSS
- 📖 [PortSwigger Reflected XSS](https://portswigger.net/web-security/cross-site-scripting/reflected)
- ✅ Lab: [Reflected XSS into HTML context](https://portswigger.net/web-security/cross-site-scripting/reflected/lab-html-context-nothing-encoded)

### Day 63 — Stored XSS
- 📖 [PortSwigger Stored XSS](https://portswigger.net/web-security/cross-site-scripting/stored)
- ✅ Lab: [Stored XSS into HTML context](https://portswigger.net/web-security/cross-site-scripting/stored/lab-html-context-nothing-encoded)

### Day 64 — DOM-Based XSS
- 📖 [PortSwigger DOM XSS](https://portswigger.net/web-security/cross-site-scripting/dom-based)
- 🎥 [DOM XSS Deep Dive — LiveOverflow](https://www.youtube.com/watch?v=FHIoUhHpMts)
- ✅ Lab: [DOM XSS via document.write](https://portswigger.net/web-security/cross-site-scripting/dom-based/lab-document-write-sink)

### Day 65 — XSS Contexts
**What to learn:** HTML context, attribute context, JS context, URL context — payloads differ per context
- 📖 [PortSwigger XSS Contexts](https://portswigger.net/web-security/cross-site-scripting/contexts)
- ✅ Labs: Complete 3 XSS context labs on PortSwigger

### Day 66 — XSS Filter Bypass
- 📖 [PortSwigger XSS Cheat Sheet](https://portswigger.net/web-security/cross-site-scripting/cheat-sheet)
- 🎥 [XSS Filter Bypass — The XSS Rat](https://www.youtube.com/watch?v=bB1Pqbp77_M)
- ✅ Task: Try 5 different payloads from the cheat sheet in DVWA (Medium security)

### Day 67 — CSP — Content Security Policy
**What to learn:** What CSP is, how it prevents XSS, common CSP misconfigs that allow bypass
- 📖 [PortSwigger CSP](https://portswigger.net/web-security/cross-site-scripting/content-security-policy)
- ✅ Tool: [CSP Evaluator by Google](https://csp-evaluator.withgoogle.com/)

### Days 68–72 — XSS Labs Sprint
- ✅ Complete all [PortSwigger XSS Labs](https://portswigger.net/web-security/all-labs#cross-site-scripting) — Apprentice level minimum
- ✅ DVWA XSS Reflected + Stored (Low, Medium, High)

### Days 73–75 — XSS in Bug Bounty Context
- 🎥 [Finding XSS in Real Apps — NahamSec](https://www.youtube.com/watch?v=IWbmP0Z-yQg)
- 🎥 [XSS Bug Bounty Tips — The XSS Rat](https://www.youtube.com/watch?v=5O80ITYluGo)
- ✅ Task: Read 3 real XSS bug bounty reports on [HackerOne Disclosed](https://hackerone.com/hacktivity)

---

## SQL Injection (Days 76–92)

### Day 76 — SQLi Theory
- 📖 [PortSwigger SQLi](https://portswigger.net/web-security/sql-injection)
- 🎥 [SQL Injection Full Course — Rana Khalil](https://www.youtube.com/playlist?list=PLuyTk2_mYISKed0gkiP-CaSKY7AXEh6O7)
- 🎥 [SQLi Explained — PwnFunction](https://www.youtube.com/watch?v=ciNHn38EyRc)

### Day 77 — In-Band SQLi (Error-Based)
- 📖 [PortSwigger Error-Based SQLi](https://portswigger.net/web-security/sql-injection/examining-the-database)
- ✅ Lab: [SQL injection UNION attack — find columns](https://portswigger.net/web-security/sql-injection/union-attacks/lab-determine-number-of-columns)

### Day 78 — UNION-Based SQLi
- ✅ Lab: [UNION attack — retrieve data from other tables](https://portswigger.net/web-security/sql-injection/union-attacks/lab-retrieve-data-from-other-tables)
- ✅ Lab: [UNION attack — retrieve multiple values in single column](https://portswigger.net/web-security/sql-injection/union-attacks/lab-retrieve-multiple-values-in-single-column)

### Day 79 — Blind SQLi — Boolean Based
- 📖 [PortSwigger Blind SQLi](https://portswigger.net/web-security/sql-injection/blind)
- ✅ Lab: [Blind SQLi with conditional responses](https://portswigger.net/web-security/sql-injection/blind/lab-conditional-responses)

### Day 80 — Blind SQLi — Time Based
- ✅ Lab: [Blind SQLi with time delays](https://portswigger.net/web-security/sql-injection/blind/lab-time-delays)
- ✅ Task: Try `'; WAITFOR DELAY '0:0:5'--` in DVWA and observe the delay

### Day 81 — SQLmap
- 🎥 [SQLmap Tutorial — HackerSploit](https://www.youtube.com/watch?v=nVj8MUKkzQk)
- ✅ Task: Run SQLmap against DVWA: `sqlmap -u "http://localhost/dvwa/vulnerabilities/sqli/?id=1&Submit=Submit" --cookie="PHPSESSID=xxx;security=low" --dbs`

### Days 82–87 — SQLi Labs Sprint
- ✅ Complete all [PortSwigger SQLi Labs](https://portswigger.net/web-security/all-labs#sql-injection) — Apprentice + Practitioner
- ✅ DVWA SQLi (Low, Medium, High)

### Days 88–92 — SQLi in Real World
- 🎥 [Finding SQLi in Bug Bounty — NahamSec](https://www.youtube.com/watch?v=ZAdsCWqJ1wQ)
- ✅ Task: Read 5 real SQLi bug reports on HackerOne Disclosed
- ✅ Task: Write a one-page SQLi remediation guide (parameterized queries, ORM usage, WAF)

---

## Authentication Attacks (Days 93–105)

### Day 93 — Authentication Vulnerabilities Theory
- 📖 [PortSwigger Authentication](https://portswigger.net/web-security/authentication)
- 🎥 [Authentication Attacks — Rana Khalil](https://www.youtube.com/playlist?list=PLuyTk2_mYISLEcFxHbmOsIPzO6Kk7JU5l)

### Day 94 — Username Enumeration
- ✅ Lab: [Username enumeration via different responses](https://portswigger.net/web-security/authentication/password-based/lab-username-enumeration-via-different-responses)

### Day 95 — Brute Force Attacks
- ✅ Lab: [Broken brute-force protection — IP block](https://portswigger.net/web-security/authentication/password-based/lab-broken-bruteforce-protection-ip-block)
- ✅ Task: DVWA Brute Force (Medium security) — bypass lockout

### Day 96 — Password Reset Flaws
- 📖 [OWASP Forgot Password Guide](https://cheatsheetseries.owasp.org/cheatsheets/Forgot_Password_Cheat_Sheet.html)
- ✅ Lab: [Password reset poisoning via middleware](https://portswigger.net/web-security/authentication/other-mechanisms/lab-password-reset-poisoning-via-middleware)

### Day 97 — Multi-Factor Authentication Bypass
- 🎥 [MFA Bypass Techniques — STÖK](https://www.youtube.com/watch?v=b0l_pAuMHBs)
- ✅ Lab: [2FA simple bypass](https://portswigger.net/web-security/authentication/multi-factor/lab-2fa-simple-bypass)

### Days 98–105 — Auth Labs Sprint
- ✅ Complete all [PortSwigger Authentication Labs](https://portswigger.net/web-security/all-labs#authentication)
- ✅ Read 5 auth-related bug reports on HackerOne

---

## CSRF (Days 106–112)

### Day 106 — CSRF Theory
- 📖 [PortSwigger CSRF](https://portswigger.net/web-security/csrf)
- 🎥 [CSRF Explained — PwnFunction](https://www.youtube.com/watch?v=eWEgUcHPle0)

### Day 107 — CSRF Bypasses
- 📖 [Bypassing CSRF Defenses](https://portswigger.net/web-security/csrf/bypassing-token-validation)
- ✅ Lab: [CSRF where token not tied to user session](https://portswigger.net/web-security/csrf/bypassing-token-validation/lab-token-not-tied-to-user-session)

### Days 108–112 — CSRF Labs
- ✅ Complete all [PortSwigger CSRF Labs](https://portswigger.net/web-security/all-labs#csrf)

---

## IDOR and Access Control (Days 113–122)

### Day 113 — IDOR Theory
- 📖 [PortSwigger IDOR](https://portswigger.net/web-security/access-control/idor)
- 🎥 [IDOR Explained — NahamSec](https://www.youtube.com/watch?v=3K1-a7dnA60)
- 🎥 [IDOR Bug Bounty Guide — InsiderPhD](https://www.youtube.com/watch?v=EkqIoVOKa7I)

### Days 114–118 — IDOR Labs
- ✅ Complete all [PortSwigger Access Control Labs](https://portswigger.net/web-security/all-labs#access-control)
- ✅ Read 10 IDOR reports on HackerOne Disclosed — understand why each was valid

### Days 119–122 — Privilege Escalation
- 📖 [PortSwigger Privilege Escalation](https://portswigger.net/web-security/access-control)
- ✅ Lab: [User role controlled by request parameter](https://portswigger.net/web-security/access-control/lab-user-role-controlled-by-request-parameter)

---

## SSRF, XXE, File Upload (Days 123–130)

### Days 123–125 — SSRF
- 📖 [PortSwigger SSRF](https://portswigger.net/web-security/ssrf)
- 🎥 [SSRF Explained — PwnFunction](https://www.youtube.com/watch?v=ih5R_c16bKc)
- ✅ Labs: Complete [PortSwigger SSRF Labs](https://portswigger.net/web-security/all-labs#server-side-request-forgery-ssrf)

### Days 126–128 — XXE
- 📖 [PortSwigger XXE](https://portswigger.net/web-security/xxe)
- ✅ Labs: [PortSwigger XXE Labs](https://portswigger.net/web-security/all-labs#xml-external-entity-xxe-injection)

### Days 129–130 — File Upload Vulnerabilities
- 📖 [PortSwigger File Upload](https://portswigger.net/web-security/file-upload)
- ✅ Labs: [PortSwigger File Upload Labs](https://portswigger.net/web-security/all-labs#file-upload-vulnerabilities)

---

## 🏆 Phase 2 Checkpoint

- ✅ All PortSwigger Apprentice labs completed
- ✅ At least 10 Practitioner labs completed
- ✅ Read 25+ real bug bounty reports on HackerOne
- 📜 Earn: [TryHackMe — Jr Penetration Tester Certificate](https://tryhackme.com/path/outline/jrpentester)

---

*Next: [Phase 3 — API Security](365_phase-3-api-security.md)*

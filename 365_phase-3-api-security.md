# Phase 3 — API Security (Days 131–190)

> APIs are where modern bugs live. Learn to test them the way attackers do.

---

## REST API Fundamentals (Days 131–140)

### Day 131 — REST API Basics for Security
**What to learn:** Resources, endpoints, HTTP verbs in APIs, status codes, JSON structure, headers
- 📖 [REST API Security — OWASP](https://owasp.org/www-project-api-security/)
- 🎥 [REST API Concepts — Traversy Media](https://www.youtube.com/watch?v=Q-BpqyOT3a8)
- ✅ Task: Use [reqres.in](https://reqres.in) — test every endpoint with curl and Postman

### Day 132 — API Authentication Types
**What to learn:** API keys, Basic auth, Bearer tokens, OAuth — how each is attacked
- 📖 [API Authentication Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/REST_Security_Cheat_Sheet.html)
- ✅ Task: Find a public API — identify what auth it uses — test what happens with a wrong/missing token

### Day 133 — Reading API Documentation as an Attacker
**What to learn:** What to look for in Swagger/OpenAPI docs — undocumented params, admin endpoints, version differences
- 🎥 [Attacking APIs from Documentation — NahamSec](https://www.youtube.com/watch?v=yCUQBc2rY9Y)
- ✅ Task: Open any public Swagger UI — list all endpoints — identify which ones touch user data

### Day 134 — API Recon Techniques
**What to learn:** Finding API endpoints via JS files, Wayback Machine, Google Dorking, Burp crawling
- 🎥 [API Recon — TCM Security](https://www.youtube.com/watch?v=Ov9bfgdcBkk)
- ✅ Task: Visit any web app — open DevTools Network tab — filter for `/api/` — list all API calls made

### Days 135–140 — crAPI Practice Lab
- ✅ Install crAPI (deliberately vulnerable API): `docker-compose -f docker-compose.yml --compatibility up -d`
- 📖 [crAPI GitHub](https://github.com/OWASP/crAPI)
- ✅ Complete all crAPI challenges — find BOLA, broken auth, excessive data exposure

---

## OWASP API Security Top 10 (Days 141–160)

### Day 141 — API1: Broken Object Level Authorization (BOLA/IDOR)
- 📖 [OWASP API1 BOLA](https://owasp.org/API-Security/editions/2023/en/0xa1-broken-object-level-authorization/)
- 🎥 [BOLA/IDOR in APIs — NahamSec](https://www.youtube.com/watch?v=3K1-a7dnA60)
- ✅ Lab: PortSwigger — [Exploiting an API endpoint using documentation](https://portswigger.net/web-security/api-testing/lab-exploiting-api-endpoint-using-documentation)

### Day 142 — API2: Broken Authentication
- 📖 [OWASP API2](https://owasp.org/API-Security/editions/2023/en/0xa2-broken-authentication/)
- ✅ Task: Test crAPI login endpoint — try brute force, password spraying, token reuse

### Day 143 — API3: Broken Object Property Level Authorization
- 📖 [OWASP API3](https://owasp.org/API-Security/editions/2023/en/0xa3-broken-object-property-level-authorization/)
- ✅ Task: In crAPI — try sending extra properties in a PUT request (mass assignment)

### Day 144 — API4: Unrestricted Resource Consumption
- 📖 [OWASP API4](https://owasp.org/API-Security/editions/2023/en/0xa4-unrestricted-resource-consumption/)
- ✅ Task: Find an API endpoint with no rate limiting — how would you test it responsibly?

### Day 145 — API5: Broken Function Level Authorization
- 📖 [OWASP API5](https://owasp.org/API-Security/editions/2023/en/0xa5-broken-function-level-authorization/)
- ✅ Task: In crAPI — access admin endpoints as a regular user

### Day 146 — API6: Unrestricted Access to Sensitive Business Flows
- 📖 [OWASP API6](https://owasp.org/API-Security/editions/2023/en/0xa6-unrestricted-access-to-sensitive-business-flows/)

### Day 147 — API7: Server Side Request Forgery
- 📖 [OWASP API7 SSRF](https://owasp.org/API-Security/editions/2023/en/0xa7-server-side-request-forgery/)
- ✅ Lab: PortSwigger SSRF via API

### Day 148 — API8: Security Misconfiguration
- 📖 [OWASP API8](https://owasp.org/API-Security/editions/2023/en/0xa8-security-misconfiguration/)
- ✅ Task: Test any API for: CORS *, debug endpoints enabled, verbose errors, HTTP instead of HTTPS

### Day 149 — API9: Improper Inventory Management
- 📖 [OWASP API9](https://owasp.org/API-Security/editions/2023/en/0xa9-improper-inventory-management/)
- ✅ Task: Google dork for exposed API docs: `inurl:/api/swagger-ui.html site:target.com`

### Day 150 — API10: Unsafe Consumption of APIs
- 📖 [OWASP API10](https://owasp.org/API-Security/editions/2023/en/0xa10-unsafe-consumption-of-apis/)
- ✅ Task: Complete crAPI all challenges — document each finding with endpoint, impact, and fix

---

## JWT Security (Days 161–172)

### Day 161 — JWT Basics
**What to learn:** Header.Payload.Signature structure, how signing works, where JWTs are used
- 🎥 [JWT Explained — Fireship](https://www.youtube.com/watch?v=7Q17ubqLfaM)
- ✅ Task: Decode a JWT at [jwt.io](https://jwt.io) — identify all claims

### Day 162 — JWT Algorithm Confusion (alg:none)
- 📖 [PortSwigger JWT Attacks](https://portswigger.net/web-security/jwt)
- 🎥 [JWT Attacks — Rana Khalil](https://www.youtube.com/watch?v=kqkbGJhVfFY)
- ✅ Lab: [JWT authentication bypass via unverified signature](https://portswigger.net/web-security/jwt/lab-jwt-authentication-bypass-via-unverified-signature)

### Day 163 — Weak JWT Secrets
- ✅ Lab: [JWT authentication bypass via weak signing key](https://portswigger.net/web-security/jwt/lab-jwt-authentication-bypass-via-weak-signing-key)
- ✅ Tool: [jwt_tool](https://github.com/ticarpi/jwt_tool) — install and test against crAPI

### Day 164 — JWT Algorithm Substitution (RS256 → HS256)
- ✅ Lab: [JWT authentication bypass via algorithm confusion](https://portswigger.net/web-security/jwt/algorithm-confusion/lab-jwt-authentication-bypass-via-algorithm-confusion)

### Day 165 — JWT kid Header Injection
- ✅ Lab: [JWT authentication bypass via kid header path traversal](https://portswigger.net/web-security/jwt/lab-jwt-authentication-bypass-via-kid-header-path-traversal)

### Days 166–168 — JWT Labs Sprint
- ✅ Complete all [PortSwigger JWT Labs](https://portswigger.net/web-security/all-labs#jwt)

### Days 169–172 — JWT in Real Bug Bounty
- 🎥 [JWT Vulnerabilities in Real Apps — STÖK](https://www.youtube.com/watch?v=b0l_pAuMHBs)
- ✅ Task: Read 5 JWT bug reports on HackerOne Disclosed
- ✅ Task: Write a JWT security checklist — what to test every time you see a JWT

---

## OAuth 2.0 Security (Days 173–180)

### Day 173 — OAuth 2.0 Flows
**What to learn:** Authorization code flow, implicit flow, client credentials — what each is for
- 📖 [PortSwigger OAuth](https://portswigger.net/web-security/oauth)
- 🎥 [OAuth 2.0 Explained — Fireship](https://www.youtube.com/watch?v=t18YB3xDfXI)

### Day 174 — OAuth Misconfigurations
- ✅ Lab: [Authentication bypass via OAuth implicit flow](https://portswigger.net/web-security/oauth/lab-oauth-authentication-bypass-via-oauth-implicit-flow)

### Day 175 — CSRF in OAuth
- ✅ Lab: [Forced OAuth profile linking](https://portswigger.net/web-security/oauth/lab-oauth-forced-oauth-profile-linking)

### Days 176–180 — OAuth Labs Sprint
- ✅ Complete all [PortSwigger OAuth Labs](https://portswigger.net/web-security/all-labs#oauth-authentication)
- ✅ Read 5 OAuth bug reports on HackerOne
- 📜 Earn: [PortSwigger Web Security Academy Completion Badge](https://portswigger.net/web-security) for API Security section

---

## GraphQL Security (Days 181–190)

### Day 181 — GraphQL Basics for Pentesters
- 📖 [HackTricks GraphQL](https://book.hacktricks.xyz/network-services-pentesting/pentesting-web/graphql)
- 🎥 [GraphQL Pentesting — TCM Security](https://www.youtube.com/watch?v=NPDp7GHmMa4)

### Days 182–185 — GraphQL Attacks
**What to learn:** Introspection abuse, batching attacks, IDOR in GraphQL, injection via queries
- ✅ Lab: [PortSwigger GraphQL Labs](https://portswigger.net/web-security/all-labs#graphql-api-vulnerabilities)
- ✅ Tool: [InQL Burp Extension](https://github.com/doyensec/inql) — install and test

### Days 186–190 — API Security Review
- ✅ Full crAPI walkthrough — document all findings in pentest report format
- 🎥 [Full API Pentesting Course — TCM Security](https://www.youtube.com/watch?v=Ov9bfgdcBkk)
- ✅ Task: Create your personal API testing checklist — save it to your GitHub

---

*Next: [Phase 4 — Tools Deep Dive](365_phase-4-tools.md)*

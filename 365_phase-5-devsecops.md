# Phase 5 — DevSecOps (Days 241–290)

> Security that doesn't ship with the code is security that doesn't exist. Learn to bake it in.

---

## CI/CD Security Fundamentals (Days 241–252)

### Day 241 — What is DevSecOps
- 🎥 [DevSecOps Explained — TechWorld with Nana](https://www.youtube.com/watch?v=nrhxNNH5lt0)
- 📖 [OWASP DevSecOps Guide](https://owasp.org/www-project-devsecops-guideline/)
- ✅ Task: Draw the security touchpoints in a CI/CD pipeline (design → code → build → test → deploy)

### Day 242 — Git and GitHub Security
**What to learn:** Branch protection rules, signed commits, secret scanning, `.gitignore` importance
- 🎥 [Git Security Best Practices — GitHub](https://www.youtube.com/watch?v=93uQSyYJfXo)
- ✅ Task: Check if any of your repos have accidentally committed secrets using [git-secrets](https://github.com/awslabs/git-secrets)

### Day 243 — GitHub Actions Basics
- 🎥 [GitHub Actions Full Course — TechWorld with Nana](https://www.youtube.com/watch?v=R8_veQiYBjI)
- ✅ Task: Create a simple `.github/workflows/main.yml` that runs `echo "Hello"` on push

### Day 244 — Securing GitHub Actions
**What to learn:** Least-privilege permissions, pinning action versions, avoiding `pull_request_target` misuse
- 📖 [GitHub Actions Security Best Practices](https://docs.github.com/en/actions/security-guides/security-hardening-for-github-actions)
- ✅ Task: Review one of your workflow files — add `permissions: contents: read` to restrict scope
```yaml
permissions:
  contents: read      # minimum needed
  security-events: write  # only if uploading SARIF
```

### Day 245 — GitHub Secrets Management
**What to learn:** How GitHub Secrets work, environment secrets vs repo secrets, never hardcoding credentials
- 📖 [GitHub Encrypted Secrets](https://docs.github.com/en/actions/security-guides/encrypted-secrets)
- ✅ Task: Add `MY_API_KEY` and `DATABASE_URL` as secrets in your repo → use them in a workflow

### Day 246 — CI/CD Secret Scanning
**What to learn:** detect-secrets, git-secrets, Gitleaks — catching secrets before they hit remote
- 📖 [detect-secrets GitHub](https://github.com/Yelp/detect-secrets)
- ✅ Install and run:
```bash
pip install detect-secrets
detect-secrets scan > .secrets.baseline
detect-secrets audit .secrets.baseline
```
- ✅ Add to GitHub Actions:
```yaml
- name: Detect Secrets
  run: |
    pip install detect-secrets
    detect-secrets scan --baseline .secrets.baseline
```

### Day 247 — Gitleaks
```bash
# Install
brew install gitleaks  # or download binary

# Scan entire repo history
gitleaks detect --source . --report-format json

# Scan staged files before commit
gitleaks protect --staged
```
- 🎥 [Gitleaks Tutorial — Jake Gillberg](https://www.youtube.com/watch?v=2GqMz8Kntf4)

### Day 248 — Dependency Scanning — pip-audit
```bash
pip install pip-audit
pip-audit -r requirements.txt

# In GitHub Actions:
- name: Audit Python Dependencies
  run: |
    pip install pip-audit
    pip-audit -r requirements.txt --fail-on-vuln
```

### Day 249 — Dependency Scanning — npm audit
```bash
npm audit
npm audit --audit-level=high  # fail only on high+
```
- ✅ Task: Run `npm audit` on any Node project — fix or document every HIGH/CRITICAL finding

### Day 250 — OWASP Dependency-Check
- 📖 [OWASP Dependency-Check](https://owasp.org/www-project-dependency-check/)
- ✅ Task: Run OWASP Dependency-Check against your secure-pipeline project

### Days 251–252 — Build a Dependency Scan Pipeline
```yaml
name: Dependency Security Scan
on: [push, pull_request]
permissions:
  contents: read
jobs:
  audit:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Python Dependency Audit
        run: |
          pip install pip-audit
          pip-audit -r requirements.txt
      - name: Secret Detection
        run: |
          pip install detect-secrets
          detect-secrets scan --baseline .secrets.baseline
```
- ✅ Push this to your `secure-pipeline` repo

---

## SAST — Static Analysis (Days 253–264)

### Day 253 — What is SAST
**What to learn:** SAST vs DAST, what SAST can and cannot find, false positives, how to triage
- 📖 [OWASP SAST Guide](https://owasp.org/www-community/Source_Code_Analysis_Tools)
- 🎥 [SAST Explained — Snyk](https://www.youtube.com/watch?v=dRrqfNjlxiM)

### Day 254 — Bandit (Python SAST)
```bash
pip install bandit
bandit -r ./src -ll -f txt           # fail on HIGH only
bandit -r ./src -f json -o report.json
```
- 📖 [Bandit Docs](https://bandit.readthedocs.io/)
- ✅ Task: Run Bandit against a Python project — read every finding — which are false positives?

### Day 255 — Semgrep (Multi-language SAST)
```bash
pip install semgrep
semgrep --config=p/owasp-top-ten .
semgrep --config=p/python .
semgrep --config=p/javascript .
```
- 📖 [Semgrep Docs](https://semgrep.dev/docs/)
- 🎥 [Semgrep Tutorial — Semgrep Official](https://www.youtube.com/watch?v=v8-vJkJFGRI)
- ✅ Task: Write a custom Semgrep rule that catches hardcoded passwords

### Day 256 — ESLint Security Plugin (JavaScript)
```bash
npm install eslint eslint-plugin-security --save-dev
```
- 📖 [eslint-plugin-security](https://github.com/eslint-community/eslint-plugin-security)

### Day 257 — CodeQL (GitHub Advanced Security)
- 📖 [CodeQL GitHub Actions](https://docs.github.com/en/code-security/code-scanning/using-codeql-code-scanning-with-your-existing-ci-system)
- ✅ Task: Enable CodeQL scanning on your secure-rbac-api repo (free for public repos)
```yaml
- name: Initialize CodeQL
  uses: github/codeql-action/init@v3
  with:
    languages: javascript, python
- name: Perform CodeQL Analysis
  uses: github/codeql-action/analyze@v3
```

### Days 258–260 — SAST in CI/CD Pipeline
- ✅ Add Bandit + Semgrep to your `secure-pipeline` GitHub Actions:
```yaml
- name: SAST - Bandit
  run: |
    pip install bandit
    bandit -r src/ -ll --exit-zero -f txt
    
- name: SAST - Semgrep
  uses: semgrep/semgrep-action@v1
  with:
    config: p/owasp-top-ten
```

### Days 261–264 — Secure Code Review Practice
- 🎥 [Secure Code Review — Rana Khalil](https://www.youtube.com/watch?v=rAwxFw25x3E)
- ✅ Task: Review [Damn Vulnerable Node Application](https://github.com/appsecco/dvna) source code — find all vulns manually before running SAST
- ✅ Task: Compare your manual findings vs what Semgrep and Bandit find

---

## DAST — Dynamic Analysis (Days 265–272)

### Day 265 — DAST with OWASP ZAP
- 🎥 [OWASP ZAP Full Tutorial — OWASP](https://www.youtube.com/watch?v=Bm9YXn7uQKs)
- ✅ Install ZAP: [https://www.zaproxy.org/download/](https://www.zaproxy.org/download/)
- ✅ Task: Run ZAP Spider + Active Scan against DVWA

### Day 266 — ZAP in CI/CD (GitHub Actions)
```yaml
- name: DAST - ZAP Baseline Scan
  uses: zaproxy/action-baseline@v0.12.0
  with:
    target: 'http://localhost:3000'
```

### Day 267 — Nikto in Pipeline
```bash
nikto -h http://localhost -Format json -output nikto-report.json
```

### Days 268–272 — Full Security Pipeline
- ✅ Build a complete pipeline combining: SAST (Bandit/Semgrep) + Dependency audit + Secret detection + DAST (ZAP)
- ✅ All security gates must block the build on HIGH/CRITICAL findings
- ✅ Push final version to `secure-pipeline` repo

---

## Container Security (Days 273–282)

### Day 273 — Docker Security Basics
**What to learn:** Non-root containers, minimal base images, no secrets in Dockerfiles, read-only filesystem
- 🎥 [Docker Security — TechWorld with Nana](https://www.youtube.com/watch?v=KINjI1tlo2w)
- ✅ Task: Find 5 security issues in this Dockerfile:
```dockerfile
FROM ubuntu:latest
RUN apt-get install -y nodejs
COPY . .
ENV API_KEY=supersecretkey123
RUN npm install
CMD ["node", "app.js"]
```

### Day 274 — Trivy — Container Image Scanning
```bash
# Install Trivy
brew install aquasecurity/trivy/trivy

# Scan a Docker image
trivy image node:18
trivy image --severity HIGH,CRITICAL nginx:latest
```
- 📖 [Trivy GitHub](https://github.com/aquasecurity/trivy)

### Day 275 — Trivy in GitHub Actions
```yaml
- name: Scan Docker Image
  uses: aquasecurity/trivy-action@master
  with:
    image-ref: 'your-image:tag'
    severity: 'HIGH,CRITICAL'
    exit-code: '1'
```

### Days 276–280 — Docker Hardening
- ✅ Rewrite the insecure Dockerfile from Day 273 — fix all 5 issues
- ✅ [TryHackMe — Docker Security Room](https://tryhackme.com/room/dockerrodeo)

### Days 281–282 — Kubernetes Security Basics
- 🎥 [Kubernetes Security — TechWorld with Nana](https://www.youtube.com/watch?v=oBf5lrmquYI)
- 📖 [NSA Kubernetes Hardening Guide](https://media.defense.gov/2022/Aug/29/2003066362/-1/-1/0/CTR_KUBERNETES_HARDENING_GUIDANCE_1.2_20220829.PDF)

---

## Cloud Security Basics (Days 283–290)

### Day 283 — AWS IAM Security
**What to learn:** Least privilege IAM, dangerous policies, role chaining, instance profiles
- 🎥 [AWS IAM Full Course — freeCodeCamp](https://www.youtube.com/watch?v=SXQfMQ78KgM)
- 📖 [AWS IAM Best Practices](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html)

### Day 284 — S3 Bucket Misconfiguration
**What to learn:** Public bucket detection, bucket policy misconfigs — how data leaks happen
- 🎥 [S3 Bucket Security — CloudSec](https://www.youtube.com/watch?v=DYoKZsq3LjY)
- ✅ Tool: [S3Scanner](https://github.com/sa7mon/S3Scanner)

### Day 285 — AWS Security Tools
- [Prowler](https://github.com/prowler-cloud/prowler) — AWS security assessment
- [ScoutSuite](https://github.com/nccgroup/ScoutSuite) — Multi-cloud security auditing

### Days 286–290 — Phase 5 Review
- ✅ All 5 tools running in your `secure-pipeline` CI/CD
- ✅ Every security gate blocks on finding
- 📜 Earn: [Google Cloud — Security in Google Cloud](https://www.coursera.org/specializations/security-google-cloud-platform) (free audit)

---

*Next: [Phase 6 — Bug Bounty](365_phase-6-bug-bounty.md)*

# 🧨 Code Crack

Security analysis and remediation AI Skill.

Code Crack consists of two specialized AI skills:

- **crack-seer** → Detects security vulnerabilities
- **dr-crack** → Generates structured remediation plans and optionally applies secure fixes

Together, they create a clean, production-ready security workflow.

---

Separation of concerns:

- crack-seer = Detection only
- dr-crack = Remediation only

---

# 🧨 crack-seer

Static security analyzer.

### What It Does

- Scans entire project codebase
- Detects security vulnerabilities
- Categorizes risks:
  - Critical
  - High
  - Medium
  - Low
- Maps issues to:
  - OWASP Top 10
  - CWE IDs
- Assigns severity score (0–10)
- Generates stable Issue IDs (CRK-001 format)

### Vulnerabilities Covered

- Hardcoded secrets
- API key exposure
- Insecure local storage
- Authentication flaws
- Authorization bypass risks
- Injection vulnerabilities (SQL, command, etc.)
- XSS / CSRF
- Insecure network usage (HTTP)
- Weak cryptography
- Sensitive logging
- Debug configurations in production
- Dependency vulnerabilities
- Misconfigured CORS

### Output

Generates: SECURITY_REPORT.md

---

# 🩺 dr-crack

Security remediation engine.

### What It Does

- Reads `SECURITY_REPORT.md`
- Processes issues by severity (Critical → Low)
- Explains root cause
- Provides step-by-step fix instructions
- Supplies secure code examples
- Describes potential migration or side effects
- Suggests verification steps after fixing

### Output

Generates: SECURITY_FIX_PLAN.md

# 🤖 Auto-Fix Mode (Optional)

If explicitly requested, dr-crack can apply fixes automatically (e.g., "Fix automatically", "Apply patches", "Fix with AI").

Rules:

- Fixes one issue at a time
- Shows:
  - File name
  - Before code
  - After code
  - Explanation
- Waits for confirmation before continuing
- Does not modify multiple issues in a single step
- Preserves project architecture style

---

# 🔄 Workflow

Project Code
↓
crack-seer
↓
SECURITY_REPORT.md
↓
dr-crack
↓
SECURITY_FIX_PLAN.md
↓
(Optional) AI Patch Mode
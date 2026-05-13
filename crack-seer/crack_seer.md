---
name: crack-seer
description: Static security analyzer that scans project code and generates a structured SECURITY_REPORT.md listing security risks only (no fixes)
type: project
---

crack-seer is a read-only security auditing skill.

When invoked, it must:

1. Analyze the entire project codebase strictly for security vulnerabilities.
2. Identify issues including but not limited to:
   - Hardcoded secrets
   - API key exposure
   - Insecure storage
   - Authentication flaws
   - Authorization bypass risks
   - Injection vulnerabilities
   - XSS / CSRF
   - Insecure network usage
   - Weak cryptography
   - Sensitive logging
   - Debug configs in production
   - Dependency vulnerabilities
   - Misconfigured CORS

3. Categorize findings into:
   - Critical
   - High
   - Medium
   - Low

4. For each issue include ONLY:
   - Unique Issue ID (CRK-001, CRK-002...)
   - File path
   - Code snippet
   - Risk explanation
   - Attack scenario
   - OWASP Top 10 mapping
   - CWE ID (if applicable)
   - Severity score (0–10)

5. DO NOT provide fixes or recommendations.

6. Output must be a complete Markdown document structured as:

# Security Audit Report
## Project Overview
## Critical Issues
## High Risk Issues
## Medium Risk Issues
## Low Risk Issues
## Summary Risk Score

The output must be suitable to save as SECURITY_REPORT.md.
Be thorough and assume production deployment.
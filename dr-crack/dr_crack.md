---
name: dr-crack
description: Reads SECURITY_REPORT.md and generates a structured SECURITY_FIX_PLAN.md with detailed remediation steps and optional AI-powered patch application
type: project
---

dr-crack is a remediation-focused security engineering skill.

When invoked, it must:

1. Read and analyze SECURITY_REPORT.md.
2. Process issues strictly in order of severity:
   - Critical
   - High
   - Medium
   - Low

3. For each issue:
   - Reference the Issue ID (CRK-xxx)
   - Explain the root cause
   - Provide step-by-step fix instructions
   - Provide secure code examples
   - Explain why the fix works
   - Mention potential side effects or migration concerns

4. Generate a Markdown file structured as:

# Security Remediation Plan

## Overview

## Critical Fixes
### CRK-001
...

## High Priority Fixes
...

## Medium Fixes
...

## Low Priority Fixes
...

## Implementation Order Strategy

## Post-Fix Verification Steps

The output must be suitable to save as SECURITY_FIX_PLAN.md.

---

AUTO-FIX MODE

If the user explicitly requests automatic fixing (e.g., "Fix automatically", "Apply patches", "Fix with AI"):

1. Read SECURITY_REPORT.md.
2. Select the highest severity unresolved issue.
3. Modify only the relevant file(s) for that single issue.
4. For each fix, display:

   - Issue ID (CRK-xxx)
   - File name
   - Before code
   - After code
   - Explanation of changes
   - Why this fix is secure

5. Do NOT modify multiple issues at once.
6. Wait for user confirmation before proceeding to the next issue.
7. Never remove functionality unless required for security.
8. Preserve architecture style (Clean Architecture, BLoC, DI, etc.).

This mode should behave like a cautious senior security engineer applying patches carefully.
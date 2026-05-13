<p align="center">
  <img src="https://em-content.zobj.net/source/apple/391/bomb_1f4a3.png" width="120" />
</p>

<h1 align="center">CodeCrack</h1>

<p align="center">
  <strong>security analysis and remediation AI skills</strong>
</p>

<p align="center">
  <a href="https://github.com/risal-ea/code-crack/stargazers"><img src="https://img.shields.io/github/stars/risal-ea/code-crack?style=flat&color=red" alt="Stars"></a>
  <a href="https://github.com/risal-ea/code-crack/commits/main"><img src="https://img.shields.io/github/last-commit/risal-ea/code-crack?style=flat" alt="Last Commit"></a>
  <a href="LICENSE"><img src="https://img.shields.io/github/license/risal-ea/code-crack?style=flat" alt="License"></a>
</p>

<p align="center">
  <a href="#what-it-does">What It Does</a> •
  <a href="#install">Install</a> •
  <a href="#crack-seer">crack-seer</a> •
  <a href="#dr-crack">dr-crack</a> •
  <a href="#workflow">Workflow</a>
</p>

---

Two AI skills. One security workflow. Drop into any agent — Claude Code, Codex, Cursor, and more.

- **crack-seer** → scans codebase, finds every vulnerability, outputs `SECURITY_REPORT.md`
- **dr-crack** → reads report, writes `SECURITY_FIX_PLAN.md`, optionally patches files one by one

Separation of concerns: crack-seer = detection only. dr-crack = remediation only.

## What It Does

<table>
<tr>
<td width="50%">

### 👁️ crack-seer output

```
## Critical Issues

### CRK-001
File: lib/api/client.dart
Snippet: final apiKey = "sk-prod-abc123";
Risk: Hardcoded API key exposed in source
Attack: Attacker reads repo, steals key
OWASP: A02 Cryptographic Failures
CWE: CWE-798
Severity: 9.5 / 10
```

</td>
<td width="50%">

### 🩺 dr-crack output

```
## Critical Fixes

### CRK-001 — Hardcoded API Key
Root cause: Secret committed to source control.
Fix: Move to env var or secrets manager.
Secure example: final key = Platform.environment['API_KEY'];
Side effects: Requires env setup in CI/CD.
Verify: grep -r "sk-prod" . → no results.
```

</td>
</tr>
</table>

**Same codebase. Full coverage. Zero guessing.**

```
┌──────────────────────────────────────┐
│ VULNERABILITIES CAUGHT  ████████ 13+ │
│ OWASP COVERAGE          ████████ 100%│
│ FIXES APPLIED           ████████  1× │
│ ARCHITECTURE PRESERVED  ████████ YES │
└──────────────────────────────────────┘
```

## Install

### ⚡ Claude Code

Claude Code supports skills natively via `SKILL.md` files in `~/.claude/skills/`.

```bash
# crack-seer
mkdir -p ~/.claude/skills/crack-seer
curl -fsSL https://raw.githubusercontent.com/risal-ea/code-crack/main/crack-seer/SKILL.md \
  -o ~/.claude/skills/crack-seer/SKILL.md

# dr-crack
mkdir -p ~/.claude/skills/dr-crack
curl -fsSL https://raw.githubusercontent.com/risal-ea/code-crack/main/dr-crack/SKILL.md \
  -o ~/.claude/skills/dr-crack/SKILL.md
```

**Trigger:** type `/crack-seer` or say *"Audit this repo for security issues."*
Then `/dr-crack` or *"Generate a fix plan."*
Auto-fix: *"Apply patches automatically."*

---

### 🤖 OpenAI Codex

Codex reads from `AGENTS.md`. Add skills globally or per project.

```bash
# Global (all projects)
mkdir -p ~/.codex
curl -fsSL https://raw.githubusercontent.com/risal-ea/code-crack/main/crack-seer/crack_seer.md >> ~/.codex/AGENTS.md
echo "" >> ~/.codex/AGENTS.md
curl -fsSL https://raw.githubusercontent.com/risal-ea/code-crack/main/dr-crack/dr_crack.md >> ~/.codex/AGENTS.md

# Per project (in your repo root)
curl -fsSL https://raw.githubusercontent.com/risal-ea/code-crack/main/crack-seer/crack_seer.md > AGENTS.md
echo "" >> AGENTS.md
curl -fsSL https://raw.githubusercontent.com/risal-ea/code-crack/main/dr-crack/dr_crack.md >> AGENTS.md
```

**Trigger:** *"Run crack-seer on this project."* → *"Run dr-crack."* → *"Fix automatically."*

Verify active instructions: `codex "Summarize the current instructions."`

---

### 🖱️ Cursor

Cursor reads rules from `.cursor/rules/*.mdc` (recommended) or `.cursorrules` (legacy).

```bash
mkdir -p .cursor/rules

# crack-seer rule
printf -- '---\ndescription: Security vulnerability scanner. Invoke when asked to audit, scan, or analyze for security issues.\nglobs: "**/*"\n---\n' \
  > .cursor/rules/crack-seer.mdc
curl -fsSL https://raw.githubusercontent.com/risal-ea/code-crack/main/crack-seer/crack_seer.md \
  >> .cursor/rules/crack-seer.mdc

# dr-crack rule
printf -- '---\ndescription: Security remediation engine. Invoke when asked to fix or patch vulnerabilities from SECURITY_REPORT.md.\nglobs: "**/*"\n---\n' \
  > .cursor/rules/dr-crack.mdc
curl -fsSL https://raw.githubusercontent.com/risal-ea/code-crack/main/dr-crack/dr_crack.md \
  >> .cursor/rules/dr-crack.mdc
```

Open Agent mode (`Cmd+I` → Agent) and say:
*"Run crack-seer on this project and generate SECURITY_REPORT.md"*
Then: *"Run dr-crack and create SECURITY_FIX_PLAN.md"*

## crack-seer

Static security analyzer. Read-only. No fixes.

Scans for:

| Category | Examples |
|----------|---------|
| Secrets | Hardcoded API keys, tokens, passwords |
| Storage | Insecure local storage, plaintext persistence |
| Auth | Authentication flaws, authorization bypass |
| Injection | SQL, command, path traversal |
| Web | XSS, CSRF, misconfigured CORS |
| Network | HTTP instead of HTTPS, no cert pinning |
| Crypto | Weak algorithms, broken implementations |
| Code | Sensitive logging, debug configs in prod |
| Deps | Known vulnerable dependency versions |

Each issue gets:

- **Issue ID** — stable identifier (CRK-001, CRK-002…)
- **File path + code snippet**
- **Risk explanation + attack scenario**
- **OWASP Top 10 mapping**
- **CWE ID**
- **Severity score** (0–10)

**Output:** `SECURITY_REPORT.md`

## dr-crack

Remediation engine. Reads `SECURITY_REPORT.md`. Writes fix plan.

Processes issues Critical → High → Medium → Low.

For each issue:
- Root cause explanation
- Step-by-step fix instructions
- Secure code examples
- Migration notes and side effects
- Post-fix verification steps

**Output:** `SECURITY_FIX_PLAN.md`

### Auto-Fix Mode

Say *"Fix automatically"*, *"Apply patches"*, or *"Fix with AI"*.

Rules:
- One issue at a time — highest severity first
- Shows file name, before code, after code, explanation
- Waits for confirmation before next issue
- Never removes functionality unless required for security
- Preserves architecture style (Clean Architecture, BLoC, DI, etc.)

Behaves like a cautious senior security engineer applying patches carefully.

## Workflow

```
Project Code
    ↓
crack-seer    →    SECURITY_REPORT.md
    ↓
dr-crack      →    SECURITY_FIX_PLAN.md
    ↓
(Optional) Auto-Fix Mode    →    patches applied file by file
```

## Quick Reference

| Tool | Files to use | Install location |
|------|-------------|-----------------|
| Claude Code | `SKILL.md` | `~/.claude/skills/<skill-name>/SKILL.md` |
| Codex | `crack_seer.md` + `dr_crack.md` | `~/.codex/AGENTS.md` or `./AGENTS.md` |
| Cursor | `crack_seer.md` + `dr_crack.md` | `.cursor/rules/*.mdc` or `.cursorrules` |

## Links

- [crack-seer/SKILL.md](./crack-seer/SKILL.md) — Claude Code skill definition
- [crack-seer/crack_seer.md](./crack-seer/crack_seer.md) — full instructions (Codex / Cursor)
- [dr-crack/SKILL.md](./dr-crack/SKILL.md) — Claude Code skill definition
- [dr-crack/dr_crack.md](./dr-crack/dr_crack.md) — full instructions (Codex / Cursor)
- [Issues](https://github.com/risal-ea/code-crack/issues) — bug, feature, weird behavior

## License

MIT — find bug. fix bug. ship safe code.
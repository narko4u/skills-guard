# Skills Guard — Security Scanner for AI Agent Skills

**The first security scanner built for the agent skill ecosystem.**

[![Buy on Gumroad](https://img.shields.io/badge/Buy%20on%20Gumroad-FFA500?style=for-the-badge&logo=gumroad&logoColor=white)](https://empirelab1.gumroad.com/l/skills-guard)

---

## Why Skills Guard?

Skills are the new attack surface. AI agents run skill code that has unfettered access to credentials, filesystems, networks, and system resources. Hardcoded API keys, prompt injection payloads, dangerous function calls — and until now, no tool to find them.

Skills Guard is a static analysis scanner purpose-built for the AI agent skill ecosystem. It inspects your skill code before you ship it, catching security issues that standard linters and SAST tools were never designed to detect.

---

## Vulnerability Categories

| Category | What It Detects |
|---|---|
| **Credential Leaks** | OpenAI keys, AWS access keys, GitHub tokens, JWTs, RSA/EC private keys, database connection strings |
| **Dangerous Calls** | `exec`, `eval`, `subprocess.Popen`, `os.system`, `pickle.load`, `ctypes`, `marshal`, `shutil.rmtree` |
| **Network Access** | `requests.get`, `urllib` calls, raw socket connections, SSH clients, FTP connections |
| **Filesystem Scope** | Arbitrary file reads/writes, path traversal patterns, `tempfile` misuse, file overwrites |
| **Prompt Injection** | DAN (Do Anything Now) attacks, jailbreak patterns, system prompt override attempts, token/instruction leaks |

---

## Trust Scoring

Every scan produces a **0–100 trust score** with a clear severity breakdown:

```
Trust Score: 78/100 — Moderate Risk

  HIGH      2 findings      Credential Leaks
  MEDIUM    5 findings      Dangerous Calls, Network Access
  LOW       8 findings      Filesystem Scope, Prompt Injection
```

High scores mean production-ready. Low scores mean your skill needs a security review.

---

## Quick Start

```bash
pip install skills-guard

# Scan a single skill file
skills-guard scan ./my_skill.py

# Scan an entire skill directory
skills-guard scan ./skills/ --recursive

# Output as JSON for CI/CD pipelines
skills-guard scan ./my_skill.py --json
```

---

## API

```bash
# Single scan
POST /scan
Content-Type: application/json
{
  "code": "def run():\n    import os\n    os.system('rm -rf /')",
  "language": "python"
}

# Batch scan
POST /scan-batch
Content-Type: application/json
{
  "skills": [
    {"id": "skill-1", "code": "...", "language": "python"},
    {"id": "skill-2", "code": "...", "language": "python"}
  ]
}
```

---

## SaaS Registry

Publish your scanned skills to the **Skills Guard Registry** — a public directory of AI agent skills with verified trust scores. Users can discover safe, vetted skills by category, trust score, and capability.

| Feature | Free Tier | Pro ($99/mo) |
|---|---|---|
| Scans per month | 100 | 10,000 |
| Registry publishing | — | Unlimited |
| API access | Rate-limited | Full access |
| CI/CD integration | — | ✓ |
| Priority support | — | ✓ |

**Per-scan pricing:** $0.01/scan (billed overages)

---

## Get Started Now

[**Buy Skills Guard on Gumroad →**](https://empirelab1.gumroad.com/l/skills-guard)

Free tier includes 100 scans per month. No credit card required.

---

*Built by **Empire Labs Pty Ltd** (ACN 693 862 145)*

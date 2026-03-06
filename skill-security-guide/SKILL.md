---
name: skill-security-guide
description: Security best practices guide for passing ClawHub security scans with "Benign" ratings. Use when creating or reviewing skills to ensure they meet security standards.
homepage: https://clawhub.ai/docs/security
metadata: {"clawdbot":{"emoji":"🔒","requires":{"bins":[],"env":[]},"primaryEnv":""}}
---

# Skill Security Guide

A comprehensive guide to help your skills pass ClawHub security scans with "Benign" ratings.

## Why This Matters

ClawHub performs automated security scans on all uploaded skills. Skills that don't meet security standards are marked as "Suspicious" and users are warned before installation.

## Golden Rule: Metadata Format

**ALWAYS use JSON format for metadata in SKILL.md:**

```yaml
---
name: your-skill-name
description: Your skill description
homepage: https://example.com
metadata: {"clawdbot":{"emoji":"🔧","requires":{"bins":["python"],"packages":["package-name"],"env":["ENV_VAR_1","ENV_VAR_2"]},"primaryEnv":"ENV_VAR_1"}}
---
```

### ❌ Wrong Format (YAML multi-line)

```yaml
metadata:
  requires:
    bins: ["python"]
    env: ["KEY"]
```

### ✅ Correct Format (JSON single-line)

```yaml
metadata: {"clawdbot":{"requires":{"bins":["python"],"env":["KEY"]}}}
```

## Security Checklist

Before submitting your skill to ClawHub:

### SKILL.md
- [ ] Metadata is JSON single-line format
- [ ] All required `bins` are declared (python, node, etc.)
- [ ] All required `env` variables are declared
- [ ] `primaryEnv` is set to the main credential variable
- [ ] Clear `emoji` icon is specified

### Code Security
- [ ] No SSL verification disabled (no `ssl.CERT_NONE`)
- [ ] No sensitive information printed in logs/output
- [ ] Credentials read from environment variables only
- [ ] Only access declared API endpoints

### Documentation
- [ ] Functionality description is accurate (no misleading claims)
- [ ] Dependencies are fully declared
- [ ] All documentation files are consistent

## Common Security Issues

### Issue 1: Metadata Format Error

**Symptom**: Security scan shows "registry summary claimed 'Required env vars: none'"

**Fix**: Convert YAML multi-line to JSON single-line

```yaml
# ❌ Wrong
metadata:
  requires:
    env: ["KEY"]

# ✅ Correct
metadata: {"clawdbot":{"requires":{"env":["KEY"]}}}
```

### Issue 2: SSL Verification Disabled

**Symptom**: Security scan mentions "insecure practices"

**Fix**: Remove SSL disabling code

```python
# ❌ Wrong
ssl_context = ssl.create_default_context()
ssl_context.verify_mode = ssl.CERT_NONE

# ✅ Correct
import urllib.request
with urllib.request.urlopen(url, timeout=30) as response:
    ...
```

### Issue 3: Sensitive Information Leak

**Symptom**: Security scan mentions "guidance that prints secret material"

**Fix**: Only check variable existence, don't display content

```powershell
# ❌ Wrong
Write-Host "SecretKey: $($env:SECRET_KEY.Substring(0,10))..."

# ✅ Correct
if ($env:SECRET_KEY) { Write-Host "✅ Credentials configured" }
```

### Issue 4: Misleading Functionality Claims

**Symptom**: Security scan mentions "behavioral mismatch" or "misleading claim"

**Fix**: Ensure documentation matches actual code behavior

```markdown
# ❌ Wrong (if code doesn't actually do this)
## Features
- Automatically removes watermarks

# ✅ Correct
## Features
- Supports watermark control via API parameter
```

## Complete Example: Benign-Rated Skill

```yaml
---
name: tavily
description: AI-optimized web search via Tavily API. Returns concise, relevant results for AI agents.
homepage: https://tavily.com
metadata: {"clawdbot":{"emoji":"🔍","requires":{"bins":["node"],"env":["TAVILY_API_KEY"]},"primaryEnv":"TAVILY_API_KEY"}}
---

# Tavily Search

AI-optimized web search using Tavily API.

## Usage

```bash
node {baseDir}/scripts/search.mjs "your search query"
```

## Requirements

- Node.js installed
- TAVILY_API_KEY environment variable set

Get your API key at: https://tavily.com
```

## Pre-Submission Verification

Run these checks before submitting:

```bash
# 1. Check metadata format
grep "^metadata:" SKILL.md

# 2. Check for SSL disabling
grep -r "CERT_NONE" scripts/

# 3. Check for sensitive info in docs
grep -i "secretkey\|api_key" README.md SKILL.md

# 4. Verify documentation consistency
# Ensure SKILL.md, README.md, and package.yaml all match
```

## Relationship with skill-creator-2

This skill is **complementary** to [skill-creator-2](https://clawhub.ai/yixinli867/skill-creator-2):

| Aspect | skill-creator-2 | skill-security-guide |
|--------|-----------------|----------------------|
| Skill structure design | ✅ Detailed guide | Not covered |
| Progressive disclosure | ✅ Detailed guide | Not covered |
| **ClawHub security review** | ❌ Not covered | ✅ **Specialized guide** |
| **Metadata JSON format** | ❌ Not covered | ✅ **Core content** |
| **SSL/Security best practices** | ❌ Not covered | ✅ **Detailed guide** |
| **Security checklist** | ❌ Not covered | ✅ **Complete checklist** |

**Use both skills together**:
1. Use `skill-creator-2` to design and structure your skill
2. Use `skill-security-guide` to ensure it passes ClawHub security scans

## License

MIT License

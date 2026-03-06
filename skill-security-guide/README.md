# Skill Security Guide

A comprehensive guide to help your skills pass ClawHub security scans with "Benign" ratings.

## Why This Matters

ClawHub performs automated security scans on all uploaded skills. Skills that don't meet security standards are marked as "Suspicious" and users are warned before installation.

## Quick Start

### The Golden Rule

**ALWAYS use JSON format for metadata in SKILL.md:**

```yaml
---
name: your-skill
description: Your skill description
metadata: {"clawdbot":{"emoji":"🔧","requires":{"bins":["python"],"env":["API_KEY"]},"primaryEnv":"API_KEY"}}
---
```

### Common Mistakes to Avoid

| Mistake | Impact | Fix |
|---------|--------|-----|
| YAML metadata | "Required env vars: none" error | Use JSON format |
| SSL verification disabled | "Insecure practices" warning | Use standard HTTPS |
| Printing secrets | "Sensitive material" warning | Check existence only |
| Misleading claims | "Behavioral mismatch" warning | Accurate documentation |

## Security Checklist

Before submitting your skill:

- [ ] Metadata is JSON single-line format
- [ ] All required `bins` are declared
- [ ] All required `env` variables are declared
- [ ] `primaryEnv` is set to main credential
- [ ] No SSL verification disabled
- [ ] No secrets printed in logs/output
- [ ] Documentation matches actual behavior

## Examples

### Good Example (Benign Rating)

See `tavily-search` skill:
- Clean JSON metadata
- Declares all dependencies
- No insecure practices
- Accurate documentation

### Bad Example (Suspicious Rating)

Common issues:
- Multi-line YAML metadata
- Missing env declarations
- SSL verification disabled
- Misleading feature claims

## Relationship with skill-creator-2

This skill is **complementary** to [skill-creator-2](https://clawhub.ai/yixinli867/skill-creator-2), not a replacement:

| Aspect | skill-creator-2 | clawhub-security-guide |
|--------|-----------------|------------------------|
| Skill structure design | ✅ Detailed guide | Not covered |
| Progressive disclosure | ✅ Detailed guide | Not covered |
| **ClawHub security review** | ❌ Not covered | ✅ **Specialized guide** |
| **Metadata JSON format** | ❌ Not covered | ✅ **Core content** |
| **SSL/Security best practices** | ❌ Not covered | ✅ **Detailed guide** |
| **Security checklist** | ❌ Not covered | ✅ **Complete checklist** |

**Use both skills together**:
1. Use `skill-creator-2` to design and structure your skill
2. Use `clawhub-security-guide` to ensure it passes ClawHub security scans

## License

MIT

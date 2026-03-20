# Runbook — <runbook title>

## Purpose
Provide a simple step-by-step procedure for <what this runbook helps validate, troubleshoot, or execute>.

## Scope
This runbook is for <scope of use, environment, or limitation>.

## Tools Used
- <tool 1>
- <tool 2>
- `<command / utility 1>`
- `<command / utility 2>`

---

## Procedure

### 1. <First Step Title>
<brief instruction for the first step>

---

### 2. <Second Step Title>
Run:

```powershell
<command>
```

If <condition>, then <action>.

### 3. <Third Step Title>
Run:

```powershell
<command>
```

If <condition>, then <action>.

### 4. <Fourth Step Title>
Run:

```powershell
<command>
```

If <condition>, then <action>.

---

## Decision Guide

| Check | Result | Next Step |
|-------|--------|-----------|
| <check 1> | ❌ Fails | <action> |
| <check 2> | ❌ Fails | <action> |
| <check 3> | ❌ Fails | <action> |
| All checks | ✅ Pass | <interpretation / next step> |

---

## Next Action / Escalation

If the issue cannot be reproduced, <monitoring / retest instruction>.

If the issue is reproducible, escalate based on which layer failed:

- **<layer / area 1>** — escalate to <owner / team>
- **<layer / area 2>** — escalate to <owner / team>
- **<layer / area 3>** — escalate to <owner / team>
# Runbook — Website Unreachable Basic Check

## Purpose
Provide a simple step-by-step procedure for checking whether a website is unreachable due to DNS, HTTP, or network path issues.

## Scope
This runbook is for basic website reachability validation using local terminal and browser-based checks.

## Tools Used
- Browser
- PowerShell / Terminal
- `nslookup`
- `curl.exe`
- `tracert`

---

## Procedure

### 1. Confirm the Reported Issue
Open the target site in a browser and observe what happens.

---

### 2. Check DNS Resolution
Run:

```powershell
nslookup <domain>
```

If the domain resolves to an IP address, DNS is working.

---

### 3. Check HTTP/HTTPS Response
Run:

```powershell
curl.exe -I https://<domain>
```

If the request returns a valid HTTP status such as `200 OK`, the site is reachable at the application layer.

---

### 4. Check the Route/Path
Run:

```powershell
tracert <domain>
```

If the trace reaches the destination, the route/path is working.

---

## Decision Guide

| Check | Result | Next Step |
|---|---|---|
| DNS | ❌ Fails | Investigate name resolution or DNS server issues |
| DNS ✅ / HTTP | ❌ Fails | Investigate website/service or HTTPS access issues |
| DNS ✅ / HTTP ✅ / Route | ❌ Fails | Investigate network connectivity or upstream routing |
| All checks | ✅ Pass | Issue may be intermittent or not reproducible |

---

## Next Action / Escalation

If the issue **cannot be reproduced**, monitor for recurrence and retest when the problem appears again.

If the issue **is reproducible**, escalate based on which layer failed:
- **DNS** — escalate to DNS/naming team
- **HTTP** — escalate to web/application team
- **Network path** — escalate to network/infrastructure team
````
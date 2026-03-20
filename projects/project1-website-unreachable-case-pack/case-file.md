# Project 1 — Website Unreachable Case Pack

## Issue
Website appears unreachable from my environment.

## Target
`example.com`

## Environment
- Local machine
- PowerShell terminal
- Browser-based validation

## Checks Performed

### 1. DNS Check
**Command:** `nslookup example.com`  
**Result:** The domain resolved successfully and returned both IPv4 and IPv6 addresses.  
**Interpretation:** DNS resolution is working correctly, so DNS is not the cause of the issue.

### 2. HTTP Check
**Command:** `curl.exe -I https://example.com`  
**Result:** The request returned `HTTP/1.1 200 OK` with normal response headers.  
**Interpretation:** HTTPS connectivity and HTTP response are working correctly, so the site is reachable at the application layer.

### 3. Route/Path Check
**Command:** `tracert example.com`  
**Result:** The trace reached the destination IP address successfully in 10 hops.  
**Interpretation:** Network path connectivity is working. One intermediate timeout appeared, but the destination was still reached, so there is no confirmed route/path failure.

## Diagnosis
There is no evidence of an active DNS, HTTP, or route/path failure during testing. The reported issue could not be reproduced from the test environment at the time of validation.

## Next Action
Monitor for recurrence and repeat the checks if the issue happens again. If the problem reappears, retest from the affected machine or network to determine whether the issue is intermittent or environment-specific.

## Conclusion
Based on the DNS, HTTP, and route/path checks, the issue could not be reproduced during testing. The domain resolved successfully, the site returned `200 OK`, and the route trace reached the destination. There is no current evidence of an active DNS, HTTP, or network path problem.

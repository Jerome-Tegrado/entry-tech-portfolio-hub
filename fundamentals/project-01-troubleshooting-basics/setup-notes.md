# Setup Notes

## Project Information
- Track: Fundamentals
- Project Number: 01
- Project Name: Website Unreachable Case Pack
- Label: Fundamentals - Troubleshooting Basics

## Procedure
1. Confirm the reported issue in a browser.
2. Check DNS resolution with `nslookup <domain>`.
3. Check HTTP/HTTPS response with `curl.exe -I https://<domain>`.
4. Check network path with `tracert <domain>`.

## Decision Guide
- DNS fails: investigate resolver or DNS server path.
- DNS passes and HTTP fails: investigate web service or TLS/application path.
- DNS and HTTP pass and route fails: investigate network path.
- All checks pass: treat as intermittent or environment-specific until reproduced.


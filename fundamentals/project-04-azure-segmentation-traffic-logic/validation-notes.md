# Validation Notes

## Validation Checks
- Backend local service check:
  - `curl http://localhost`
  - Result: nginx page returned
- Allowed path check (frontend to backend HTTP):
  - `curl http://10.20.1.5`
  - Result: success
- Blocked path check (frontend to backend SSH):
  - `nc -zvw 5 10.20.1.5 22`
  - Result: denied/timeout after deny rule

## Validation Outcome
Traffic behavior matched intended segmentation logic: required service path allowed and unintended management path blocked.


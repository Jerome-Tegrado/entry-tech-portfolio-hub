# Validation Notes

## Validation Sequence
1. Baseline test
   - `ssh jerome@135.171.176.24`
   - Result: success
2. Block test
   - `deny-ssh` rule applied at higher priority than `allow-ssh`
   - Result: SSH timeout/failure
3. Restore test
   - `deny-ssh` rule removed
   - Result: SSH success

## Validation Outcome
Network control behavior matched expectation and confirmed NSG priority-driven traffic enforcement.


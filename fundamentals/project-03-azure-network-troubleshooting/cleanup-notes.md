# Cleanup Notes

## Cleanup Context
- Project Number: 03
- Label: Fundamentals - Azure Network Troubleshooting
- Date: March 26, 2026

## Reason for Cleanup
The lab resources were removed after the hands-on activity was completed and all required screenshot evidence was captured. Cleanup was performed to avoid unnecessary Azure cost and to keep the environment clean after validating the NSG blocking and restoration flow.

## Resources Targeted
- Resource Group(s):
  - `rg-p2p1-nsg-lab`
- Resource(s):
  - `vm-p2p1`
  - `vnet-p2p1`
  - `subnet-workload`
  - `nsg-p2p1`
  - `pip-vm-p2p1`
  - VM network interface created during deployment
- Dependencies:
  - VM depended on the network interface, subnet, virtual network, and public IP
  - NSG was associated to `subnet-workload`
  - Deleting the resource group removes all contained resources together

## Pre-Cleanup Checks
- Backup/export completed:
  - Not applicable for this lab
- Evidence captured:
  - Yes, screenshots for baseline success, deny-rule failure, and restored success were saved
- Approval/reference:
  - Cleanup performed after confirming the lab execution was complete

## Cleanup Steps
1. Step: Confirm lab completion and saved evidence
   - Action/Command:
     - Review screenshots and notes
     - Confirm baseline success, deny-rule failure, and restored success were already captured
   - Expected Result:
     - All proof needed for documentation is available before deleting resources

2. Step: Delete the resource group
   - Action/Command:
     - In Azure Portal, open resource group `rg-p2p1-nsg-lab`
     - Click `Delete resource group`
     - Type `rg-p2p1-nsg-lab` to confirm deletion
     - Submit the deletion request
   - Expected Result:
     - Azure begins deleting all resources inside the resource group

3. Step: Validate cleanup completion
   - Action/Command:
     - Check Azure Portal to confirm `rg-p2p1-nsg-lab` no longer appears in the resource group list
   - Expected Result:
     - Resource group and all lab resources are removed successfully

## Post-Cleanup Validation
- Verification command(s):
  - Azure Portal resource group list check
- Screenshot path(s):
  - Optional screenshot of deleted or deleting resource group status
- Confirmation notes:
  - Cleanup is successful when `rg-p2p1-nsg-lab` is no longer present and no lab resources remain running

## Issues Encountered
- Issue:
  - No major cleanup issue was confirmed during the documented flow
  - Resolution:
    - Not applicable

## Final Status
- Cleanup completed (Yes/No): Yes


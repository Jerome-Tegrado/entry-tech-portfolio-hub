# Cleanup Notes

## Cleanup Context
- Project Name: Phase 2, Project 2 — ASG Segmentation Lab
- Date: March 29, 2026

## Reason for Cleanup
The resources were removed because the core hands-on implementation and validation for the ASG Segmentation Lab were already complete. The required proof was achieved by showing that frontend-to-backend HTTP traffic on port 80 was allowed and that frontend-to-backend SSH traffic on port 22 was blocked after the deny rule was applied.

## Resources Targeted
- Resource Group(s):
  - `rg-p2p2-asgseg-lab`
- Resource(s):
  - `all resources under the resource group`
- Dependencies:
  - The frontend VM depended on its network interface, public IP, OS disk, and SSH key resource
  - The backend VM depended on its network interface, OS disk, and SSH key resource
  - `nsg-p2p2-asgseg-lab` depended on subnet association for enforcement
  - `asg-p2p2-asgseg-frontend` and `asg-p2p2-asgseg-backend` depended on NIC membership for traffic grouping

## Pre-Cleanup Checks
- Backup/export completed:
  - Not required for this temporary lab environment
- Evidence captured:
  - All required screenshots and command-output proofs were saved before deletion
- Approval/reference:
  - Cleanup was based on successful completion of the lab’s core hands-on validation

## Cleanup Steps
1. Step: Confirm proof artifacts were already saved
   - Action/Command:
     - Reviewed the project evidence folder and confirmed that the required screenshots and command outputs were already captured
   - Expected Result:
     - All needed setup, validation, and proof artifacts were available before resource deletion

2. Step: Delete the Azure resource group
   - Action/Command:
     - Opened `rg-p2p2-asgseg-lab` in Azure Portal
     - Clicked **Delete resource group**
     - Typed the resource group name for confirmation
     - Submitted the deletion request
   - Expected Result:
     - Azure started deleting all resources contained inside `rg-p2p2-asgseg-lab`

3. Step: Verify cleanup completion
   - Action/Command:
     - Refreshed the Azure Portal resource group list and confirmed that `rg-p2p2-asgseg-lab` no longer appeared
   - Expected Result:
     - The resource group and all included resources were successfully removed from the subscription

## Post-Cleanup Validation
- Verification command(s):
  - Azure Portal check that `rg-p2p2-asgseg-lab` no longer exists
  - Optional Azure CLI check:
    ```bash
    az group exists --name rg-p2p2-asgseg-lab
    ```
- Screenshot path(s):
  - `resource-group.png`
  - `cleanup.png`
- Confirmation notes:
  - No remaining resources for this lab existed after cleanup
  - The lab environment no longer incurred Azure usage after deletion was completed

## Issues Encountered
- Issue:
  - Azure’s default `AllowVnetInBound` rule could allow same-VNet internal traffic unless a stronger blocked-path proof was added
  - Resolution:
    - A deny rule on port 22 was created and validated before cleanup to prove unintended traffic was blocked

- Issue:
  - Old `.pem` files from past lab work were found in the public repository
  - Resolution:
    - These keys were treated as exposed old lab keys that should not be reused, and repository cleanup was identified as a separate follow-up task

## Final Status
- Cleanup completed (Yes/No): Yes
# Cleanup Notes

## Cleanup Context
- Project Number: 02
- Label: Fundamentals - Azure Operations Basics
- Date: 2026-03-20

## Reason for Cleanup
The resources were removed after successful setup, validation, and evidence capture to complete the cleanup portion of the project and avoid unnecessary resource usage or possible charges.

## Resources Targeted
- Resource Group(s): `rg-project2-azure-setup`
- Resource(s): `storageproject02`
- Dependencies: Storage account was contained inside the target resource group and was deleted together with the resource group.

## Pre-Cleanup Checks
- Backup/export completed: Not required for this project
- Evidence captured: Yes - setup proof screenshots were already captured before deletion
- Approval/reference: Cleanup performed as part of the planned project completion steps

## Cleanup Steps
1. Step: Review the target resource group before deletion
   - Action/Command: Opened `rg-project2-azure-setup` in Azure Portal and confirmed the included resource was `storageproject02`
   - Expected Result: Correct resource group and resource are identified before deletion

2. Step: Confirm resource group deletion
   - Action/Command: Selected **Delete resource group**, entered the resource group name `rg-project2-azure-setup`, and submitted the deletion
   - Expected Result: Azure accepts the deletion request and starts removing the resource group and its contained resources

3. Step: Verify cleanup result
   - Action/Command: Checked the Resource Groups view in Azure Portal and confirmed the resource group no longer appeared after deletion
   - Expected Result: `rg-project2-azure-setup` is no longer listed and its resources are removed

## Post-Cleanup Validation
- Verification command(s): Portal-based verification used; resource group no longer visible in Resource Groups list
- Screenshot path(s):
  - `evidence/Pre-Deletion.png`
  - `evidence/Deleted.png`
- Confirmation notes: The resource group `rg-project2-azure-setup` and the storage account `storageproject02` were successfully removed.

## Issues Encountered
- Issue: None
  - Resolution: Not applicable

## Final Status
- Cleanup completed (Yes/No): Yes



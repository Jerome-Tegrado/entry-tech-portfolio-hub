# Setup Notes

## Setup Context
- Project Number: 02
- Label: Fundamentals - Azure Operations Basics
- Date: 2026-03-20

## Prerequisites
- Access requirements:
  - Access to Microsoft Azure Portal
  - Access to Azure Cloud Shell
  - Active Azure subscription
- Tools needed:
  - Azure Portal
  - Azure Cloud Shell
  - Azure CLI
- Required permissions/roles:
  - Permission to create a resource group
  - Permission to create a storage account
  - Permission to view resources in the subscription

## Baseline Checks
- Current state:
  - No existing project resource group was confirmed before setup.
- Check command(s):
  - `az group list --output table`
- Expected baseline output:
  - The command should list available resource groups and confirm whether the target project resource group exists.

## Setup Steps
1. Step: Create the resource group
   - Action/Command:
     - Created resource group `rg-project2-azure-setup` in Azure Portal
   - Expected Output:
     - Resource group is created successfully in the `southeastasia` region

2. Step: Verify the resource group using Azure Cloud Shell
   - Action/Command:
     - `az group list --output table`
   - Expected Output:
     - Resource group `rg-project2-azure-setup` appears with location `southeastasia` and status `Succeeded`

3. Step: Create the storage account
   - Action/Command:
     - Created storage account `storageproject02` inside resource group `rg-project2-azure-setup`
   - Expected Output:
     - Storage account is deployed successfully and shows provisioning state `Succeeded`

## Configuration Details
- Naming pattern:
  - Resource Group: `rg-project2-azure-setup`
  - Storage Account: `storageproject02`
- Region:
  - Southeast Asia (`southeastasia`)
- Tags:
  - None
- SKU/Cost choices:
  - Performance: Standard
  - Replication: Locally-redundant storage (LRS)

## Validation
- Verification command(s):
  - `az group list --output table`
- Screenshot path(s):
  - `evidence/Resource_Group.png`
  - `evidence/Storage_Account_Overview.png`
- Success criteria:
  - Resource group exists and shows status `Succeeded`
  - Storage account exists inside the correct resource group
  - Storage account provisioning state shows `Succeeded`

## Risks and Notes
- Risk:
  - Leaving cloud resources deployed may create unnecessary cost
  - Mitigation:
    - Use only a minimal setup and delete the resource group after proof and documentation are completed



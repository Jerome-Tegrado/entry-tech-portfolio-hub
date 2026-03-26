# Setup Notes

## Setup Context
- Project Name: Phase 2 Project 1 - NSG Blocking Lab
- Date: March 26, 2026

## Prerequisites
- Access requirements:
  - Active Azure subscription
  - Access to Azure Portal
- Tools needed:
  - Azure Portal
  - Windows PowerShell for SSH testing
- Required permissions/roles:
  - Permission to create and delete resource groups
  - Permission to create networking and compute resources in Azure

## Baseline Checks
- Current state:
  - Resource group, VNet, subnet, NSG, and VM were created
  - NSG was already associated to the subnet
  - SSH access was not yet confirmed
- Check command(s):
  - `ssh jerome@135.171.176.24`
- Expected baseline output:
  - Successful SSH login to the Ubuntu VM after the required allow SSH rule is present in the NSG

## Setup Steps
1. Step: Create the core Azure network resources
   - Action/Command:
     - Create resource group `rg-p2p1-nsg-lab`
     - Create virtual network `vnet-p2p1` with address space `10.20.0.0/16`
     - Create subnet `subnet-workload` with `10.20.1.0/24`
     - Create network security group `nsg-p2p1`
     - Associate `nsg-p2p1` to `subnet-workload`
   - Expected Output:
     - Resource group, VNet, subnet, and NSG are created successfully
     - NSG is attached to the subnet

2. Step: Create the virtual machine
   - Action/Command:
     - Create VM `vm-p2p1`
     - Use Ubuntu Server 24.04 LTS - x64 Gen2
     - Place VM in `vnet-p2p1` and `subnet-workload`
     - Create public IP `pip-vm-p2p1`
     - Set NIC network security group to `None`
     - Allow selected inbound port `SSH (22)` during VM creation
   - Expected Output:
     - Ubuntu VM is deployed successfully
     - Public IP is assigned
     - VM is running

3. Step: Add allow SSH rule for baseline access
   - Action/Command:
     - In `nsg-p2p1`, add inbound rule:
       - Name: `allow-ssh`
       - Service: `SSH`
       - Protocol: `TCP`
       - Action: `Allow`
       - Priority: `100`
   - Expected Output:
     - Inbound SSH traffic is allowed through the subnet-level NSG
     - VM becomes reachable through SSH

4. Step: Validate baseline connectivity
   - Action/Command:
     - Run `ssh jerome@135.171.176.24`
   - Expected Output:
     - SSH login succeeds
     - Terminal access to the Ubuntu VM is established

5. Step: Edit allow rule and add deny rule to intentionally block access
   - Action/Command:
     - Edit `allow-ssh` in `nsg-p2p1` and change its priority from `100` to `110`
     - Add a new inbound rule in `nsg-p2p1`:
       - Name: `deny-ssh`
       - Service: `SSH`
       - Protocol: `TCP`
       - Action: `Deny`
       - Priority: `100`
   - Expected Output:
     - `allow-ssh` is moved to priority `110`
     - `deny-ssh` is created at priority `100`
     - Because lower number means higher priority, the deny rule overrides the allow rule
     - SSH traffic is blocked

6. Step: Validate failed connectivity
   - Action/Command:
     - Run `ssh jerome@135.171.176.24`
   - Expected Output:
     - SSH connection times out
     - Access failure confirms the deny rule is working

7. Step: Restore access
   - Action/Command:
     - Delete `deny-ssh` from `nsg-p2p1`
     - Run `ssh jerome@135.171.176.24` again
   - Expected Output:
     - SSH login succeeds again
     - Access restoration confirms NSG rule change took effect

8. Step: Clean up resources
   - Action/Command:
     - Delete resource group `rg-p2p1-nsg-lab`
   - Expected Output:
     - All lab resources are deleted
     - No ongoing lab cost remains

## Configuration Details
- Naming pattern:
  - Resource Group: `rg-p2p1-nsg-lab`
  - Virtual Network: `vnet-p2p1`
  - Subnet: `subnet-workload`
  - Network Security Group: `nsg-p2p1`
  - Virtual Machine: `vm-p2p1`
  - Public IP: `pip-vm-p2p1`
- Region:
  - Southeast Asia
- Tags:
  - None used
- SKU/Cost choices:
  - Ubuntu Server 24.04 LTS - x64 Gen2
  - Public IP used Standard SKU with Static assignment
  - VM size should ideally be the smallest practical available size for low-cost lab testing

## Validation
- Verification command(s):
  - `ssh jerome@135.171.176.24`
- Screenshot path(s):
  - VM creation evidence
  - Allow SSH rule at priority 100
  - Baseline SSH success
  - Edited allow SSH rule at priority 110
  - NSG deny rule at priority 100
  - SSH timeout after deny rule
  - Final SSH success after removing deny rule
- Success criteria:
  - SSH works after allow rule is added
  - SSH fails after deny rule is added
  - SSH works again after deny rule is removed

## Risks and Notes
- Risk:
  - Baseline access may fail if the subnet NSG does not yet allow SSH
  - Incorrect NSG rule priority may prevent the deny rule from taking effect
  - Leaving the VM or public IP running after testing may cause unnecessary cost
  - Confusing subnet-level NSG with NIC-level NSG may complicate troubleshooting
  - Forgetting to save screenshots before cleanup may remove proof needed for documentation
  - Exposing credentials in notes or chat creates security risk
  - Local network restrictions may be mistaken for Azure-side blocking
  - Deleting the wrong resource group may remove unrelated resources
  - Mitigation:
    - Add `allow-ssh` before baseline testing
    - Initially set `allow-ssh` to priority `100`
    - During deny-rule testing, edit `allow-ssh` to priority `110`
    - Set `deny-ssh` priority to `100`
    - Keep NIC network security group as `None`
    - Save screenshots before deleting resources
    - Delete the whole lab resource group after completion
    - Wait briefly after NSG changes before retesting

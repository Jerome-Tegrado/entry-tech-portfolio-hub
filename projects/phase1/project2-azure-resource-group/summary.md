# Summary

## Project Information
- Project Name: NSG Blocking Lab
- Project ID: Phase 2 Project 1
- Date: March 26, 2026

## Objective
The goal of this activity was to build a simple Azure networking lab that demonstrates how a Network Security Group can control VM connectivity at the subnet level. The lab aimed to prove a clean before, fail, and restore flow by first allowing SSH access, then blocking it with a deny rule, and finally restoring access by removing that rule.

## Scope
- In Scope:
  - Create a resource group, virtual network, subnet, network security group, public IP, and virtual machine
  - Associate the NSG to the subnet
  - Test SSH access to the Ubuntu VM
  - Add and remove NSG rules to prove access control behavior
  - Capture screenshots as evidence
  - Clean up lab resources after completion
- Out of Scope:
  - Application Security Groups
  - Multi-VM architecture
  - NIC-level NSG as the main filtering design
  - Load balancers, Bastion, or DDoS protection
  - Production-grade hardening and long-term security design

## Environment
- Platform/Cloud: Microsoft Azure
- Region: Southeast Asia
- Account/Subscription (non-sensitive): Personal Azure subscription
- Tools Used:
  - Azure Portal
  - Windows PowerShell
  - SSH client

## Work Completed
1. Created the core lab resources, including the resource group, VNet, subnet, NSG, public IP, and Ubuntu virtual machine.
2. Configured subnet-level NSG behavior by adding an allow SSH rule for baseline testing, then modifying rule priority and adding a deny SSH rule for blocking validation.
3. Validated the full connectivity flow by confirming SSH success before blocking, SSH failure during deny enforcement, and SSH success again after removing the deny rule.

## Key Results
- Successfully deployed a working Azure VM inside `vnet-p2p1` and `subnet-workload`
- Confirmed that subnet-level NSG rules directly affected inbound SSH connectivity to the VM
- Proved the full access-control flow: baseline success, intentional failure, and restored success

## Evidence
- Screenshot(s):
  - VM creation and configuration
  - Networking tab showing `vnet-p2p1` and `subnet-workload`
  - Allow SSH rule
  - Baseline SSH success
  - Deny SSH rule
  - SSH timeout after deny rule
  - Final SSH success after removing deny rule
- Command output(s):
  - `ssh jerome@135.171.176.24`
- Diagram(s):
  - Accomplished

## Issues Encountered
- Issue:
  - Initial SSH test timed out before baseline validation
  - Resolution:
    - Added an `allow-ssh` inbound NSG rule so SSH traffic could reach the VM for baseline testing
- Issue:
  - Deny rule could not override the allow rule when both priorities conflicted
  - Resolution:
    - Edited `allow-ssh` from priority `100` to `110`, then created `deny-ssh` at priority `100` so the deny rule would take precedence

## Lessons Learned
- A VM is placed into a VNet and subnet through its NIC, which is automatically created and attached during VM creation
- A public IP is different from the subnet placement; it provides internet-facing access but does not place the VM into the VNet
- NSG priority order matters because lower numbers are processed first
- Subnet-level NSG is a clean and beginner-friendly way to demonstrate traffic filtering in Azure
- Baseline connectivity should always be confirmed first before testing an intentional failure scenario

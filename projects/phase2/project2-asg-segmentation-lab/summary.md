# Summary

## Project Information
- Project Name: ASG Segmentation Lab
- Project ID: Phase 2 — Project 2
- Date: March 29, 2026

## Objective
The goal of this activity was to build and validate an Azure network segmentation lab using Application Security Groups and Network Security Group rules. The project aimed to prove that intended frontend-to-backend HTTP traffic is allowed while unintended SSH traffic is blocked through explicit security configuration.

## Scope
- In Scope:
  - Creation of the Azure lab resource group, VNet, subnet, frontend VM, backend VM, NSG, and ASGs
  - Configuration of ASG-based NSG rules for allowed and blocked traffic paths
  - Installation of `nginx` on the backend VM for HTTP validation
  - Validation of frontend-to-backend HTTP access on port 80
  - Validation of blocked frontend-to-backend SSH access on port 22
- Out of Scope:
  - Public internet exposure testing as a required success criterion
  - Production hardening or long-term deployment
  - Advanced routing, peering, VPN, or Bastion-based access design

## Environment
- Platform/Cloud: Microsoft Azure
- Region: Southeast Asia
- Account/Subscription (non-sensitive): Active Azure subscription used for temporary lab testing
- Tools Used:
  - Azure Portal
  - Azure VM Run Command
  - `curl`
  - `nginx`
  - `netcat` :contentReference[oaicite:1]{index=1}

## Work Completed
1. Created the Azure lab resources for the ASG segmentation setup, including the resource group, virtual network, subnet, frontend VM, backend VM, NSG, and frontend/backend ASGs.
2. Configured segmentation wiring by associating the NSG to the subnet, assigning NICs to ASGs, and creating an allow rule for frontend-to-backend HTTP traffic on port 80.
3. Installed and validated `nginx` on the backend VM, confirmed allowed HTTP connectivity from frontend to backend, and added a deny rule to block SSH traffic on port 22 for stronger segmentation proof.

## Key Results
- The backend VM successfully hosted a working `nginx` service for HTTP validation.
- The frontend VM successfully reached the backend VM on port 80 using the backend private IP `10.20.1.5`.
- The frontend VM could not reach the backend VM on port 22 after the deny rule was applied, confirming blocked unintended traffic. 

## Evidence
- Screenshot(s):
  - `resource-group.png`
  - `vnet-subnet.png`
  - `nsg.png`
  - `asg-frontend.png`
  - `asg-backend.png`
  - `vm-frontend.png`
  - `vm-backend.png`
  - `vm-asg-frontend.png`
  - `vm-asg-backend.png`
  - `nsg-associate-subnet.png`
  - `nsg-rule-allow-frontendtobackend-http.png`
  - `success-frontend-backend-connection.png`
  - `nsg-rule-deny-port22.png`
  - `denied-port22.png`
- Command output(s):
  - `curl http://localhost`
  - `curl http://10.20.1.5`
  - `nc -zvw 5 10.20.1.5 22`
- Diagram(s):
  - Accomplished

## Issues Encountered
- Issue:
  - Azure’s default `AllowVnetInBound` rule can still allow same-VNet traffic if no explicit deny rule blocks it.
  - Resolution:
    - An explicit deny validation was added on port 22 to provide stronger proof that unintended traffic was blocked.

- Issue:
  - Private `.pem` key files may be accidentally uploaded to a public repository.
  - Resolution:
    - The project notes established that `.pem` files should not be uploaded, `*.pem` and `*.key` should be added to `.gitignore`, and previously exposed old keys should not be reused. :contentReference[oaicite:5]{index=5}

## Lessons Learned
- ASG-based grouping makes NSG rules easier to manage than relying only on direct IP-based rules.
- Successful local service validation does not automatically prove public or cross-machine reachability; path-specific testing is still required.
- Stronger segmentation proof often requires both an allowed-path test and an explicit blocked-path test.
- Public IP presence alone does not automatically mean a VM is publicly reachable on a given port.
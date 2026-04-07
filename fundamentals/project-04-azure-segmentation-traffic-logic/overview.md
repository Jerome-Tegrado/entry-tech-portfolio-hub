# Overview

## Project Information
- Track: Fundamentals
- Project Number: 04
- Project Name: ASG Segmentation Lab
- Status: Completed
- Label: Fundamentals - Azure Segmentation and Traffic Logic
- Date: March 2026

## What This Project Proves
- Cleaner traffic control design with ASGs
- Service segmentation understanding in Azure networking
- Architecture reasoning for allow-path versus blocked-path validation
- Support-aware network logic with explicit deny checks

## Environment
- Microsoft Azure (Southeast Asia)
- Azure Portal
- Azure VM Run Command
- Commands/tools: `curl`, `nginx`, `nc`

## Outcome Summary
Validated allowed frontend-to-backend HTTP on port 80 and blocked frontend-to-backend SSH on port 22 using ASG-targeted NSG rules.

## Evidence
- `evidence/success-frontend-backend-connection.png`
- `evidence/denied-port22.png`
- `evidence/nsg-rule-allow-frontendtobackend-http.png`
- `evidence/nsg-rule-deny-port22.png`
- `diagrams/asg-segmentation-lab-diagram.drawio.png`


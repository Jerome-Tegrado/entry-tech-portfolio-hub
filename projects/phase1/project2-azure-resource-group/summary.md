# Summary

## Project Information
- Project Name: Azure Setup + Cleanup Proof
- Project ID: Phase 1 Project 2
- Date: 2026-03-20

## Objective
The goal of this activity was to perform a simple Azure resource setup and cleanup task as beginner cloud proof. The project focused on creating a resource group and storage account, validating that the deployment worked, capturing evidence, and then removing the resources responsibly.

## Scope
- In Scope:
  - Create one Azure resource group
  - Use Azure Cloud Shell
  - Create one Azure Storage Account
  - Capture setup evidence
  - Delete the resource group and included resource
  - Capture cleanup evidence
  - Document setup and cleanup actions
- Out of Scope:
  - Advanced Azure networking
  - IAM or role configuration changes
  - Monitoring, alerting, or logging setup
  - Production workload deployment
  - Multi-resource architecture

## Environment
- Platform/Cloud: Microsoft Azure
- Region: Southeast Asia
- Account/Subscription (non-sensitive): Azure subscription 1
- Tools Used: Azure Portal, Azure Cloud Shell, Azure CLI, Resource Groups, Storage Account

## Work Completed
1. Created the resource group `rg-project2-azure-setup` in Azure.
2. Used Azure Cloud Shell and created the storage account `storageproject02`.
3. Captured setup evidence, removed the resource group, and verified cleanup completion.

## Key Results
- Successfully created and validated a resource group and storage account in Azure.
- Captured proof of both setup and cleanup for project documentation.
- Completed the activity with cleanup discipline to avoid leaving unused cloud resources running.

## Evidence
- Screenshot(s):
  - `evidence/Resource_Group.png`
  - `evidence/Storage_Account_Overview.png`
  - `evidence/Pre-Deletion.png`
  - `evidence/Deleted.png`
- Command output(s):
  - `az group list --output table`
- Diagram(s):
  - None

## Issues Encountered
- Issue: No major issue encountered during setup or cleanup
  - Resolution: Not applicable

## Lessons Learned
- A resource group acts as a logical container that helps organize and manage related Azure resources.
- The Storage Account Overview page is stronger proof of successful deployment than only pre-creation or review screens.
- Cleanup is an important part of cloud work because it shows cost awareness and responsible resource handling.
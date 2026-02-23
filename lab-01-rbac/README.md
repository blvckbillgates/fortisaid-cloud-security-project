# Lab 01: Azure RBAC Walkthrough - Users + Groups + Group-Based RBAC (Portal, PowerShell, Bash)

## What I Built
A proof-of-concept showing how to:  
1. Create users and groups in Microsoft Entra ID.  
2. Assign users to groups.  
3. Assign an Azure RBAC role to a group (not a user).  
4. Verify effective access at a resource group scope (FortisAid-Lab, East US).  

Built to demonstrate least privilege and reduce permission sprawl by using group-based access control.

## Target Architecture (What I Intended)
Users:  
- Emmanuel Tobi (Senior Admin)  
- Tobi Babalola (Junior Admin)  
- Eneattah Grace (Service Desk)  

Groups:  
- Senior Admins  
- Junior Admins  
- Service Desk  

RBAC:  
- Assign Virtual Machine Contributor → to Service Desk group  
- Scope: Resource Group FortisAid-Lab  

## Step-by-Step Guide
Full details in PDF – here are highlights with code.  

### Create Users and Groups
Portal: Entra ID > Users > New user.  

PowerShell (scripts/create-users.ps1):  
```powershell
New-AzureADUser -DisplayName "Emmanuel Tobi" -UserPrincipalName "emmanuel.tobi@domain.com" -Password "P@ssw0rd"  
# Repeat for others  

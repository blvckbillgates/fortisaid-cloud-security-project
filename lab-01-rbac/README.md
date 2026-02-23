# Lab 01: Azure RBAC Walkthrough: Users + Groups + Group-Based RBAC (Portal, PowerShell, Bash)

## What I Built
A proof-of-concept showing how to:  
1. Create users and groups in Microsoft Entra ID  
2. Assign users to groups  
3. Assign an Azure RBAC role to a group (not a user)  
4. Verify effective access at a resource group scope (FortisAid-Lab, East US)  

Built to demonstrate least privilege and reduces permission sprawl by using group-based access control.

## Step 0: Target Architecture (What I Intended)
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
- Portal: Entra ID > Users > New user for each.  
- PowerShell: New-AzureADUser -DisplayName "Emmanuel Tobi" etc.  
- Bash: az ad user create --display-name "Emmanuel Tobi" etc.  
- Groups: Entra ID > Groups > New group (Security type).  
- Assignments: Add members to groups.  
- RBAC: Resource groups > FortisAid-Lab > IAM > Add role assignment > Role: Virtual Machine Contributor > Assign to group.  

Verification: az role assignment list --resource-group FortisAid-Lab  
 
## Outcomes
- Scalable access control.  

## Key Learnings
- Group-based RBAC for least privilege.  

## Extensions
- Automate with scripts/create-users.ps1.  

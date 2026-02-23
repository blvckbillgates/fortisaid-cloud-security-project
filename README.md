# FortisAid Cloud Security Engineering Portfolio

## Medium Links
https://medium.com/@tobibabalola21
## LinkedIn
https://www.linkedin.com/in/tobi-babalola001/

## Overview
This repo showcases 9 AZ-500 labs demonstrating cloud security skills in Azure. Each lab folder includes:  
- README.md: Objectives, architecture, step-by-step guides, challenges, learnings, extensions.  
- PDF: Original lab document (e.g., AZ500 LAB 1.pdf).  
- Screenshots/visuals are in my Medium posts (linked in each README)
- scripts/: Code/scripts from PDF (e.g., az commands as .ps1 files).  
- configs/: Config files if applicable (e.g., YAML/JSON).  

Labs use Azure. Reproduce with az CLI/PowerShell.

## Tech Stack
- Azure CLI, PowerShell  
- Bicep/ARM, YAML (Kubernetes)  
- KQL (Queries)  
- Azure Portal, Defender, Sentinel  

## Lab Index

| Lab # | Topic | Key Skills 
|-------|-------|------------
| 01 | Azure RBAC Walkthrough: Users + Groups + Group-Based RBAC (Portal, PowerShell, Bash) | Entra ID users/groups, assignments, RBAC to group, verification 
| 02 | Network Security Groups and Application Security Groups (NSG + ASG) | VNet/subnet setup, ASG grouping, NSG for inbound least-privilege 
| 03 | Azure Firewall – Controlled Egress Architecture | Firewall deployment, route tables, L7 filtering (Bing/DNS allow), validation
| 04 | Configuring and Securing Azure Container Registry (ACR) and Azure Kubernetes Service (AKS) | ACR build/push, AKS deploy (free tier), managed identity RBAC, LoadBalancers 
| 05 | Securing Azure Storage with Virtual Network Service Endpoints | Endpoints enablement, storage restrictions, VM validation, SMB mount 
| 06 | Azure Monitor Agent (AMA) – Enterprise Monitoring & Security Telemetry Architecture | RG/LAW/VM setup, DCRs for telemetry, KQL investigation, SIEM foundation 
| 07 | Microsoft Defender for Servers Plan 2 – Agentless Enterprise Protection Architecture | Subscription enablement, FIM/JIT, workspace integration, agentless validation 
| 08 | Just-in-Time (JIT) VM Access – Attack Surface Reduction via Dynamic NSG Enforcement | JIT enablement, NSG injection/removal, brute-force reduction 
| 09 | Microsoft Sentinel SIEM & SOAR Implementation | Sentinel onboarding, Activity ingestion, detection rules, playbook escalation 

 

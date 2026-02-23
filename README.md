# FortisAid Cloud Security Engineering Portfolio

# OVERVIEW

This repository documents the design and implementation of security controls within a simulated healthcare organisation, FortisAid.

FortisAid represents a cloud-native environment handling sensitive patient and operational data, requiring strong identity protection, network isolation, workload hardening, telemetry visibility, and rapid threat detection.

The goal of this portfolio is not to demonstrate isolated lab completion, but to showcase how security controls are layered together to reduce risk across an end-to-end Azure environment.

Each lab reflects a realistic security engineering decision that contributes to a broader defence-in-depth strategy.

# About FortisAid

FortisAid is a fictional healthcare platform used to simulate enterprise cloud security challenges such as:

* Protection of sensitive patient data

* Controlled administrative access to critical workloads

* Reduction of lateral movement across virtual networks

* Secure container deployment pipelines

* Continuous workload monitoring and posture assessment

* Threat detection and automated incident response

ThiS also reflects my growth toward **cloud security engineer and security platform roles**
Labs use Azure. 

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

 
## Medium Links
https://medium.com/@tobibabalola21
## LinkedIn
https://www.linkedin.com/in/tobi-babalola001/

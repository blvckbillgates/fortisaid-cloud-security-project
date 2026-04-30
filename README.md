# FortisAid Cloud Security Project

## Overview
This repository documents the design and implementation of layered security
controls within **FortisAid**, a simulated cloud-native healthcare organisation
handling sensitive patient and operational data.

The project is not a collection of isolated labs. Each lab represents a
deliberate security engineering decision — identity protection, network
isolation, workload hardening, telemetry visibility, and automated threat
response — that together form a defence-in-depth strategy across an end-to-end
Azure environment.

> **Every lab has a dedicated write-up explaining the *why*, not just the *how*.**

## About FortisAid
FortisAid is a fictional healthcare platform used to simulate enterprise cloud
security challenges:

- Protection of sensitive patient data (PHI)
- Controlled administrative access to critical workloads
- Reduction of lateral movement across virtual networks
- Secure container deployment pipelines
- Continuous workload monitoring and posture assessment
- Threat detection and automated incident response

This project also reflects my progression toward **cloud security engineer**
and **security platform** roles.

All labs are built on **Microsoft Azure**.

## Tech Stack
- **Infrastructure & Config:** Azure CLI, PowerShell, Bicep/ARM, YAML (Kubernetes)
- **Query & Detection:** KQL (Kusto Query Language)
- **Platform:** Azure Portal, Microsoft Defender for Cloud, Microsoft Sentinel

## Design Philosophy
Every lab answers a specific security question:

| Lab | Security Question |
|:---|:---|
| 01 – RBAC | How do we assign least-privilege access at scale using groups? |
| 02 – NSG + ASG | How do we micro-segment workloads and reduce lateral movement? |
| 03 – Azure Firewall | How do we control egress traffic and prevent data exfiltration? |
| 04 – ACR + AKS | How do we secure container images and control cluster access? |
| 05 – Storage Endpoints | How do we isolate storage accounts from the public internet? |
| 06 – AMA + DCR | How do we build a telemetry pipeline that feeds a SIEM? |
| 07 – Defender Plan 2 | How do we deploy agentless protection (FIM, JIT, vulnerability scanning)? |
| 08 – JIT Access | How do we eliminate standing administrative access to VMs? |
| 09 – Sentinel | How do we build detection rules and automated incident response? |

## Lab Index & Write-Ups

### [01 – Designing Least-Privilege Access in Azure (RBAC)](https://medium.com/@tobibabalola21/designing-least-privilege-access-in-azure-users-groups-group-based-rbac-fortisaid-lab-1-44888cac7ca5)
**Key skills:** Entra ID users/groups, role assignments, group-based RBAC, verification

### [02 – Network Segmentation with NSGs and ASGs](https://medium.com/@tobibabalola21/network-segmentation-with-nsgs-and-asgs-fortisaid-lab-02-983dc6308cc8)
**Key skills:** VNet/subnet setup, ASG grouping, NSG for inbound least-privilege

### [03 – Controlled Egress with Azure Firewall and Forced Routing](https://medium.com/@tobibabalola21/controlled-egress-with-azure-firewall-and-forced-routing-fortisaid-lab-03-67e1342d1378)
**Key skills:** Firewall deployment, route tables, L7 filtering (Bing/DNS allow), validation

### [04 – Securing Container Supply Chains with ACR and AKS](https://medium.com/@tobibabalola21/securing-container-supply-chains-with-acr-and-aks-fortisaid-lab-04-3cdbbd72a174)
**Key skills:** ACR build/push, AKS deploy (free tier), managed identity RBAC, LoadBalancers

### [05 – Storage Network Isolation with Service Endpoints](https://medium.com/@tobibabalola21/storage-network-isolation-with-service-endpoints-fortisaid-lab-05-5cb37e7d2a87)
**Key skills:** Endpoints enablement, storage restrictions, VM validation, SMB mount

### [06 – Building Security Telemetry with AMA and Data Collection Rules](https://medium.com/@tobibabalola21/building-security-telemetry-with-ama-and-data-collection-rules-fortisaid-lab-06-f651b875a68d)
**Key skills:** RG/LAW/VM setup, DCRs for telemetry, KQL investigation, SIEM foundation

### [07 – Agentless Workload Protection with Defender for Servers Plan 2](https://medium.com/@tobibabalola21/agentless-workload-protection-with-defender-for-servers-plan-2-fortisaid-lab-07-6bc03478bcef)
**Key skills:** Subscription enablement, FIM/JIT, workspace integration, agentless validation

### [08 – Reducing Administrative Exposure with Just-in-Time VM Access](https://medium.com/@tobibabalola21/reducing-administrative-exposure-with-just-in-time-vm-access-fortisaid-lab-08-0145e85f7704)
**Key skills:** JIT enablement, NSG injection/removal, brute-force reduction

### [09 – Building a Cloud SOC with Microsoft Sentinel](https://medium.com/@tobibabalola21/building-a-cloud-soc-with-microsoft-sentinel-fortisaid-lab-09-33303e0199fe)
**Key skills:** Sentinel onboarding, Activity ingestion, detection rules, playbook escalation

## What This Project Demonstrates
- Cloud security engineering with a defence-in-depth mindset
- Translating healthcare compliance requirements into Azure-native controls
- Working across identity, network, container, storage, and SIEM domains
- Communicating technical decisions in writing (each lab has a public post)

## Related Projects
- [FortisAid GRC Policy Sprint](https://github.com/blvckbillgates/fortisaid-grc-policy-sprint)
- [FortisAid Cyber Threat Intelligence Sprint](https://github.com/blvckbillgates/fortisaid-cti-sprint)

## Connect
- **Medium:** [@tobibabalola21](https://medium.com/@tobibabalola21)
- **LinkedIn:** [Tobi Babalola](https://www.linkedin.com/in/tobi-babalola001/)

## Confidentiality
FortisAid is a fictional organisation. All lab configurations and documentation are
original educational work.

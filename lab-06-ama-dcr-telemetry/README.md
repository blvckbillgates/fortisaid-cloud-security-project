**Lab 06 — Azure Monitor Agent (AMA) + Data Collection Rules Telemetry Architecture**

 **Objectives**

This lab implements a centralized monitoring architecture using Azure Monitor Agent (AMA) and Data Collection Rules (DCRs) to provide security visibility and operational telemetry for virtual machines.

The goals were to:

* Deploy centralized telemetry ingestion

* Implement policy-driven monitoring using DCRs

* Enable log-based investigation using KQL

* Validate telemetry ingestion and pipeline integrity

 **Environment**

* Region: West US 2

* Monitoring Resource Group: AZ500LAB131415

* Monitored VM: AZ500LAB131415

* Log Analytics Workspace: lgawIgnite

* Storage Account: strgactignitetobi

**Architecture Diagram**

Add architecture diagram placeholder

Suggested diagram:
VM → Azure Monitor Agent → Data Collection Rule → Log Analytics Workspace → Security investigation

 **Step-by-Step Walkthrough**

**Step 1** — Create Monitoring Resource Group

Provisioned a dedicated resource group to isolate monitoring infrastructure.

**Step 2** — Deploy Monitored Virtual Machine

Provisioned a Windows Server VM used to generate telemetry.

Operational constraints encountered:

* Regional SKU limitations

* Core quota restrictions

Deployment parameters were adjusted accordingly.

**Step 3** — Create Log Analytics Workspace

Created a centralized telemetry repository to store and query monitoring data.

Purpose:

* Performance monitoring

* Log investigation

* Future SIEM integration

**Step 4** — Deploy Supporting Storage Account

Provisioned storage to support monitoring infrastructure.

Noted constraint: Storage account names must be globally unique.

 **Configure AMA + DCR Telemetry Pipeline**
 
**Step 5** — Create Data Collection Rule (DCR)

Configured policy-driven telemetry routing.

* Platform: Windows

* Data sources: CPU, Memory, Disk, Network performance counters

* Collection frequency: 60 seconds

* Destination: Log Analytics Workspace

This separates telemetry policy from workload configuration.

**Step 6** — Generate Runtime Activity

Connected to the VM via RDP and generated system activity to ensure telemetry capture.

**Step 7** — Validate Telemetry Using KQL

```kql
Perf
| take 10
```

Observed initial ingestion delay, then confirmed telemetry visibility after activity generation and time range adjustment.

**Challenges & Resolutions**

**Issue** — Telemetry ingestion delay

Initial queries returned no data.

Resolution:
Generated workload activity and adjusted query time range to allow ingestion pipeline completion.

**Issue** — SKU and quota constraints

Deployment required adjusting VM configuration to match regional availability.

✅ Outcomes

* Centralized telemetry successfully configured

* Policy-driven monitoring implemented

* Performance data visible in Log Analytics

* Telemetry pipeline integrity validated

 **Key Learnings**

* AMA separates monitoring logic from VM configuration

* DCR enables scalable and consistent telemetry onboarding

* Telemetry ingestion delay is expected behavior

* Centralized logging reduces security blind spots

 **Extensions**

* Integrate AMA telemetry with Microsoft Sentinel

* Expand DCR coverage to security event logs

* Implement alert rules based on performance anomalies

* Add Defender for Cloud signal correlation

For screenshots and growth reflections, see my Medium post [link]

**Lab 09 — Microsoft Sentinel SIEM + SOAR Detection Pipeline**
 
 **Objectives**

This lab implements an end-to-end cloud SOC workflow by onboarding Microsoft Sentinel, ingesting Azure Activity logs, creating detection rules, and automating incident response using a SOAR playbook.

The goals were to:

* Deploy Sentinel on an existing Log Analytics Workspace

* Ingest Azure Activity telemetry

* Create detection analytics rules

* Build an automated incident severity escalation playbook

* Validate detection and automated response behavior

 **Environment**

* Resource Group: FortisAid-Lab05

* Log Analytics Workspace: FortisAid-LAW

* Detection Source: Azure Activity Logs

* SOAR Engine: Logic Apps

 **Architecture Diagram**

Add architecture diagram placeholder

Suggested diagram:
Azure Activity Logs → Log Analytics → Sentinel Analytics Rule → Incident → SOAR Playbook → Severity escalation

 **Step-by-Step Walkthrough**

**Step 1** — Onboard Microsoft Sentinel

Enabled Sentinel on the existing Log Analytics Workspace and confirmed workspace linkage.

**Step 2** — Connect Azure Activity Logs

Installed Azure Activity connector and assigned policy to stream subscription activity logs into the workspace.

Observed initial policy propagation delay before telemetry appeared.

**Step 3** — Validate Log Ingestion

Confirmed Activity logs appeared in the workspace.

```kql
AzureActivity
| take 10
```

This validated telemetry availability for detection engineering.

 **Detection Engineering**
**Step 4** — Deploy Built-in Detection Rule

Enabled the rule detecting suspicious resource creation or deployment behavior.

Verified the rule appeared under active analytics rules and generated incidents during testing.

 **SOAR Automation**
**Step 5** — Create Playbook

Deployed a Logic App playbook that updates incident severity.

The workflow:

* Sentinel incident trigger

* Update incident action

* Severity set to High

**Step 6** — Create Custom Detection Rule

```kql
AzureActivity
| where ResourceProviderValue =~ "Microsoft.Security"
| where OperationNameValue =~ "Microsoft.Security/locations/jitNetworkAccessPolicies/delete"
```

Configured rule to:

* Run every 5 minutes

* Create incidents

* Attach automation rule to trigger the playbook

**Step 7** — Trigger Detection and Validate Response

Removed a JIT policy to generate a telemetry event.

Validated:

* Sentinel incident creation

* Playbook execution

* Automatic severity escalation

 **Challenges & Resolutions**
**Issue** — Azure Activity ingestion delay

Telemetry initially absent after connector deployment.

**Resolution**:
Waited for policy remediation cycle and verified connector status.

**Issue** — Analytics rule returning zero results

**Resolution**:
Adjusted query time range and allowed ingestion delay.

**Issue** — SOAR execution permission failure

**Resolution**:
Verified RBAC scope for Logic App Sentinel connector.

 **Outcomes**

* Sentinel successfully onboarded

* Azure Activity logs ingested and queryable

* Detection rules generated incidents

* SOAR playbook executed automatically

* Incident severity escalation validated

 **Key Learnings**

* Detection reliability depends on telemetry ingestion timing

* Sentinel automation requires correct RBAC scope

* Playbooks enable rapid incident response without manual intervention

* SOC effectiveness depends on correlation between telemetry, detection, and automation

 **Extensions**

* Integrate Defender alerts into Sentinel correlation rules

* Build anomaly-based KQL detection rules

* Add automated notification workflows

* Implement incident triage playbooks

For screenshots and growth reflections, see my Medium post [link]

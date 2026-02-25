**Lab 07 — Defender for Servers Plan 2 (Agentless Workload Protection)**

 **Objectives**

This lab enables Microsoft Defender for Servers Plan 2 and validates modern agentless workload protection capabilities across the FortisAid environment.

The goals were to:

* Enable Defender Plan 2 at subscription scope

* Validate VM protection state and recommendations

* Configure File Integrity Monitoring (FIM)

* Implement Just-in-Time access prerequisites

* Confirm agentless security architecture

 **Environment**

* Region: West US 2

* Resource Group: fortisaid-lab05

* Protected VM: FortisAid-VM-Private05

* Log Analytics Workspace: FortisAid-LAW

 **Architecture Diagram**

Add architecture diagram placeholder

Suggested diagram:
VM → Defender control plane → Agentless scanning + FIM → Security recommendations

 **Step-by-Step Walkthrough**

**Step 1** — Enable Defender Plan 2

Opened Defender for Cloud and enabled Servers Plan 2 at subscription level.

This activated workload protection features including vulnerability assessment, FIM, and JIT integration.

**Step 2** — Validate VM Protection State

Confirmed:

* VM running

* VM visible in Defender Inventory

* Security recommendations populated

This verified Defender recognition of the workload.

 **Configure File Integrity Monitoring**
**Step 3** — Enable FIM

Configured File Integrity Monitoring and bound the workspace.

This enabled monitoring of sensitive system file changes and established investigation visibility.

 **Prepare for JIT Access**
**Step 4** — Confirm JIT Eligibility

Validated VM readiness for Just-in-Time configuration:

* NSG attached

* Workspace integrated

* Defender inventory visibility

 **Validate Agentless Architecture**
**Step 5** — Confirm No Guest Extension Required

Verified that Azure Monitor Agent was not installed on the VM.

This confirmed modern Defender Plan 2 capabilities operate using control-plane agentless scanning.

**Challenges & Resolutions**
**Issue** — Expectation of AMA requirement

Initial assumption was that Defender Plan 2 required Azure Monitor Agent installation.

**Resolution**:
Validated that modern Defender Plan 2 supports agentless scanning for vulnerability assessment and FIM.

**Issue** — Defender inventory delay

VM did not appear immediately in inventory.

**Resolution**:
Allowed Defender evaluation cycle to complete and refreshed inventory view.

 **Outcomes**

* Defender Plan 2 successfully enabled

* VM protection state validated

* File Integrity Monitoring configured

* Agentless security architecture confirmed

 **Key Learnings**

* Modern Defender protection does not rely on guest extensions

* Agentless scanning reduces operational overhead and deployment friction

* Defender recommendations provide continuous posture visibility

* Control-plane protection is a critical security evolution


For screenshots and growth reflections, see my Medium post [link]

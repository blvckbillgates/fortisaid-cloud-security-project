**Lab 08 — Just-in-Time VM Access (Dynamic Attack Surface Reduction)**

 **Objectives**

This lab implements Just-in-Time (JIT) VM access using Microsoft Defender for Cloud to eliminate permanently exposed management ports and enforce time-bound, IP-restricted administrative access.

The goals were to:

* Remove permanently open RDP/SSH ports

* Restrict administrative access to approved IPs

* Validate dynamic NSG rule injection and removal

* Reduce brute-force and lateral movement exposure

 **Environment**

* Region: West US 2

* Resource Group: fortisaid-lab05

* VM: FortisAid-VM-Private05

* Defender Plan: Servers Plan 2 (enabled)

 **Architecture Diagram**

Add architecture diagram placeholder

Suggested diagram:
Admin → JIT request → Defender control plane → Temporary NSG rule → VM access → Rule removed

 **Step-by-Step Walkthrough**

**Step 1** — Open JIT Configuration

Navigated to Defender for Cloud workload protections and opened the Just-in-Time VM access blade.

Confirmed VM appeared under Not Configured.

**Step 2** — Enable JIT on the VM

Configured JIT parameters:

* Port: 3389 (RDP)

* Protocol: TCP

* Allowed source: Current public IP

* Maximum duration: 1 hour

Saved configuration and confirmed VM moved to Configured.

**Step 3** — Request Temporary Access

Submitted an access request specifying:

* Management port

* Requestor IP

* Access duration

Confirmed request approval.

**Step 4** — Validate NSG Rule Injection

Verified that Defender dynamically created a temporary inbound NSG rule allowing access only from the approved IP within the configured time window.

**Step 5** — Confirm Automatic Rule Removal

After the access window expired, refreshed NSG inbound rules and confirmed the temporary rule was automatically removed.

This validated automatic attack surface restoration.

 **Challenges & Resolutions**

**Issue** — Confusion between legacy and modern configuration paths

Older documentation referenced VM configuration blade.

**Resolution**:
Used modern Defender control-plane configuration path.

**Issue** — Assumption that AMA was required

**Resolution**:
Confirmed JIT enforcement operates agentlessly through dynamic NSG rule manipulation.

 **Outcomes**

* Management ports were no longer permanently exposed

* Temporary access enforced with IP and time restrictions

* Automatic NSG rule lifecycle validated

* Attack surface significantly reduced

 **Key Learnings**

* JIT is a control-plane security enforcement mechanism

* Dynamic NSG manipulation reduces operational exposure

* Time-bound access is critical for zero-trust administrative security

* Removing persistent management ports dramatically reduces brute-force risk

 **Extensions**

* Combine JIT with PIM for privileged session elevation

* Enable JIT alerting and audit logging

* Integrate JIT access events with Sentinel detection rules

* Expand JIT protection across additional workloads

For screenshots and growth reflections, see my Medium post [link]

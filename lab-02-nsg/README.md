**Lab 02 — NSG Network Segmentation
 Objectives**

This lab implements network segmentation using Network Security Groups (NSGs) to restrict lateral movement between workloads and enforce controlled communication inside the FortisAid virtual network.

The goals were to:

* Enforce workload isolation

* Control east-west traffic

* Understand NSG rule evaluation order

* Reduce lateral movement attack surface

** Architecture Diagram**

Add architecture diagram placeholder

Suggested diagram:
Web VM → App VM → DB VM with NSG filtering between tiers

** Step-by-Step Walkthrough
Step 1 **— Create Network Security Group

* Created an NSG to control inbound and outbound traffic.

```bash
az network nsg create
--name FortisAid-NSG
--resource-group <rg>
--location <region>
```
  
**Step 2** — Associate NSG to Subnet or NIC

* Applied the NSG to the workload subnet to enforce centralized filtering.

**Step 3 **— Create Segmentation Rules

* Configured rules allowing only required communication between workloads.

```bash
az network nsg rule create
--name allow-web
--priority 100
--access Allow
--direction Inbound
```
  
**Step 4 **— Validate Traffic Behavior

* Tested connectivity between workloads to confirm:

* Allowed communication succeeded

* Unauthorized traffic was blocked

* NSG rules enforced as expected

 **Challenges & Resolutions**

* Unexpected traffic allowed

* Observed that default NSG rules can override segmentation intent.

**Resolution**:
* Reviewed default rules and adjusted custom rule priority.

 **Outcomes**

* Segmentation successfully enforced

* Lateral movement exposure reduced

* Traffic policy clearly validated

 **Key Learnings**

* NSG rule priority is critical to enforcement

* Default rules must be considered during segmentation design

* Network segmentation is foundational for zero-trust architecture

 

For screenshots and growth reflections, see my Medium post [link]

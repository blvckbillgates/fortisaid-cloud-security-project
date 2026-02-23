**Lab 03 — Azure Firewall Controlled Egress** 

 **Objectives**

This lab implements centralized outbound inspection using Azure Firewall to restrict internet access and enforce application-layer filtering.

The goals were to:

* Force outbound traffic through Azure Firewall

* Allow only approved external destinations

* Block unauthorized outbound traffic

* Validate routing-based inspection enforcement

 **Architecture Diagram**

Add architecture diagram placeholder

Suggested diagram:
Workload subnet → Route Table → Azure Firewall → Internet

 **Step-by-Step Walkthrough**

**Step 1** — Deploy Firewall

```bash
az network firewall create
--name FortisAid-FW01
--resource-group <rg>
--location <region>
```

**Step 2** — Create Route Table

```bash
az network route-table create
--name FortisAid-RT
--resource-group <rg>
```

**Step 3** — Force Traffic Through Firewall

```bash
az network route-table route create
--name default-route
--address-prefix 0.0.0.0/0
--next-hop-type VirtualAppliance
```

**Step 4** — Configure Application Filtering

```bash
az network firewall application-rule create
--name allow-bing
--target-fqdns www.bing.com

```

**Step 5** — Validate Filtering

Tested browsing behavior:

* Bing allowed

* Other sites blocked

* Route enforcement confirmed

 **Challenges & Resolutions**

**Traffic bypass observed**

Initial routing misconfiguration allowed traffic to bypass firewall.

**Resolution**:
Validated route table association with workload subnet.

 **Outcomes**

* Outbound inspection successfully enforced

* Application filtering validated

* Default deny posture confirmed

**Key Learnings**

* Route tables are critical for firewall enforcement

* Application rules enable L7 filtering

* Egress control significantly reduces data exfiltration risk

**Extensions**

* Enable TLS inspection

* Integrate Firewall Policy

* Add DNAT for controlled inbound exposure

For screenshots and growth reflections, see my Medium post [link]

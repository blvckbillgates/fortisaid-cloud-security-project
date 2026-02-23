**Lab 05 — Storage Network Isolation with Service Endpoints**

 **Objectives**

This lab implements network-level protection for Azure Storage by restricting access to approved virtual network subnets using Service Endpoints.

The goals were to:

* Restrict storage access to selected virtual networks

* Validate subnet-based authorization behavior

* Demonstrate that port reachability does not imply access authorization

* Securely mount an Azure File Share from an approved subnet

**Environment**

* Region: West US 2

* Resource Group: fortisaid-lab05

* VNet: fortisaid-vnet05 (10.0.0.0/16)

* Subnets: Public, Private

* Storage Account: fortisaidstorage05

* File Share: fortisaid-files

 **Architecture Diagram**

Add architecture diagram placeholder

Suggested diagram:
Public VM (denied) → Storage Account ← Private VM (allowed via Service Endpoint)

 **Step-by-Step Walkthrough**

**Step 1** — Create Resource Group

```powershell
New-AzResourceGroup -Name fortisaid-lab05 -Location "West US"
```

**Step 2** — Create Virtual Network and Subnets

Configured a VNet with separate Public and Private subnets to validate network authorization behavior.

**Step 3** — Deploy Virtual Machines

* One VM deployed in Public subnet

* One VM deployed in Private subnet

* RDP enabled for testing

**Step 4** — Create Storage Account

Configured storage with secure transfer enabled.

**Step 5** — Create Azure File Share

Created file share named:

fortisaid-files

**Enable Service Endpoint Protection**

**Step 6** — Enable Service Endpoint on Private Subnet

Enabled Microsoft.Storage service endpoint on the Private subnet.

**Step 7** — Restrict Storage to Selected Networks

Configured storage networking:

* Selected networks only

* Added VNet: fortisaid-vnet05

* Allowed subnet: Private

This enforced subnet-based authorization.

 **Validate Network Isolation**

**Step 8** — Test From Public VM (Expected Failure)

Test SMB connectivity:

```powershell
Test-NetConnection fortisaidstorage05.file.core.windows.net -Port 445
```

Port was reachable, but mounting failed.

Attempt mount:

```powershell
net use Z: \fortisaidstorage05.file.core.windows.net\fortisaid-files /user:Azure\fortisaidstorage05
```

Expected result:

Authentication failure (Error 86)

This confirmed subnet-level authorization enforcement.

**Step 9** — Test From Private VM (Expected Success)

```powershell
Test-NetConnection fortisaidstorage05.file.core.windows.net -Port 445
```

Mount succeeded:

```powershell
net use Z: \fortisaidstorage05.file.core.windows.net\fortisaid-files /user:Azure\fortisaidstorage05
dir Z:
```

Directory listing confirmed successful secure access.

 **Challenges & Resolutions**

Confusion between network reachability and authorization

Initial assumption was that open SMB port implied access permission.

Resolution:
Validated that storage enforces subnet identity before allowing authentication.

 **Outcomes**

* Storage restricted to approved subnet

* Public subnet blocked despite valid credentials

* Secure SMB mount achieved from authorized subnet

 **Key Learnings**

* Port reachability does not equal authorization

* Service Endpoints enforce subnet identity

* Storage network rules override valid credentials

* Layered validation is essential for enterprise storage security

 **Extensions**

* Replace Service Endpoints with Private Endpoints

* Integrate storage firewall logging

* Implement identity-based SMB authentication

* Add Defender for Storage threat detection

For screenshots and growth reflections, see my Medium post [link]

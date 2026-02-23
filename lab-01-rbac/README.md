**Lab 01 — Azure RBAC & Least Privilege Enforcement**
**Objectives**

This lab establishes the identity security foundation for the FortisAid environment by implementing Azure Role-Based Access Control (RBAC) and validating least-privilege access boundaries.

The goals were to:

* Understand Azure RBAC scope hierarchy

* Assign roles with minimal privileges

* Validate permission inheritance and effective access

* Prevent privilege escalation through overly broad role assignments


**Architecture Diagram**

Add architecture diagram placeholder

Suggested diagram:
User → RBAC Role Assignment → Resource Group / Resource → Access Decision

**Step-by-Step Walkthrough**
**Step 1** — Identify Access Scope

Selected the appropriate scope for role assignment to avoid unnecessary privilege exposure.

RBAC scope hierarchy considered:

* Subscription

* Resource Group

* Resource

Resource-level scope was preferred to enforce least privilege.

**Step 2** — Assign RBAC Role

Assigned a Reader role to a test identity at the resource scope.

   New-AzRoleAssignment `
  -ObjectId <user-object-id> `
  -RoleDefinitionName Reader `
  -Scope <resource-scope>


**Step 3** — Validate Effective Permissions

Used the Azure Portal Check access feature to confirm:

* Role assignment applied correctly

* No inherited elevated permissions existed

* Resource access matched expected privilege level

**Step 4** — Test Access Boundaries

Attempted administrative actions using the assigned identity to confirm:

* Read operations succeeded

* Write operations were blocked

* Access control enforcement behaved as expected

**Challenges & Resolutions**
Permission inheritance confusion

Observed that inherited permissions from higher scopes can unintentionally elevate access.

**Resolution:**
* Used Effective Access view and limited assignments strictly to resource-level scope.

 Outcomes

* Least-privilege access successfully enforced

* Role assignment boundaries validated

* Identity exposure surface reduced

 **Key Learnings**
* RBAC scope design is critical for minimizing blast radius

* Inherited permissions can silently override security intent

* Resource-level assignments improve isolation and auditability

 Extensions
* Integrate Azure AD Privileged Identity Management (PIM)

* Implement custom RBAC roles      

* Introduce just-in-time role elevation

For screenshots and growth reflections, see my Medium post [link]

# SC-500 Learning Notes: Week 4

## Topic: Enforce Security Governance and Regulatory Compliance (Part 1)

**Scope this week:** the first three modules of the path. The remaining modules are covered in Week 5 (Part 2).


### Key Concepts I Learned

## Azure Policy and Resource Locks

#### Policy effects (what happens when a resource fails evaluation)

| Effect | What it does | When to use it |
|---|---|---|
| Audit | Marks the resource noncompliant in the dashboard, takes no other action | Phase 1 discovery, no disruption |
| Deny | Blocks the create/update request at the ARM layer before the resource exists | Phase 2 enforcement, after remediating existing resources |
| DeployIfNotExists | Checks for a related resource or setting and deploys it automatically if missing | Provisioning configs alongside a resource, e.g. diagnostic settings |
| Modify | Adds, updates, or removes a tag or property at create/update time | Enforcing tagging or default configurations |
| AuditIfNotExists | Like Audit, but evaluates an associated resource rather than the resource itself | Checking a VM has a required extension installed |

**Audit-first rollout pattern:** assign with Audit, review compliance results, communicate findings to app teams, then switch to Deny after remediating existing resources.

#### Scope hierarchy and assignment
- Assignments inherit down the chain: management group, then subscription, then resource group, then resource.
- Assign org-wide baselines at the **management group** scope so new subscriptions inherit them automatically. MCSB is typically assigned at the root management group.
- **Exclusions** carve out justified exceptions (e.g. a sandbox subscription). Use sparingly and document the justification.
- Full evaluation runs every 24 hours. Trigger an on-demand scan with `az policy state trigger-scan --resource-group <rg-name>`.

#### Built-in definitions and initiatives
- Hundreds of built-in definitions maintained by Microsoft. Find them under **Policy > Definitions**, filtered by **Category** (e.g. Security Center, Storage, Key Vault).
- Each definition is JSON specifying evaluation logic, target resource type, and default effect.
- **Initiatives** (policy sets) bundle related definitions into one assignable unit. The **Microsoft Cloud Security Benchmark (MCSB)** initiative covers compute, network, data, identity, and privileged access. Assigning an initiative deploys all related controls together.
- Assign via **Policy > Assignments > + Assign initiative**. Review results under **Policy > Compliance**.

#### Custom policy definitions
- Needed when built-in definitions cannot enforce organization-specific rules (mandatory tags, a specific customer-managed key, a designated Log Analytics workspace).
- **Anatomy:** `mode` (`All` evaluates every resource type including those without tag/location support; `Indexed` evaluates only tag/location-supporting types), `parameters` (always include an `effect` parameter with `allowedValues` so you can toggle audit vs enforce), and `policyRule` (the `if` condition and `then` effect, with `existenceCondition` for the *IfNotExists* effects).
- Author under **Policy > Definitions > + Policy definition**, set the definition location to a management group, and use the **Evaluate** tab to test the rule against a real resource before assigning.

#### Remediation tasks
- DeployIfNotExists and Modify policies identify but do not auto-fix pre-existing resources. A **remediation task** applies the config to existing noncompliant resources.
- Requires a **managed identity** on the assignment with the right RBAC role (e.g. Monitoring Contributor for diagnostic settings, Network Contributor for network rules). Missing the role causes the task to fail with an authorization error.
- Create via **Policy > Remediation > + Remediation task**.

#### Policy exemptions
- **Waiver:** the risk is accepted, no compensating control, leadership signed off.
- **Mitigated:** a compensating control satisfies the same objective through an alternative mechanism.
- Support optional expiration dates that force periodic review. Exemptions stay visible in the compliance view and reports for audit trail.

#### Resource locks

| Lock type | Effect | Typical use |
|---|---|---|
| Delete | Blocks deletion, allows read and write | VNets, NSGs, Recovery Services vaults, Key Vaults, DNS zones |
| ReadOnly | Blocks deletion and modification, allows read only | Genuinely configuration-only resources |

- **ReadOnly caution:** it can break things that look like reads. Listing storage account keys is treated as a write, so ReadOnly blocks it; ReadOnly on a VNet can stop VMs starting in some configs.
- **Inheritance:** a lock on a parent scope protects all children, but shows only on the parent where it was created.
- **Permissions:** creating or removing locks needs `Microsoft.Authorization/locks/write` and `/delete`, granted by **Owner** and **User Access Administrator**. Contributor can manage resources but not locks, which enforces separation of duties.
- Locks **override all RBAC**, including Owner. The lock must be removed before anyone can delete or modify the resource.
- Apply via the resource's **Settings > Locks > + Add**. Enforce at scale with a DeployIfNotExists policy that deploys Delete locks on matching resources.

## Defender for Cloud Security Controls and Remediation

#### Environment settings (configure before you govern)
- Per-subscription settings for data collection, autoprovisioning, and workload protection plan coverage. Onboard at **management group** scope so child subscriptions inherit the config.
- Autoprovisioning deploys the **Azure Monitor Agent** (replaces the retired Log Analytics/MMA agent), the **Defender for Endpoint sensor**, and the **vulnerability assessment agent**.
- Point data collection at a **central Log Analytics workspace** (often in a dedicated security tooling subscription) for cross-subscription visibility.

#### Security standards
- A standard is a collection of controls; each control maps to one or more policy definitions. Assigning a standard makes Defender evaluate resources and surface findings as recommendations.
- **MCSB** is the default, cannot be removed, and covers identity, network, data protection, compute, and logging.
- **Regulatory standards** (CIS, NIST SP 800-53, ISO 27001, PCI DSS, SOC 2) add controls beyond the baseline. One resource can be evaluated against several standards at once.
- **Custom standards** are built from an Azure Policy initiative and appear alongside built-in standards in the dashboard.

#### Recommendation anatomy
Each recommendation shows the resource, subscription, severity (Critical, High, Medium, Low), secure score value, and remediation description. Some are out of scope until the relevant Defender plan is enabled.

#### Four mechanisms to deploy controls at scale

| Situation | Mechanism |
|---|---|
| A Fix button is present and the change is safe to automate | **Fix** (bulk automated deployment) |
| Backed by a DeployIfNotExists or Modify policy, needs a resource or extension deployed | **Policy remediation task** |
| The fix needs an owner decision or custom app config | **Governance rule** (assign owner + deadline of 7, 14, 30, or 90 days, with escalation) |
| A compensating control exists or leadership accepted the risk | **Exemption** (waiver or mitigated) |

- **Fix** runs asynchronously; resources move Unhealthy to Healthy on the next cycle (roughly 30 to 60 minutes for changed resources, up to 24 hours dashboard-wide). Review the fix logic first, since some changes affect connectivity.
- **Governance rules** operate at the recommendation level and can auto-assign ownership by severity, resource type, or Owner tag. Tag-based ownership scales best.
- **Exemptions affect the secure score** (a waiver removes the resource from the denominator), so use them only when genuinely justified.

#### Tracking progress
Secure score trend (week over week), recommendation age (surfaces overdue items), and the governance report (accountability by team).

## Regulatory Compliance in Defender for Cloud

#### Standard types
- **Security benchmarks:** MCSB, the default baseline, multicloud across Azure, AWS, and GCP. MCSB v2 is in preview with expanded risk-based controls and AI coverage.
- **Regulatory standards:** ISO 27001, NIST SP 800-53, PCI-DSS, plus emerging frameworks like DORA and the EU AI Act.
- **Custom standards:** aligned to internal policy; require Defender CSPM to create KQL-based custom recommendations.

#### Controls and assessment states
A standard breaks into controls (groups of recommendations).

| State | Indicator | Meaning |
|---|---|---|
| Passing | Green | All in-scope resources comply |
| Failing | Red | One or more resources do not comply |
| Not available | Greyed out | Cannot be automatically assessed |

Greyed-out controls are usually procedural controls (e.g. security awareness training), platform responsibilities under shared responsibility (physical datacenter security), or controls with no automated assessment yet. Use **manual attestation** with evidence to mark these compliant.

#### Two portals, two responsibilities

| Azure portal (portal.azure.com) | Defender portal (security.microsoft.com) |
|---|---|
| Configuration hub: assign standards, set scope, manage policies, create custom standards | Monitoring interface: view scores, control details, filter recommendations, track remediation (read-only) |
| Needs Owner or Policy Contributor to add a standard | Needs Reader to view compliance data (Security Reader is not enough) |

Adding nondefault regulatory standards needs at least one paid Defender plan (any except Defender for Servers Plan 1 or Defender for API Plan 1).

#### Navigate and investigate
- Dashboard: **Cloud security > Regulatory compliance** in the Defender portal. Shows lowest-performing standards and pass rates. Expand a standard to see controls by category.
- **Control details** has three tabs: **Overview** (what the control protects), **Your Actions** (automated assessments linked to recommendations, plus manual assessments you attest), and **Microsoft Actions** (platform controls Microsoft manages).
- Investigation path: standard, then failing control, then failing assessment, then affected resources, then remediation. Compliance assessments run roughly every 12 hours, so wait a cycle before the dashboard reflects a fix.
- Filter the **Recommendations** page by framework to focus audit-deadline work. Many recommendations satisfy several standards at once.

#### Assign standards and report
- Assign in the Azure portal: **Defender for Cloud > Regulatory compliance > Manage compliance policies > Security policies**, then toggle the standard **On**. Assign at management group level for aggregate tracking. Initial data can take up to 12 hours. A standard with no in-scope resources does not appear until relevant resources exist.
- **Reports:** Download report as **PDF** (formatted point-in-time summary for auditors) or **CSV** (resource-level assessment data). The **Compliance over time workbook** shows the trend, which many frameworks require as evidence of continuous improvement.
- **Microsoft Purview Compliance Manager** integration is automatic once standards are assigned and unifies compliance across Microsoft 365, endpoints, cloud, and on-premises. Allow up to seven days to populate.

---

### Lab / Hands-On Work
Portal procedures practiced across the three modules:
- Assign the MCSB initiative at management group scope, then review results in **Policy > Compliance**.
- Author a custom policy definition, test it with the **Evaluate** tab, then create a remediation task with a managed identity holding the correct RBAC role.
- Apply Delete and ReadOnly resource locks and observe inheritance from a resource group.
- Configure Defender for Cloud environment settings and assign a regulatory standard.
- Remediate recommendations using Fix, a policy remediation task, a governance rule, and an exemption.
- Navigate the regulatory compliance dashboard, drill from a failing control to affected resources, and download a PDF and CSV report.

**What happened / Result**
- Not yet implemented 

**Challenges I faced**
- N/A

---

### My Takeaways
- Azure Policy governs configuration, resource locks govern existence. Policy blocks bad configs; locks stop deletion of good ones.
- Roll out with Audit first, then Deny. Discovery before enforcement avoids breaking production.
- Assign at the management group scope so new subscriptions inherit controls automatically.
- Remediation tasks fail silently on permissions. Grant the managed identity its RBAC role before running the task.
- Separation of duties is built in: Contributor manages resources but cannot touch locks, and locks override even Owner.
- Standards generate recommendations; the four mechanisms (Fix, remediation task, governance rule, exemption) deploy or formally waive the controls at scale.
- Compliance work spans two portals: configure in Azure, monitor in Defender. Greyed-out controls need manual attestation, not more automation.
- Exemptions and waivers move the secure score without deploying a control, so overuse produces a misleading posture.

---

### Questions I Still Have
N/A
---

### Resources I Found Useful
- [Enforce governance with Azure Policy and resource locks](https://learn.microsoft.com/en-us/training/modules/enforce-governance-azure-policy-resource-locks/)
- [Configure security controls and remediate recommendations in Defender for Cloud](https://learn.microsoft.com/en-us/training/modules/configure-defender-cloud-security-controls/)
- [Evaluate regulatory compliance in Defender for Cloud](https://learn.microsoft.com/en-us/training/modules/evaluate-regulatory-compliance/)

_Submitted by: Dare Ademola (Oluwatidamilare)_

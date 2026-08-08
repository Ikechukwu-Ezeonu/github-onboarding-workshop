# SC-500 Learning Notes: Week 5

## Topic: Enforce Security Governance and Regulatory Compliance (Part 2)


### Key Concepts I Learned

## RBAC Role Assignments and Least Privilege

#### Scope hierarchy and least privilege
- Four scope levels: management group, then subscription, then resource group, then resource. Children inherit parent assignments, and RBAC alone cannot block an inherited permission.
- Assign at the **narrowest scope** that lets the person or workload do the job. A network engineer managing VNets in one resource group gets Network Contributor at that resource group, not Contributor at the subscription. Broad Owner assignments create an unnecessary blast radius.

#### Choose the right built-in role (service-specific first)
Over 300 built-in roles exist. Check for a `<service> Contributor` or `<service> Reader` before falling back to the general roles. Roles with "Data" in the name grant data plane access.

| General role | Grants | Use only when |
|---|---|---|
| Owner | Full control plus role assignment delegation | The user must assign roles to others |
| Contributor | Full resource management, no role assignment | No service-specific role fits |
| Reader | Read-only across the scope | Audit, monitoring, view-only |

Examples of narrower roles: Network Contributor, Virtual Machine Contributor, Key Vault Secrets User, Storage Blob Data Reader, Monitoring Reader.

#### Managed identity assignments
System-assigned identities are tied to the resource lifecycle; user-assigned identities are independent and shareable across resources. Least privilege applies identically: a workload that reads one vault's secrets gets Key Vault Secrets User scoped to that vault, not Key Vault Administrator at subscription scope.

#### Verify before assigning, and the ordering rule
- Use **Access control (IAM) > Check access** to see existing, conflicting, and group-inherited assignments before adding a new one.
- **Always add the narrower assignment before removing the broader one.** Removing first can lock the user out of resources they actively use.

#### Assignment limits and scale
- Up to 4,000 role assignments per subscription (direct, managed identity, and group-based combined).
- Use **group-based assignments** to scale: the assignment belongs to the group, so adding or removing members does not consume assignments.
- Use ARM or Bicep `roleAssignments` in source control for consistency and audit trail rather than portal drift.

#### Custom Azure RBAC roles
Needed when the narrowest built-in role still over-grants, or a required combination spans services no built-in role covers. JSON structure:
- **Actions:** control plane operations (manage the resource through ARM).
- **NotActions:** subtracts from wildcard grants. This is not a Deny; another assignment could still grant the action. Only Azure Policy Deny or an RBAC Deny assignment creates a true deny.
- **DataActions / NotDataActions:** data plane operations (reading blob content, retrieving secret values).
- **AssignableScopes:** where the role can be assigned; must include at least the subscription where the definition lives.

Limits: 5,000 custom role definitions per tenant, 2,000 assignments per subscription per custom role. Create via **IAM > + Add > Add custom role** (start from scratch, clone a built-in role, or upload JSON). Cloning a built-in role and trimming is faster than starting empty.

#### Microsoft Entra custom roles (a separate system)

| | Azure RBAC custom role | Microsoft Entra custom role |
|---|---|---|
| Controls | Azure resources (VMs, storage) | Directory objects (users, groups, apps) |
| Created in | Azure portal IAM, or ARM/Bicep | Microsoft Entra admin center |
| Assignable scope | Management group, subscription, resource group, or resource | Tenant-wide or a single app registration only |
| Limit per tenant | 5,000 | 100 |

The two permission systems are independent: an Azure RBAC role has no effect on directory operations and vice versa. Custom roles are not auto-updated when new resource operations ship, so reserve them for stable, well-understood permission sets.

#### Evaluate and remediate overprivileged access

| Overprivilege category | Risk | Detection |
|---|---|---|
| Standing privilege at excessive scope | Owner at subscription when RG-level Contributor would do | Defender CSPM CIEM over-provisioned analysis |
| Dormant assignments | Role held but no authentication in 90+ days | Defender CSPM CIEM dormant identity recommendations |
| Guest accounts with elevated access | External users at Contributor or higher on a subscription | Defender CSPM identity recommendations plus Azure Advisor |

- **Defender CSPM with CIEM** correlates assignments with actual usage (e.g. "Remove unused role assignments for subscription Owners"). Full entitlement analysis needs the paid Defender CSPM plan; foundational CSPM gives only basic identity recommendations.
- **Azure Advisor** flags structural risks: more than three Owners on a subscription, and deprecated accounts still holding assignments. Configuration-based and immediate; exports to CSV.
- **Microsoft Entra access reviews** (Entra admin center > Identity Governance > Access reviews) ask reviewers to confirm each assignment. Set "Apply results automatically" to Yes and "If reviewers don't respond" to Remove access, so removal is the default. Creates an audit trail.
- **Right-sizing outcomes:** remove entirely (dormant accounts), downgrade to a less-permissive role at narrower scope, convert to PIM-eligible (standing access becomes just-in-time), or retain with the access review approval as documentation. Run reviews on a recurring cadence (quarterly for Owner and Contributor at subscription scope).

## Azure Backup Security Features

#### Why backup infrastructure is the target
Ransomware hits backups before production. The destruction workflow: obtain backup admin credentials, disable soft delete, stop backup with data deletion, delete the vault, then encrypt production. The goal of these controls is to make backup destruction impossible for a single compromised account, even one holding Backup Contributor.

#### Two deletion-protection layers

| Layer | Prevents | Irreversible option |
|---|---|---|
| Enhanced soft delete | Immediate permanent deletion of recovery points | Always-on (locks the retention period) |
| Vault immutability | Modification or deletion of recovery points before retention expires | Enabled and Locked (WORM) |

- **Enhanced soft delete:** deleted recovery points enter a recoverable state at no extra cost. Enforced by default (Secure by default) and cannot be disabled in GA regions. Retention is configurable from 14 to 180 days (default 14). **Always-on** makes the retention period irreversible, so not even a Global Administrator can shorten or disable it. Configure at least 90 days for production. Coverage includes Azure VMs, SQL and SAP HANA in Azure VMs, Azure Files vaulted backup, and MARS-protected on-premises servers.
- **Vault immutability:** WORM behavior. Three states: Disabled (default), Enabled (reversible), and Enabled and Locked (irreversible by anyone including Global Admins). After locking you can increase retention but never decrease it.
- Soft delete provides a recovery window after deletion; immutability prevents the deletion in the first place. They complement each other.

#### Security posture rating (target: Excellent)

| Tier | Requirements |
|---|---|
| Excellent | A deletion-protection mechanism (locked immutability OR always-on soft delete) AND Multi-User Authorization |
| Good | Immutability enabled and locked, OR soft delete in any configuration |
| Fair | MUA only, without immutability or enhanced soft delete |
| Poor | No advanced features (default for new vaults) |

New vaults start at Good because soft delete is enforced. Reaching Excellent requires adding MUA on top of a locked deletion protection.

#### Multi-User Authorization (MUA) and Resource Guard
MUA requires two separate administrators to authorize critical operations, converting a single-credential attack into a collusion requirement.

| Operation | Without MUA | With MUA |
|---|---|---|
| Shorten soft delete retention | Vault admin executes immediately | Vault admin requests, Resource Guard owner approves |
| Stop backup with data delete | Vault admin executes immediately | Requires approval |
| Remove MUA protection | Vault admin executes immediately | Requires approval |

- **Resource Guard** is a separate Azure resource acting as gatekeeper. The vault admin must **not** hold Contributor, Backup MUA Admin, or Backup MUA Operator on it, or self-approval defeats the control. Deploy it in a different subscription (same region as the vault), owned by a separate security team.
- It protects two mandatory operations (disable soft delete or security features, and remove MUA) plus nine optional ones. All optional operations except Restore are enabled by default.
- **Config flow:** security admin creates the Resource Guard; vault admin is assigned Reader on it; vault admin sets **Properties > Multi-User Authorization > Protect with Resource Guard**. The approval flow uses Microsoft Entra PIM: the vault admin activates an eligible Backup MUA Operator assignment, which raises an approval request; PIM revokes the role when the window ends.

#### Backup RBAC roles (least privilege)

| Role | Permits | Use for |
|---|---|---|
| Backup Contributor | Full management including stop backup with delete and create vaults | Initial vault setup; the two named admins who submit MUA requests |
| Backup Operator | Same, but cannot stop backup with data delete, disable soft delete, or delete data | Day-to-day operations, automation, and service accounts |
| Backup Reader | View only | Monitoring, compliance audit, SOC review, helpdesk |

Assign Backup Operator for automation to limit the blast radius of a compromised service credential.

#### Encryption
Default is platform-managed keys (AES-256, no configuration). **Customer-managed key (CMK)** encryption uses keys in your Key Vault that you control. CMK is a one-way commitment and is only supported on new vaults with no registered backup items, so configure it at vault creation if it is a compliance requirement.

## Security Controls in Infrastructure as Code

#### Two enforcement layers that cover different paths

| Layer | Enforcement point | Coverage |
|---|---|---|
| Microsoft Security DevOps (MSDO) scanning | CI/CD pipeline | Templates committed through the PR workflow |
| Azure Policy Deny | Azure Resource Manager API | Every deployment path (CLI, portal, API, pipeline) |

Pipeline scanning catches violations during code review; Policy Deny catches them at deployment regardless of origin. Use both.

#### Connect source control to Defender for Cloud
**Environment settings > + Add environment > GitHub or Azure DevOps** (GitHub App install, or OAuth / PAT for Azure DevOps). Defender then generates DevOps security recommendations (exposed secrets, open-source component vulnerabilities, IaC misconfigurations) under the **DevOps** category.

#### Microsoft Security DevOps (MSDO) extension
- Runs security tools inside the pipeline. GitHub Action: `microsoft/security-devops-action`. Azure DevOps task: `MicrosoftSecurityDevOps@1`.
- By default it runs secrets, code, container, and IaC scanning. Scope to templates only with `categories: 'IaC'`. Pin the action to a version tag, not `@latest`.
- Findings surface as GitHub Code Scanning alerts or Azure DevOps pipeline annotations, and are ingested into Defender for Cloud within 24 hours.

#### Scanning engines inside MSDO
- **Template Analyzer:** ARM and Bicep, Azure-specific checks (secure transfer, TLS minimum 1.2, diagnostic logs, public access, permissive network rules).
- **PSRule for Azure:** applies Well-Architected and Cloud Adoption Framework rules to ARM and Bicep.
- **Checkov:** open-source, broad coverage across Bicep, ARM, Terraform, Kubernetes, Dockerfiles, and Helm, for mixed-IaC environments.

#### Block noncompliant merges (shift-left)
Findings appear as GitHub Code Scanning alerts or Azure DevOps annotations. Configure severity-based blocking through **GitHub branch protection rules** or **Azure DevOps branch policy**, requiring the MSDO check to pass before merge. You can block High and Critical while allowing Low to pass.

#### Agentless scanning
For repos that cannot modify pipelines (legacy or vendor-managed). Defender scans GitHub and Azure DevOps repos directly every 24 hours, no pipeline change. Enable via the connector's **Settings > DevOps threat landscape > IaC scanning**. Complementary to MSDO: MSDO gives fast PR feedback, agentless gives centralized coverage.

#### Policy-as-code workflow
Manage policy definitions, initiatives, and assignments as source-controlled code: **Author** (JSON or Bicep alongside the IaC) → **Test in Audit** in dev → **Validate** (catches real violations, no false positives) → **Promote to Deny** in production → **Monitor**. The Deny effect blocks noncompliant creation at the ARM layer before the resource exists.

#### Enterprise Policy as Code (EPAC)
Open-source PowerShell module for managing Azure Policy at management-group scale through CI/CD. Defines assignments in JSON mapped to scopes, deploys consistently, and detects drift between the desired state in code and the live configuration. It is a community and Microsoft-maintained governance layer, not a native Azure Policy feature (aka.ms/epac).

#### Secure Bicep authoring patterns
Reduce findings at the source: use the `@secure()` decorator on secret parameters, reference Key Vault secrets with the `existing` keyword and `getSecret()` instead of hardcoding, and assign managed identities rather than passing service principal credentials.


### Lab / Hands-On Work
The Lab portal wasn't opening

**What happened / Result**
N/A

**Challenges I faced**
N/A

---

### My Takeaways
- Least privilege is two jobs: assign narrow, then hunt down and right-size the broad assignments that already exist. Dormant Owner accounts are the highest-value target.
- Add the narrower role before removing the broader one, every time, to avoid locking users out.
- Convert standing elevated access to PIM-eligible rather than leaving it permanent; access reviews with auto-removal keep the backlog from rebuilding.
- Backup security is layered: soft delete gives a recovery window, immutability prevents the deletion, and MUA stops a single compromised admin from disabling either. Excellent tier needs a locked deletion protection plus MUA.
- The Resource Guard only works if the vault admin cannot approve their own requests, so role separation across subscriptions is the whole point.
- Enforce IaC security at every path: MSDO scans the pipeline (shift-left, cheapest fix), Azure Policy Deny backstops every other deployment route at the ARM layer.
- Policy-as-code brings version control, audit trail, and dev-to-prod promotion to governance itself; EPAC scales it across management groups.

---

### Questions I Still Have
N/A

### Resources I Found Useful
- Learning path: [Enforce security governance and regulatory compliance](https://learn.microsoft.com/en-us/training/paths/security-governance-compliance/)
- [Manage and right-size RBAC role assignments for least privilege](https://learn.microsoft.com/en-us/training/modules/manage-right-size-rbac-role-assignments/)
- [Protect backup data with Azure Backup security features](https://learn.microsoft.com/en-us/training/modules/protect-backup-data-azure-backup-security/)
- [Implement security controls in infrastructure as code](https://learn.microsoft.com/en-us/training/modules/implement-security-controls-infrastructure-as-code/)
- EPAC: aka.ms/epac · PSRule for Azure: aka.ms/ps-rule-azure
- Related certifications: SC-300, AZ-500, SC-100

_Submitted by: Dare Ademola (Oluwatidamilare)_

# My Notes — Abiola Habeeb

---

## Key Concepts I Learned

Part 2 of enforcing security governance and regulatory compliance, covering **RBAC, Azure Backup protection, and Infrastructure as Code (IaC) security**.

- **RBAC scope and inheritance.** Roles can be assigned at four scopes — **Management Group → Subscription → Resource Group → Resource** — and a role assigned higher up **cascades down** to everything below it (child inherits every parent assignment). RBAC alone cannot block an inherited permission, so the key discipline is assigning at the **lowest scope needed**. If an engineer needs access in three resource groups, assign the role at each resource group rather than at the subscription — this **limits the blast radius** if the account is compromised.
- **Least privilege everywhere.** Avoid handing out Owner/Contributor by default; match the role to the task. The same principle applies to **managed identities** — a system-assigned identity is tied to its resource's lifecycle, a user-assigned one is standalone and reusable.
- **Custom roles have four parts:** **Actions** (control-plane operations), **NotActions** (subtracted from Actions — not a deny), **DataActions** (data-plane, e.g. reading a blob or a Key Vault secret), and **AssignableScopes**. Azure RBAC custom roles and **Entra ID** custom roles are **not the same** — one governs Azure resources, the other governs directory objects, and neither affects the other.
- **Assignment limits.** There is a ceiling of **4,000 role assignments per subscription**. The fix as you approach it is to **assign roles to security groups, not individual users**, and to automate assignments with IaC.
- **Evaluate and remediate over-privilege.** Use **Microsoft Entra Access Reviews** (requires P2) and Defender for Cloud to find standing privilege, dormant assignments (no sign-in for 90 days), and guest accounts with elevated access. Then **remove, downgrade, convert to PIM-eligible (just-in-time), or document** each finding, and schedule recurring reviews.
- **Azure Backup protection.** **Soft delete** (enabled by default, 14–180 days, 90+ recommended for production) prevents immediate permanent deletion and is the first layer of defense. **Vault immutability** (WORM — write once, read many) can be Disabled / Enabled / Enabled-and-locked (irreversible). **Multi-User Authorization (MUA)** adds a Resource Guard so a second approver must sign off on posture-weakening operations. Backup roles follow least privilege — **Backup Operator** for day-to-day, Contributor only for setup.
- **Encryption.** Platform-Managed Keys (Microsoft-managed, AES-256, zero config) vs **Customer-Managed Keys** (your key in your own Key Vault for data sovereignty). CMK can only be set on a new vault and cannot be reverted.
- **Secure IaC.** Scan templates **before deployment** using **Microsoft Security DevOps (MSDO)** in CI/CD (Template Analyzer for ARM/Bicep, Checkov for multi-cloud) and agentless scanning in Defender for Cloud. Layer this with **Azure Policy Deny** so every deployment path is covered (roll out Audit → validate → Deny). Secure Bicep patterns: use `@secure()` on sensitive parameters, reference Key Vault instead of hardcoding secrets, and use managed identity instead of a service principal.

---

## Lab / Hands-On Work

### What I did


### What happened / Result


### Challenges I faced


---

## My Takeaways

Through this training I now understand that governance is about *scope and restraint*, not just handing out access. The biggest lesson was how broad, high-scope role assignments create a large blast radius — assigning at the resource-group level and using least privilege is what contains damage when an account is compromised. I also see that protection has to extend to backups (soft delete, immutability, and multi-user authorization stop an attacker or a mistake from wiping recovery points) and to the pipeline itself, where scanning IaC before deployment and enforcing Azure Policy catches misconfigurations and exposed secrets before they ever reach production. Continuous review — access reviews, compliance checks — is what keeps all of this from drifting back into an insecure state.

---

## Questions I Still Have

- When permissions from different scopes overlap (e.g. Contributor at subscription and Owner at a resource group), what is the exact effective-permission behaviour, and how do deny assignments and Azure Policy interact with it?
- For the over-privilege remediation, how do you safely convert standing Owner assignments to PIM-eligible without disrupting active work?
- What's the recommended way to scale Azure Policy enforcement across many subscriptions (e.g. Enterprise Policy as Code)?

---

## Resources I Found Useful

- Bootcamp — Naija AI and Cloud Security (Microsoft Naija Security Usergroup) GitHub
- [Enforce security governance and regulatory compliance — full learning path](https://learn.microsoft.com/en-us/training/paths/security-governance-compliance/)
- [Manage and right-size RBAC role assignments for least privilege](https://learn.microsoft.com/en-us/training/modules/manage-right-size-rbac-role-assignments/)
- [Protect backup data with Azure Backup security features](https://learn.microsoft.com/en-us/training/modules/protect-backup-data-azure-backup-security/)
- [Implement security controls in infrastructure as code](https://learn.microsoft.com/en-us/training/modules/implement-security-controls-infrastructure-as-code/)

---

*Submitted by: Abiola Habeeb · https://github.com/abiolahabeeb*

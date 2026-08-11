# My Notes — Abiola Habeeb

---

## Key Concepts I Learned

- **Azure Policy** is the enforcement engine that evaluates resources against JSON-defined rules (policy definitions) to keep an environment compliant with a security baseline. A single rule is a **policy definition**; a bundle of many definitions is an **initiative**; attaching one to a scope is an **assignment**. Scope flows top-down: **Management Group → Subscription → Resource Group → Resource**, and higher assignments cascade down. The four effects are **Audit** (flags only, no changes), **Deny** (blocks non-compliant creation/updates), **DeployIfNotExists** (auto-deploys a missing setting), and **Modify** (adds/changes properties like tags).
- **Role-Based Access Control (RBAC)** rests on three parts — the **Principal** (user, group, service principal, or managed identity), the **Role Definition** (built-in or custom set of allowed actions, e.g. Contributor's wildcard `*` limited by NotActions), and the **Scope**. The guiding rule is **least privilege**, reinforced by regular **access reviews** to confirm assigned roles are still needed.
- **Resource Locks** prevent accidental loss: **CanNotDelete** allows edits but blocks deletion, while **ReadOnly** blocks both write and delete (view only). Deleting a resource group is permanent and unrecoverable, and only **Owner** or **User Access Administrator** can remove a lock.
- **Global Admin elevation gotcha** — a Global Admin (an Entra ID role) has no Azure authority by default, but can toggle "Access management for Azure resources = Yes" to inherit **User Access Administrator** across all subscriptions. A strong reminder of why least privilege and monitoring matter even for trusted roles.
- **Microsoft Defender for Cloud** measures security posture (**Secure Score**), surfaces misconfigurations and vulnerabilities, and maps the environment to compliance standards such as the **Microsoft Cloud Security Benchmark (default, CIS + NIST)**, **ISO 27001**, **NIST**, and **PCI-DSS**. It collects logs into a central **Log Analytics Workspace** (queried with KQL) and offers **Fix** (automatic) or **Take action** (manual) remediation. Being compliant/certified is what lets an organization pass audits and be trusted with projects.

---

## Lab / Hands-On Work

### What I did


### What happened / Result


### Challenges I faced


---

## My Takeaways

Through this training I now understand that being in Azure does not make an environment secure by default — governance has to be deliberately enforced. Azure Policy sets and enforces the baseline, RBAC with least privilege controls who can do what, resource locks guard against irreversible mistakes, and Defender for Cloud continuously measures posture and maps it to compliance standards. My most surprising takeaway was learning how a Global Admin can elevate into full Azure control, and I now also understand why compliance frameworks like ISO 27001 and PCI-DSS exist — without them, an organization can be rejected as an untrusted vendor and fail audits.

---

## Questions I Still Have

- When multiple compliance standards apply at once (MCSB, ISO 27001, PCI-DSS), how do teams manage the overlapping controls — is a common control framework the standard approach?
- What are the best practices for rolling out **Deny** policies in production without accidentally blocking legitimate work or locking out administrators?

---

## Resources I Found Useful

- [Microsoft Learn — Azure Policy, Azure RBAC, resource locks, and Microsoft Defender for Cloud](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/security-controls-policy)
- [Microsoft Service Trust Portal](https://servicetrust.microsoft.com/) 

---

*Submitted by: Abiola Habeeb · https://github.com/abiolahabeeb*

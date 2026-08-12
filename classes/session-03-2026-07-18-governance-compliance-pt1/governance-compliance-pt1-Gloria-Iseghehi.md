# My Notes — Gloria Iseghehi

---

## Key Concepts I Learned

- Azure Policy is a governance service that helps organizations enforce standards and evaluate Azure resources for compliance.
- Azure Policy uses **policy definitions**, which are JSON-based rules that determine whether Azure resources comply with organizational requirements.
- A **policy initiative** is a collection of multiple policy definitions grouped together to achieve a broader compliance objective.
- Azure Policy evaluates resources when they are created or updated, when a new policy or initiative is assigned, when an existing assignment is modified, and automatically every 24 hours.
- Azure Policy can be assigned at different scopes, including **Management Group**, **Subscription**, **Resource Group**, and **Resource**.
- Policy effects determine how Azure responds to non-compliant resources. Common effects include **Audit**, **Deny**, **DeployIfNotExists**, and **Modify**.
- Azure Role-Based Access Control (RBAC) controls access to Azure resources using three key components: **Principal**, **Role Definition**, and **Scope**.
- Resource Locks help protect important Azure resources from accidental deletion or modification by using **CanNotDelete** and **ReadOnly** locks.

---

## Lab / Hands-On Work

### What I did

- Learned how Azure Policy is used to enforce security governance and regulatory compliance across Azure resources.
- Explored the differences between **Policy Definitions**, **Initiatives**, and **Assignments**.
- Studied the different events that trigger Azure Policy evaluations.
- Learned how Azure RBAC works by understanding the relationship between principals, role definitions, and scopes.
- Studied how Resource Locks protect critical resources from accidental deletion or modification.

### What happened / Result

- I understood that Azure Policy automatically evaluates resources during creation, updates, policy assignments, assignment changes, and through its daily compliance evaluation cycle.
- I learned that Azure Policy can audit, deny, modify, or automatically remediate resources depending on the configured policy effect.
- I gained a better understanding of how RBAC manages permissions while Azure Policy enforces compliance.
- I also learned that Resource Locks provide an additional layer of protection for important Azure resources.

### Challenges I Faced

- Understanding the differences between Azure Policy, Azure RBAC, and Resource Locks since they all contribute to Azure security but have different purposes.
- Remembering the different policy effects and when Azure Policy evaluates resources.

---

## My Takeaways

- Azure Policy is an important governance tool that helps organizations maintain security and regulatory compliance by enforcing rules across Azure resources.
- Azure RBAC and Azure Policy complement each other. **RBAC controls who can perform actions on Azure resources, while Azure Policy controls whether resources comply with organizational standards.**
- Resource Locks help prevent accidental deletion or modification of critical resources, adding another layer of protection.
- Combining Azure Policy, RBAC, and Resource Locks helps organizations implement the principle of least privilege and strengthen their overall security posture.

---

## Questions I Still Have

- In what scenarios should **DeployIfNotExists** be used instead of **Modify** in Azure Policy?
- Which Azure built-in roles are required to create and assign Azure Policies at different scopes?

---

## Resources I Found Useful

- Microsoft Learn – Security Governance and Compliance learning path
- Microsoft Learn – Azure Policy documentation
- Class notes and instructor demonstrations

---

*Submitted by: Gloria Iseghehi · Glowriaose*
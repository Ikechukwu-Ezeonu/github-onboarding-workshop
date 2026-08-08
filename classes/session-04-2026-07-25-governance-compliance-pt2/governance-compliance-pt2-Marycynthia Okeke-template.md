# My Notes — Marycynthia Okeke

## Key Concepts I Learned

- Azure Policy provides governance by ensuring Azure resources comply with organizational standards.
- Azure Policy has four major effects for handling non-compliant resources:
  - **Audit** – Detects and reports non-compliant resources without blocking operations.
  - **Deny** – Prevents the creation or modification of resources that violate a policy.
  - **DeployIfNotExists** – Automatically deploys required configurations if they are missing.
  - **Modify** – Automatically adds, updates, or removes properties/tags to enforce standards.
- Each Azure Policy effect serves a different stage of governance, from monitoring to enforcement and automatic remediation.
- Role-Based Access Control (RBAC) governance involves not only assigning permissions correctly but also identifying and remediating excessive privileges.

---

## Lab / Hands-On Work

### What I did

- Learned how Azure Policy enforces governance across Azure resources.
- Reviewed the four Azure Policy effects and when each should be used.
- Studied how to evaluate privileged access using RBAC governance.
- Explored methods for detecting overprivileged identities using Microsoft Defender for Cloud CSPM and Azure Advisor.

### What happened / Result

- Understood the differences between Audit, Deny, DeployIfNotExists, and Modify policy effects.
- Learned how organizations can automatically enforce security standards using Azure Policy.
- Gained knowledge of common overprivileged access scenarios and the Microsoft tools used to detect them.

### Challenges I faced

- Understanding when to use each Azure Policy effect in real-world scenarios.
- Distinguishing between policy enforcement (Azure Policy) and access management (RBAC).

---

## My Takeaways

- Azure Policy is a critical governance tool that helps maintain compliance automatically.
- Organizations should begin with **Audit** to identify issues before moving to **Deny** for strict enforcement.
- **DeployIfNotExists** and **Modify** reduce manual effort by automatically remediating configuration drift.
- RBAC governance should include continuous monitoring for excessive permissions, dormant accounts, and guest users with elevated access.
- Microsoft Defender for Cloud CSPM and Azure Advisor provide valuable insights into identity risks and overprivileged access.

---

## Questions I Still Have

- How can custom Azure Policies be created and assigned across multiple subscriptions?


---

## Resources I Found Useful

<!-- Any links, docs, or Microsoft Learn modules you found helpful -->

---

*Submitted by: Marycynthia Okeke · Nechy-Okeke*

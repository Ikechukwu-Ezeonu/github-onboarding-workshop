# My Notes — IKECHUKWU EZEONU

---

## Key Concepts I Learned

<!-- Write the main ideas covered in today's session -->

- Enforcing Policy Compliance: Implementing Azure Policy for pre-deployment compliance to block non-compliant infrastructure definitions before deployment into production.
- Soft Delete & Immutable Vaults: Soft delete retains deleted backup data for a configurable period to recover from accidental deletion or ransomware attacks. Immutable vaults prevent backup policy modification or deletion even by subscription owners
- Built-in vs. Custom Roles: Built-in roles (e.g., Owner, Contributor, Reader) cover common scenarios, but custom Azure RBAC and Microsoft Entra ID roles allow precise control by specifying exact action sets (Actions, NotActions, DataActions)

---

## Lab / Hands-On Work

<!-- Describe what you did in the lab. Include steps, commands, or screenshots descriptions -->

### What I did


### What happened / Result


### Challenges I faced

- Custom RBAC DataActions: Distinguishing between management plane operations (Actions) and data plane access (DataActions) in JSON definitions was a bit confusing initially.

---

## My Takeaways

<!-- What was most valuable to you personally from this session? -->
- Security must be integrated early into the developer workflow (Shift-Left) through automated IaC scanning and pre-deployment policy checks.

- Backing up data isn't enough; backups must be protected against malicious deletion using immutable vaults and multi-person administrative locks (MUA).

- Identity governance is an ongoing process—access reviews and PIM are critical for maintaining least-privilege control over time

---

## Questions I Still Have

<!-- Anything you want to follow up on or ask the mentor -->

-
-

---

## Resources I Found Useful

<!-- Any links, docs, or Microsoft Learn modules you found helpful -->

- https://learn.microsoft.com/en-us/training/modules/manage-right-size-rbac-role-assignments/4-evaluate-remediate-overprivileged-access
- https://learn.microsoft.com/en-us/training/modules/protect-backup-data-azure-backup-security/2-enable-soft-delete-immutable-vaults
- https://learn.microsoft.com/en-us/training/modules/implement-security-controls-infrastructure-as-code/2-scan-iac-templates-defender-devops

---

*Submitted by: Ikechukwu Ezeonu · Ikechukwu-Ezeonu*

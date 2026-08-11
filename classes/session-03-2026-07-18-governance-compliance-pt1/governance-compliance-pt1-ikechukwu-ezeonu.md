# My Notes — IKECHUKWU EZEONU



---

## Key Concepts I Learned

<!-- Write the main ideas covered in today's session -->

-**Azure Policy Governance & Resource Locks**:
  - Built-in policies vs. Custom policies (using JSON logic with `if/then` conditions and parameters).
  - Policy effects: `Audit`, `Deny`, `DeployIfNotExists`, and `Modify`.
  - Governance scope hierarchy: Management Groups → Subscriptions → Resource Groups → Individual Resources.
  - Resource locks (`CanNotDelete` and `ReadOnly`) to prevent accidental deletion or unauthorized modification of critical infrastructure.
- **Defender for Cloud & Security Standards**:
  - Customizing security standards and assigning benchmarks (such as Microsoft Cloud Security Benchmark).
  - Deploying automated remediation controls at scale using `DeployIfNotExists` / `Modify` policy effects and logic apps.
- **Evaluating Regulatory Compliance**:
  - Understanding regulatory compliance frameworks (e.g., PCI-DSS, ISO 27001, SOC 2, HIPAA).
  - Using the Defender for Cloud **Regulatory Compliance Dashboard** to assess gaps, investigate non-compliant controls, and improve overall security posture.

---

## Lab / Hands-On Work

<!-- Describe what you did in the lab. Include steps, commands, or screenshots descriptions -->

### What I did
1. Assigned a built-in policy definition (e.g., "Require a tag on resources" or "Secure transfer to storage accounts should be enabled") with an `Audit` effect to test existing compliance state without breaking running workloads.
2. Configured Azure Resource Locks (`CanNotDelete` and `ReadOnly`) on production resource groups to protect critical assets from accidental modification or removal.
3. Navigated Microsoft Defender for Cloud to customize security standards, assigned regulatory compliance benchmarks (e.g., Microsoft Cloud Security Benchmark / NIST), and executed automated remediation tasks to fix non-compliant resources at scale.

### What happened / Result
- Evaluated compliance across all subscriptions using the Policy Compliance dashboard.
- Tested Resource Locks by attempting to delete a locked resource, confirming that ARM blocks deletion requests regardless of user RBAC permissions unless the lock is removed.

### Challenges I faced
- Understanding the difference between Policy effects like `AuditIfNotExists` against `DeployIfNotExists`.

---

## My Takeaways

<!-- What was most valuable to you personally from this session? -->
- **Audit-First Pattern**: Always roll out policies with the `Audit` effect first to measure compliance impact before switching to `Deny` to prevent operational outages.
- **Defense in Depth**: Resource locks act as a necessary layer of safety on top of RBAC roles, even subscription owners cannot bypass a `CanNotDelete` lock without removing it first.
- **Continuous Compliance**: Defender for Cloud streamlines audit readiness by auto-mapping technical controls to industry standards like PCI-DSS or ISO 27001.

---

## Questions I Still Have

<!-- Anything you want to follow up on or ask the mentor -->

- How can we efficiently test custom Azure Policy JSON rules locally or in a sandbox before applying them to root management groups since a testing environment will have the same number of deployed resources and systems as the production environment? 

---

## Resources I Found Useful

<!-- Any links, docs, or Microsoft Learn modules you found helpful -->

- Assign built-in policy definitions: (https://learn.microsoft.com/en-us/training/modules/enforce-governance-azure-policy-resource-locks/2-assign-built-in-policy-definitions)
- Create and deploy custom policy definitions: (https://learn.microsoft.com/en-us/training/modules/enforce-governance-azure-policy-resource-locks/3-create-deploy-custom-policy-definitions)
- Implement resource locks: (https://learn.microsoft.com/en-us/training/modules/enforce-governance-azure-policy-resource-locks/4-implement-resource-locks)
- Configure Defender for Cloud security standards: (https://learn.microsoft.com/en-us/training/modules/configure-defender-cloud-security-controls/2-configure-defender-cloud-security-standards)
- Deploy remediation controls at scale: (https://learn.microsoft.com/en-us/training/modules/configure-defender-cloud-security-controls/3-deploy-remediation-controls-scale)
- Understand compliance standards and controls: (https://learn.microsoft.com/en-us/training/modules/evaluate-regulatory-compliance/2-understand-compliance-standards-controls)
- Navigate compliance dashboard and investigate gaps: (https://learn.microsoft.com/en-us/training/modules/evaluate-regulatory-compliance/3-navigate-compliance-dashboard-investigate-gaps)
- Assign standards and communicate compliance posture: (https://learn.microsoft.com/en-us/training/modules/evaluate-regulatory-compliance/4-assign-standards-communicate-compliance-posture)

---

*Submitted by: Ikechukwu Ezeonu · Ikechukwu-Ezeonu*

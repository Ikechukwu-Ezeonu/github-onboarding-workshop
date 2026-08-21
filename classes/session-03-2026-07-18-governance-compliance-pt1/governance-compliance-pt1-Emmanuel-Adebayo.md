# My Notes — Emmanuel Adebayo


## Key Concepts I Learned

<!-- Write the main ideas covered in today's session -->

- **Azure Security Governance:** Learned how to enforce strict corporate governance and regulatory compliance across cloud environments to proactively prevent non-compliant resource deployments.
- **Azure Policy Hierarchy:** Understood the structural building blocks of Azure Policy, including how policy definitions dictate security rules, how assignments apply them to scopes, and how initiatives group multiple definitions together.
- **Resource Protection & Guardrails:** Explored how to use resource locks to prevent accidental deletion or modification of critical cloud assets.
- **Compliance Posture:** Examined security standards and assessed compliance posture inside Microsoft Defender for Cloud to keep cloud environments aligned with regulatory frameworks.

---

## Lab / Hands-On Work

<!-- Describe what you did in the lab. Include steps, commands, or screenshots descriptions -->
1. I navigate how to use resouce lock either to stop delete or read only
2. I reviewed different standerd available in the defender for cloud.
3. Explored how to assign azure policy.

### What I did
1. Explored the Azure Policy dashboard to review built-in definitions and the structure of JSON policy rules.
2. Walked through the process of creating a policy assignment and grouping policies into a compliance initiative.
3. Navigated the Microsoft Defender for Cloud portal to review cloud security standards and evaluate the overall compliance posture score.
4. Analyzed security recommendations within Defender for Cloud and reviewed the step-by-step remediation workflows to fix non-compliant configurations.

### What happened / Result
- Gained a clear understanding of how to implement automated guardrails that block engineers from creating unapproved or insecure resources.
- Identified where to find actionable remediation steps to improve an organization's regulatory compliance rating.

### Challenges I faced
- Distinguishing between the specific scopes of a single policy definition versus a broader policy initiative was slightly confusing initially, but tracking how they aggregate in the dashboard cleared it up.

---

## My Takeaways

<!-- What was most valuable to you personally from this session? -->
The most valuable lesson for me was understanding how automated governance works. Instead of manually checking every deployed resource, using Azure Policy and Defender for Cloud allows security teams to enforce compliance standards automatically, ensuring the environment remains secure by default.

---

## Questions I Still Have

<!-- Anything you want to follow up on or ask the mentor -->

- When a resource is flagged as non-compliant, does Azure Policy support automatic remediation scripts to fix it instantly without manual intervention?
- How frequently does Microsoft Defender for Cloud update the compliance posture dashboard after a fix has been applied?

---

## Resources I Found Useful

<!-- Any links, docs, or Microsoft Learn modules you found helpful -->

- [Microsoft Learn: What is Azure Policy?](https://microsoft.com)
- [Microsoft Learn: Regulatory compliance in Microsoft Defender for Cloud](https://microsoft.com)

---

*Submitted by: Emmanuel Adebayo · 19Emade*

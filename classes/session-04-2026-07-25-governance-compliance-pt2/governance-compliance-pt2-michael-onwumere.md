# My Notes — Michael Chinonso Onwumere

## Key Concepts I Learned

- Learned how Azure Backup uses **Vault Immutability (WORM - Write Once, Read Many)** to prevent backup data from being modified or deleted, protecting against ransomware and accidental deletion.
- Understood the importance of **Multi-User Authorization (MUA)**, which requires approval from another authorized user before performing sensitive backup operations.
- Explored the different **Azure Backup RBAC roles**:
  - **Backup Contributor** – Creates and manages backup vaults and policies.
  - **Backup Operator** – Performs backup and restore operations.
  - **Backup Reader** – Monitors backup status and views configurations without making changes.
- Learned the difference between **Platform-Managed Keys (PMK)** and **Customer-Managed Keys (CMK)** for protecting data encryption.
- Introduced to **Infrastructure as Code (IaC)**, which allows cloud infrastructure to be deployed and managed using code.
- Learned about **Policy as Code**, where governance and compliance policies are defined, managed, and enforced automatically through code.

---

## Lab / Hands-On Work

### What I did

- Reviewed Azure Backup security features, including Vault Immutability and Multi-User Authorization.
- Examined the different Backup RBAC roles and understood when each role should be assigned based on the principle of least privilege.
- Learned how encryption keys protect backup data using Platform-Managed Keys and Customer-Managed Keys.
- Learned how Infrastructure as Code and Policy as Code help automate cloud deployments while maintaining security and compliance.
- Followed the instructor's teachings and documented key concepts.

### What happened / Result

- I gained a better understanding of how Azure Backup secures critical data against accidental deletion and malicious attacks.
- I now understand the importance of assigning only the permissions users need through RBAC.
- I also learned how automation using Infrastructure as Code and Policy as Code improves consistency, governance, and regulatory compliance.

### Challenges I faced

- Understanding the practical differences between Platform-Managed Keys and Customer-Managed Keys took some time.
- Differentiating the responsibilities of the three Backup RBAC roles required careful attention during the session.
- There was no practical demonstration of what was discussed by the instructor, due to unstable network during the session and this affected the practical comprehension of what was taught. 
- There is no available subscribed azure environment for hands-on practice.

---

## My Takeaways

The biggest lesson for me was that cloud security is not only about protecting resources but also about enforcing governance through proper access control, secure backups, encryption, and automation. Applying the principle of least privilege and automating governance with policies can significantly improve an organization's security posture.

---

## Questions I Still Have

- In what scenarios should an organization choose Customer-Managed Keys instead of Platform-Managed Keys?
- What are some real-world examples of implementing Policy as Code in Azure environments?

---

## Resources I Found Useful

- Microsoft Learn – Azure Backup documentation
- Microsoft Learn – Azure Policy documentation
- Microsoft Learn – Azure RBAC documentation
- https://learn.microsoft.com/en-us/training/paths/security-governance-compliance/

---

*Submitted by: Michael Chinonso Onwumere · @MichaelOnwumere*

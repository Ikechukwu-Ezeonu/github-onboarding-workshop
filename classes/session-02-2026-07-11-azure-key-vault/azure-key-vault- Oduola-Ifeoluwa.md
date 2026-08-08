# My Notes — ODUOLA Ifeoluwa 

---

## Key Concepts I Learned

<!-- Write the main ideas covered in today's session -->

- Defense in depth: Security is layered across identity, network, and monitoring to protect sensitive assets.

- Azure Key Vault: Centralized service for managing secrets, keys, and certificates securely.

- RBAC vs Access Policies: Understanding how modern RBAC replaces legacy access policies for more flexible management.


---

## Lab / Hands-On Work

<!-- Describe what you did in the lab. Include steps, commands, or screenshots descriptions -->

### What I did
- Followed the demo walkthrough of securing Key Vault with role-based access control (RBAC) and network restrictions.

- Configured role assignments using RBAC.

- Enabled logging and monitoring for secret access.


### What happened / Result
- The demo showed that only authorized identities could access secrets.
- Key Vault access was restricted to authorized identities.
- Audit logs captured all secret retrieval attempts.
- Conditional access successfully blocked unauthorized sign-ins.


### Challenges I faced
Since it was a demo, I didn’t practice directly, but I anticipate challenges in:

- Configuring conditional access policies correctly.
- Understanding how conditional access rules apply without disrupting legitimate workflows.

---

## My Takeaways

<!-- What was most valuable to you personally from this session? -->
- Managed identities simplify security: They remove the need to store secrets in code.
- Compliance alignment: Defense in depth helps meet regulatory requirements for sensitive workloads.

---

## Questions I Still Have

<!-- Anything you want to follow up on or ask the mentor -->

- How does Key Vault integrate with Azure Policy for compliance enforcement?
-

---

## Resources I Found Useful

<!-- Any links, docs, or Microsoft Learn modules you found helpful -->

- Microsoft Learn: Secure Azure Key Vault https://learn.microsoft.com/en-us/azure/key-vault/general/secure-key-vault
 - YouTube session: Secure Azure Key Vault with defense in depth for the cloud & AI workloads https://www.youtube.com/watch?v=GKqpej4X9B0

---

*Submitted by: Oduola Ifeoluwa · Ife005 *

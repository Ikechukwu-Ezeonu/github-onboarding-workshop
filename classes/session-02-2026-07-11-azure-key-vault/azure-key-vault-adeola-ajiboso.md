# My Notes — [Adeola Ajiboso]

## Key Concepts I Learned
- I learned that Azure Key Vault is designed to store and manage secrets, cryptographic keys, and certificates securely. It plays an important role in protecting applications by reducing the need to hardcode credentials.
- Azure Role-Based Access Control (RBAC) is the preferred method for granting permissions to Azure Key Vault resources. RBAC makes it easier to manage access securely and follows modern authorization practices.

- I learned about the type of Network and Data Protection Controls. We have Firewall and Network access, Soft delete and purge protection and Operational guardrails.

---

## Lab / Hands-On Work
### What I did
During the practical session, I:

- Created an Azure Key Vault.
- Deployed an Azure App Service.
- Enabled a System-Assigned Managed Identity for the application.
- Configured RBAC permissions for the Key Vault.
- Explored how applications securely access secrets without exposing credentials.
- Used the Kudu console to understand how Managed Identities work behind the scenes.
- Reviewed logging and monitoring options for Azure Key Vault

### What happened / Result
- The App Service was successfully assigned a managed identity.

### Challenges I faced
- While working on the lab, I experienced an authorization error when trying to create a secret in Azure Key Vault. This helped me understand that:

- Appropriate RBAC roles must be assigned before performing certain actions.
Permission changes may take a few minutes before they become active.
- Understanding the differences between RBAC and legacy access policies is important when troubleshooting access-related issues.

---

## My Takeaways

<!-- What was most valuable to you personally from this session? -->


---

## Questions I Still Have

<!-- Anything you want to follow up on or ask the mentor -->

-
-

---

## Resources I Found Useful

<!-- Any links, docs, or Microsoft Learn modules you found helpful -->
- [Secure Azure Key Vault with defense in depth for the cloud & AI workload](https://www.youtube.com/watch?v=GKqpej4X9B0&t=2145s)

- [Azure Key Vault documentation](https://learn.microsoft.com/en-us/azure/key-vault/general/)
---
*Submitted by: [Adeola Ajiboso] · [Ajiboso-Adeola]*

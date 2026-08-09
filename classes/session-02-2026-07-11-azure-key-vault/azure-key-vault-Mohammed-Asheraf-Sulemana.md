# My Notes — [Mohammed Asheraf Sulemana]

## Key Concepts I Learned

- Azure Key Vault is a secure cloud service used to store and manage sensitive information such as secrets, cryptographic keys, and digital certificates.
- Defense in Depth is a security strategy that uses multiple layers of protection so that if one security control fails, other controls continue to protect the resource.
- Access to Azure Key Vault can be controlled using Azure Role-Based Access Control (RBAC) or Key Vault access policies to ensure only authorized identities can retrieve or manage secrets.
- Managed Identities allow Azure services to securely authenticate to Azure Key Vault without storing credentials in application code.
- Security features such as Soft Delete and Purge Protection help prevent accidental or malicious deletion of secrets and keys.

---

## Lab / Hands-On Work

### What I did

- Explored the Azure Key Vault service and its purpose in securing sensitive information.
- Learned the differences between secrets, keys, and certificates stored in Azure Key Vault.
- Reviewed how Azure RBAC can be used to control access to Key Vault resources.
- Observed how applications can securely retrieve secrets from Key Vault using Managed Identities.

### What happened / Result

- I understood why storing passwords, API keys, and connection strings directly in application code is considered a security risk.
- I learned that Azure Key Vault provides a centralized and secure location for managing sensitive information.
- I saw how Defense in Depth improves security by combining multiple protection mechanisms rather than relying on a single control.

### Challenges I faced

- Initially, I found it difficult to distinguish between secrets, keys, and certificates.
- I also needed more time to understand how Managed Identities communicate with Azure Key Vault without using stored credentials.

---

## My Takeaways

This session showed me that protecting sensitive information is a critical part of cloud security. Instead of storing secrets inside applications or configuration files, Azure Key Vault provides a secure and centralized solution. I also learned that Defense in Depth is about applying multiple security layers to reduce risk, rather than depending on a single security measure.

---

## Questions I Still Have

-none at the moment

---

## Resources I Found Useful

- Microsoft Learn – Introduction to Azure Key Vault
- Microsoft Learn – Secure secrets with Azure Key Vault
- Microsoft Learn – Managed Identities for Azure Resources
- Microsoft Learn – Defense in Depth Security Strategy

---

*Submitted by: [Mohammed Asheraf Sulemana] · [Shaiba-00*]
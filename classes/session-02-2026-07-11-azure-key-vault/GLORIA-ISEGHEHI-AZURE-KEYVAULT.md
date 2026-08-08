# My Notes — Gloria Iseghehi

## Key Concepts I Learned

- Azure Key Vault is a secure cloud service used to store and manage sensitive information such as secrets, encryption keys, and certificates.
- Instead of hardcoding passwords, API keys, or connection strings in application code, they should be stored securely in Azure Key Vault.
- Azure Key Vault stores three main object types:
  - **Secrets** – Passwords, API keys, tokens, and connection strings.
  - **Keys** – Cryptographic keys used for encryption, decryption, and signing.
  - **Certificates** – X.509 certificates used to secure websites and applications with TLS/SSL.
- Microsoft Entra ID is used to authenticate users and applications before they can access Key Vault.
- Azure RBAC is the recommended authorization model for controlling access to Key Vault resources. I also learned that Key Vault access policies are now considered a legacy approach.
- Managed Identities allow Azure resources to securely access Key Vault without storing credentials in application code.
- Key Vault also provides additional security features such as encryption at rest, soft delete, purge protection, network restrictions, and monitoring.

---

## Lab / Hands-On Work

### What I Did

Since I don't yet have access to an Azure lab environment, I supplemented the bootcamp session by watching YouTube demonstrations that showed how Azure Key Vault is created, configured, and used in real-world scenarios. This helped me connect the theory from class with practical implementation.

### What I Learned

Watching the demonstrations gave me a clearer understanding of how applications securely retrieve secrets from Azure Key Vault using Managed Identities instead of storing credentials directly in code. It also helped me visualize how Key Vault is configured and integrated into Azure workloads.

---

## Challenges I Faced

One concept I wanted to clarify was the authorization model used by Azure Key Vault. I already understood that Microsoft Entra ID can handle both authentication and authorization, but I initially thought Key Vault access policies were responsible for authorization within Key Vault while Entra ID handled authentication. During the session, the facilitator explained that Azure RBAC is now the recommended authorization model for Key Vault, while access policies are a legacy approach. That clarification helped me better understand how access to Key Vault is managed today.

---

## My Takeaways

- Identity is the foundation of Azure security.
- Sensitive information should never be hardcoded into applications.
- Azure Key Vault provides a centralized and secure location for storing secrets, keys, and certificates.
- Managed Identities eliminate the need to store credentials in application code.
- Azure RBAC is the modern and recommended way to manage authorization for Azure Key Vault.

---

## Questions I Still Have

- Are there any scenarios where organizations still prefer Key Vault access policies over Azure RBAC?
- What are the recommended strategies for secret rotation in production environments?

---

## Resources I Found Useful

- Microsoft Learn – Azure Key Vault documentation
- Microsoft Learn – Azure RBAC documentation
- Microsoft Learn – Managed Identities
- YouTube demonstrations on creating and using Azure Key Vault

---

**Submitted by:** Gloria Iseghehi · Glowriaose
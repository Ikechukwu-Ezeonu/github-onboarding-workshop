# My Notes — IKECHUKWU EZEONU


---

## Key Concepts I Learned

<!-- Write the main ideas covered in today's session -->

-Azure Key Vault is a cloud service used to securely store and manage cryptographic keys, secrets (such as passwords, connection strings, and API keys), and digital certificates. It helps applications avoid hardcoding sensitive information.

-Access to Key Vault can be controlled using Azure RBAC or Key Vault Access Policies. RBAC is the recommended authorization model because it provides centralized access management through Microsoft Entra ID and supports least-privilege access.

-Keys, secrets, and certificates each serve different purposes:
    -Keys perform cryptographic operations such as encryption, decryption, signing, and verification.
    -Secrets store sensitive information that applications need during runtime.
    -Certificates simplify certificate lifecycle management by combining certificates with their associated private keys.

-Key Vault supports soft delete and purge protection, allowing deleted vaults and objects to be recovered while preventing accidental or malicious permanent deletion.

-Key Vault logging can be integrated with Azure Monitor, Log Analytics, and Microsoft Sentinel for auditing and threat investigation.

-Microsoft Defender for Cloud continuously assesses Key Vault configurations and provides recommendations to improve security posture and detect suspicious activities.

-I learned that Defender for Key Vault is different from CSPM scanning. Defender for Key Vault protects the vault from external threats while Defender CSPM scanning protects the environment from secrets exposed outside the vault. Both plans are complementary to provide full coverage for the Key Vault security posture. Activating one of the solutions and leaving the other creates a gap in the Key Vault security posture.

---

## Lab / Hands-On Work

<!-- Describe what you did in the lab. Include steps, commands, or screenshots descriptions -->

### What I did

-Created an Azure Key Vault.
-Configured Azure RBAC permissions for users to access the Key Vault.
-Added and managed secrets within the vault.
-Enabled soft delete and purge protection.

### What happened / Result

-Successfully deployed a secure Azure Key Vault.
-Verified that only authorized users could access secrets based on assigned RBAC roles.
-Successfully stored, retrieved, updated, and deleted secrets.
-Confirmed that deleted objects could be recovered using soft delete.

### Challenges I faced

-Understanding the traditional Key Vault Access Policies and how it differs from Azure RBAC.
-Remembering which built-in RBAC role provides the minimum permissions required for different administrative tasks.
-Understanding certificate lifecycle management and how certificates differ from secrets and keys.

---

## My Takeaways

<!-- What was most valuable to you personally from this session? -->

-Hardcoding secrets and keys is a very bad security practice.

-Azure Key Vault is not simply a secure storage location but a core security service that protects sensitive assets across Azure environments. 

-Implementing RBAC, enabling soft delete and purge protection, monitoring access logs, and integrating Microsoft Defender for Cloud significantly improve an organization's security posture. 

-I also learned that following the principle of least privilege is essential when granting access to Key Vault resources.

---

## Questions I Still Have

<!-- Anything you want to follow up on or ask the mentor -->

-I still don't fully understand the concept of using certificates in production.
-What are the best practices for automatically rotating secrets and certificates in production environments?

---

## Resources I Found Useful

<!-- Any links, docs, or Microsoft Learn modules you found helpful -->

-Microsoft Learn is a very useful source for this learning.
- https://learn.microsoft.com/en-us/training/modules/configure-secure-key-vault/
- https://learn.microsoft.com/en-us/training/modules/manage-keys-secrets-key-vault/
- https://learn.microsoft.com/en-us/training/modules/manage-certificates-monitor-key-vault/
- https://learn.microsoft.com/en-us/training/modules/defend-key-vault-defender-cloud/

---

*Submitted by: Ikechukwu Ezeonu · Ikechukwu-Ezeonu*

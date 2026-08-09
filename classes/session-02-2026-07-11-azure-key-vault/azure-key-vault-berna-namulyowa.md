# My Notes — Berna Namulyowa

## Key Concepts I Learned
<!-- Write the main ideas covered in today's session -->

**Secure Azure Key Vault with Defense-in-Depth for Cloud & AI Workloads**

**Configure and secure Azure App Configuration secrets**
- Azure App Configuration is a service that centrally manages application settings and feature flags. Microsoft recommends the following for app configuration secrets:
  - Use Azure Key Vault to store secrets — cryptographic secrets, database passwords, and API keys.
  - Use RBAC and managed identities (system-assigned or user-assigned) to eliminate hardcoded credentials, connection strings, and manually shared or rotated app secrets.
  - Rotate secret versions centrally, according to company policy.
  - Enable Defender to monitor access to the vault.

**AI workload secret exposure: the attack chain**
- A single exposed secret can escalate into a full workload compromise. Exposed secrets in AI scripts, such as SAS tokens, can let attackers authenticate as legitimate users — for example through prompt injection — leading to data exfiltration and workload compromise.
- Any exposed AI secret allows attackers to bypass the perimeter and exfiltrate data. This is why Microsoft recommends a defense-in-depth strategy combining Azure workload identities, Microsoft Purview, and Defender for Cloud AI services to detect anomalies.

**Key components of Key Vault**
- **Secrets** — passwords, connection strings, and API keys.
- **Keys** — cryptographic keys used to encrypt and decrypt data.
- **Certificates** — used for TLS and workload trust boundaries; Key Vault manages the X.509 certificate lifecycle and renewal. Azure has two trusted certificate partners: GlobalSign and DigiCert.

**Three settings that govern vault security**
- The SKU (Stock Keeping Unit — Standard or Premium tier), deletion protection properties, and public network access.
- Both tiers protect keys and secrets at rest and in transit, but differ in how the keys are stored and processed (Premium supports HSM-backed keys).

**The two authorization planes**
- **Control plane** — governs vault-level administration: create/delete the vault, configure network and firewall rules, assign Azure policy, and view vault metadata. It does not grant access to the actual secrets, keys, or certificates stored inside.
- **Data plane** — governs access to the vault's contents: reading and writing keys, secrets, and certificates.
- Microsoft Entra ID validates identity for both planes, and access to each plane is independent of the other.

**Access control: Azure RBAC vs. Vault Access Policies**
- **Azure RBAC** (Microsoft's recommended model) — best for environments adopting a unified Zero Trust model. It offers one consistent authorization model across Azure, auditable and scoped role assignments, and works cleanly with managed identities. It operates through two core steps: authentication and authorization.
- **Vault Access Policies** (legacy pattern) — used to limit permissions per user or resource. Risks include:
  - High risk of policy drift.
  - A separate permission model per vault.
  - Still visible in many existing environments.
    
**Managed Identity Secret retrieval flow**
<img width="940" height="378" alt="image" src="https://github.com/user-attachments/assets/af8cc48b-786e-4034-a7bd-16019e36c878" />


**Managed identities**
- **System-assigned identity** — a one-to-one relationship between identity and resource. It's tied to a specific resource, can't be shared, and is deleted automatically when the resource is deleted. Best for simple, single-resource workloads.
- **User-assigned identity** — a one-to-many relationship. It exists independently of any single resource and persists even if an application is deleted. Best for sharing one identity across a fleet of resources.

**Network and data protection controls**
- Firewall and network access restrictions.
- Soft delete and purge protection.
- Operational guardrails.

**Defender for Key Vault**
- Provides HSM support, certificate auto-renewal, key rotation policies, and CSPM secret scanning.
- Not enabled by default — must be turned on manually in the Azure portal under Microsoft Defender for Cloud.

## My Takeaways
<!-- What was most valuable to you personally from this session? -->
Understanding the split between the control plane and data plane clarified why an administrator can manage a vault's configuration without ever being able to read its secrets — and why Azure RBAC is the safer, more auditable choice over legacy Vault Access Policies.

Seeing how a single exposed secret (like a SAS token in an AI script) can cascade into a full workload compromise made the case for defense-in-depth — combining managed identities, RBAC, network controls, and Defender for Key Vault — much more concrete.

---

## Questions I Still Have
<!-- Anything you want to follow up on or ask the mentor -->
-I want to do the Lab but failed to get access to the Portal.
-

---

## Resources I Found Useful
<!-- Any links, docs, or Microsoft Learn modules you found helpful -->
- [Implement Azure Key Vault — Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/implement-azure-key-vault/)
- [Microsoft Defender for Key Vault: benefits and features](https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-for-key-vault-introduction)
- [Security recommendations for AI workloads on Azure infrastructure — Cloud Adoption Framework](https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/scenarios/ai/infrastructure/security)
- [Azure AI security best practices](https://learn.microsoft.com/en-us/azure/security/fundamentals/ai-security-best-practices)
- [Understand how Microsoft Defender for Cloud supports AI security and governance in Azure — Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/defender-for-cloud-ai-understand-protections/)


---

*Submitted by: Berna Namulyowa · nbernah*

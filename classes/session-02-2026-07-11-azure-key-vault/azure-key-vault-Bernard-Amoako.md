# My Notes — [Bernard Amoako Agyemang]

---

## Key Concepts I Learned

- Azure Key Vault is a cloud service that securely stores and manages secrets(passwords, API keys, connection strings), encryption keys (cryptographic keys), and certificates(TLS/SSL certificates) in a single, centralised vault. 
  
- Data protection features of Azure Key Vault include **soft delete** (recover from accidental deletion), **purge protection** (prevent permanent removal), **network restrictions** (limit exposure), and **automated rotation** of secrets/keys. 
  
- The two access‑control of Azure Key Vault are: legacy **Access Policies** (per‑vault, data‑plane only) and recommended **Azure RBAC** (unified, covers control + data plane, and is the default for new deployments). 
  
- Defence‑in‑depth for Key Vault combines perimeter security (firewalls), identity & access (managed identities, least‑privilege RBAC), data encryption, monitoring & auditing (Azure Monitor, logs, alerts), and operational safeguards (soft delete, purge protection, rotation). 
  
- Managed identities allow Azure resources (VMs, App Services, Functions) to access Key Vault without hard‑coding credentials. 
  
- Best practice recommends **one vault per application, per region, and per environment** to limit the blast radius of a potential breach.

---

## Lab / Hands-On Work
### What I did
- Observed the end‑to‑end secure integration: App Service (with System‑Assigned Managed Identity) → Microsoft Entra ID authentication → Azure Key Vault secret storage.

- Watched the instructor configure RBAC roles (`Key Vault Secrets Officer` for admin, `Key Vault Secrets User` for the Managed Identity) and enable System‑Assigned Managed Identity from the App Service Identity tab.
   
- Explored the Kudu+ debug console to acquire the Identity Endpoint token via PowerShell and retrieve a secret—revealing the behind‑the‑scenes authentication flow.

- Witnessed a troubleshooting session where secret retrieval failed due to the Access Configuration being set to `Vault Access Policy` instead of `RBAC`, highlighting the critical role of correct permission configuration.
   
- Reviewed networking restrictions (firewall, VNet integration), Microsoft Defender for Cloud, and Diagnostic Settings (audit logs) as essential hardening and monitoring layers.
### What happened / Result
- The zero‑credential pattern was fully demonstrated—Managed Identity issues a token via IMDS, the token is exchanged for Key Vault access, and secrets are retrieved without any hard‑coded credentials.
   
- The RBAC misconfiguration error was a powerful lesson—a single incorrect permission model setting can break the entire access flow, reinforcing the importance of selecting the right model from the start.

- Networking restrictions and diagnostic logging were presented as critical non‑negotiable layers for defence‑in‑depth, providing both perimeter protection and full access traceability.
### Challenges I faced
- Not having my own Azure subscription meant I couldn't follow along hands‑on or test alternative configurations during the session.

- The authentication flow (Managed Identity → IMDS token → Key Vault access) didn't fully click on first viewing—rewatching the video was essential to internalise each step.

- The permission model confusion (Access Policies vs. RBAC) only became clear when the error occurred; the troubleshooting segment made the concept stick far better than theory alone.

---

## My Takeaways

- Centralising secrets in Key Vault eliminates the massive security risk of hard‑coding credentials in source code or configuration files.

- RBAC is the clear recommendation for new deployments—it’s more secure, unified across Azure, and simpler to audit than legacy Access Policies.

- A true defence‑in‑depth strategy for Key Vault must cover network restrictions, identity management, encryption, active monitoring, and operational safeguards (soft delete / purge protection).

- Managed identities are a game‑changer because they let Azure resources (VMs, Functions, App Services) authenticate to Key Vault without any manual credential handling.

---

## Questions I Still Have

- I have none at the moment.

---

## Resources I Found Useful

- **YouTube Channel:** [Microsoft Naija Security User Group](https://youtu.be/GKqpej4X9B0?si=4fXrcMCoIKR4mtif)
- **Microsoft Learn Module:** [Configure and manage Azure Key Vault](https://learn.microsoft.com/en-us/training/paths/configure-key-vault-security/)

---

*Submitted by: [Bernard Amoako Agyemang] · [sudoNard]*

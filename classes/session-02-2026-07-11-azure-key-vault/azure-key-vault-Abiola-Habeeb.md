# My Notes — Abiola Habeeb

---

## Key Concepts I Learned

This session covered **securing Azure Key Vault with a defense-in-depth approach** for cloud and AI workloads. The theme throughout was "everything starts and ends with identity."

- **Why Key Vault exists — the risk model.** Developers commonly hardcode secrets, API keys, and credentials directly in source code, app config, or IaC templates (e.g. Terraform), leave long-lived secrets shared across services, and never rotate them. In an AI workload a single exposed secret can escalate into full workload compromise: secret in config → credential discovered (from a repo, logs, or dumps) → privilege reuse → data exfiltration and unauthorized execution. The recommended pattern is to **store secrets in Key Vault, use RBAC + managed identities, rotate/version secrets centrally (every 3–6 months), and monitor with Defender** — together these replace hardcoded secrets across the stack.
- **The three Key Vault object types.** **Secrets** (passwords, connection strings, API keys — alphanumeric, used by apps/automation at runtime); **Keys** (cryptographic keys for encrypt/decrypt/sign — RSA or EC, sizes 2048/3072/4096, with rotation policies); and **Certificates** (TLS for websites/apps). Key Vault integrates with two trusted certificate authorities — **DigiCert and GlobalSign** — where you hold an account *outside* Azure; alternatively you can import a third-party X.509 certificate along with its private key.
- **Two authorization planes (a key gotcha).** The **control plane** manages the vault itself (create/delete the vault, configure network/firewall, assign policy, view metadata — roles like Key Vault Contributor/Owner). The **data plane** is the actual content (read/write secrets, keys, certificates). **Control-plane access does NOT grant data-plane access** — they are independent authorization decisions, so you must be assigned a role *on the vault itself* (e.g. having Owner on the subscription is not enough to read a secret).
- **RBAC over legacy Access Policies.** Microsoft is deprecating vault Access Policies and has asked all customers to migrate to **Azure RBAC** — it gives a unified, zero-trust, auditable authorization model, whereas access policies risk policy drift and aren't cleanly auditable. Activity logs retain **90 days**.
- **Managed Identity (MSI) flow.** The identity requests a token → Entra ID validates it and issues a token → the app presents it to Key Vault as a **bearer token** → the vault authorizes and returns the value. Every managed identity shows up as an enterprise application; tokens **auto-rotate every 24 hours** (no manual rotation), and all access is logged. **System-assigned** identity is 1:1 and tied to its resource's lifecycle (deleted with it); **user-assigned** is standalone, reusable across many resources, and independent — the two can coexist.
- **Network and data protection.** Restrict with firewall (trusted networks only), **private endpoints**, and disabling public network access with explicit exceptions — but note this can break Microsoft-managed services that need to reach the vault (Azure Monitor, Azure Backup), so balance with a private endpoint. **Soft delete** is on by default on new vaults (7–90 day retention, restorable with the right permission and cannot be turned off), and **purge protection** blocks irreversible destruction — once enabled and deleted, the vault stays for the full retention period and *even Microsoft cannot purge it early* (a real cost concern with Managed HSM, billed hourly).
- **Defender for Key Vault** is **not enabled by default** — you enable it in Defender for Cloud at subscription level. It detects suspicious/malicious access patterns and abuse paths and gives actionable recommendations.
- **Least privilege for the vault.** There are many Key Vault RBAC roles (Administrator, Reader, Secrets Officer, Secrets User, Certificate Officer/User, Crypto Officer/User). Assign the **minimum** needed — e.g. **Key Vault Secrets User** just to read a secret.

---

## Lab / Hands-On Work

### What I did


### What happened / Result


### Challenges I faced


---

## My Takeaways

Through this training I now understand that Key Vault is a core part of a zero-trust, defense-in-depth strategy — it's the "bank vault" where secrets, keys, and certificates live so they never have to be hardcoded. The single biggest lesson was the **control-plane vs data-plane distinction**: being an Owner or having a broad subscription role does not automatically let you read a secret, and this trips up a lot of people. I also now see *why* the security process matters even though developers often want to cut corners — if a workload is compromised, it's the security engineer who has to investigate, and an environment that isn't compliant (e.g. not using Key Vault) gets flagged by Azure Policy and fails audits like ISO 27001. Combining RBAC + managed identity + monitoring is what removes hardcoded secrets safely.

---

## Questions I Still Have

- When migrating from legacy Access Policies to RBAC, what's the safest rollout order so live workloads don't lose access mid-migration?
- For the managed-identity fetch that briefly failed with a "does not have secret get permission" error — beyond RBAC propagation delay, what are the usual root causes to check first?
- Can Key Vault diagnostic logs be exported to an external SIEM (e.g. Splunk / Sentinel), and what's the recommended connector approach?

---

## Resources I Found Useful

- Bootcamp — Naija AI and Cloud Security (Microsoft Naija Security Usergroup) GitHub
- [Microsoft Learn — Configure and secure Azure Key Vault; manage keys, secrets, and certificates](https://learn.microsoft.com/en-us/azure/key-vault/secrets/secure-secrets)
- [Microsoft Learn — Azure RBAC for Key Vault and managed identities](https://learn.microsoft.com/en-us/azure/key-vault/general/rbac-guide)
- [Microsoft Learn — Microsoft Defender for Key Vault](https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-for-key-vault-introduction)

---

*Submitted by: Abiola Habeeb · https://github.com/abiolahabeeb*

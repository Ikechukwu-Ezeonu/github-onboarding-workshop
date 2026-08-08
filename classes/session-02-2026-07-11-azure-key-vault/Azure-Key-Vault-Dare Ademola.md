# SC-500 Learning Notes: Week 3

## Topic: Secure Azure Key Vault with Defense in Depth (Cloud & AI Workloads)

### Key Concepts I Learned

#### 1. Defense in depth
Layered, independent security controls across identity, network, and monitoring, arranged so that no single control's failure results in compromise. Key Vault is not a single product fix; it is one layer in a wider strategy.

#### 2. Why app configuration is the wrong place for secrets

| Anti-pattern | Security-engineered pattern |
|---|---|
| API keys and tokens in app settings | Store secrets in Azure Key Vault |
| Credentials copied into IaC templates | Use RBAC and managed identities |
| Long-lived secrets shared across services | Rotate and version secrets centrally |
| No rotation ownership | Monitor anomalous access with Defender |

**Bottom line:** Key Vault, RBAC, and managed identities replace hardcoded secrets everywhere in the stack.

#### 3. Threat model: the AI workload secret exposure chain
1. **Secret stored in config:** key appears in app settings or code.
2. **Credential discovered:** attacker finds it via repo, logs, or memory dumps.
3. **Privilege reuse:** the secret grants access to the vault, data stores, or APIs.
4. **Impact:** data exfiltration and unauthorized workload execution.

#### 4. Key Vault object types

| Object | Holds | Used for |
|---|---|---|
| Secrets | Passwords, connection strings, API keys | Apps and automation at runtime |
| Keys | Cryptographic keys (encrypt / decrypt / sign) | Key lifecycle, rotation, crypto operations |
| Certificates | X.509 certificates and lifecycle renewal | TLS and workload trust boundaries |

#### 5. Access model: two planes, two authorization decisions
Both planes authenticate through Microsoft Entra ID, but authorization is independent on each. Control-plane access does **not** automatically grant data-plane access, and vice versa.

| | Control plane | Data plane |
|---|---|---|
| Governs | The vault itself | Items inside the vault (keys, secrets, certs) |
| Uses | Azure Resource Manager (ARM) token | Data-plane token |
| Operations | Create/delete vault, configure network & firewall, assign Azure Policy, view metadata | Read/write keys, secrets, certificates |
| Roles | Key Vault Contributor, Owner | Secrets User, Crypto Officer, Certificates Officer, Administrator |

#### 6. Azure RBAC vs legacy vault access policies

| Azure RBAC (recommended) | Vault access policies (legacy) |
|---|---|
| Unified authorization model across Azure | Separate permission model per vault |
| Role assignments are auditable and scoped | Higher risk of policy drift |
| Works cleanly with managed identities | Still visible in existing environments |

Migrate to RBAC wherever you control the vault.

#### 7. Managed Identity secret retrieval flow
Fetches secrets with zero stored credentials. One-time setup: assign a managed identity to the resource, then grant it RBAC access to Key Vault.
1. **Request token:** the SDK requests a token from the local IMDS endpoint.
2. **Authenticate:** Entra ID verifies identity and issues a token.
3. **Call Key Vault:** the app presents the token as Bearer auth.
4. **Authorize & return:** RBAC is checked; the secret is returned over TLS.

**Benefits:** no hardcoded credentials, passwordless auth, tokens auto-rotate (~24h), every access logged and auditable.

#### 8. Managed Identity: two types

| System-assigned | User-assigned |
|---|---|
| One identity, one resource | One identity, many resources |
| Created directly on a single resource | Created as its own standalone resource |
| Deleted automatically with the resource | Persists until explicitly deleted |
| Cannot be shared | Attached to multiple resources at once |
| Best for single-resource workloads | Best for sharing one identity across a fleet |

#### 9. Network and data protection controls
- **Firewall / network access:** allow trusted networks only; use private endpoints for sensitive workloads; treat public network access as an explicit exception. (Note: disabling public access affects some Microsoft-managed services such as Azure Monitor and Backup; review the "trusted Microsoft services" bypass before enabling it.)
- **Soft delete:** preserves deleted objects in a recoverable state for 7 to 90 days (default 90). Enabled by default on new vaults, cannot be disabled after creation, and the retention period is set only at creation.
- **Purge protection:** blocks permanent (irreversible) deletion of a soft-deleted object until retention expires, regardless of permissions. Even subscription owners are blocked. Critical for encryption-at-rest: if the protecting key is destroyed, the data becomes unreadable.
- **Operational guardrails:** least-privilege role assignments, rotation ownership and interval policy, alerting and incident-response integration.

#### 10. Microsoft Defender for Key Vault
Surfaces suspicious access patterns and anomalous operations, potential abuse paths across identity and resource context, and actionable recommendations in Defender for Cloud. **Not enabled by default:** enable it per-service under *Defender for Cloud → Environment settings → select subscription → toggle Microsoft Defender for Key Vault*. It then applies to all vaults in the subscription.

**Alert response (4 steps):**
1. Identify the source: which identity triggered the alert, and is it recognized?
2. Respond to the immediate threat: restrict or remove access to stop further exposure.
3. Measure the impact: which secrets were accessed, and for how long?
4. Take action: rotate affected credentials and notify downstream application owners.

---

### Lab / Hands-On Work: Deploy and Secure Azure Key Vault
Entirely through the Azure Portal. Target architecture: App/VM → Managed Identity → Entra ID (authenticates) → Key Vault (RBAC-controlled, network-restricted, fully audit-logged).

**Part 1: Deploy and configure access**
1. **Create the vault:** search Key Vaults → **+ Create** → set a unique name, region, and resource group → **Review + Create**.
2. **Configure RBAC:** open **Access control (IAM)** → **+ Add → Add role assignment** → assign **Key Vault Secrets Officer** to your account.
3. **Add a secret:** **Objects → Secrets → + Generate/Import** → enter a name and value → **Create**.

**Part 2: Secure and verify**
4. **Restrict network access:** **Networking** → set Public access to **Disabled** or **Selected networks** → **Save**.
5. **Connect via managed identity:** enable a **system-assigned identity** on the app/VM → in the vault's IAM, assign **Key Vault Secrets User** → confirm under role assignments.
6. **Enable monitoring:** **Monitoring → Diagnostic settings** → add a setting, enable **AuditEvent** → send logs to a **Log Analytics workspace**.

**What happened / Result**
- Yet to complete the lab due to infrastructure availability

**Challenges I faced**
- 

---

### My Takeaways
- Use Key Vault as the authoritative secret, key, and certificate boundary.
- Prefer Azure RBAC with managed identities for workload access over legacy access policies.
- Apply firewall controls plus soft delete and purge protection as anti-destruction guardrails.
- Enable Defender for Key Vault and validate findings during posture reviews.
- Control-plane and data-plane authorization are independent; grant each deliberately.

---

### Questions I Still Have
- N/A

---

### Resources I Found Useful
- Microsoft Learn path: [Configure and manage secrets in Azure Key Vault](https://learn.microsoft.com/en-us/training/paths/configure-key-vault-security/)
- Related certifications: SC-300 (closest fit), AZ-500, SC-100

---

_Submitted by: Dare Ademola (Oluwatidamilare)_

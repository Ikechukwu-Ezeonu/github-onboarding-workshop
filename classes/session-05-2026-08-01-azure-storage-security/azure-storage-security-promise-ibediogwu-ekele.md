# My Notes — Promise Ibediogwu Ekele

---

## Key Concepts I Learned

### 1. Storage Account Keys Are a Master Password — Treat Them That Way

The most important anti-pattern covered in this session was the common practice of hardcoding storage account keys directly in application code or sharing them across teams. A storage account key grants full, unrestricted access to every service in the account — blob, file, queue, and table — with no expiry and no scope limit. If a key leaks, the attacker owns everything.

The Mentor emphasized that many real-world breaches start from a storage key found in a public GitHub repository or embedded in a configuration file. The fix: move toward **Microsoft Entra ID (RBAC)** authentication and use **Azure Key Vault** to store any remaining secrets.

The comparison that crystallized this for me:

| Authentication Method | Scope | Lifespan | Security Level |
|---|---|---|---|
| **Storage Account Keys** | Global — full account access | Permanent (until rotated) | ⚠ High Risk |
| **SAS Tokens** | Limited — service or resource level | Time-bound | 🟡 Moderate Risk |
| **Entra ID (RBAC)** | Granular — user, group, managed identity | Session-bound | ✅ Best Practice |

---

### 2. Private Endpoints: Keeping Storage Traffic Off the Public Internet

A private endpoint assigns a **private IP address** from your Virtual Network (VNet) directly to your storage account. Once configured, the storage account is reachable only from within the VNet — or through connected networks like VPN or ExpressRoute. Traffic never traverses the public internet.

Without private endpoints, even a hardened storage account with firewall rules is still a public internet endpoint — visible to port scanners and brute-force attempts. Private endpoints make the account invisible to the public internet entirely.

- **Before private endpoint:** Storage account accessible via public endpoint — firewall rules provide the only protection
- **After private endpoint:** Storage account has no public endpoint — traffic routes through VNet private IP (10.x.x.x)
- **DNS resolution:** A private DNS zone must be configured so `storageaccount.blob.core.windows.net` resolves to the private IP, not the public one

---

### 3. Shared Access Signatures (SAS) — Scope and Revocability Matter

SAS tokens grant time-limited, scoped access to specific resources without sharing account keys. The session made a distinction I had not fully understood before:

| SAS Type | Signed By | Max Duration | Revocation | Recommended? |
|---|---|---|---|---|
| **Account SAS** | Storage account key | Arbitrary | Rotate account key (disruptive) | ❌ Avoid |
| **Service SAS (stored policy)** | Account key via stored access policy | Set by policy | Delete the policy — instant | ✅ Yes |
| **User Delegation SAS** | Entra ID user credential | Max 7 days | Revoke Entra ID token | ✅ Best practice |

> **Personal insight from a project called FinTrust I did:** During my hands-on work, I discovered this distinction directly — the portal defaults to User Delegation SAS, which caps at ~7 days and cannot reference a stored access policy. For 90-day auditor access with an instant kill switch, I needed a Service SAS backed by a stored access policy. The session explained *why* this matters from a security architecture perspective.

---

## Lab / Hands-On Work

Following the session demonstration, I applied the security concepts directly to my **FinTrust Financial Services** storage project — a lab environment I built. The scenario: migrating sensitive client documents (KYC records, loan files, audit reports) from laptops and USB drives to hardened Azure Blob Storage.

---

### What I Did

#### Step 1 — Hardened the Storage Account Baseline

I applied the anti-pattern fixes our mentor outlined:

- **Disabled anonymous blob access** — every request must present a valid credential
- **Enforced HTTPS-only** with TLS 1.2 minimum
- **Disabled shared key access** where possible, shifting toward Entra ID authentication
- **Configured blob soft delete (14 days)** and blob versioning to protect against accidental deletion and overwrites

![Configuration-blade](https://github.com/promibe/assets/blob/main/shot-2.png)

![Data protection blade showing soft delete (14 days) and versioning enabled](https://github.com/promibe/assets/blob/main/Shot-12-enabling-versioning-and-soft-delete.png)

#### Step 2 — Implemented Entra ID RBAC at Container Scope

Rather than using storage account keys for internal staff access, I created Entra ID security groups and assigned data-plane roles **at container scope** — not account scope. This directly implements what Emmanuel called "the shift from legacy storage account keys to Entra ID."

- `FinTrust-Docs-Readers` → Storage Blob Data Reader on `client-documents` only
- `FinTrust-Docs-Contributors` → Storage Blob Data Contributor on `client-documents` only

**Why container scope matters:** Assigning at account scope grants access to all containers — audit-reports, archive-records — regardless of role. Container scope enforces least privilege at the resource level, which the speaker identified as a core defense-in-depth principle.

![Container IAM blade showing group role assignments at container scope.](https://github.com/promibe/assets/blob/main/shot-4-RBAC-assignment.png)

---

#### Step 3 — Tested Access Controls with Negative Tests

The speaker's most important point: **security must be verified through what it blocks, not just what it allows.** I tested both the happy path and the denial path:

- Reader user downloads a file → ✅ Allowed
- Reader user attempts upload → ❌ `AuthorizationPermissionMismatch` — role does not permit write

![Reader user downloading a file successfully](https://github.com/promibe/assets/blob/main/shot-5-Ada-successfully-downloaded-the-file.png)

![Reader user denied on upload — error visible in portal](https://github.com/promibe/assets/blob/main/shot-6-Ada-unable-to-upload-a-file.png)

---

#### Step 4 — Implemented SAS with Stored Access Policy (Revocable Access)

This was the most directly relevant lab exercise to the session. External auditors needed 90 days of read-only access but had no company accounts — exactly the scenario Emmanuel referenced when discussing SAS tokens as a controlled alternative to account keys.

I generated a **Service SAS** backed by a stored access policy named `auditor-q3-2026`. The SAS token carries no permissions itself — it references the policy by name. Deleting the policy instantly invalidates every SAS built on it.

**Testing read-only enforcement (R4):**

![Azure Storage Explorer connected via SAS token. No Azure login — anonymous, account-less access. Activity log confirms "used SAS, discovery completed"](https://github.com/promibe/assets/blob/main/Shot-9-Accessing-the-blob-container-with-storage-explorer.png)

**Write attempt blocked:**

![AzCopy upload attempt: RESPONSE 403 AuthorizationPermissionMismatch. Total bytes transferred: 0. Least privilege enforced](https://github.com/promibe/assets/blob/main/Shot-10b-failed-to-copy-file-into-the-blob-container-using-Azcopy.png)

**The kill switch — policy deleted:**

![Same SAS token after stored access policy deleted: ERROR CODE: AuthenticationFailed. "SAS identifier cannot be found for specified signed identifier." Instant revocation without rotating account keys](https://github.com/promibe/assets/blob/main/Shot-11-failed-to-download-file-after-deleting-the-access-policy.png)

---

#### Step 5 — Lifecycle Management for Cost-Aligned Data Tiering

Mr Emmanuel covered storage redundancy options (LRS, ZRS, GZRS) and the importance of aligning cost to access frequency. I implemented this through lifecycle management rules on the archive container:

- Not modified in 90 days → Cool tier
- Not modified in 365 days → Archive tier

![Lifecycle rule showing the tiering conditions and the JSON policy code view](https://github.com/promibe/assets/blob/main/Shot-14-Lifecycle-management.png)

---

### What Happened / Result

| Test Performed | Expected Result | Actual Result | Session Concept |
|---|---|---|---|
| Entra ID Reader uploads a blob | Denied | ✅ `AuthorizationPermissionMismatch` | RBAC least privilege |
| Entra ID Reader downloads a blob | Allowed | ✅ File downloaded successfully | Identity-based access |
| Auditor SAS token: upload attempt | Denied | ✅ `403 AuthorizationPermissionMismatch` — 0 bytes transferred | SAS scoped permissions |
| Auditor SAS token: delete policy | SAS becomes invalid | ✅ `403 AuthenticationFailed` — "SAS identifier not found" | Revocability — kill switch |

---

### Challenges I Faced

**User Delegation SAS vs Service SAS:** The portal defaults to User Delegation SAS, which caps at ~7 days and cannot reference stored access policies. For the 90-day auditor scenario I needed a Service SAS signed with the account key. This forced me to understand why the session distinguishes between SAS types — they have fundamentally different signing mechanisms and revocation paths.

**The `$root` mystery:** When I pasted a raw container SAS URL into a browser without `restype=container&comp=list`, Azure interpreted the path as a blob in the hidden `$root` container and returned "Signature did not match." The fix was two API parameters that tell the REST API the resource is a container, not a blob. This taught me that Blob Storage is a raw REST API — the SDK and Storage Explorer handle this invisibly, which is why the lab demo in the session looked seamless.

**Control plane vs data plane:** Being Owner of a storage account does not grant permission to read blobs with Entra ID authentication. Owner is a control-plane role (manage the Azure resource); Storage Blob Data Reader is a data-plane role (read the actual data). The session covered this distinction conceptually — I learned it by hitting the error.

---

## My Takeaways

The most valuable insight from this session was the framing of storage security as **three distinct layers**:

| Layer | Question | Azure Control | HTTP Error if Rejected |
|---|---|---|---|
| **Network** | Can the request physically reach the endpoint? | Private endpoints, firewall rules, public network access toggle | `AuthorizationFailure (403)` |
| **Authentication** | Has the request proven who it is? | SAS tokens, Entra ID, account keys | `AuthenticationFailed (403)` |
| **Authorization** | Is that identity allowed this operation? | RBAC roles, SAS permissions, stored access policies | `AuthorizationPermissionMismatch (403)` |

Every security control in the session maps to one of these layers — and every error I encountered in the lab produced a different HTTP status code depending on which layer rejected the request. Being able to read which layer failed from the error code alone cuts debugging time significantly.

The session also reinforced that **Microsoft Defender for Storage is not optional** for production environments. The speaker's guidance — use Azure Policy to audit or deny creation of storage accounts without Defender enabled — provides organizational enforcement at scale, which is meaningfully different from enabling it manually per account.

**Personal connection to my FinTrust project:** Every lab step in this session I had already encountered in practice during my AZ-104 project work. The session gave me the *why* — the security architecture reasoning behind decisions I had made because the project brief required them. SAS tokens with stored access policies are not just a portfolio technique; they are the recommended pattern for time-limited external access precisely because they support instant revocation without disrupting other credentials.

---

## Questions I Still Have

- **Private endpoint DNS in hybrid environments:** The session showed private endpoints in an all-Azure scenario. In a hybrid setup where on-premises apps must also reach the storage account, how does DNS resolution work — does the private DNS zone integrate with on-premises DNS, and what are the gotchas?

- **Defender for Storage cost at scale:** The speaker mentioned ~$10/month per account plus malware scanning fees. For an organization with hundreds of storage accounts, is there a way to estimate or cap the scanning cost before enabling at scale?

- **Stored access policy rotation strategy:** If a SAS token backed by a stored access policy is widely distributed to hundreds of clients, what is the recommended rotation pattern — create a new policy, distribute the new SAS, then delete the old policy? Is there a recommended overlap window?

---

## Resources I Found Useful

- [Microsoft Learn — Authorize access to blobs using Microsoft Entra ID](https://learn.microsoft.com/azure/storage/blobs/authorize-access-azure-active-directory)
- [Microsoft Learn — Grant limited access to Azure Storage resources using SAS](https://learn.microsoft.com/azure/storage/common/storage-sas-overview)
- [Microsoft Learn — Use private endpoints for Azure Storage](https://learn.microsoft.com/azure/storage/common/storage-private-endpoints)
- [Microsoft Learn — Microsoft Defender for Storage](https://learn.microsoft.com/azure/defender-for-cloud/defender-for-storage-introduction)
- [My FinTrust Project — GitHub](https://github.com/promibe/fintrust-secure-storage)

---

*Submitted by: Promise Ibediogwu Ekele — https://github.com/promibe*

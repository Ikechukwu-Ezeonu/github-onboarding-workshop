# My Notes — Marycynthia Okeke

## Key Concepts I Learned
Azure Key Vaults & Defense-in-Depth

During this class, I gained a better understanding of how Azure Key Vault strengthens security by providing a centralized location for storing and managing sensitive information.

I learned that Azure Key Vault is the recommended service for securely storing secrets, encryption keys, and certificates instead of embedding them in applications or configuration files.

I also learned about the importance of key rotation, centralized secret versioning, and monitoring suspicious access patterns with Microsoft Defender. These practices help reduce the risk of compromised credentials and improve an organization's overall security posture.

One important takeaway was understanding how the exposure of a single secret can potentially lead to the compromise of an entire workload if proper security controls are not in place.

For certificate management, Azure Key Vault can integrate with DigiCert and GlobalSign for certificate issuance and lifecycle management. However, an organization must maintain a separate account with either provider, as these services are not automatically included with Microsoft Azure.

Azure Key Vault Authorization Models: I learned that Azure Key Vault supports two authorization planes:

Control Plane – Used to manage the Key Vault resource itself (creation, configuration, deletion, and access management).
Data Plane – Used to access the data stored inside the vault, such as secrets, keys, and certificates.
Azure RBAC (Role-Based Access Control): Azure RBAC is the modern and recommended authorization model for Azure Key Vault because it:

Provides a unified access management model across Azure resources.
Supports scoped and auditable role assignments.
Integrates seamlessly with managed identities.
Simplifies access management compared to older permission models.
Legacy Access Policies: I also learned about Legacy Access Policies, which:

Use a separate permission model for each Key Vault.
Can introduce policy drift over time due to inconsistent configurations.
Are still available in many existing Azure environments but are gradually being replaced by Azure RBAC.
Core Components of Azure Key Vault Azure Key Vault is designed to manage three primary types of sensitive assets:

Secrets -Used to securely store sensitive information such as:

Passwords -API keys -Connection strings

Keys -Used for cryptographic operations, including: a. Encryption b. Decryption c. Digital signing

Certificates -Used to manage X.509 certificates and support their issuance, storage, and renewal throughout their lifecycle.

Managed Identities I learned about the two types of managed identities available in Azure: -System-Assigned Managed Identity *Created and enabled directly on an Azure resource. *The identity has the same lifecycle as the resource. *Intended for use by a single Azure resource.

-User-Assigned Managed Identity *Created as an independent Azure resource. *Can be assigned to multiple Azure resources. *Enables identity reuse across different services and workloads. *Data Protection and Network Security Controls

I also learned about several security features that help protect Azure Key Vault:

* Firewall and Network Access – Restricts access to the Key Vault using network rules and private connectivity.
* Soft Delete and Purge Protection – Prevents accidental or malicious deletion of vault contents by allowing recovery and protecting against permanent removal.
   Operational Guard Rails – Provides built-in safeguards and governance features that help maintain secure configurations and reduce operational risks.

---

## Lab / Hands-On Work

I observed the class demo but will participate fuly when practice accounts are created for us.

### What I did


### What happened / Result


### Challenges I faced


---

## My Takeaways

My key take away is the knowledge of how to use azure key vault to secure secrets and passwords in Azure

---

## Questions I Still Have

---

## Resources I Found Useful

---

*Submitted by: Marycynthia Okeke · Nechy-Okeke*

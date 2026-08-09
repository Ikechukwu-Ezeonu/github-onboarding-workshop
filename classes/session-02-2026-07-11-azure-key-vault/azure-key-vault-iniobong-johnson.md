# My Notes — Iniobong Johnson

---

## Key Concepts I Learned

### Key Vault Authorization Models
- I learned about the two access authorization models for Azure Key Vault, the Control Plane and the Data Plane.
- The Control Plane is used to manage the Key Vault resource itself. Roles such as Owner and Key Vault Contributor can perform actions such as creating or deleting a Key Vault, assigning Azure policies, and configuring network and firewall settings.
- The Data Plane controls access to the information stored inside the Key Vault, including secrets, keys, and certificates. Data Plane access can be granted through roles such as Key Vault Secrets User, Key Vault Crypto Officer, Key Vault Administrator, and Key Vault Certificates Officer.
- Having access to the Control Plane does not automatically provide access to the Data Plane. Access to both planes must be authorized independently.

### Azure Role Based Access Control
- The recommended access control model for Azure Key Vault is Azure Role Based Access Control, Azure RBAC.
- Azure RBAC provides a unified authorization model and allows role assignments to be reviewed and audited. This makes it easier for organizations to monitor who has access to Key Vault resources and what actions they are allowed to perform.

### Managed Identities
- I also learned about Managed Identities, which are available in two forms, system assigned and user assigned.I also learned about Managed Identities, which are available in two forms, system assigned and user assigned.
- A system assigned managed identity is connected to one Azure resource. Its lifecycle is tied to that resource, which means the identity is automatically deleted when the resource is deleted.
- A user assigned managed identity is created as a separate Azure resource. One user assigned identity can be connected to several Azure resources.
-System assigned and user assigned managed identities can also be used together, depending on the requirements of the organization.

### Soft Delete and Purge Protection

Another concept that stood out to me was soft delete and purge protection.
- Soft delete is automatically enabled by Microsoft. It helps protect Key Vaults and their contents from accidental or unauthorized deletion by allowing deleted resources to remain recoverable for a specified retention period.
- Purge protection provides an additional layer of protection. Once purge protection is enabled, it cannot be disabled. A deleted Key Vault cannot be permanently removed until the retention period has ended.
- During the retention period, the same Key Vault name cannot be reused. This may affect users who rely on paid third party services connected to the deleted Key Vault because they may continue to incur charges while waiting for the retention period to end.

### Key Vault Naming

When creating a Key Vault, Azure checks whether the chosen name is already being used. Key Vault names must be globally unique before Azure approves the creation of the resource.

---

## My Takeaways

My major takeaway from the session was the instructor’s advice about logging out of web applications when they are no longer being used.
- When a user logs in again, the application usually creates a new session. If an attacker gains access to browser information or session data, they may be able to manipulate or hijack the active session.
- This reinforced the importance of properly ending sessions, protecting browser data, and following secure authentication practices.

---

*Submitted by: Iniobong Johnson · Inib12*

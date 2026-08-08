# My Notes — [Oroma Jemima Unufe]

> # What I Learnt – Day 3 (Cloud & AI Security Bootcamp)

* Azure Key Vault is the recommended service for securely storing **secrets, cryptographic keys, and certificates** instead of keeping them in application code or configuration files.

* Storing API keys, passwords, tokens, or connection strings in application settings is a security anti-pattern because they can be exposed through source code, logs, or configuration files.

* A single exposed secret can lead to an attack chain: **secret exposure → credential discovery → privilege misuse → data theft or system compromise**.

* Azure Key Vault stores three types of objects:

  * **Secrets** – passwords, API keys, connection strings, and tokens.
  * **Keys** – cryptographic keys used for encryption, decryption, and digital signatures.
  * **Certificates** – X.509 certificates used for TLS/HTTPS and secure communication.

* Azure Key Vault uses two authorization planes:

  * **Control Plane** – manages the Key Vault resource (creation, deletion, networking, firewall, and policies).
  * **Data Plane** – manages the data inside the Key Vault (reading and writing secrets, keys, and certificates).

* Microsoft Entra ID authenticates users, applications, and services before they are granted access to Azure Key Vault.

* Access to the **Control Plane** does not automatically grant access to the **Data Plane**, and vice versa.

* Azure **Role-Based Access Control (RBAC)** is the recommended authorization model because it provides centralized, auditable, and scalable access management.

* **Vault Access Policies** are the older (legacy) authorization model and are gradually being replaced by Azure RBAC.

* **Managed Identity** allows Azure resources to authenticate securely without storing passwords or secrets in application code.

* The Managed Identity secret retrieval process involves:

  1. Requesting an authentication token.
  2. Authenticating through Microsoft Entra ID.
  3. Accessing Azure Key Vault using the token.
  4. Azure RBAC verifying permissions before returning the secret.

* Managed Identities eliminate hardcoded credentials, automatically rotate tokens, and ensure every access is logged for auditing.

* There are two types of Managed Identity:

  * **System-Assigned Managed Identity** – created for a single Azure resource and deleted when that resource is deleted.
  * **User-Assigned Managed Identity** – created independently and can be shared across multiple Azure resources.

* Additional security controls for Azure Key Vault include:

  * Configuring firewall and network restrictions.
  * Enabling Soft Delete and Purge Protection.
  * Using Microsoft Defender for Key Vault to monitor threats and investigate security alerts.

* The overall best practice is to centralize secrets in Azure Key Vault, use Azure RBAC with Managed Identities, and continuously monitor access using Microsoft Defender.

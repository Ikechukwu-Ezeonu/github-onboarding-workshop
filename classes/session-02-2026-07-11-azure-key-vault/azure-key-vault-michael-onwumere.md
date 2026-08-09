# My Notes - Michael Chinonso Onwumere

### Cloud Security & AI Bootcamp — Weekly Session Report

### Date: July 11, 2026 

### Instructor: Oluwatosin Ajala

### Topic: Secure Azure Key Vault with Defense in Depth for the Cloud & AI Workloads
________________________________________

### Key Concepts I Learned

•	Azure Key Vault is a managed cloud service that provides a secure, centralized location for storing and managing secrets, cryptographic keys, and X.509 certificates — keeping sensitive data out of application code and configuration files.

•	Hardcoding secrets (API keys, passwords, connection strings) directly in application config files or source code is a dangerous security anti-pattern. A single exposed secret can escalate into full workload compromise through a predictable 

### attack chain:
1.	Secret stored in config → 2. Credential discovered → 3. Privilege reuse → 4. Data exfiltration & unauthorized execution.
 
#### •	Key Vault Object Types — Azure Key Vault stores three distinct categories of sensitive objects:

Secrets: Passwords, connection strings, API keys	Used by apps and automation at runtime

Keys: Cryptographic keys for encrypt/decrypt/sign	Key lifecycle, rotation, and crypto operations

Certificates: X.509 certificates	TLS and workload trust boundaries

#### •	Two Independent Authorization Planes — Azure Key Vault enforces access through two separate planes, both authenticated via Microsoft Entra ID:

o	Control Plane — Manages the Key Vault resource itself (create/delete vault, configure network & firewall, assign Azure Policy). Roles: Key Vault Contributor, Owner.

o	Data Plane — Controls access to the actual secrets, keys, and certificates. Roles: Secrets User, Crypto Officer, Certificates Officer, Administrator.

o	⚠️ Access to the Control Plane does not automatically grant Data Plane access — these are independent authorization decisions.
 
#### •	Azure RBAC vs. Legacy Vault Access Policies — Azure RBAC is the recommended access control model for Key Vault:
o	✅ Azure RBAC — Unified authorization across Azure, role assignments are auditable and scoped, works cleanly with Managed Identities.

o	❌ Vault Access Policies (Legacy) — Separate permission model per vault, higher risk of policy drift, still present in existing environments.
 
#### •	Managed Identities eliminate the need to store credentials in application code by allowing Azure resources to authenticate directly to Key Vault. The retrieval flow works as follows:

1.	Request Token — SDK requests a token from the local IMDS endpoint.
2.	
3.	Authenticate — Entra ID verifies identity and issues a token.
4.	
5.	Call Key Vault — App presents the token as Bearer auth.
6.	
7.	Authorize & Return — RBAC is checked; secret is returned over TLS.
 
#### •	Microsoft Defender for Cloud enhances Key Vault security by detecting suspicious access patterns, generating actionable security recommendations, and continuously monitoring for potential threats.

#### •	Defense-in-Depth controls for Key Vault include: Firewall rules, Soft Delete, Purge Protection, and automated Key Rotation — layering multiple safeguards around sensitive data.
________________________________________

### Lab / Hands-On Work

What I Did

•	Explored the three Azure Key Vault object types — Secrets, Keys, and Certificates — and their respective use cases.

•	Studied the Key Vault access model, understanding the distinct responsibilities of the Control Plane and Data Plane and how each is independently authorized through Microsoft Entra ID.

•	Compared Azure RBAC (recommended) with legacy Vault Access Policies, identifying the limitations of the legacy approach.

•	Traced the full Managed Identity secret retrieval flow — from token request to authorized secret return — understanding how this eliminates hardcoded credentials entirely.

•	Reviewed the differences between System-Assigned and User-Assigned Managed Identities and when each is appropriate.

•	Explored operational security controls: Firewall rules, Soft Delete, Purge Protection, and Key Rotation.

•	Studied how Microsoft Defender for Cloud integrates with Azure Key Vault to detect threats and enforce security posture.
What Happened / Result

By the end of the session, I had a clear understanding of how Azure Key Vault protects sensitive information and why it should always be used instead of storing secrets in application settings or source code.

I also understood how Managed Identities, Azure RBAC, and Microsoft Defender for Cloud work together to form a robust, defense-in-depth strategy for securing cloud workloads — one where no single point of failure can result in full compromise.
________________________________________

### Some key images for these learnings are: 
<img width="1148" height="425" alt="Key 1" src="https://github.com/user-attachments/assets/80c51021-63e6-4871-9e46-bbf260d0b33b" />
<img width="743" height="295" alt="Key 2" src="https://github.com/user-attachments/assets/ed6065c4-3e36-4f82-86d4-95aca468a070" />
<img width="737" height="294" alt="Key 3" src="https://github.com/user-attachments/assets/d4c552c5-5680-4e22-a71e-33b2bb622aa7" />
<img width="730" height="275" alt="Key 4" src="https://github.com/user-attachments/assets/6c57289d-a0b7-46ae-a917-4e4150b2f1a1" />
<img width="749" height="295" alt="Key 5" src="https://github.com/user-attachments/assets/044cb189-0df0-419c-a7ae-083f7f909579" />

### Challenges I Faced

•	Control Plane vs. Data Plane — Initially confusing to separate their responsibilities. The key insight was that the Control Plane manages the vault itself, while the Data Plane manages what's inside the vault. Access to one does not grant the other.

•	System-Assigned vs. User-Assigned Managed Identities — Understanding the lifecycle differences: System-Assigned identities are tied to the resource lifecycle (deleted with the resource), while User-Assigned identities are independent and can be shared across multiple resources.

•	RBAC + Managed Identity relationship — Grasping how Managed Identity provides authentication while RBAC provides authorization — two distinct layers working together.

Another challenge I faced was not having access to a full Azure subscription. This limited my ability to practice the concepts I learned and fully engage in the hands-on lab exercises.

### My Takeaways

The most important lesson from this session is that identity is as critical as the secret itself.

What stood out most was the attack chain diagram — seeing how a single secret stored carelessly in a config file can cascade into full workload compromise through credential discovery and privilege reuse. This made the value of Managed Identities immediately concrete: by eliminating stored credentials entirely, you remove the first link in that attack chain.
Another significant insight was around token hygiene: authentication tokens carry identity information and remain valid until they expire. Simply closing a browser tab does not invalidate a token. If a token is compromised, it can be used to access resources on behalf of the user until it expires. This reinforces good security hygiene practices:

•	Always sign out of applications after use — do not just close the browser.

•	Never hardcode secrets in application code or config files.

•	Use Managed Identities to eliminate stored credentials entirely.

•	Enforce least-privilege access through Azure RBAC with tightly scoped role assignments.

•	Apply defense-in-depth: layer Key Vault controls with Microsoft Defender for Cloud monitoring.
________________________________________

### Questions I Still Have

•	How does Azure Key Vault integrate with Azure App Service and Azure Functions in real-world production environments? What does the Managed Identity setup look like end-to-end in a live deployment?

•	What are the best practices for automating secret rotation across multiple applications without causing downtime?

•	How should teams handle secret versioning in Key Vault when rotating credentials used by several dependent services simultaneously?

•	In what scenarios would User-Assigned Managed Identity be preferred over System-Assigned, especially in microservices architectures?
________________________________________

### Resources I Found Useful

•	Microsoft Learn — Azure Key Vault Overview

•	Microsoft Learn — Secure Azure Key Vault

•	Microsoft Defender for Cloud Documentation

•	Azure Managed Identity Documentation

•	Azure RBAC Documentation
________________________________________
Submitted by: Michael Chinonso Onwumere · @MichaelOnwumere


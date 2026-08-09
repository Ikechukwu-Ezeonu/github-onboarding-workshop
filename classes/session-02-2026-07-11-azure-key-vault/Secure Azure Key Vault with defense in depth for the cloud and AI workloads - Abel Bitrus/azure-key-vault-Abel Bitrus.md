# My Notes — Abel Bitrus

## Key Concepts I Learned ##
* Configure and secure azure key vault
* Manage keys and secrets in azure key vault.
* Manage certificates and monitor azure key vault.
* protect azure key vault with Microsoft Defender.

Azure Key Vault is an essential part of the Microsoft Azure cloud platform that can serve in many ways from storing secrets, keys, certificates etc. Careless developers and engineers acros the information technology landscape make mistakes of storing their API Keys, secrets within their code which makes it easier for attackers to extract those information that exposes organizational resources to attacks and exploit. Key vault, RBAC, managed identies provides an alternative of hardcoding your secrets, and keys within the code.
Key vault managed Identities are: System Assigned or User Assigned permission to manage key vaults resources.
Key vault object types are:

- Secrets: passwords, connection strings, API Keys.
- Keys: cryptography keys for encryption/decryption.
- Certificate: X.509 certificates and life-cycle renewal.

Microsoft supports two certificate authority partners:

* Global Certs.
* Digicerts.

Access authorization models:

- Control Plane: Identity and management of azure resources, users here don’t have access to the data plane it has to be assigned.

- Data Plan: This is the plane were the resources are stored like secret, keys, certificates. Users here can’t access the control plane.

Just because you have access to one plane does not mean you have access to another plane access have to be issues to you for each plane. Even if you are the owner of a vault.

Azure uses RBAC instead of legacy access policies to mange permissions. As to who can access what.

Azure key vault managed identities:

- User Assigned: user can access several key vaults and resources. It is not tied to a service or application.

- System Assigned: This is an identity that are created for applications and services. They are strictly tied to them,when the service or application is deleted or removed the identity is also deleted or removed.

Azure Key Vault Data Protection.

This includes network and data protection controls:

- Firewalls and network access: Allow trusted networks only, use private endpoints for sensitive workloads, treat public network access as an explicit exception.

- Soft delete and purge protection: soft delete prevents accidental immediate loss, purge protection blocks irreversible destruction, Frames these as anti-destruction security controls.purge protection is not enabled by default, but you can enable it for a certain time period, you can’t delete it until that time elapse.

NOTE BELOW:

Recovery options
Soft delete protection will automatically be enabled on key vault. This feature allows you to recover or permanently delete a key vault and secrets for the duration of the retention period. This protection applies to the key vault and the secrets stored within the key vault.
To enforce a mandatory retention period and prevent the permanent deletion of key vaults or secrets prior to the retention period elapsing, you can turn on purge protection. When purge protection is enabled, secrets cannot be purged by users or by Microsoft. (Time period range from 7 - 90 days)


- Operational Guardrails: least privilege role assignments, rotational ownership and interval policy, alerting and incident-response integration.

Defender for key vault

* What defender for key vault surfaces:
- Helps protects the key vault from suspicious access patterns and anomalous operations.
- Potential abuse paths across identity and resource context, 
- Actionable recommendations in defender for cloud.

* Supplemental Capabilities:

- Managed HSM support.
- Certifcate auto-renewal.
- Key rotation policies.
- CSPM secret scanning.































## Lab / Hands-On Work ##

- I went to the key vault resources in my azure platform, and created a key vault as seen below:




RBAC Selected for access management.


Public Network selected for this lab but virtual/private networks will be used for live environment to improve security.

Summary of key vault configuration.


Azure key vault created.




RBAC user based role assigned to access key vault.





### What I did ##

- Created a key vault.
- Created RBAC user based role for access to the key vault.


### What happened / Result ##

- key vault was created with user based RBAC user based permissions


### Challenges I faced ###

Creating a system based RBAC permission requires services like App services to be able to test the system based RBAC. But I get the concept behind it. It is linked to services and when services are deleted the role based access is deleted with it.


## My Takeaways ##

Key vault is important in security within the azure platform as it creates a services to manage key vault objects like secrets, keys and certificates. And also provide the means to access this objects effectively either by using the RBAC user based access or system based access.

## Questions I Still Have ##

None

## Resources I Found Useful ##

All resources were useful.

Submitted by: Abel Bitrus· Github: abelbitruslearnlabs
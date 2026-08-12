# My Notes — Emmanuel Adebayo


## Key Concepts I Learned

<!-- Write the main ideas covered in today's session -->

- **Defense in Depth for Cloud & AI:** Understood how to apply multi-layered security controls to protect cryptographic keys, secrets, and certificates used by cloud apps and AI workloads.
- **Credential Risks:** Discussed the severe security threats of storing secrets directly in plain text configuration files, credential exposure/discovery, and the dangers of privilege reuse across environments.
- **Key Vault Management:** Explored the core functional pillars of Azure Key Vault: configuring infrastructure, lifecycle management of keys/secrets, handling certificates, and enabling robust monitoring.
- **Threat Detection:** Learned how to actively protect Azure Key Vault from malicious access and exfiltration attempts using Microsoft Defender for Cloud.

---

## Lab / Hands-On Work

<!-- Describe what you did in the lab. Include steps, commands, or screenshots descriptions -->

### What I did
1. Initiated the deployment and foundational configuration of an Azure Key Vault instance.
2. Explored the portal interfaces for manually adding, versioning, and managing secrets and keys.
3. Reviewed the configurations required for certificate management and structural logging/monitoring.
4. Examined how to integrate and enable Microsoft Defender protections on the Key Vault resource.

### What happened / Result
- Mapped out the step-by-step workflow required to isolate sensitive application credentials away from source code.
- Gained a clear view of how diagnostic logs track who accesses specific secrets.

### Challenges I faced
- Encountered configuration issues and errors during the initial Azure Key Vault setup process (such as networking/access policy adjustments), which required troubleshooting the permission models to resolve access blocks.

---

## My Takeaways

<!-- What was most valuable to you personally from this session? -->
The most valuable part was recognizing how critical it is to move secrets out of application configuration files. Learning how a single discovered credential or reused privilege can compromise an entire AI workload made me realize why Azure Key Vault is foundational for cloud security.

---

## Questions I Still Have

<!-- Anything you want to follow up on or ask the mentor -->

- What are the best practices for resolving common deployment blocks and access policy errors when first spinning up a Key Vault?
- When securing an AI workload, should the application authenticate to the Key Vault using Managed Identities or Service Principals?

---

## Resources I Found Useful

<!-- Any links, docs, or Microsoft Learn modules you found helpful -->

- [Microsoft Learn: Secure access to an Azure Key Vault](https://microsoft.com)
- [Microsoft Learn: Microsoft Defender for Key Vault overview](https://microsoft.com)

---

*Submitted by: Emmanuel Adebayo · 19Emade*

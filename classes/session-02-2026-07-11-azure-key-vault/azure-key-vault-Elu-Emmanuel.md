# My Notes — Elu Uchenna Emmanuel

---

## Key Concepts I Learned

<!-- Write the main ideas covered in today's session -->
- Key Vault object types (Keys, secrets and certificate)
- Compare RBAC with Legacy access policy
- Security controls, Network access, Soft delete and Purge protection
- Enabling defender for Key Vault (MS defender for cloud >> defender plans and enable)
- Deploy and secure azure Key Vault

---

## Lab / Hands-On Work

<!-- Describe what you did in the lab. Include steps, commands, or screenshots descriptions -->

### What I did

- Configure azure key vault, define the network access
- Determine the tier and the recovery option
- Create secret and add role assignment to a key vault
- Retrieve the secret using a managed identity

### What happened / Result

- Key Vault was created, secret added but managed identity unable to retrieve.
- After investigating, observed Legacy access was selected instead of RBAC from access configuration.

### Challenges I faced

- Script writing while creating an app service
- Error observed, the application does not have secret get permission

---

## My Takeaways

<!-- What was most valuable to you personally from this session? -->
- Being able to create a key vault, create a secret, add assignment 

---

## Questions I Still Have

<!-- Anything you want to follow up on or ask the mentor -->

- Guide with understanding scripting / powershell

---

## Resources I Found Useful

<!-- Any links, docs, or Microsoft Learn modules you found helpful -->

- https://learn.microsoft.com/en-us/training/paths/configure-key-vault-security/
- https://www.youtube.com/watch?v=GKqpej4X9B0&t=1602s

---

*Submitted by: Elu Uchenna Emmanuel · eluemma*

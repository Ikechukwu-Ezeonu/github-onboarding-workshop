# My Notes — Promise Ibediogwu Ekele

---

## Key Concepts I Learned

### Azure Role-Based Access Control (RBAC)

- Learned how Azure RBAC implements the principle of least privilege by assigning only the required permissions needed for users, applications, and teams.
- Understood the four main RBAC assignment scopes:
  - Management Group
  - Subscription
  - Resource Group
  - Resource Level
- Learned that assigning permissions at broader scopes such as subscription level increases the security risk because a compromised identity can impact a larger number of resources.
- Understood the importance of avoiding unnecessary role assignments like Owner or Contributor and instead using specific built-in roles based on job responsibilities.
- Example:
  - A network administrator should receive Network Contributor access at the required Resource Group level instead of Contributor access at the entire subscription level.

---

### Microsoft Entra Access Reviews and Identity Governance

- Learned that access management requires continuous monitoring because users can accumulate unnecessary permissions over time, a problem known as privilege creep.
- Understood how Microsoft Entra Access Reviews help organizations periodically review user access and validate whether permissions are still required.
- Learned that access reviews can be configured with automatic remediation actions, such as removing access when users fail to respond during the review period.
- Understood how access reviews support compliance requirements by providing visibility and accountability around privileged access.

---

### Azure Policy and Policy Initiatives

- Learned that Azure Policy is a governance service used to enforce organizational standards and compliance requirements across Azure environments.
- Understood the difference between RBAC and Azure Policy:
  - RBAC controls **who can perform an action**.
  - Azure Policy controls **what configurations and actions are allowed within the environment**.
- Learned that Azure Policy can deny non-compliant resource deployments even when a user has sufficient RBAC permissions.
- Example:
  - A user with Contributor access can still be blocked from deploying a public storage account if an Azure Policy denies public access.

### Azure Policy Definitions and Initiatives

- Learned that a Policy Definition represents a single rule that evaluates Azure resources against a specific requirement.
- Example:
  - Enforcing HTTPS-only communication for storage accounts.
  - Restricting resource locations.
  - Requiring specific security configurations.

- Learned that a Policy Initiative is a collection of multiple policy definitions grouped together to achieve broader compliance goals.
- Understood that initiatives simplify policy management by allowing administrators to assign multiple related policies as a single governance package.
- Example:
  - A security baseline initiative can include policies requiring encryption, network restrictions, tagging standards, and monitoring configurations.

---

### Azure Policy Effects

- Learned that Azure Policy effects determine what happens when a resource does not comply with a policy rule.

The major effects discussed include:

- **Audit**
  - Identifies and reports non-compliant resources without blocking deployment.
  - Useful during assessment phases before enforcing strict controls.
  - Helps organizations understand their current security posture.

- **Deny**
  - Blocks the creation or modification of resources that violate defined security requirements.
  - Helps prevent insecure configurations from entering production.

- **DeployIfNotExists**
  - Automatically deploys required configurations when they are missing.
  - Helps organizations maintain compliance without requiring manual intervention.
  - Example:
    - Automatically deploying monitoring agents or diagnostic settings to resources that do not have them enabled.

- **Modify**
  - Automatically changes resource properties to bring them into compliance.

---

### Azure Backup Security

- Learned the importance of protecting backup infrastructure against accidental deletion, malicious administrators, and ransomware attacks.
- Studied important Azure Backup security features:

**Soft Delete**
- Provides protection against accidental deletion by allowing deleted backup items to be recovered within a retention period.

**Vault Immutability**
- Prevents modification or deletion of backup data during the configured retention period.
- Helps protect backups from ransomware and malicious actions.

**Multi-User Authorization (MUA)**
- Learned how Resource Guard enables approval-based protection for sensitive backup operations.
- Understood that critical actions require approval from another administrator, reducing the risk of a compromised privileged account performing destructive actions.

---

### Infrastructure as Code (IaC) Security

- Learned that Infrastructure as Code enables organizations to deploy cloud resources consistently through templates such as Bicep and Terraform.
- Understood that security checks should be integrated into CI/CD pipelines before infrastructure reaches production.
- Learned how Microsoft Security DevOps (MSDO) can scan Infrastructure as Code templates to detect:
  - Security misconfigurations
  - Exposed secrets
  - Weak security practices
  - Compliance issues

- Learned secure Bicep development practices, including the use of `@secure()` decorators to prevent sensitive values from appearing in deployment logs.

---

### Managed Identities

- Learned how Managed Identities provide secure authentication between Azure services without storing credentials manually.
- Understood that Managed Identities reduce security risks associated with:
  - Hardcoded passwords
  - API keys
  - Stored secrets

- Learned the difference between:
  - System Assigned Managed Identity
  - User Assigned Managed Identity

---

## Lab / Hands-On Work

### What I did

- No official hands-on lab was provided for this session; however, I followed the instructor's practical demonstrations and reviewed the implementation steps.
- I studied the RBAC configuration process, including assigning roles at different Azure scopes and selecting appropriate built-in roles based on least privilege principles.
- I followed the demonstration of Azure Policy implementation, including policy definitions, initiatives, and different policy effects such as Audit, Deny, and DeployIfNotExists.
- I reviewed how Azure Backup security controls such as Soft Delete, Vault Immutability, and Resource Guard are configured.
- I followed the Infrastructure as Code security discussion around securing Bicep templates and integrating security scanning into deployment pipelines.

Additionally, I have applied several concepts from this session in my personal Azure projects, including:

- Implementing Azure RBAC using appropriate role assignments.
- Creating Azure Policies to enforce security requirements.
- Restricting insecure storage configurations using policy rules.
- Working with Managed Identities for secure service authentication.
- Applying security best practices when deploying Azure resources.

---

### What happened / Result

- I gained a stronger understanding of how Azure governance works beyond simple resource deployment.
- I understood how RBAC, Azure Policy, and Security controls work together to create a secure Azure environment.
- I learned that cloud security is achieved through multiple layers:
  - Identity control through RBAC
  - Governance enforcement through Azure Policy
  - Data protection through Azure Backup security
  - Secure deployment practices through IaC security

- The session helped me connect several concepts I had already implemented in my personal Azure projects with enterprise security practices.

---

### Challenges I faced

- Understanding the relationship between RBAC and Azure Policy initially required more clarification because both influence resource operations but serve different purposes.
- Resource Guard and Multi-User Authorization are advanced backup security features, and I need more practical exposure to fully understand their implementation in enterprise environments.
- I need more hands-on practice integrating Microsoft Security DevOps into real CI/CD pipelines.

---

## My Takeaways

The biggest takeaway from this session was understanding that Azure security is not only about protecting resources but also about establishing proper governance, identity management, and operational controls.

I learned that assigning permissions without considering scope and business requirements can increase the blast radius of a security incident. Least privilege and continuous access reviews are therefore critical security practices.

The Azure Policy discussion was also valuable because it showed how organizations enforce compliance at scale. Instead of depending only on administrators to follow security standards, Azure Policy allows organizations to automatically monitor, prevent, and remediate non-compliant resources.

The session also strengthened my understanding of how security should be integrated throughout the cloud lifecycle, from infrastructure deployment using IaC to protecting critical data using Azure Backup security features.

---

## Questions I Still Have

- What are the recommended approaches for designing RBAC models in large enterprise Azure environments?
- When should organizations use Audit policies before moving to Deny policies?
- What are the best practices for managing large collections of Azure Policies through Policy Initiatives?
- How can Resource Guard be implemented effectively in a multi-team enterprise environment?
- How can Microsoft Security DevOps be integrated into production GitHub Actions or Azure DevOps pipelines?

---

## Resources I Found Useful

- Microsoft Learn: Azure Role-Based Access Control (RBAC)
  https://learn.microsoft.com/azure/role-based-access-control/

- Microsoft Learn: Azure Policy Overview
  https://learn.microsoft.com/azure/governance/policy/overview

- Microsoft Learn: Azure Policy Effects
  https://learn.microsoft.com/azure/governance/policy/concepts/effect-basics

- Microsoft Learn: Azure Policy Initiatives
  https://learn.microsoft.com/azure/governance/policy/concepts/initiative-definition-structure

- Microsoft Learn: Azure Backup Security Features
  https://learn.microsoft.com/azure/backup/security-overview

- Microsoft Learn: Azure Resource Guard and Multi-User Authorization
  https://learn.microsoft.com/azure/backup/multi-user-authorization

- Microsoft Learn: Secure Azure Deployments Using Bicep
  https://learn.microsoft.com/azure/azure-resource-manager/bicep/

- Microsoft Security DevOps
  https://learn.microsoft.com/azure/defender-for-cloud/azure-devops-extension

---

*Submitted by: Promise Ibediogwu Ekele · https://github.com/promibe*
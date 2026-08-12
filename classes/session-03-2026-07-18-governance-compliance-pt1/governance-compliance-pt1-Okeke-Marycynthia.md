# My Notes — Okeke Marycythia

## Key Concepts I Learned

The "Why" of Security Controls: Deploying applications without security is like building a house without doors—anyone can enter, steal, or delete critical resources.

Resource locks, Azure Policy, and Defender for Cloud ensure non-compliant or malicious deployments are blocked.

Azure Policy Triggers: Azure Policy checks your cloud resources against rules written in JSON format. It evaluates them when resources are created or updated, when policies are assigned or modified, and automatically every 24 hours.

Management Groups and Scopes: Management Groups are created at the very top level (Microsoft Entra ID/tenant level).

Because they sit at the highest level, any security policies set here automatically apply to and control all subscriptions underneath them.

Policy Compliance Effects:

*Audit: Checks resources and flags them as non-compliant on the dashboard, but does not stop them from running (used in Phase 1 to *test policies without breaking things).

*Deny: Blocks the creation or update of non-compliant resources and returns an error (used in Phase 2 to enforce rules).

*DeployIfNotExists: Checks if a required setting or resource exists; if it is missing, Azure creates it automatically (e.g., adding diagnostic logs to a VM).

*Modify: Automatically adds, updates, or removes tags or properties when a resource is created or updated.

Defender for Cloud Auto-Provisioning & Standards: Defender for Cloud automatically deploys three key monitoring tools (Azure Monitor Agent, Defender for Endpoint, and Vulnerability Assessment). It measures your environment against security standards like MCSB, NIST SP 800-53, ISO 27001, and PCI DSS.

Fixing Security Issues: Security recommendations can be fixed automatically using the "Fix" button or Policy Remediation Tasks. If an issue requires a manual decision, Governance Rules assign it to a resource owner. 
If a risk is accepted, an Exemption (Waiver or Mitigated control) is applied.

Portals & Permissions:
*Azure Portal: Used to set up and manage policies (requires Owner or Policy Contributor roles).

*Defender Portal: Used to track compliance scores and monitoring details (requires at least the Reader role—Security Reader alone is not enough).

Three Components of Access Assignment: Setting up access or policies requires defining three things: the Principal (who gets access), the Role Definition (what they can do), and the Scope (where it applies).

## Lab / Hands-On Work

<!-- Describe what you did in the lab. Include steps, commands, or screenshots descriptions -->

### What I did


### What happened / Result


### Challenges I faced


---

## My Takeaways

*Security isn't an afterthought; enforcing guardrails at the management group level guarantees inheritance across every child subscription automatically.

*Combining Azure Policy's enforcement effects (Deny, DeployIfNotExists, Modify) with Defender for Cloud's continuous assessment creates a proactive defense environment.


---

## Questions I Still Have

When configuring custom security standards in Defender for Cloud, what are the best practices for setting up governance rule deadlines for resource owners?

---

## Resources I Found Useful

https://learn.microsoft.com/en-us/training/paths/security-governance-compliance/ 
(https://github.com/MicrosoftLearning/mslearn-sec-identity/blob/master/Instructions/Labs/Lab-1D-Configure-Policy-RBAC.md)
https://github.com/Azure/azure-policy/tree/master/built-in-policies

-

---

*Submitted by: Marycynthia Okeke · Nechy-Okeke*

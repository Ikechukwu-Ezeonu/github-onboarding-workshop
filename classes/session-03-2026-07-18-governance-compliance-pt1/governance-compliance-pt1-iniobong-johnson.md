# My Notes — Iniobong Johnson

---

## Key Concepts I Learned

- Azure Policy helps enforce organisational standards and maintain a consistent baseline across an Azure environment.
- A policy definition describes the rule or requirement that should be applied to Azure resources. It contains the conditions to evaluate and the effect that should occur when those conditions are met.
- A policy is a single definition, while an initiative is a collection of related policy definitions grouped together to achieve a broader goal.
- A scope determines where a policy applies. Azure Policy can be assigned at the management group, subscription, resource group, or individual resource level.
- Management group  are created in the Entra ID and captures all subscriptions under one structure.
- Azure Policy supports different effects, including Audit, Deny, DeployIfNotExists, and Modify. The effect used depends on the purpose of the policy and the action that should be taken when a resource does not meet the required standard.
- When a resource group is deleted, the resource group itself cannot be restored.
- The main components of an Azure role assignment are the security principal, role definition, and scope.
- A security principal can be a user, group, service principal, or managed identity.
- The role definition specifies the permissions granted, while the scope determines where those permissions apply.
- After a policy definition or initiative has been created, it must be assigned to a scope before it can take effect.

---

## My Takeaways

- My key takeaway from the session is the importance of being careful when deleting a resource group or resource in Azure. A deleted resource group cannot be restored as a complete unit, and deleting it may also remove all the resources contained within it.

- I also learned that Azure Policy and role assignments serve different purposes. Azure Policy helps enforce organisational standards and compliance requirements, while role assignments control who can access Azure resources and what actions they are permitted to perform.

---

*Submitted by: Iniobong Johnson · Inib12*

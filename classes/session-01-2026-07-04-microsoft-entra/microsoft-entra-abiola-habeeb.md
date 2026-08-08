# My Notes — Abiola Habeeb

---

## Key Concepts I Learned

- **Identity is the new security perimeter.** In modern cloud environments, protecting user identities is the first line of defense, and Microsoft Entra ID is the platform that manages authentication and authorization for users, devices, and applications.
- **Multi-Factor Authentication (MFA)** strengthens sign-in security by requiring something you know (password) plus something you have (authenticator app, phone) or something you are (biometrics). Even if a password is compromised, MFA blocks most account-takeover attacks.
- **Conditional Access (CA)** is the policy engine in Microsoft Entra that evaluates signals — user identity, group membership, device platform, location, target application, and sign-in risk — before deciding to allow access, block it, or require additional controls like MFA. All configured conditions must be satisfied for a policy to apply.
- **Privileged Identity Management (PIM)** enforces the Principle of Least Privilege by replacing permanent admin roles with Just-in-Time (JIT), time-bound role activation, often with approval and justification required. This shrinks the attack surface for privileged accounts.
- **Microsoft 365 Copilot Declarative Agents** let you build an AI-powered assistant that understands natural language, runs on top of the Microsoft 365 Copilot infrastructure, and can be optimized for a specific scenario using instructions.
- **API plugins** allow a declarative agent to connect to external systems (e.g., a repairs management system) so it can answer authoritatively from real business data. Plugins authenticate in two main ways:
  - **API Key Authentication** — a shared secret sent with each request; simple, but not user-specific.
  - **OAuth 2.0 with Microsoft Entra ID** — users are authenticated individually and the plugin receives access tokens, making it the recommended approach for enterprise scenarios.

---

## Lab / Hands-On Work

### What I did

- Explored **Microsoft Entra Conditional Access** in the Entra admin center.
- Created a Conditional Access policy, assigned it to a test group, and configured conditions including device platform and target cloud apps.
- Enabled the policy first in **Report-only mode**, then reviewed the **Sign-in Logs** to see how the policy was evaluated for my test user.
- Reviewed **Privileged Identity Management (PIM)** and how eligible role assignments and Just-in-Time activation work.
- Followed the Microsoft Learn module on **authenticating API plugins for Microsoft 365 Copilot Declarative Agents**, covering both API Key and OAuth 2.0 flows, and explored the project setup using the **Microsoft 365 Agents Toolkit** in Visual Studio Code.

### What happened / Result

- The Conditional Access policy behaved exactly as configured once all conditions were correctly set — this showed me in practice that CA evaluates *every* condition (user, app, platform, location) before enforcing a control.
- The Sign-in Logs proved very useful for troubleshooting: they show which policies were applied, not applied, or in report-only mode for each sign-in attempt.
- For the Copilot module, I focused on understanding the authentication flow — how the agent calls the API, how the API key or the Entra-issued access token is attached to requests, and why OAuth 2.0 provides secure, user-specific access.

### Challenges I faced

- Understanding why a Conditional Access policy may silently not apply — for example, if the target resource (cloud app) is not configured or the test device doesn't match the targeted platform.
- Full hands-on testing of Copilot API plugins requires a Microsoft 365 Copilot license, so I concentrated on the concepts, configuration files, and authentication flow instead of a complete end-to-end build.

---

## My Takeaways

The most valuable insight for me is that security in the Microsoft cloud is layered: MFA protects the sign-in, Conditional Access decides *when and how* access is granted based on risk signals, and PIM limits *how long* privileged access exists. Together they implement Zero Trust — never trust, always verify, and grant the least privilege needed.

I also now understand that extending Copilot with API plugins is only safe when authentication is done properly. OAuth 2.0 through Microsoft Entra ID is the enterprise-grade choice because access is tied to the individual user, tokens expire, and permissions can be governed centrally — unlike a shared API key.

---

## Questions I Still Have

- When multiple Conditional Access policies apply to the same user and app, how exactly are they combined — and which controls take precedence?
- What are the best practices for rolling out CA policies in production without locking out administrators (break-glass accounts, phased rollout, report-only mode)?
- Is there a developer/sandbox route to practice building and testing Copilot API plugins without a full Copilot license?
- How does token refresh and expiration work for OAuth-authenticated plugins behind the scenes?

---

## Resources I Found Useful

- [Microsoft Learn — Microsoft Entra Conditional Access](https://learn.microsoft.com/en-us/entra/identity/conditional-access/)
- [Microsoft Learn — Microsoft Entra Privileged Identity Management (PIM)](https://learn.microsoft.com/en-us/entra/id-governance/privileged-identity-management/)
- [Microsoft Learn — Authenticate your API plugin for Declarative Agents with secured APIs](https://learn.microsoft.com/en-us/training/modules/copilot-declarative-agent-api-plugin-auth/)
- [Microsoft Entra Sign-in Logs documentation (for troubleshooting CA policies)](https://learn.microsoft.com/en-us/entra/identity/conditional-access/troubleshoot-conditional-access)
- Session recording and mentor guidance from the bootcamp

---

Submitted by: [Abiola Habeeb](https://github.com/abiolahabeeb)

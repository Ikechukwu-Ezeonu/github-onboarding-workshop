# My Notes — Mohammed Asheraf Sulemana

---

## Key Concepts I Learned

1. **Entra ID as the Gatekeeper**
   - Microsoft Entra ID is the central control plane for securing both regular enterprise apps and new AI tools.
   - Learned to secure user access using Multi-Factor Authentication (MFA), Self-Service Password Reset (SSPR), and passwordless options (Windows Hello, Passkeys).

2. **Conditional Access Strategy**
   - Policies enforce access rules based on real-time signals: user/sign-in risk, device compliance, and trusted locations (IPs).
   - Always deploy in **Report-only mode** first to test the impact before turning policies fully **On**.

3. **Privileged Identity Management (PIM)**
   - Protects high-level admin roles by shifting from permanent access to Just-In-Time (JIT) access.
   - Uses time-bound activation and approval workflows to maintain a defense-in-depth posture.

4. **Securing AI Agent API Plugins**
   - Declarative agents act like assistants retrieving data from locked rooms; securing their APIs is critical to stop data leaks.
   - Compared **API keys** (simpler, service-to-service) against the **OAuth 2.0 framework** (granular, delegated access acting like a valet key).

---

## Lab / Hands-On Work

### What I did
- Watched the live training sessions and reviewed the Microsoft Learn module on API plugin security.
- Set up a Copilot API plugin in VS Code by configuring the manifest and OpenAPI description files.
- Tracked how Entra tenant configurations and Conditional Access rules block or allow plugin traffic based on risk signals.

### What happened / Result
- Successfully built a Microsoft 365 Copilot API plugin integrated with clear data boundaries.
- Verified how the system enforces MFA and blocks unauthorized access via the environment demos.

### Challenges I faced
- **Setup & Access:** Had issues installing the Microsoft 365 Agents Toolkit extension in VS Code (fixed with a clean reinstall) and lacked full admin tenant access for solo practice.
- **Time Constraints:** Balancing full-time job demands, bootcamp milestones, and studying for upcoming certification exams made managing study time difficult.

---

## My Takeaways

- **AI Security is the New Frontier:** We used to focus entirely on securing user-to-application traffic. Now, we must secure AI-to-API traffic. Without strict Entra identity boundaries, an AI agent essentially has a master key to the backend.
- **Layered Security Wins:** Combining MFA, Conditional Access, and PIM creates a rock-solid perimeter. 
- **Test Before Enforcing:** Relying on Report-only mode and step-by-step demos ensures you can safely validate major policy changes before they disrupt users.

---

## Resources I Found Useful

- **Community Video:** [Secure Access to Resources using Microsoft Entra - MNSUG YouTube Session](https://youtu.be/R7zxI-k3NoQ)
- **Microsoft Learn:** [Authenticate your API plugin for declarative agents with secured APIs](https://learn.microsoft.com/en-us/training/modules/copilot-declarative-agent-api-plugin-auth/)
- **Workspace:** [GitHub Onboarding Workshop Classes Directory](https://github.com/AGK001/github-onboarding-workshop)

---

*Submitted by: Mohammed Asheraf Sulemana · Shaiba-00*

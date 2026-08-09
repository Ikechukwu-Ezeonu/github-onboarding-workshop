# Session 15 — App Platform Security — Part 1 (Modules 1–2)

**SC-500 — Securing Azure App Service and API management**

| | |
|---|---|
| **Date** | Saturday, 10 October 2026 |
| **Mentor** | Oyimafu Emmanuel |
| **Moderator** | Chidiebere Ihejirika |
| **Microsoft Learn** | [Implement app security in Azure](https://learn.microsoft.com/en-us/training/paths/secure-application-platform-services/) |
| **Modules Covered** | Modules 1–2 |

---

## About This Session

Modern applications are built on platforms like Azure App Service, Azure Functions, and API Management. Securing these platforms means controlling who can call your app, how secrets are passed to it, and what happens when someone tries to attack it.

Part 1 covers managed identities (letting your app authenticate to other Azure services without storing any passwords), securing Azure App Service with authentication, HTTPS enforcement, and access restrictions, and protecting APIs using Azure API Management policies.

**By the end of this session you will be able to:**
- Configure managed identities for App Service and Azure Functions
- Apply authentication and network access restrictions to App Service
- Use Azure API Management to throttle, authenticate, and log API calls
- Explain why managed identities are preferred over connection strings

---

## How to Submit Your Notes

> You do not need to know git commands. Just follow these 5 steps.

1. **Fork** this repository — click the **Fork** button at the top-right of the [main repo page](https://github.com/Microsoft-Naija-Security-Usergroup/github-onboarding-workshop)
2. **Navigate** into `classes/session-15-2026-10-10-app-platform-security-pt1/` on your forked repo
3. **Download** the template file `app-platform-security-pt1-yourname-template.md` — click it, then click the **Raw** button, then right-click and choose *Save As*
4. **Rename** the file on your computer — replace `yourname` with your actual name in lowercase with hyphens, e.g. `app-platform-security-pt1-firstname-lastname.md`
5. **Fill in your notes** using any text editor (Notepad, VS Code, TextEdit)
6. **Upload** your completed file back to GitHub — go into `classes/session-15-2026-10-10-app-platform-security-pt1/` on your fork, click **Add file → Upload files**, drag in your file, then click **Commit changes**
7. **Open a Pull Request** — the facilitator will review your notes before merging

---

## Session Files

| File | Purpose |
|------|---------|
| `README.md` | This file — session overview and instructions |
| [`app-platform-security-pt1-yourname-template.md`](./app-platform-security-pt1-yourname-template.md) | Template to download, rename, and fill in |

---

*MNSUG SC-500 Mentorship Program · Saturday, 10 October 2026 · Learn. Secure. Innovate.*

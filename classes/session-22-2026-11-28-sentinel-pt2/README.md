# Session 22 — Microsoft Sentinel — Part 2 (Modules 3–5)

**SC-500 — Threat detection, analytics rules, and incident management**

| | |
|---|---|
| **Date** | Saturday, 28 November 2026 |
| **Mentor** | Musbau Olagunju |
| **Moderator** | Susan Onyekachi-Lawal |
| **Microsoft Learn** | [Configure Microsoft Sentinel environments](https://learn.microsoft.com/en-us/training/paths/implement-activity-event-collection-sentinel/) |
| **Modules Covered** | Modules 3–5 |

---

## About This Session

With data flowing into Sentinel, Part 2 is about making Sentinel actually detect threats. Analytics Rules are the heart of this — they are queries written in KQL (Kusto Query Language) that run on a schedule and create Incidents when suspicious patterns are found.

You will learn how to create and tune Analytics Rules, understand the MITRE ATT&CK framework (a map of attacker techniques that Sentinel uses to categorise threats), manage the Incidents queue, and investigate an incident using the Investigation Graph to understand what happened and what was affected.

**By the end of this session you will be able to:**
- Create Scheduled and Near-Real-Time Analytics Rules in Sentinel
- Map detected threats to MITRE ATT&CK techniques
- Manage and prioritise incidents in the Sentinel Incidents queue
- Use the Investigation Graph to trace an attack across entities

---

## How to Submit Your Notes

> You do not need to know git commands. Just follow these 5 steps.

1. **Fork** this repository — click the **Fork** button at the top-right of the [main repo page](https://github.com/Microsoft-Naija-Security-Usergroup/github-onboarding-workshop)
2. **Navigate** into `classes/session-22-2026-11-28-sentinel-pt2/` on your forked repo
3. **Download** the template file `sentinel-pt2-yourname-template.md` — click it, then click the **Raw** button, then right-click and choose *Save As*
4. **Rename** the file on your computer — replace `yourname` with your actual name in lowercase with hyphens, e.g. `sentinel-pt2-firstname-lastname.md`
5. **Fill in your notes** using any text editor (Notepad, VS Code, TextEdit)
6. **Upload** your completed file back to GitHub — go into `classes/session-22-2026-11-28-sentinel-pt2/` on your fork, click **Add file → Upload files**, drag in your file, then click **Commit changes**
7. **Open a Pull Request** — the facilitator will review your notes before merging

---

## Session Files

| File | Purpose |
|------|---------|
| `README.md` | This file — session overview and instructions |
| [`sentinel-pt2-yourname-template.md`](./sentinel-pt2-yourname-template.md) | Template to download, rename, and fill in |

---

*MNSUG SC-500 Mentorship Program · Saturday, 28 November 2026 · Learn. Secure. Innovate.*

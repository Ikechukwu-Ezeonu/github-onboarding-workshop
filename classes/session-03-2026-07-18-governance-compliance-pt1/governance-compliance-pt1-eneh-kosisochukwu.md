# My Notes — ENEH KOSISOCHUKWU

> **How to use this file:**
> 1. **Download** this file to your computer — click the **Raw** button on GitHub, then right-click and *Save As*, OR click the download icon at the top-right of the file view
> 2. **Rename** the downloaded file — replace `yourname` with your actual first and last name in lowercase, separated by hyphens, e.g. `microsoft-entra-oyimafu-emmanuel.md`
> 3. **Open** the renamed file in any text editor (Notepad, VS Code, TextEdit) and fill in your notes below
> 4. **Upload** your file to GitHub — go into this session folder on your forked repo, click **Add file → Upload files**, drag in your completed file, then click **Commit changes**
> 5. **Open a Pull Request** back to the main repo — the facilitator will review your notes before merging

---

## Key Concepts I Learned

<!-- Write the main ideas covered in today's session -->

- Governance is basically how an organisation sets the rules for how cloud resources should be used, and compliance is proving you're actually following those rules (plus external ones like GDPR, ISO 27001 etc)
- Azure Policy lets you enforce rules at scale, e.g. deny resources being created outside allowed regions or force tagging. Learned the difference between a policy definition and an initiative (initiative = a group of policies bundled together)
- Resource locks (ReadOnly and CanNotDelete) stop people from accidentally deleting or changing important stuff, even if they have the right RBAC role

---

## Lab / Hands-On Work

<!-- Describe what you did in the lab. Include steps, commands, or screenshots descriptions -->

### What I did

Followed along in the Azure portal. Created a policy assignment that requires a specific tag on resource groups, then tried creating a resource group without the tag to see it fail. Also applied a CanNotDelete lock on a resource group and attempted to delete it. Had a quick look around the Microsoft Purview compliance portal too, mostly the Compliance Manager section to see how the compliance score works.

### What happened / Result

The policy did its job, deployment without the tag got blocked with a deny error which was satisfying to see lol. The delete attempt on the locked resource group also failed as expected. Compliance Manager showed a baseline score with recommended improvement actions mapped to standards, didn't go too deep into it but got the general idea.

### Challenges I faced

None really, everything worked as expected this time.

---

## My Takeaways

<!-- What was most valuable to you personally from this session? -->

The main thing that stuck with me is that governance should be set up early, not after resources are already all over the place. Also that policy enforcement > relying on people to remember to do the right thing. The tag deny demo made it very real.

---

## Questions I Still Have

<!-- Anything you want to follow up on or ask the mentor -->

- None for now

---

## Resources I Found Useful

<!-- Any links, docs, or Microsoft Learn modules you found helpful -->

- Microsoft Learn — Introduction to Azure Policy: https://learn.microsoft.com/en-us/training/modules/intro-to-azure-policy/
- Azure resource locks docs: https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/lock-resources

---

*Submitted by: Eneh Kosisochukwu · [Your GitHub username]*

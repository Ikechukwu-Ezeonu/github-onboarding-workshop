# My Notes — Promise Ibediogwu Ekele

---

## Key Concepts I Learned

<!-- Write the main ideas covered in today's session -->

- **Zero Trust Architecture** is a security principle, not a product — built on three pillars: *Always Verify*, *Assume Breach*, and *Principle of Least Privilege*. It shapes how secure environments are designed rather than being a tool you install.
- **Network segmentation** matters as much as perimeter defense. Dividing a network into smaller, isolated subnets/groups reduces the attack surface and prevents lateral movement if one resource is compromised.
- **NSGs vs. ASGs**: NSGs control traffic at the subnet/NIC level using IP and port rules, while ASGs let you group VMs logically by role (e.g., "Web Server") so rules can target the *application group* instead of hardcoded IP addresses — making policies scale much better.
- **DDoS Protection** comes in two tiers: **DDoS IP Protection** for small/minimal environments, and **DDoS Network Protection** for enterprise-grade, complex architectures. The three main attack types are Volumetric, Protocol, and Application Layer attacks.
- **NSG rule evaluation** is priority-based — lower numbers win, and once a rule matches, evaluation stops (no further rules are checked).
- **Network Watcher**, especially the **IP Flow Verify** feature, is the go-to tool for confirming whether specific traffic is actually allowed or blocked by current security rules.
- **Azure Virtual Network Manager (AVNM)** centralizes network security policy management across multiple subscriptions and VNets.
- The **Microsoft Cloud Security Benchmark** is the reference framework (similar in spirit to NIST) for best-practice Azure security controls, and should guide decisions like "NSG vs. Firewall vs. Private Endpoint."

---

## Lab / Hands-On Work

<!-- Describe what you did in the lab. Include steps, commands, or screenshots descriptions -->

### What I did

I built a segmented lab network (`AZ500LAB07`) inside resource group `NSGClass-rg`, made up of one VNet (`myVirtualNetwork`, `10.0.0.0/16`) with a `default` subnet, hosting two VMs: `myVmWeb` (`10.0.0.4`) and `myVMMgmt` (`10.0.0.5`).

![Lab architecture diagram](images/WhatsApp_Image_2026-08-20_at_1_03_39_PM.jpeg)
*Target architecture: VNet, subnet, NSG, ASGs, and the two VMs with their intended traffic paths.*

1. **Created two Application Security Groups** — `myAsgMgmtServer` and `myAsgWebserver` — plus the virtual network, all inside `NSGClass-rg`.

   ![ASG and VNet deployment succeeded](images/WhatsApp_Image_2026-08-20_at_1_06_09_PM.jpeg)

2. **Created and configured an NSG** (`myNSG`) with inbound rules pointed at the ASGs instead of raw IPs:
   - `Allow-RDP` (3389) → `myAsgMgmtServer`
   - `Deny-RDP` (3389) → `myAsgWebserver`
   - `Allow-HTTPS` (443) → `myAsgWebserver`
   - `Allow-HTTP` (80) → `myAsgWebserver`

   ![myNSG inbound security rules](images/WhatsApp_Image_2026-08-20_at_1_23_06_PM.jpeg)

3. **Deployed the two VMs** (`myvmmgt`, `myvmweb`) into the resource group along with their NICs, disks, and public IPs.

   ![Resource group with deployed VMs](images/WhatsApp_Image_2026-08-20_at_2_31_22_PM.jpeg)
   ![Full resource listing](images/WhatsApp_Image_2026-08-20_at_3_16_40_PM.jpeg)

4. **Associated each VM's NIC with its ASG** — `myvmmgt` → `myAsgMgmtServer`, `myvmweb` → `myAsgWebServer`.

   ![myvmmgt associated with myAsgMgmtServer](images/WhatsApp_Image_2026-08-20_at_3_29_51_PM__1_.jpeg)
   ![myvmweb associated with myAsgWebServer](images/WhatsApp_Image_2026-08-20_at_3_29_51_PM.jpeg)

5. **Tested RDP connectivity** against both VMs to confirm the rules were actually being enforced.

6. **Installed IIS on `myvmweb`** using the Run Command feature (`RunPowerShellScript`), then browsed to its public IP over HTTP to confirm the web server was live.

   ![Run Command installing IIS](images/WhatsApp_Image_2026-08-20_at_4_07_56_PM.jpeg)
   ![IIS default page reachable over HTTP](images/WhatsApp_Image_2026-08-20_at_4_32_55_PM.jpeg)

7. Separately, I provisioned an **Azure DDoS Protection Plan** (`MyDdosProtectionPlan`) and a linked VNet (`MyVirtualNetwork`) inside resource group `LabM06-rg`, and set up a public IP (`MyPublicIPAddress`) as the protected endpoint, with metrics and alerts configured for monitoring.

   ![LabM06-rg with DDoS plan and VNet](images/WhatsApp_Image_2026-08-20_at_10_26_48_PM.jpeg)
   ![MyPublicIPAddress overview](images/WhatsApp_Image_2026-08-20_at_10_33_22_PM.jpeg)

### What happened / Result

- RDP to **`myvmmgt`** (Management ASG) **succeeded** — the Server Manager dashboard loaded normally.

  ![Successful RDP to myvmmgt](images/WhatsApp_Image_2026-08-20_at_3_54_00_PM.jpeg)

- RDP to **`myvmweb`** (Web ASG) **failed as expected**, with a "Remote Desktop can't connect" error — confirming the `Deny-RDP` rule was correctly enforced.

  ![Failed RDP to myvmweb](images/WhatsApp_Image_2026-08-20_at_3_55_50_PM.jpeg)

- The IIS installation completed successfully (Common HTTP Features, Default Document, etc.), and the default IIS "Welcome" page loaded correctly in the browser at `102.37.107.19` — confirming HTTP/HTTPS access was allowed to the web server while RDP remained blocked.

  ![IIS welcome page](images/WhatsApp_Image_2026-08-20_at_4_32_55_PM.jpeg)

- For the DDoS Protection Plan, the **metrics dashboard** ("Max Inbound packets dropped DDoS") stayed flat at 0/s, and the **alerts blade** showed no alerts fired — meaning the resource only ever received normal, non-attack traffic during the exercise.

  ![DDoS metrics chart](images/WhatsApp_Image_2026-08-20_at_10_37_28_PM.jpeg)
  ![No DDoS alerts found](images/WhatsApp_Image_2026-08-20_at_11_03_17_PM.jpeg)

Overall, this confirmed that ASGs + a single NSG successfully enforced role-based segmentation: the management server was reachable only by RDP, and the web server was reachable only by HTTP/HTTPS — exactly matching the intended architecture.

### Challenges I faced

I was able to configure Azure DDoS Protection and successfully deploy and expose an NGINX/IIS web server on my VM, but I struggled to demonstrate the actual **mitigation behavior** of the DDoS Protection Plan in a controlled lab environment. I initially tried to understand how increasing traffic would affect the protected resource, but realized that a normal HTTP load test does not represent a real DDoS attack and would not trigger Azure's DDoS mitigation mechanisms. Rather than generate excessive traffic that could disrupt the VM or network, I chose not to attempt it. This helped me understand the real difference between a controlled load test and an actual simulated DDoS attack — genuine DDoS simulation requires authorized third-party load-generation tools and prior notice to Microsoft, which was outside the scope of this lab.

---

## My Takeaways

<!-- What was most valuable to you personally from this session? -->

The most valuable part of this session was seeing, hands-on, that security isn't just a perimeter wall — it's internal segmentation done well. Using ASGs to let rules "follow the workload" instead of chasing IP addresses made the whole NSG configuration far cleaner and easier to reason about. Verifying the RDP allow/deny behavior with real connection attempts (rather than just trusting the rule config) was also a good habit to build — it's the difference between assuming a rule works and actually proving it. On the DDoS side, the biggest lesson wasn't technical configuration at all — it was realizing that a load test and a DDoS attack are not the same thing, and that "trying harder" to force a mitigation event would have been the wrong move in a live lab environment.

---

## Questions I Still Have

<!-- Anything you want to follow up on or ask the mentor -->

- What is the safe, Microsoft-sanctioned way to actually simulate a DDoS attack against a test resource (approved tools, notification process, etc.)?
- In a real enterprise setup, how do NSGs, Azure Firewall, and DDoS Network Protection get layered together without creating conflicting or redundant rules?
- How does Azure Virtual Network Manager (AVNM) change this workflow when managing NSG/ASG-style rules across many subscriptions at once?

---

## Resources I Found Useful

<!-- Any links, docs, or Microsoft Learn modules you found helpful -->

- [Microsoft cloud security benchmark](https://learn.microsoft.com/en-us/security/benchmark/azure/) — reference framework for Azure security controls, recommended by the facilitator
- [IP flow verify overview — Azure Network Watcher](https://learn.microsoft.com/en-us/azure/network-watcher/ip-flow-verify-overview) — how to check if traffic is allowed/denied by NSG rules
- [Diagnose a VM traffic filter problem — Azure Network Watcher](https://learn.microsoft.com/en-us/azure/network-watcher/diagnose-vm-network-traffic-filtering-problem) — hands-on quickstart for IP flow verify
- Lab guide provided for the NSG/ASG exercise (AZ500LAB07 / NSGClass-rg)

---

*Submitted by: Promise Ibediogwu Ekele · [Your GitHub username]*

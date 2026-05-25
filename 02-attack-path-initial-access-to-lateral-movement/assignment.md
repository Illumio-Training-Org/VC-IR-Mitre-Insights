---
slug: attack-path-initial-access-to-lateral-movement
id: zlzcql2ai3ft
type: challenge
title: 'Module 2: The Attack Path — Initial Access to Lateral Movement'
teaser: The first half of the kill chain — and the point where Illumio's detection
  capability becomes decisive.
notes:
- type: text
  contents: |-
    # Module 2: The Attack Path — Initial Access to Lateral Movement

    An attacker does not go from zero to ransomware in one step. They move through a sequence of Tactics — gathering information, finding a way in, establishing a foothold, and then spreading.

    This module covers the first half of that path. Most of the early-stage Tactics happen before Illumio Insights can see them — but understanding them explains why, by the time an alert fires, the attacker has already done significant groundwork.

    **The single takeaway: Lateral Movement (TA0008) is where the blast radius of an incident is determined — and it is where Illumio's detection and containment capabilities are strongest.**

    Estimated time: 25–30 minutes
difficulty: ""
timelimit: 3600
lab_config:
  default_layout_sidebar_size: 0
enhanced_loading: null
---

In this module you will research the **first half of the ATT&CK kill chain** using the MITRE ATT&CK website — from Reconnaissance through to Lateral Movement. You will connect the Techniques you find to what Illumio Insights detects and why it matters.

> [!NOTE]
> **Estimated time:** 25–30 minutes. This module involves web-based research on the MITRE ATT&CK website. Take time to read the detail — understanding the context behind a Technique is as important as knowing it exists.

---

# Task 1: The Early-Stage Tactics
==========

## Task 1.1 – Reconnaissance and Resource Development

**1 )** The first two Tactics — **Reconnaissance (TA0043)** and **Resource Development (TA0042)** — happen *before* the attacker makes contact with your environment. They are largely invisible to your security tools.

Navigate to each Tactic on the MITRE ATT&CK website and read the overview:

- https://attack.mitre.org/tactics/TA0043/
- https://attack.mitre.org/tactics/TA0042/

**2 )** Under **Reconnaissance**, the attacker maps your organisation before launching. Key Techniques include:

| Technique | Description |
|---|---|
| T1590 | Gather Victim Network Information — mapping IP ranges, DNS, network topology |
| T1591 | Gather Victim Org Information — employees, structure, business relationships |
| T1598 | Phishing for Information — targeted emails designed to harvest credentials before the main attack |

**3 )** Under **Resource Development**, the attacker builds their infrastructure:

| Technique | Description |
|---|---|
| T1583 | Acquire Infrastructure — registering domains, renting hosting for C2 servers |
| T1588 | Obtain Capabilities — purchasing or stealing malware and offensive tools |
| T1608 | Stage Capabilities — uploading tools to staging servers, ready for delivery |

> [!NOTE]
> These two Tactics happen entirely outside your environment. Your active defences begin at Initial Access (TA0001). But understanding that attackers have already researched and mapped your estate before they strike explains why their Initial Access attempts are often precise and well-targeted rather than opportunistic.

---

## Task 1.2 – Initial Access (TA0001)

**1 )** Navigate to:

https://attack.mitre.org/tactics/TA0001/

**2 )** Initial Access is where the attacker makes their first move *into* your environment. Review the full list of Techniques on the page and focus on these four most common ones:

| Technique | Description |
|---|---|
| **T1566** | Phishing — malicious email attachments or links |
| **T1190** | Exploit Public-Facing Application — exploiting a vulnerability in an internet-accessible system |
| **T1078** | Valid Accounts — using legitimate stolen credentials to log in |
| **T1133** | External Remote Services — logging in via internet-exposed VPN or RDP |

**3 )** Select **T1566 – Phishing** and review the Sub-Techniques:

- **.001** – Spearphishing Attachment
- **.002** – Spearphishing Link
- **.003** – Spearphishing via Service (e.g., LinkedIn, Teams, Slack)
- **.004** – Spearphishing Voice

> [!IMPORTANT]
> T1566 is consistently one of the most common Initial Access Techniques across all major threat actor groups. Scroll to the **Procedure Examples** section and note how many documented groups use it. This is the entry point for the majority of significant breaches — which is why email security and user awareness training remain critical investments regardless of how sophisticated your network controls are.

**4 )** Return to TA0001 and select **T1190 – Exploit Public-Facing Application**. Read the description and note the range of platforms affected. This Technique covers major edge-device exploitation campaigns including Log4Shell, Citrix Bleed, and GoAnywhere — high-profile incidents where unpatched internet-facing applications gave attackers immediate access.

---

## Task 1.3 – Execution, Persistence, and Privilege Escalation

**1 )** After gaining Initial Access, the attacker runs code (**Execution, TA0002**), establishes a foothold that survives reboots (**Persistence, TA0003**), and works to get higher permissions (**Privilege Escalation, TA0004**).

Spend 3–4 minutes reviewing the Techniques listed under each:

- https://attack.mitre.org/tactics/TA0002/
- https://attack.mitre.org/tactics/TA0003/
- https://attack.mitre.org/tactics/TA0004/

**2 )** Three Techniques worth noting from this stage:

| Technique | Tactic | Why it matters |
|---|---|---|
| T1059 | Execution | Command and Scripting Interpreter — attackers use PowerShell, cmd, bash to run their tools |
| T1053 | Persistence | Scheduled Task/Job — attacker adds a scheduled task so their code runs automatically after a reboot |
| T1055 | Privilege Escalation | Process Injection — injecting malicious code into a legitimate running process to inherit its permissions |

> [!TIP]
> These three Tactics are primarily the territory of **EDR and endpoint security tools**. Illumio Insights and segmentation become most powerful in the *next* stage — when the attacker starts moving. Before that, they are operating on a single compromised endpoint and may be invisible to network-layer tools.

---

# Task 2: Lateral Movement — The Illumio Sweet Spot
==========

## Task 2.1 – What Lateral Movement Is

**1 )** Navigate to:

https://attack.mitre.org/tactics/TA0008/

**2 )** **Lateral Movement (TA0008)** is the Tactic where an attacker moves from their initial foothold to other hosts within your environment. This is typically where the blast radius of an incident is determined — an attacker who cannot move laterally stays on one host; one who can will spread across your entire estate.

**3 )** The key Techniques under TA0008:

| Technique | Description |
|---|---|
| **T1021** | Remote Services — using RDP, SMB, SSH, WinRM to access other hosts |
| **T1550** | Use Alternate Authentication Material — pass-the-hash, pass-the-ticket attacks |
| **T1570** | Lateral Tool Transfer — copying attacker tools from one compromised host to another |
| **T1563** | Remote Service Session Hijacking — hijacking an existing legitimate remote session |

---

## Task 2.2 – Researching T1021 Remote Services

**1 )** Select **T1021 – Remote Services** on the MITRE ATT&CK website. This is the most commonly used Lateral Movement Technique across all major threat actor groups.

**2 )** Review the Sub-Techniques and the ports they use:

| Sub-Technique | Protocol | Default Port |
|---|---|---|
| T1021.001 | Remote Desktop Protocol (RDP) | 3389 |
| T1021.002 | SMB/Windows Admin Shares | 445 |
| T1021.003 | Distributed Component Object Model (DCOM) | 135 |
| T1021.004 | SSH | 22 |
| T1021.005 | VNC | 5900 |
| T1021.006 | Windows Remote Management (WinRM) | 5985/5986 |

**3 )** Select **T1021.002 – SMB/Windows Admin Shares** and scroll to the **Procedure Examples** section.

> [!NOTE]
> **WannaCry (2017)** and **NotPetya (2017)** both used SMB (port 445) as their lateral movement mechanism via the EternalBlue exploit (MS17-010). The Procedure Examples for T1021.002 document many groups that still use SMB today — including Lazarus Group, Wizard Spider, and FIN6. This is not a historical technique: it is actively exploited in every ransomware campaign that causes widespread damage.

**4 )** Select **T1021.001 – Remote Desktop Protocol** and review the **Mitigations** section. Note which mitigations are documented — particularly **M1035 (Limit Access to Resource Over Network)**, which is the category Illumio enforces.

---

## Task 2.3 – Lateral Movement in Illumio Insights

**1 )** In your **Illumio Console**, navigate to:

**Insights → Risky Traffic**

**2 )** The **Risky Traffic** view surfaces network flows using protocols associated with lateral movement. Look specifically for traffic on ports **3389 (RDP)**, **445 (SMB)**, and **5985/5986 (WinRM)** — the Sub-Technique ports from T1021.

**3 )** For each risky traffic flow displayed, consider:

- Is this flow expected? Is this a known administrative connection between hosts that should communicate?
- Is this a workload that should be *receiving* RDP or SMB connections?
- Does the source make sense — is it a known admin jump host, or is it an unexpected workload?

> [!IMPORTANT]
> **T1021 (Remote Services)** is one of the most-used Lateral Movement Techniques across all major APT groups and ransomware operators. The Risky Traffic view in Illumio Insights is specifically designed to surface these flows. An unexpected SMB connection from a workstation to a database server is a concrete, observable signal of T1021.002 in progress.

**4 )** Navigate to:

**Insights → Resource Traffic**

This view shows traffic at the individual workload level. Select any workload you identified from the Risky Traffic view and review what it is communicating with. This gives you the workload-level map of potential lateral movement paths in your environment.

---

**✅ Module 2 Complete**

You have researched the first half of the ATT&CK kill chain and connected Lateral Movement directly to what Illumio Insights surfaces. In Module 3 you will cover the later-stage Tactics — Exfiltration and Command and Control — and the specific Insights views that detect them.

Proceed to **Module 3: Exfiltration, C2 & Illumio Detection**.

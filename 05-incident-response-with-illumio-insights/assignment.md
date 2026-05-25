---
slug: incident-response-with-illumio-insights
id: bqbujsbrzrgq
type: challenge
title: 'Module 5: Incident Response with Illumio Insights'
teaser: Framework knowledge meets operational practice — running a formal IR investigation,
  mapping findings to ATT&CK, and taking containment action.
notes:
- type: text
  contents: |-
    # Module 5: Incident Response with Illumio Insights

    Modules 1–4 built the framework knowledge. This module is where it becomes operational.

    You will run a formal IR investigation using the Illumio Insights Agent, map what you find to ATT&CK Tactics, document your analyst verdict, and take containment action against a compromised workload.

    Every concept from the previous modules converges here: the 14 Tactics, the Lateral Movement techniques, the APT group profiles, the Insights views. This is the hands-on culmination of the core course.

    **The single takeaway: Insights translates network behaviour into ATT&CK language and gives you the tools to act on it — from detection through to quarantine — in a single workflow.**

    Estimated time: 20–25 minutes
difficulty: ""
timelimit: 2700
lab_config:
  default_layout_sidebar_size: 0
enhanced_loading: null
---

In this module you will use the **Illumio Insights Agent** to investigate suspicious activity in your environment, interpret findings through the ATT&CK framework, record your analyst verdict, and quarantine a workload.

> [!NOTE]
> **Estimated time:** 20–25 minutes. This module uses your Illumio Insights console directly. The specific findings you see will reflect your own environment's traffic — they will differ from the examples shown.

---

# Task 1: Launching and Reading an Investigation
==========

## Task 1.1 – The Insights Agent

**1 )** In your **Illumio Console**, navigate to:

**Insights → Insights Agent**

**2 )** Review the persona focus areas displayed. Each represents a different analyst role — the Insights Agent adapts its analysis and recommendations based on which you select. For this investigation, select **Incident Response**.

**3 )** Select **Start Investigation** at the top of the page.

> [!NOTE]
> If a previous IR investigation exists, select **View Details** and use the **+** icon at the top of the page to start a new one.

**4 )** Select **Last 24 hours** from the time range options, then select **Investigate**.

**5 )** Wait for the analysis to complete. When it does, read the **Summary** at the top of the page. Identify:

- Which ATT&CK Tactic IDs are mentioned in the summary?
- Which workloads are flagged?
- What is the assessed severity?

> [!TIP]
> Map each Tactic ID in the summary to the 14 Tactics you learned in Module 1. If you see **TA0008**, that is Lateral Movement. If you see **TA0010**, that is Exfiltration. If you see **TA0011**, that is Command and Control. The summary is translating observed network behaviour into ATT&CK language — and you now speak that language fluently enough to act on it.

---

## Task 1.2 – Reading the Investigation Sections

**1 )** Navigate to **Insights → Agent Summaries** and select the Incident Response summary you just created.

**2 )** Work through each section in order:

---

**Overview**

- Review the number of network records analysed and the time range covered
- Note the ATT&CK Tactics identified — cross-reference each with your Module 1 knowledge
- Remember there are 14 total MITRE ATT&CK Tactics; the ones flagged here are the ones Insights has evidence for in your environment's actual traffic

---

**Workloads in Flow**

- Select **Workloads in Flow** to see which specific workloads are involved in the detected activity
- Note the **Quarantine** option in the Actions column — you will use this in Task 2.2
- Consider: are these workloads whose compromise would represent a critical risk to your business? What data or services do they host?

---

**Findings**

- Select **Findings** to see a detailed breakdown of the detected threats
- Select **View Details** on the highest-severity Finding
- For each Finding, map the ATT&CK Tactic and Technique cited to the MITRE pages you visited in Modules 2 and 3 — you should now recognise what each one means

> [!TIP]
> If you see multiple Findings, start with the highest severity. In a real incident, the highest-severity Finding determines which team gets paged first and what containment action is taken immediately.

---

**Recommended Actions**

- Return to the **Investigation Analysis** tab and select **Recommended Actions**
- Review the Severity levels: **LOW**, **MEDIUM**, **HIGH**, **CRITICAL**
- Each Action is attributed to a specific team — note that different actions go to different functions (Network Engineering, Security Operations, Compliance, etc.)

> [!NOTE]
> In a real IR scenario, Recommended Actions would be worked simultaneously by different team members — not sequentially. The Insights Agent's role is to give each team member the right information for their function in a single place, eliminating the time lost to manual investigation and cross-team coordination.

---

# Task 2: Analyst Actions
==========

## Task 2.1 – Analyst Verdict and Tags

**1 )** At the bottom of the **Investigation Analysis** page, select **Assign Tags**.

**2 )** Review the available verdict classifications:

| Tag | Meaning |
|---|---|
| **True Positive** | The alert fired correctly — genuine malicious activity confirmed |
| **False Positive** | The alert fired but there was no malicious activity |
| **Benign Positive** | The alert fired and is correct, but this is expected and authorised business traffic |
| **False Positive – Data Quality** | The alert logic is correct, but the underlying data is inaccurate (e.g., an internal IP misclassified as external) |

> [!NOTE]
> Two additional classifications matter for understanding your detection programme quality — they do not appear as tags but are essential concepts:
> - **True Negative** — No malicious activity, and the system correctly did *not* alert. This is the desired baseline state.
> - **False Negative** — Malicious activity occurred but was *not detected*. This is the most dangerous outcome — the attack you did not see.

**3 )** Apply a verdict tag that honestly reflects what you observed. If the investigation flagged legitimate administrative RDP traffic between known hosts, **Benign Positive** is appropriate. If the activity is unexpected and unexplained, **True Positive** is the conservative and correct choice.

**4 )** Select **Comments** and add a brief investigation note. Include:
- Which ATT&CK Tactic(s) were flagged
- Which workloads were involved
- Your verdict and the reasoning behind it

> [!TIP]
> In a real SOC environment, investigation comments create a formal audit trail. A comment like *"TA0008 flagged on Finance-DB-01. Unexpected RDP from Workstation-14. No change window open. Tagging True Positive and escalating for containment."* gives any colleague the full context without re-running the investigation.

---

## Task 2.2 – Quarantine

**1 )** Return to **Workloads in Flow** in the Investigation Analysis.

**2 )** In the **Actions** column, select **Quarantine** for the first workload listed.

**3 )** Read the information in the confirmation dialogue carefully — it explains exactly what quarantine does and which traffic is blocked versus preserved. Critical services (DNS, PCE communication) and SSH for responders are typically preserved so the workload remains manageable.

**4 )** Select **Quarantine** to confirm.

> [!IMPORTANT]
> In a production environment, quarantining a workload immediately restricts its network connectivity and may impact business operations. In a real incident, always confirm with the workload owner before quarantining unless the severity justifies immediate action without approval. The ATT&CK Tactic you are containing is **Lateral Movement (TA0008)** — quarantine prevents the compromised workload from being used as a pivot point to reach other hosts.

**5 )** From the left-hand menu, select **Quarantine** to view all currently quarantined workloads, including the one you just added.

**6 )** Select the quarantined workload and then select **Restore**. Read the restoration information and confirm.

> [!NOTE]
> In a real incident, restoration happens only after the workload is confirmed clean and the threat is fully remediated — malware removed, credentials rotated, root cause identified. For this exercise, restore immediately to return the environment to its original state.

---

## Task 2.3 – Closing the ATT&CK Loop

**1 )** You have completed a full IR workflow. Map what you just did back to the MITRE ATT&CK framework:

| What Insights showed | ATT&CK Tactic | ATT&CK Technique |
|---|---|---|
| Risky Traffic (RDP/SMB/WinRM flows) | TA0008 Lateral Movement | T1021 Remote Services |
| Malicious IP Threat (outbound to known bad IP) | TA0011 Command and Control | T1071 Application Layer Protocol |
| External Data Transfer anomaly | TA0010 Exfiltration | T1041 / T1567 |
| Quarantine action taken | — | Blast radius contained |

**2 )** This mapping is the core value of combining MITRE ATT&CK with Illumio Insights. Every alert becomes a named Tactic. Every Tactic points to documented Techniques, Mitigations, and Detection Strategies on the MITRE website. Every containment action maps to a specific chokepoint in the attacker's kill chain. The framework turns detection into a structured, repeatable response — not a one-off reaction.

**3 )** The groups you studied in Module 4 — APT28, APT41, APT39, Lazarus Group — all have documented profiles that include the exact Techniques Illumio Insights just flagged. The alert you investigated is not abstract; it maps to real, documented adversary behaviour. That is the practical value of the framework.

---

**✅ Module 5 Complete — Core Course Complete**

You have completed the five core modules of this course. You can now:

- Navigate the MITRE ATT&CK framework and research any Tactic, Technique, or group
- Connect ATT&CK Tactics to the specific Illumio Insights views that surface them
- Run a formal IR investigation, apply analyst verdicts, and take containment action
- Understand which APT groups use which Techniques — and what that means for your environment

---

> [!NOTE]
> **Module 6 is optional extension content** covering the ATT&CK Navigator (web-hosted, no installation required), Sub-Techniques in depth, ATT&CK Mitigations, IOCs, IOAs, and YARA rules. Estimated additional time: ~50–60 minutes. There is no time pressure — explore at your own pace.

If you have time and would like to go further, proceed to **Module 6 (Optional): ATT&CK Navigator & Defensive Coverage**.

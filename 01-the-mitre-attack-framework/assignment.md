---
slug: the-mitre-attack-framework
id: eybjapebqvn2
type: challenge
title: 'Module 1: The MITRE ATT&CK Framework'
teaser: The industry-standard language for describing how attackers operate — and
  the foundation for everything Illumio Insights surfaces.
notes:
- type: text
  contents: |-
    # Module 1: The MITRE ATT&CK Framework

    Before you can investigate an incident or respond to an alert, you need a shared language for describing what attackers do. MITRE ATT&CK is that language — and it is the one Illumio Insights uses to label every threat it detects.

    This module introduces the framework from the ground up: what it is, how it is structured, and how the Illumio Insights console surfaces its classifications directly in your investigation workflow.

    **The single takeaway: Every ATT&CK Tactic you learn translates directly into faster, more confident incident response when Insights surfaces it in an alert.**

    Estimated time: 20–25 minutes
difficulty: ""
timelimit: 2700
lab_config:
  default_layout_sidebar_size: 0
enhanced_loading: null
---

In this module you will explore the structure of the **MITRE ATT&CK Framework** — the open-source knowledge base that documents how real-world attackers operate. By the end you will understand how the framework is organised and how Illumio Insights uses its language to describe threats in your environment.

> [!NOTE]
> **Estimated time:** 20–25 minutes. This module is foundational — every concept introduced here is used again in Modules 2 through 5.

---

# Task 1: What the MITRE ATT&CK Framework Is
==========

## Task 1.1 – The Knowledge Base

**1 )** **MITRE ATT&CK** (Adversarial Tactics, Techniques, and Common Knowledge) is a free, continuously updated knowledge base maintained by the MITRE Corporation. It documents how real threat actors operate — drawn from publicly reported incidents, malware analysis, and incident response investigations worldwide.

It is the closest thing the security industry has to a universal language for describing attacks. Security teams, vendors, regulators, and IR firms all speak it.

**2 )** The framework answers three questions about any observed attack behaviour:

| Concept | The question it answers | Example |
|---|---|---|
| **Tactic** | What is the attacker trying to achieve? | Move laterally through the network |
| **Technique** | How are they achieving it? | Use Remote Desktop Protocol (RDP) |
| **Procedure** | What exactly are they doing, step by step? | Log in via RDP with stolen credentials, copying tools from host A to host B |

> [!TIP]
> A useful mental model: a **Tactic** is the goal, a **Technique** is the method, and a **Procedure** is the specific execution. The same Tactic can be achieved by many different Techniques; the same Technique can be carried out in many different Procedures.

**3 )** The framework is used by:

- **SOC analysts** — to classify and investigate alerts
- **Threat hunters** — to proactively search for attacker behaviour patterns
- **Incident responders** — to reconstruct what an attacker did and in what sequence
- **Security engineers** — to identify gaps in detection and control coverage
- **Security vendors** — to label detections consistently so customers can correlate across tools

---

## Task 1.2 – The 14 Enterprise Tactics

**1 )** Open your browser and navigate to the MITRE ATT&CK Enterprise Tactics page:

https://attack.mitre.org/tactics/enterprise/

**2 )** The Enterprise matrix documents **14 Tactics**. They are not numbered sequentially — the framework has evolved over time and new Tactics have been added without renumbering. Read each Tactic ID and name carefully:

| Tactic ID | Tactic Name | What the attacker is doing |
|---|---|---|
| TA0043 | Reconnaissance | Gathering information before the attack begins |
| TA0042 | Resource Development | Building or acquiring tools and infrastructure |
| TA0001 | Initial Access | Getting their first foothold in the target environment |
| TA0002 | Execution | Running malicious code |
| TA0003 | Persistence | Maintaining access after reboots or interruptions |
| TA0004 | Privilege Escalation | Obtaining higher permissions |
| TA0005 | Defense Evasion | Avoiding detection by security tools |
| TA0006 | Credential Access | Stealing passwords and credentials |
| TA0007 | Discovery | Learning about the environment they are now inside |
| TA0008 | Lateral Movement | Moving from host to host within the network |
| TA0009 | Collection | Gathering data to be exfiltrated |
| TA0010 | Exfiltration | Sending data out of the environment |
| TA0011 | Command and Control | Maintaining communication with the compromised environment |
| TA0040 | Impact | Destroying, encrypting, or disrupting the target |

> [!NOTE]
> Select any Tactic ID on the MITRE website to see the full list of Techniques documented under it. Each Tactic typically has between 3 and 17 Techniques, with many Techniques having additional Sub-Techniques beneath them.

**3 )** The 14 Tactics map roughly to the **attack lifecycle** — from the earliest pre-attack activities through to the final impact on the victim. An attacker does not always use every Tactic: they pick the path of least resistance to their objective.

> [!IMPORTANT]
> The Tactics that cause the most damage — and where Illumio Insights adds the most detection value — are in the **middle and later stages**: Lateral Movement (TA0008), Exfiltration (TA0010), and Command and Control (TA0011). You will study these in depth in Modules 2 and 3.

---

## Task 1.3 – Techniques and Sub-Techniques

**1 )** Navigate to the MITRE ATT&CK Enterprise Techniques page:

https://attack.mitre.org/techniques/enterprise/

**2 )** Techniques are the core of the framework. Each Technique describes a specific method an attacker uses to achieve a Tactic. As of 2025, the Enterprise matrix documents over **200 Techniques**.

**3 )** Many Techniques have **Sub-Techniques** — more specific variations of the same method. Sub-Techniques use a decimal suffix. For example:

- **T1021** — Remote Services *(the parent Technique)*
  - **T1021.001** — Remote Desktop Protocol (RDP)
  - **T1021.002** — SMB/Windows Admin Shares
  - **T1021.006** — Windows Remote Management (WinRM)

> [!TIP]
> Sub-Techniques matter for detection. Identifying which sub-technique is in use tells you exactly which port and protocol to target. T1021.001 means close RDP (port 3389). T1021.002 means close SMB (port 445). The parent Technique alone is too broad to act on directly.

**4 )** Select **T1021 – Remote Services** on the techniques page and review the full list of Sub-Techniques. Notice that each sub-technique links to:

- **Procedure Examples** — real documented cases from known threat actors
- **Mitigations** — controls that reduce the risk of this Technique being used successfully
- **Detection Strategies** — how to spot this Technique in your environment

---

# Task 2: How Illumio Insights Uses the ATT&CK Language
==========

## Task 2.1 – Insights and ATT&CK

**1 )** In your **Illumio Console**, navigate to:

**Insights → Insights Agent**

**2 )** Select any existing investigation or persona summary. Wherever you see a Tactic label — for example, **TA0008** or **TA0010** — that label is a direct reference to the MITRE ATT&CK Tactic you just studied.

**3 )** Illumio Insights automatically maps the network behaviour it observes to ATT&CK Tactics and surfaces them in:

- **Insights Agent** investigation summaries
- The **Findings** section of each investigation
- **Recommended Actions** — each action references the Tactic it addresses

> [!NOTE]
> You do not need to manually identify which Tactic is occurring. Insights does the classification. Your role is to understand what each Tactic means so you can judge severity, prioritise response, and decide what action to take. That is the value of learning this framework.

---

## Task 2.2 – The Threat Actor Categories

**1 )** Attackers come from many different backgrounds. Understanding who is likely to target your organisation shapes which Tactics and Techniques you should prioritise:

| Threat Actor | Typical Motivation | Most Likely Tactics |
|---|---|---|
| Nation-state groups | Espionage, sabotage | Persistence, Lateral Movement, Exfiltration |
| Criminal gangs | Financial gain, ransomware | Initial Access, Lateral Movement, Impact |
| Hacktivists | Political or ideological goals | Initial Access, Impact, Defacement |
| Insider threats | Grievance, financial gain | Collection, Exfiltration |
| Lone attackers | Financial gain, notoriety | Initial Access, Credential Access |

**2 )** Risk profiles vary significantly by industry. A financial services organisation faces different priorities than a hospital or a power company — but Lateral Movement (TA0008) appears in the attack path of nearly every major incident regardless of sector. It is the universal chokepoint.

---

**✅ Module 1 Complete**

You now understand the structure of the MITRE ATT&CK framework and how Illumio Insights uses its language. In Module 2 you will research the first half of the attack kill chain — from Initial Access through to Lateral Movement — using the ATT&CK website.

Proceed to **Module 2: The Attack Path — Initial Access to Lateral Movement**.

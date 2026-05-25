---
slug: threat-actor-groups
id: ycdwszguj2sq
type: challenge
title: 'Module 4: Threat Actor Groups & Nation-State APTs'
teaser: The human side of ATT&CK — who uses these Techniques, why, and what that means
  for your threat model.
notes:
- type: text
  contents: |-
    # Module 4: Threat Actor Groups & Nation-State APTs

    Knowing the TTPs is one level of understanding. Knowing who uses them — their motivation, their targets, their persistence — is the context that transforms a list of Techniques into actionable threat intelligence.

    This module covers four of the most significant documented nation-state threat actor groups: Russia, China, Iran, and North Korea. You will research each on the MITRE ATT&CK website and connect their Technique profiles to what you would see in your own Illumio Insights console.

    **The single takeaway: The same Lateral Movement Techniques appear in every major APT group's profile — which means Illumio's detection of T1021 is relevant regardless of which group is targeting your organisation.**

    Estimated time: 20–25 minutes
difficulty: ""
timelimit: 3600
lab_config:
  default_layout_sidebar_size: 0
enhanced_loading: null
---

In this module you will investigate **Advanced Persistent Threat (APT) groups** — the state-sponsored and criminal organisations behind the most significant documented cyber attacks. You will use the MITRE ATT&CK website throughout and connect each group's Technique profile to what Illumio Insights detects.

> [!NOTE]
> **Estimated time:** 20–25 minutes. This module is research-based. Work at your own pace using the MITRE Groups page as your primary reference throughout.

Open the MITRE ATT&CK Groups page in your browser and keep it open:

https://attack.mitre.org/groups/

For each group, use their MITRE page to answer:
- What is their primary motivation?
- Which industries or countries do they target?
- What are their most commonly used Techniques?
- Have they been linked to any major documented campaigns?

> [!TIP]
> Use the search bar on the MITRE Groups page to find each group quickly by name or APT number. The **Associated Groups** section on each group page maps all aliases used by different vendors — the same group often has five or more names depending on who is reporting on them.

---

# Task 1: How APT Groups Are Documented
==========

## Task 1.1 – The Groups Page Structure

**1 )** Each group page on MITRE ATT&CK includes:

- A primary name and all known aliases
- Attribution details — which nation or organisation is responsible
- **Techniques Used** — a full table of every documented Technique, with source citations
- **Associated Campaigns** — specific documented operations
- **Associated Software** — malware and tools associated with this group
- **ATT&CK Navigator Layers** — a downloadable file for visualising their TTP profile (used in Module 6)

**2 )** Vendor naming is inconsistent across the industry. The **Associated Groups** section is one of the most practically useful features on each page — it prevents duplication of effort when the same group appears under different names in different threat intelligence reports.

---

## Task 1.2 – Understanding Defense Evasion

**1 )** Before researching specific groups, note that all advanced threat actors invest heavily in **Defense Evasion (TA0005)** — the Tactic dedicated to avoiding detection. Navigate to:

https://attack.mitre.org/tactics/TA0005/

**2 )** Key Defense Evasion Techniques used by APT groups:

| Technique | Description |
|---|---|
| T1070 | Indicator Removal — deleting logs, clearing event history to remove traces |
| T1036 | Masquerading — naming malware after legitimate system files to avoid scrutiny |
| T1027 | Obfuscated Files or Information — encrypting or packing payloads to evade scanning |
| T1562 | Impair Defenses — disabling AV, EDR, or logging to operate blind |

> [!NOTE]
> When reviewing a group's Technique profile, the Defense Evasion Techniques they use explain why their activity is hard to find. A group that routinely uses T1070 (Indicator Removal) will have cleaned its tracks before incident responders arrive. This context matters when you are setting detection priorities.

---

# Task 2: Nation-State Threat Actor Groups
==========

## Task 2.1 – Russia: APT28 (Fancy Bear)

**1 )** Search for **APT28** on the MITRE Groups page.

**2 )** APT28 is attributed to the **GRU** — Russian military intelligence. Active since at least 2004. Also known as: Fancy Bear, STRONTIUM, Forest Blizzard, Sofacy, Pawn Storm.

**3 )** Identify at least **three Techniques** APT28 is known to use. Look specifically for Techniques in Credential Access (TA0006), Lateral Movement (TA0008), and Defense Evasion (TA0005).

**4 )** Find one documented campaign associated with APT28 and read its summary.

> [!NOTE]
> APT28 is attributed to: interference in multiple national elections, attacks on NATO member governments, the 2015–16 German Bundestag hack, and the targeting of anti-doping agencies (WADA). Their tools include **X-Agent** (cross-platform implant), **Sofacy**, and **Komplex** (macOS). Their operations span a remarkably broad range of targets — from sports federations to defence contractors to political campaigns.

---

## Task 2.2 – China: APT41 (Wicked Panda)

**1 )** Search for **APT41** on the MITRE Groups page.

**2 )** APT41 is unique among nation-state groups — attributed to Chinese state interests but also conducting **financially motivated cybercrime** as a parallel activity. This dual mandate is unusual: most nation-state groups operate exclusively for espionage or disruption. APT41 steals intellectual property for the state *and* conducts ransomware operations for profit.

**3 )** Identify what makes APT41's targeting unusual compared to most nation-state groups. Note the range of industries they target — it is significantly broader than typical espionage actors.

**4 )** Find a Technique in APT41's profile that overlaps with the Exfiltration or C2 Techniques you researched in Module 3.

> [!NOTE]
> APT41 is widely documented for **supply chain attacks** — compromising software update mechanisms to deliver malware to thousands of downstream customers simultaneously. This is one of the most impactful attack vectors in the framework because victims install the compromised software themselves, believing it to be legitimate. The SolarWinds (2020) and 3CX (2023) incidents are textbook examples of this pattern.

---

## Task 2.3 – Iran: APT39

**1 )** Search for **APT39** on the MITRE Groups page. Also known as: Chafer, Remix Kitten, ITG07.

**2 )** APT39 is an Iranian group focused on **bulk intelligence gathering** against telecommunications, travel, and financial services organisations. They are the group associated with the **T1041** Technique you researched in Module 3.

**3 )** Identify their primary Initial Access Techniques. How do they typically get into target organisations?

**4 )** Note the Techniques they use in Credential Access and Lateral Movement. How do they progress once they are inside?

> [!NOTE]
> APT39 and APT35 (Charming Kitten/Phosphorus) are both Iranian groups but with different operational mandates. APT39 focuses on bulk data collection — particularly from telecommunications infrastructure that carries large volumes of personal and communications data. APT35 focuses on targeted credential theft against journalists, academics, dissidents, and government officials. Understanding these distinctions helps prioritise which Iranian actor profile is most relevant to your organisation's industry.

---

## Task 2.4 – North Korea: Lazarus Group

**1 )** Search for **Lazarus Group** on the MITRE Groups page.

**2 )** Lazarus Group is attributed to North Korea's **Reconnaissance General Bureau (RGB)**. They are unique among nation-state actors for combining **espionage** with **large-scale financial theft** — generating revenue to fund the regime in the face of international sanctions.

**3 )** Identify the scale of financial attacks attributed to this group. Find one campaign where they targeted financial institutions and read its summary.

**4 )** Note the Techniques they use for Initial Access. How do they establish their first foothold?

> [!NOTE]
> Lazarus Group is attributed to: the **Bangladesh Bank robbery** (2016, $81 million stolen via the SWIFT banking network), **WannaCry** (2017, using T1486 Data Encrypted for Impact and T1021.002 SMB lateral movement), and the **Ronin Bridge / Axie Infinity hack** (2022, ~$620 million in cryptocurrency). They are also responsible for the Sony Pictures hack (2014) — a destructive operation using T1485 (Data Destruction) rather than financial theft, demonstrating their range. They are the most financially destructive APT group documented in the ATT&CK framework.

---

# Task 3: Connecting Threat Actors to Illumio Insights
==========

## Task 3.1 – The Common Thread

**1 )** The four groups you have just researched — APT28 (Russia), APT41 (China), APT39 (Iran), and Lazarus Group (North Korea) — all rely heavily on **Lateral Movement (TA0008)**. Despite their different nationalities, mandates, and targets, **T1021 sub-techniques (RDP, SMB, WinRM)** appear in every group's documented profile.

**2 )** This is not a coincidence. These protocols are widely available in enterprise environments, are often poorly restricted, and provide exactly the access attackers need to move from an initial foothold to high-value targets. They are the universal lateral movement toolkit.

**3 )** In your **Illumio Console**, revisit:

**Insights → Risky Traffic**

Consider: if any of these groups had gained Initial Access to one workload in your environment, which of the Risky Traffic flows currently shown would represent their lateral movement paths? Which workloads would be their most likely next targets?

> [!TIP]
> This mental exercise — mapping known APT Technique profiles to what you observe in your own Insights console — is how you build a **threat-informed** picture of your estate's exposure. The question to ask is not "could we be targeted?" but "if we were targeted by this group, what would they try, and can I see it in Insights?"

---

## Task 3.2 – The Financial Services Threat Model

**1 )** If you work in financial services, your organisation is in the documented target set of:

- **APT28** — for geopolitical intelligence
- **APT41** — for financial data and dual-use cybercrime
- **APT39** — as a high-value data source for Iranian intelligence
- **Lazarus Group** — as a direct financial theft target via SWIFT, cryptocurrency, and payment systems

**2 )** All four groups use T1021 for lateral movement. All four would appear in Illumio Insights' Risky Traffic view. The defensive response is the same regardless of which group is responsible — restrict lateral movement protocols to only the hosts that legitimately need them.

---

**✅ Module 4 Complete**

You have researched four major nation-state threat actor groups and connected their Technique profiles to what Illumio Insights surfaces. In Module 5 you will put this knowledge to work in a full Incident Response workflow using the Insights Agent.

Proceed to **Module 5: Incident Response with Illumio Insights**.

---
slug: optional-navigator-and-defense-mapping
id: lywrvdpfrt9x
type: challenge
title: 'Module 6 (Optional): ATT&CK Navigator & Defensive Coverage'
teaser: Visualise threat actor TTP profiles, map your detection coverage, and build
  a picture of where your defences are strongest — and where the gaps are.
notes:
- type: text
  contents: |-
    # Module 6 (Optional): ATT&CK Navigator & Defensive Coverage

    This optional module goes deeper. The ATT&CK Navigator is a free MITRE-hosted visualisation tool that lets you see the full ATT&CK matrix colour-coded by threat actor, detection coverage, or your own annotations. No installation required — it runs entirely in your browser.

    The module also covers Sub-Techniques in more depth, the ATT&CK Mitigations catalogue (M-codes), IOCs, IOAs, and YARA rules — the defensive tooling that turns framework intelligence into operational detection.

    There is no time pressure on this module. Explore at your own pace — the Navigator rewards experimentation.

    Estimated time: 50–60 minutes
difficulty: ""
timelimit: 5400
lab_config:
  default_layout_sidebar_size: 0
enhanced_loading: null
---

This is optional extension content for learners who want to go further with the MITRE ATT&CK framework. No prior completion of Module 6 is required to finish the core course — but if you are here, the content that follows will significantly deepen your practical ability to use the framework for defensive planning.

> [!NOTE]
> **Estimated time:** 50–60 minutes. Work at your own pace — there are no time-sensitive steps.

---

# Task 1: The MITRE ATT&CK Navigator
==========

## Task 1.1 – Introducing the Navigator

**1 )** The **MITRE ATT&CK Navigator** is a free, open-source web application for visualising and annotating the full ATT&CK matrix. It allows you to:

- Load a threat actor group's Techniques and see them highlighted on the complete matrix
- Compare two threat actor groups side by side to identify overlapping Techniques
- Annotate the matrix with your own detection coverage — building a live gap analysis
- Export layers as JSON files or images for reporting

**2 )** Navigate to the hosted web version — no account or installation required:

https://mitre-attack.github.io/attack-navigator/

> [!NOTE]
> The Navigator runs entirely in your browser. Your work is **not saved** between sessions unless you export it as a layer file using the save function in the toolbar.

---

## Task 1.2 – Loading a Threat Actor Layer

**1 )** Open the Lazarus Group page on the MITRE ATT&CK website in a new browser tab:

https://attack.mitre.org/groups/G0032/

**2 )** Scroll down to the **ATT&CK Navigator Layers** section — located below the Techniques Used table. Download the available layer file.

> [!TIP]
> If you cannot find the Navigator Layers section, look for a button labelled **ATT&CK Navigator Layer** below the techniques table. It downloads a `.json` file.

**3 )** Return to the ATT&CK Navigator tab. Select **Open Existing Layer → Upload from Local** and upload the Lazarus Group layer file.

**4 )** The full ATT&CK matrix will now display with the Lazarus Group's documented Techniques highlighted in colour. Techniques used more frequently by this group appear in darker shading.

**5 )** Right-click any highlighted Technique cell and select **View Technique** to read its full MITRE documentation without leaving the Navigator.

---

## Task 1.3 – Comparing Two Threat Actors

**1 )** Select the **+** icon at the top of the Navigator page to add a second layer.

**2 )** Navigate to the APT28 page and download its Navigator layer:

https://attack.mitre.org/groups/G0007/

**3 )** Upload the APT28 layer as a second layer in the Navigator. Both groups' Techniques are now displayed with different colour coding on the same matrix.

**4 )** Where the two colours overlap, Techniques are used by *both* groups. Note which Techniques are shared — these represent the highest-priority detections because they are relevant to multiple major threat actors simultaneously.

> [!TIP]
> From the menu bar, select **Layer Controls → Show Control Labels** to display Technique names directly on the matrix cells. This makes it much easier to identify which specific Techniques are shared between the two groups.

**5 )** Use the **Filters** dropdown to filter the matrix by operating system — show only Techniques targeting **Windows**. For most enterprise environments, this is the most operationally relevant view.

---

## Task 1.4 – What You Are Seeing

**1 )** Note which column of the matrix has the highest concentration of highlighted cells for both groups — this is almost always **Lateral Movement (TA0008)** and **Defense Evasion (TA0005)**. These are the most universally used Tactics across all documented nation-state actors.

**2 )** The Techniques that appear in *both* layers — both Lazarus Group and APT28 — represent your highest-value detection investments. A control that blocks or detects those Techniques is effective against multiple major threat actors simultaneously.

> [!NOTE]
> You can add more layers. Try loading APT39 (Iranian group, from Module 4). Navigate to its MITRE page, download its layer, and add it as a third layer. The pattern of overlapping Lateral Movement Techniques will be consistent — reinforcing the case for T1021 restriction as the single most impactful network-level control.

---

# Task 2: Sub-Techniques and ATT&CK Mitigations in Depth
==========

## Task 2.1 – Sub-Techniques Revisited

**1 )** Return to the ATT&CK website and navigate to **T1021 – Remote Services**:

https://attack.mitre.org/techniques/T1021/

**2 )** You have seen T1021 throughout this course. This time, go through all six Sub-Techniques systematically and note the Mitigation IDs listed for each:

| Sub-Technique | Protocol | Default Port | Illumio Insights view |
|---|---|---|---|
| T1021.001 | Remote Desktop Protocol (RDP) | 3389 | Risky Traffic |
| T1021.002 | SMB/Windows Admin Shares | 445 | Risky Traffic |
| T1021.003 | DCOM | 135 | Risky Traffic |
| T1021.004 | SSH | 22 | Resource Traffic |
| T1021.005 | VNC | 5900 | Resource Traffic |
| T1021.006 | Windows Remote Management (WinRM) | 5985/5986 | Risky Traffic |

**3 )** For each Sub-Technique, the **Mitigations** section will list one or more M-codes. Note which M-codes appear most frequently across the Sub-Techniques — the most commonly appearing ones represent the controls with the broadest coverage of this Technique family.

---

## Task 2.2 – ATT&CK Mitigations (M-Codes)

**1 )** Navigate to the ATT&CK Enterprise Mitigations page:

https://attack.mitre.org/mitigations/enterprise/

**2 )** Mitigations are documented security controls that reduce the risk or effectiveness of one or more Techniques. Each is identified by an **M-code**.

**3 )** The four mitigations most directly relevant to what Illumio provides:

| Mitigation ID | Name | What it means | Illumio mapping |
|---|---|---|---|
| **M1030** | Network Segmentation | Segment networks to limit access between assets | Illumio Segmentation — the core capability |
| **M1035** | Limit Access to Resource Over Network | Restrict access to services over the network | Illumio deny rules — closing RDP/SMB/WinRM |
| **M1037** | Filter Network Traffic | Apply network traffic filtering policies | Illumio enforced policy |
| **M1031** | Network Intrusion Prevention | Detect and block malicious network activity | Illumio Insights detection and quarantine |

**4 )** Select **M1035 – Limit Access to Resource Over Network** and scroll to the **Techniques Addressed** section. Review how many Techniques list M1035 as a mitigation — this is the breadth of protection network access control provides when applied systematically.

> [!NOTE]
> The M1035 Techniques Addressed list is one of the most useful summaries in the ATT&CK framework for justifying a segmentation investment. When building a business case, this list shows exactly which documented attack Techniques are addressed by network access restrictions — the control Illumio enforces.

---

# Task 3: IOCs, IOAs, and YARA Rules
==========

## Task 3.1 – Indicators of Compromise vs. Indicators of Attack

**1 )** When investigating an incident, two detection paradigms apply:

- **IOC (Indicators of Compromise)** — Evidence that an attack has *already happened*. These are retrospective. Examples: known malicious IP addresses matched against logs, file hashes of known malware, C2 domain names extracted from captured traffic.

- **IOA (Indicators of Attack)** — Behavioural patterns that indicate an attack is *in progress*, even before a compromise is confirmed. These are real-time. Examples: an RDP connection between two workstations that have never communicated before, a database server making its first-ever outbound internet connection, a large file transfer from a host that normally generates minimal traffic.

> [!NOTE]
> IOAs are generally more powerful than IOCs for real-time defence — they can detect an attack in progress rather than confirming one after the fact. **Illumio Insights detects primarily at the IOA level**: it flags *behavioural* anomalies (unexpected lateral movement traffic, unexpected exfiltration volumes, connections to known malicious IPs) rather than relying solely on known-malicious signatures. This means it can surface novel attacks that have never been seen before — not just known indicators.

---

## Task 3.2 – YARA Rules

**1 )** **YARA rules** are pattern-matching rules used to detect and classify malicious files or network activity. They operationalise the IOCs you identify through ATT&CK research and threat intelligence — turning intelligence into actionable detection logic.

**2 )** A YARA rule has three sections:

| Section | Purpose |
|---|---|
| **Meta** | Descriptive metadata — author, severity, description, ATT&CK mapping |
| **Strings** | The patterns to match against — text strings, hex values, or regex |
| **Condition** | The logic that triggers a match — when to fire the rule |

**3 )** Here is an example YARA rule detecting T1567.002 (Exfiltration to Cloud Storage) — connecting directly to the Technique you researched in Module 3:

```
rule Cloud_Storage_Exfil_Destinations
{
meta:
    description = "Detects references to cloud storage upload APIs"
    severity = "high"
    mitre_tactic = "TA0010"
    mitre_technique = "T1567.002"
    author = "Security Operations"

strings:
    $aws      = "s3.amazonaws.com"    nocase
    $gdrive   = "drive.google.com"    nocase
    $mega     = "mega.nz"             nocase
    $dropbox  = "api.dropbox.com"     nocase
    $onedrive = "onedrive.live.com"   nocase

condition:
    any of ($aws, $gdrive, $mega, $dropbox, $onedrive)
}
```

**4 )** Note how the meta section maps the rule directly to an ATT&CK Tactic and Technique. This is standard practice — any match from this rule can be immediately classified in ATT&CK terms, feeding consistently labelled data into your SIEM and enabling correlation with Illumio Insights findings under the same Tactic (TA0010).

---

# Task 4: Mapping Illumio to the ATT&CK Matrix
==========

## Task 4.1 – Where Illumio Sits on the Full Matrix

**1 )** The final exercise in this course is a complete, honest coverage map. Where does Illumio's combined detection and containment capability sit across all 14 ATT&CK Tactics?

| ATT&CK Tactic | Illumio visibility | Illumio capability |
|---|---|---|
| TA0043 Reconnaissance | None — happens outside the environment | None |
| TA0042 Resource Development | None — attacker infrastructure, pre-attack | None |
| TA0001 Initial Access | None — endpoint/email/edge layer | None |
| TA0002 Execution | None — endpoint layer | None |
| TA0003 Persistence | None — endpoint layer | None |
| TA0004 Privilege Escalation | None — endpoint/identity layer | None |
| TA0005 Defense Evasion | None — endpoint layer | None |
| TA0006 Credential Access | None — endpoint/identity layer | None |
| TA0007 Discovery | Partial — unusual internal scanning visible in traffic | Detection via Resource Traffic |
| **TA0008 Lateral Movement** | **Strong** — RDP/SMB/WinRM flows between workloads | **Risky Traffic detection + policy block** |
| TA0009 Collection | Partial — large internal data movements before exfil | External Data Transfer (internal) |
| **TA0010 Exfiltration** | **Strong** — unusual outbound volume to external destinations | **External Data Transfer detection** |
| **TA0011 Command and Control** | **Strong** — known malicious IPs, unusual outbound connections | **Malicious IP Threats detection** |
| TA0040 Impact | Partial — encryption causes observable traffic changes | Detection via anomaly; containment limits scope |

**2 )** This table is deliberately honest. Illumio is not a replacement for EDR, email security, identity tools, or endpoint controls — it is the network layer that the other tools do not cover. Its value is specifically and defensibly in the **middle of the kill chain**.

**3 )** In the ATT&CK Navigator, this coverage map would colour TA0008, TA0010, and TA0011 as "covered" on your matrix — and leave TA0001 through TA0007 clearly uncovered, showing where other tools must do the work.

---

## Task 4.2 – Building Your Own Coverage Map

**1 )** Return to the ATT&CK Navigator:

https://mitre-attack.github.io/attack-navigator/

**2 )** Select **Create New Layer → Enterprise ATT&CK**. This opens a blank matrix showing every Technique in the framework.

**3 )** Manually select the Techniques that Illumio Insights detects in your environment (T1021, T1571, T1041, T1567, T1071, T1090) and apply a colour or score to mark them as covered.

**4 )** Export this layer as a JSON file using the save function in the toolbar. This becomes the starting point for your organisation's coverage map — a living document that you update as your detection programme matures.

> [!TIP]
> Updated quarterly and presented to stakeholders, an ATT&CK Navigator coverage map is one of the most concise ways to show the state of your detection programme. It answers the executive question — *"what can we detect, and what can't we?"* — in a single visual that references an industry-standard framework.

---

**✅ Module 6 Complete — Full Course Complete**

You have completed the entire MITRE ATT&CK with Illumio Insights course. You can now:

- Navigate the full ATT&CK framework — all 14 Tactics, Techniques, Sub-Techniques, and Mitigations
- Load threat actor layers into the Navigator and compare TTP profiles visually
- Understand the difference between IOCs and IOAs — and why Illumio Insights operates at the IOA level
- Write and interpret YARA rules mapped to ATT&CK Techniques
- Build and maintain an ATT&CK Navigator coverage map for your organisation

> [!NOTE]
> The MITRE ATT&CK website is a living resource — new Techniques are documented as novel attack methods are discovered, and existing Technique pages are updated as new Procedure Examples are published. Returning to it regularly, particularly when a new major incident is reported publicly, will continue to build your framework fluency over time.

---
slug: exfiltration-c2-and-illumio-detection
id: uuyt8zjle26r
type: challenge
title: 'Module 3: Exfiltration, C2 & Illumio Detection'
teaser: The later-stage Tactics where data leaves the network — and the Illumio Insights
  views built to detect them.
notes:
- type: text
  contents: |-
    # Module 3: Exfiltration, C2 & Illumio Detection

    The later-stage Tactics are where the damage becomes visible. By this point the attacker has a foothold, has moved where they need to be, and is now collecting data, maintaining a communication channel, and preparing to exfiltrate.

    These are also the Tactics where Illumio Insights adds the most detection value. This module connects each Tactic directly to the Insights views that surface it — Malicious IP Threats, External Data Transfer, and Country Insights.

    **The single takeaway: Exfiltration (TA0010) and Command and Control (TA0011) are the Tactics Illumio Insights is built to detect and interrupt.**

    Estimated time: 25–30 minutes
difficulty: ""
timelimit: 3600
lab_config:
  default_layout_sidebar_size: 0
enhanced_loading: null
---

In this module you will research the **later-stage Tactics** of the ATT&CK kill chain and connect each one directly to the Illumio Insights detection views that surface them in your environment.

> [!NOTE]
> **Estimated time:** 25–30 minutes.

---

# Task 1: Collection and Exfiltration
==========

## Task 1.1 – Collection (TA0009)

**1 )** Navigate to:

https://attack.mitre.org/tactics/TA0009/

**2 )** **Collection** is the Tactic where attackers gather the data they intend to exfiltrate. They may collect from multiple sources before sending anything out. Key Techniques:

| Technique | Description |
|---|---|
| T1005 | Data from Local System — browsing and copying files from the compromised host |
| T1074 | Data Staged — aggregating collected data in a central location before exfiltration |
| T1560 | Archive Collected Data — compressing or encrypting data before sending (ZIP, RAR, 7z) |
| T1114 | Email Collection — stealing data directly from mailboxes |

> [!TIP]
> **T1074 (Data Staged)** is a meaningful detection opportunity — a sudden spike in large file transfers *between* internal hosts often signals staging activity before exfiltration begins. The data is moving to a single collection point before it leaves. This internal movement is something Illumio Insights' External Data Transfer view can surface as an anomaly.

---

## Task 1.2 – Exfiltration (TA0010)

**1 )** Navigate to:

https://attack.mitre.org/tactics/TA0010/

**2 )** Review the Techniques listed. There are 9 documented Techniques for Exfiltration. Focus on these three:

| Technique | Description |
|---|---|
| **T1041** | Exfiltration Over C2 Channel — data leaves via the same channel used for C2 communications |
| **T1048** | Exfiltration Over Alternative Protocol — DNS tunnelling, ICMP, or custom protocols |
| **T1567** | Exfiltration Over Web Service — data sent to legitimate cloud storage or code repositories |

**3 )** Select **T1041 – Exfiltration Over C2 Channel** and review the page fully:

- Note the **Platforms** section — ESXi, Linux, Windows, macOS. No platform is immune.
- Scroll to **Procedure Examples** and locate **APT39** — an Iranian cyber espionage group targeting financial services and telecommunications. You will study APT39 in depth in Module 4.
- Review the **Mitigations** — note that network-based detection and traffic filtering are the primary defensive strategies documented.

**4 )** Select **T1567 – Exfiltration Over Web Service** and review the Sub-Techniques:

| Sub-Technique | Destination service |
|---|---|
| T1567.002 | Cloud Storage — AWS S3, Dropbox, Google Drive, OneDrive |
| T1567.003 | Code Repository — GitHub, GitLab, Bitbucket |
| T1567.004 | Text Storage Sites — Pastebin and similar services |

> [!NOTE]
> **T1567.002** is particularly difficult to detect because the traffic uses standard HTTPS to trusted domain names. Volume, timing, and the identity of the *source workload* — rather than the destination protocol — are the detection signals. A database server that has never previously made outbound HTTPS connections to S3 suddenly doing so is far more meaningful than the destination itself.

---

## Task 1.3 – Command and Control (TA0011)

**1 )** Navigate to:

https://attack.mitre.org/tactics/TA0011/

**2 )** **Command and Control (C2)** is the communication channel the attacker maintains with the compromised environment. It is used to issue commands, deliver additional tools, and receive exfiltrated data. Key Techniques:

| Technique | Description |
|---|---|
| **T1071** | Application Layer Protocol — C2 disguised as normal HTTP/S, DNS, or mail traffic |
| **T1105** | Ingress Tool Transfer — downloading additional tools from attacker-controlled infrastructure |
| **T1572** | Protocol Tunnelling — hiding C2 traffic inside legitimate protocols |
| **T1090** | Proxy — routing C2 traffic through intermediate servers to mask the true destination |

**3 )** Select **T1071 – Application Layer Protocol** and review the Sub-Techniques:

| Sub-Technique | Protocol |
|---|---|
| T1071.001 | Web Protocols (HTTP/HTTPS) |
| T1071.002 | File Transfer Protocols (FTP, SFTP) |
| T1071.003 | Mail Protocols (SMTP, IMAP) |
| T1071.004 | DNS |

> [!IMPORTANT]
> **T1071.004 (DNS)** is a particularly significant C2 channel because DNS traffic is almost universally allowed through firewalls and often not inspected. DNS tunnelling tools allow attackers to exfiltrate data and receive commands using nothing but DNS queries — which look like legitimate domain lookups to most network security devices. High-volume DNS queries to an unusual or newly registered domain are the primary detection signal.

---

# Task 2: Illumio Insights — Detecting the Later-Stage Tactics
==========

## Task 2.1 – Malicious IP Threats

**1 )** In your **Illumio Console**, navigate to:

**Insights → Malicious IP Threats**

**2 )** This view surfaces traffic flows from workloads in your environment to **known malicious IP addresses**, matched against threat intelligence feeds. A flow to a known malicious IP is a strong signal of **Command and Control (TA0011)** activity — specifically T1071 or one of its Sub-Techniques.

**3 )** For each malicious IP threat displayed, consider:

- Which workload is the source of the connection?
- What country or organisation does the destination IP belong to?
- What volume of traffic is moving to this destination — single packets or sustained transfer?
- Is this workload one that should be making outbound internet connections?

> [!TIP]
> Not every malicious IP hit confirms active C2. Some are from automated scanners or bots probing internet-facing services. The signal to prioritise is an *outbound* flow initiated by an internal workload that has no legitimate reason to contact external hosts — particularly if that workload is a database server, a file server, or any system that normally operates in a purely internal tier.

---

## Task 2.2 – External Data Transfer

**1 )** Navigate to:

**Insights → External Data Transfer**

**2 )** This view surfaces workloads sending unusually large volumes of data outside your environment. This is the primary detection signal for **Exfiltration (TA0010)** and also catches the **Collection/Staging (TA0009)** phase where data consolidates from multiple internal hosts to one before it leaves.

**3 )** For any flagged workloads, consider:

- What data does this workload hold? Is it a database server, a file server, an application host?
- Is this volume of outbound transfer normal for this workload type at this time of day?
- What is the destination — a known business partner, a documented cloud backup service, or an unrecognised IP?

> [!NOTE]
> Large outbound transfers to cloud storage destinations (AWS S3, Google Cloud Storage, Azure Blob) may be legitimate backup or sync operations — or they may be T1567.002 (Exfiltration to Cloud Storage). The question that resolves the ambiguity is not *where* but *who*: would this specific workload, in its normal operating role, ever initiate this type of transfer?

---

## Task 2.3 – Country Insights

**1 )** Navigate to:

**Insights → Country Insights**

**2 )** This view shows the geographic distribution of external traffic from your environment. Unexpected connections to countries your organisation does not operate in — particularly countries with known offensive cyber programmes — add context to other signals.

**3 )** Note which countries appear in your environment's traffic profile. Connections to unexpected regions are most meaningful when they appear alongside Malicious IP Threats or External Data Transfer anomalies — they strengthen the case for an active C2 or exfiltration investigation rather than confirming it on their own.

> [!TIP]
> Country Insights is a supporting signal, not a standalone indicator. Many legitimate cloud services host infrastructure globally — a connection to a data centre in an unexpected country may simply be AWS or Azure infrastructure. The value is in *unexpected* destinations appearing in combination with other Insights signals, not in the geography alone.

---

# Task 3: The End State — Impact (TA0040)
==========

## Task 3.1 – What Impact Looks Like

**1 )** Navigate to:

https://attack.mitre.org/tactics/TA0040/

**2 )** **Impact** is the final Tactic — what the attacker does once they have achieved their objectives. Key Techniques:

| Technique | Description |
|---|---|
| **T1486** | Data Encrypted for Impact — ransomware encryption of files |
| T1489 | Service Stop — disabling critical business services |
| T1485 | Data Destruction — deleting or corrupting data irreversibly |
| T1491 | Defacement — modifying website or system content |

> [!IMPORTANT]
> **T1486 – Data Encrypted for Impact is the ransomware Technique.** Every major ransomware family — Conti, LockBit, REvil, and their successors — ultimately executes T1486. But the scale of that encryption is entirely dependent on how far Lateral Movement (TA0008) was allowed to spread before it was detected. If TA0008 is contained, T1486 affects one host. If TA0008 ran unchecked, T1486 affects every host the attacker reached.

**2 )** You have now covered all 14 Tactics across three modules. The pattern is consistent across the kill chain:

| Kill chain stage | Primary tooling | Illumio's role |
|---|---|---|
| Pre-attack (TA0043, TA0042) | None visible to defenders | None |
| Initial Access to Evasion (TA0001–TA0005) | EDR, email security, patching | None |
| Credential Access to Discovery (TA0006–TA0007) | EDR, identity tooling | Partial (Resource Traffic) |
| **Lateral Movement (TA0008)** | **Network controls** | **Strong detection + containment** |
| **Collection to C2 (TA0009–TA0011)** | **Network monitoring** | **Strong detection (Insights views)** |
| Impact (TA0040) | Backup/recovery | Containment limits scope |

---

**✅ Module 3 Complete**

You have researched the later-stage ATT&CK Tactics and connected each one to the Illumio Insights views that surface them. In Module 4 you will put a face to the framework — researching the nation-state threat actor groups that use these Techniques.

Proceed to **Module 4: Threat Actor Groups & Nation-State APTs**.

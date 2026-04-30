
<p align="center">
 <img width="1672" height="941" alt="image" src="https://github.com/user-attachments/assets/e252cfbd-923f-40e0-bdb1-b4d32f5c5798" />

</p>




# 🛡️ Threat Hunt Report – SIGNALS BEFORE THE NOISE
External RDP Compromise 

---

## 📌 Executive Summary

<Brief, high-level overview of the threat hunt.  
Answer what happened, why it matters, and what was discovered in 3–4 sentences.>

---

## 🎯 Hunt Objectives

- Identify malicious activity across endpoints and network telemetry  
- Correlate attacker behavior to MITRE ATT&CK techniques  
- Document evidence, detection gaps, and response opportunities  

---

## 🧭 Scope & Environment

- **Environment:** Microsoft Sentinel (law-cyber-range workspace) – Finance department, LogN Pacific Financial Services   
- **Data Sources:**
- SigninLogs  
- CloudAppEvents  
- EmailEvents   
- **Timeframe:** 2026-02-25 → 2026-02-26 

---

## 📚 Table of Contents

- [🧠 Hunt Overview](#-hunt-overview)
- [🧬 MITRE ATT&CK Summary](#-mitre-attck-summary)
- [🔍 Flag Analysis](#-flag-analysis)
  - [🚩 Flag 1](#-flag-1)
  - [🚩 Flag 2](#-flag-2)
  - [🚩 Flag 3](#-flag-3)
  - [🚩 Flag 4](#-flag-4)
  - [🚩 Flag 5](#-flag-5)
  - [🚩 Flag 6](#-flag-6)
  - [🚩 Flag 7](#-flag-7)
  - [🚩 Flag 8](#-flag-8)
  - [🚩 Flag 9](#-flag-9)
  - [🚩 Flag 10](#-flag-10)
  - [🚩 Flag 11](#-flag-11)
  - [🚩 Flag 12](#-flag-12)
  - [🚩 Flag 13](#-flag-13)
  - [🚩 Flag 14](#-flag-14)
  - [🚩 Flag 15](#-flag-15)
  - [🚩 Flag 16](#-flag-16)
  - [🚩 Flag 17](#-flag-17)
  - [🚩 Flag 18](#-flag-18)
  - [🚩 Flag 19](#-flag-19)
  - [🚩 Flag 20](#-flag-20)
  - [🚩 Flag 21](#-flag-21)
  - [🚩 Flag 22](#-flag-22)
  - [🚩 Flag 23](#-flag-23)
  - [🚩 Flag 24](#-flag-24)
  - [🚩 Flag 25](#-flag-25)
  - [🚩 Flag 26](#-flag-26)
  - [🚩 Flag 27](#-flag-27)
  - [🚩 Flag 28](#-flag-28)
  - [🚩 Flag 29](#-flag-29)
  - [🚩 Flag 30](#-flag-30)
  - [🚩 Flag 31](#-flag-31)
  - [🚩 Flag 32](#-flag-32)
  - [🚩 Flag 33](#-flag-33)
  - [🚩 Flag 34](#-flag-34)
  - [🚩 Flag 35](#-flag-35)
  - [🚩 Flag 36](#-flag-36)
  - [🚩 Flag 37](#-flag-37)
  - [🚩 Flag 38](#-flag-38)

- [🚨 Detection Gaps & Recommendations](#-detection-gaps--recommendations)
- [🧾 Final Assessment](#-final-assessment)
- [📎 Analyst Notes](#-analyst-notes)

---

## 🧠 Hunt Overview

<High-level narrative describing the attack lifecycle, key behaviors observed, and why this hunt matters.>

---

## 🧬 MITRE ATT&CK Summary

| Flag | Technique Category | MITRE ID | Priority |
|-----:|-------------------|----------|----------|
| 1 | | T1593 | Search Open Websites/Domains | Reconnaissance | 🟡 Medium |
| T1593.001 | Search Open Websites/Domains: Social Media | Reconnaissance | 🟠 High |
| T1594 | Search Victim-Owned Websites | Reconnaissance | 🟡 Medium |
| T1589 | Gather Victim Identity Information | Reconnaissance | 🟠 High |
| T1591 | Gather Victim Org Information | Reconnaissance | 🟡 Medium | 
| 2 | | T1580 | Cloud Infrastructure Discovery | Discovery | 🟠 High |
| T1593 | Search Open Websites/Domains | Reconnaissance | 🟠 High |
| T1590 | Gather Victim Network Information | Reconnaissance | 🟡 Medium |
| T1591 | Gather Victim Org Information | Reconnaissance | 🟡 Medium |
| 3 | | T1590.005 | Gather Victim Network Information: IP Addresses | Reconnaissance | 🔴 Critical |
| T1593 | Search Open Websites/Domains | Reconnaissance | 🟠 High |
| T1590 | Gather Victim Network Information | Reconnaissance | 🟠 High |
| T1595.001 | Active Scanning: Scanning IP Blocks | Reconnaissance | 🟡 Medium |
| 4 | | T1590.005 | Gather Victim Network Information: IP Addresses | Reconnaissance | 🔴 Critical |
| T1590 | Gather Victim Network Information | Reconnaissance | 🟠 High |
| T1595 | Active Scanning | Reconnaissance | 🟠 High |
| T1133 | External Remote Services | Initial Access | 🔴 Critical |
| 5 | | T1593.001 | Search Open Websites/Domains: Social Media | Reconnaissance | 🔴 Critical |
| T1589.002 | Gather Victim Identity Information: Email Addresses | Reconnaissance | 🟠 High |
| T1591.004 | Gather Victim Org Information: Identify Roles | Reconnaissance | 🟠 High |
| T1590.005 | Gather Victim Network Information: IP Addresses | Reconnaissance | 🔴 Critical |
| 6 | <Placeholder> | <Placeholder> | <Placeholder> |
| 7 | <Placeholder> | <Placeholder> | <Placeholder> |
| 8 | <Placeholder> | <Placeholder> | <Placeholder> |
| 9 | <Placeholder> | <Placeholder> | <Placeholder> |
| 10 | <Placeholder> | <Placeholder> | <Placeholder> |
| 11 | <Placeholder> | <Placeholder> | <Placeholder> |
| 12 | <Placeholder> | <Placeholder> | <Placeholder> |
| 13 | <Placeholder> | <Placeholder> | <Placeholder> |
| 14 | <Placeholder> | <Placeholder> | <Placeholder> |
| 15 | <Placeholder> | <Placeholder> | <Placeholder> |
| 16 | <Placeholder> | <Placeholder> | <Placeholder> |
| 17 | <Placeholder> | <Placeholder> | <Placeholder> |
| 18 | <Placeholder> | <Placeholder> | <Placeholder> |
| 19 | <Placeholder> | <Placeholder> | <Placeholder> |
| 20 | <Placeholder> | <Placeholder> | <Placeholder> |
| 21 | <Placeholder> | <Placeholder> | <Placeholder> |
| 22 | <Placeholder> | <Placeholder> | <Placeholder> |
| 23 | <Placeholder> | <Placeholder> | <Placeholder> |
| 24 | <Placeholder> | <Placeholder> | <Placeholder> |
| 25 | <Placeholder> | <Placeholder> | <Placeholder> |
| 26 | <Placeholder> | <Placeholder> | <Placeholder> |
| 27 | <Placeholder> | <Placeholder> | <Placeholder> |
| 28 | <Placeholder> | <Placeholder> | <Placeholder> |
| 29 | <Placeholder> | <Placeholder> | <Placeholder> |
| 30 | <Placeholder> | <Placeholder> | <Placeholder> |
| 31 | <Placeholder> | <Placeholder> | <Placeholder> |
| 32 | <Placeholder> | <Placeholder> | <Placeholder> |
| 33 | <Placeholder> | <Placeholder> | <Placeholder> |
| 34 | <Placeholder> | <Placeholder> | <Placeholder> |
| 35 | <Placeholder> | <Placeholder> | <Placeholder> |
| 36 | <Placeholder> | <Placeholder> | <Placeholder> |
| 37 | <Placeholder> | <Placeholder> | <Placeholder> |
| 38 | <Placeholder> | <Placeholder> | <Placeholder> |
---

## 🔍 Flag Analysis

_All flags below are collapsible for readability._

---

<details>
<summary id="-flag-1">🚩 <strong>Flag 1: <Technique Name></strong></summary>

### 🎯 Objective
Identify the target organisation under investigation to anchor the threat hunt 
and correlate infrastructure, telemetry, and OSINT findings to a single entity.

### 📌 Finding
The fictional company under investigation is **PHTG**. The abbreviation was 
identified through open-source evidence analysis prior to any telemetry 
investigation. It appeared consistently across the LinkedIn post, Azure portal 
screenshot, VM naming conventions, and internal directory structures.

### 🔍 Evidence

| Field | Value |
|------|-------|
| Company Abbreviation | PHTG |
| VM Name (Exhibit B) | azwks-phtg-02 |
| Internal Path (Brief) | C:\ProgramData\PHTG\HealthCloud\ |
| Employee (Exhibit A) | Sarah Chen — Cloud Engineer at PHTG |
| Host | N/A — OSINT phase, no endpoint telemetry involved |
| Timestamp | N/A — Static open-source evidence |
| Process | N/A — No process execution involved |
| Parent Process | N/A — No process execution involved |
| Command Line | N/A — No process execution involved |

### 💡 Why it matters
A company's abbreviation appearing in VM naming conventions, internal directory 
structures, and employee social media profiles constitutes an OPSEC leak. An 
attacker correlating these signals across public sources can:
- Identify and enumerate cloud infrastructure belonging to the target
- Search for additional exposed assets using naming patterns (e.g. `azwks-phtg-*`)
- Build a target profile before conducting any active scanning

In this case, the LinkedIn post by Sarah Chen inadvertently confirmed the 
company abbreviation, the VM naming convention, and the existence of an 
internet-exposed Azure VM — all without the attacker touching a single 
packet.

### 🔧 KQL Query Used
N/A — This finding was derived entirely from open-source evidence (OSINT). 
No KQL query was required. The company abbreviation was extracted directly 
from:
- Exhibit A: LinkedIn post (employee job title and company affiliation)
- Exhibit B: Azure portal screenshot (VM name `azwks-phtg-02`)
- Hunt brief: Explicit references to PHTG throughout the briefing document

### 🖼️ Screenshot
<img width="872" height="1628" alt="image" src="https://github.com/user-attachments/assets/48e73031-9641-42fe-b651-4b4226682306" />

<img width="886" height="658" alt="image" src="https://github.com/user-attachments/assets/23c2f4bd-dd66-4553-848d-7de25334313b" />

### 🛠️ Detection Recommendation

**Hunting Tip:**  
Organisations should conduct regular OSINT reviews of employee social media 
profiles, particularly those in cloud engineering, DevOps, and IT roles. 
Key controls to implement:

- **Enforce a VM naming policy** that does not expose company abbreviations, 
  environment types, or asset roles in publicly visible resource names
- **Social media awareness training** should explicitly cover the risks of 
  photographing workstations, cloud consoles, or infrastructure dashboards
- **Azure Policy** can enforce naming conventions that obscure organisational 
  identifiers in resource names
- Periodically search LinkedIn, Twitter/X, and GitHub for company 
  abbreviations combined with cloud provider keywords to identify unintentional 
  exposure before threat actors do

</details>

---

<details>
<summary id="-flag-2">🚩 <strong>Flag 2: <Technique Name></strong></summary>

### 🎯 Objective
Identify the specific Azure virtual machine exposed in the LinkedIn post to 
anchor all subsequent telemetry queries to a concrete, named asset. Without 
a confirmed hostname, no endpoint telemetry can be scoped accurately.

### 📌 Finding
The exposed virtual machine is **azwks-phtg-02**. The name was visible in the 
Azure portal screenshot (Exhibit B) shared in the LinkedIn post, appearing both 
as the page title and confirmed in the VM properties panel. The naming 
convention reveals the asset type (workstation), the organisation (PHTG), and 
the sequential instance number (02).

### 🔍 Evidence

| Field | Value |
|------|-------|
| Host | azwks-phtg-02 |
| VM Name (Page Title) | azwks-phtg-02 |
| VM Name (Properties Panel) | azwks-phtg-02 |
| Operating System | Windows 10 Enterprise |
| Location | East US 2 (Zone 1) |
| Time Created | 12/10/2025, 3:08 AM UTC |
| Subscription | LOGIN\| Pacific - Cyber Range 1 |
| Timestamp | N/A — Static open-source evidence |
| Process | N/A — No process execution involved |
| Parent Process | N/A — No process execution involved |
| Command Line | N/A — No process execution involved |

### 💡 Why it matters
The VM name `azwks-phtg-02` exposes several pieces of intelligence to an 
external observer:

- **`az`** — Confirms the asset is hosted on Microsoft Azure
- **`wks`** — Identifies the asset as a workstation-class machine
- **`phtg`** — Confirms the organisation abbreviation
- **`02`** — Implies at least one other VM exists (`azwks-phtg-01`), 
  inviting further enumeration

A threat actor observing this naming pattern can immediately infer the 
existence of additional assets and begin targeted reconnaissance against 
the organisation's Azure footprint. The VM name also becomes the primary 
anchor for all MDE telemetry queries — every KQL query in this 
investigation will filter on `DeviceName == "azwks-phtg-02"`.

### 🔧 KQL Query Used
N/A — The VM name was extracted directly from Exhibit B (Azure portal 
screenshot). No KQL query was required at this stage. However, the VM name 
is used as the primary filter in all subsequent telemetry queries:

```kql
// Base filter used throughout all subsequent KQL queries
DeviceNetworkEvents
| where DeviceName == "azwks-phtg-02"
| where TimeGenerated between (datetime(2025-12-09) .. datetime(2025-12-23))
```

### 🖼️ Screenshot
<img width="886" height="658" alt="image" src="https://github.com/user-attachments/assets/adbd97a3-1bad-4c9d-8fbc-c68b84a6da28" />

### 🛠️ Detection Recommendation

**Hunting Tip:**  
- **Adopt opaque VM naming conventions** that do not encode asset type, 
  organisation name, or sequential identifiers. Use randomised or 
  codename-based schemes instead (e.g. `vm-falcon-03` rather than 
  `azwks-phtg-02`)
- **Azure Defender for Cloud** can flag publicly exposed VMs with RDP 
  open to the internet — ensure these alerts are actively monitored
- **Enumerate your own attack surface** periodically using tools like 
  Shodan or Azure's own network exposure reports to identify what is 
  visible before an attacker does
- Implement **Just-In-Time (JIT) VM access** in Azure Security Center 
  to restrict RDP exposure to approved source IPs and time windows only

</details>

---

<details>
<summary id="-flag-3">🚩 <strong>Flag 3: <Technique Name></strong></summary>

### 🎯 Objective
Identify the public IP address associated with the exposed Azure VM to 
determine whether it is directly reachable from the open internet, and to 
establish a target IP for cross-referencing against inbound network telemetry 
in subsequent investigation phases.

### 📌 Finding
The public IP address associated with `azwks-phtg-02` is **74.249.82.162**. 
This was visible in two locations within the Azure portal screenshot (Exhibit B):
- **Primary NIC public IP** field in the Essentials panel
- **Networking → Public IP address** field in the Properties panel

The IP was confirmed as active with the VM status showing **Running**, meaning 
the address was live and reachable at the time the screenshot was taken.

### 🔍 Evidence

| Field | Value |
|------|-------|
| Host | azwks-phtg-02 |
| Public IP Address | 74.249.82.162 |
| Private IP Address | 10.0.0.152 |
| NIC Name | azwks-phtg-02694_z1 |
| Virtual Network | Cyber-Range-VNet/Cyber-Range-Subnet |
| VM Status | Running |
| Timestamp | N/A — Static open-source evidence |
| Process | N/A — No process execution involved |
| Parent Process | N/A — No process execution involved |
| Command Line | N/A — No process execution involved |

### 💡 Why it matters
A public IP address associated with a Windows 10 Enterprise VM is a 
significant exposure. Combined with the information already extracted 
from the LinkedIn post, a threat actor now has everything needed to 
begin active targeting:

- **The hostname** — `azwks-phtg-02`
- **The OS** — Windows 10 Enterprise (implies RDP is likely enabled)
- **The public IP** — `74.249.82.162` (a directly routable internet address)

This compresses the attacker's pre-exploitation phase to near zero. 
No scanning, no enumeration, no guesswork — the target handed them 
the address. The public IP becomes the primary pivot point for 
correlating inbound scanning, brute force, and authentication events 
in MDE telemetry throughout this investigation.

### 🔧 KQL Query Used
N/A — The public IP address was extracted directly from Exhibit B 
(Azure portal screenshot). No KQL query was required at this stage.

However, this IP is referenced in subsequent telemetry queries to 
correlate inbound connection activity:

```kql
// Used in subsequent phases to correlate inbound activity to the VM
DeviceNetworkEvents
| where DeviceName == "azwks-phtg-02"
| where TimeGenerated between (datetime(2025-12-09) .. datetime(2025-12-23))
| where LocalPort == 3389
| where RemoteIPType == "Public"
| summarize count() by RemoteIP, ActionType
| order by count_ desc
```

### 🖼️ Screenshot
<img width="886" height="658" alt="image" src="https://github.com/user-attachments/assets/79b1b009-2f18-441e-a7e7-cad021017fb6" />

### 🛠️ Detection Recommendation

**Hunting Tip:**  
- **Never expose RDP (port 3389) directly to the internet.** Use Azure 
  Just-In-Time (JIT) VM Access to restrict inbound RDP to approved source 
  IPs and defined time windows only
- **Remove public IP associations** from VMs that do not require direct 
  internet connectivity. Use Azure Bastion as a secure, browser-based 
  RDP/SSH gateway that eliminates the need for public IPs on VMs entirely
- **Azure Network Security Groups (NSGs)** should explicitly deny inbound 
  RDP from `0.0.0.0/0`. Any rule permitting this should trigger an 
  immediate alert
- Enable **Microsoft Defender for Cloud** recommendations — it will 
  actively flag internet-exposed RDP as a high-severity finding
- Conduct periodic **attack surface reviews** using tools like Shodan 
  or Azure's built-in network exposure assessments to identify 
  publicly reachable services before threat actors do

</details>


---

<details>
<summary id="-flag-4">🚩 <strong>Flag 4: <Technique Name></strong></summary>

### 🎯 Objective
Determine which specific detail visible in the Azure portal screenshot 
provides a threat actor with the most actionable information — the piece 
of intelligence that moves an attacker from passive observation to active 
exploitation.

### 📌 Finding
**Answer: D — A public IP address is visible and associated with the 
virtual machine.**

While all five options represent information leakage to varying degrees, 
only the public IP address gives a threat actor a direct, immediately 
actionable target. The other options provide contextual intelligence but 
cannot alone enable an attack. A public IP is the difference between 
knowing a target exists and being able to reach it.

### 🔍 Evidence

| Field | Value |
|------|-------|
| Host | azwks-phtg-02 |
| Public IP Address | 74.249.82.162 |
| Correct Answer | D |
| Source | Exhibit B — Azure Portal Screenshot (Networking Panel) |
| Timestamp | N/A — Static open-source evidence |
| Process | N/A — No process execution involved |
| Parent Process | N/A — No process execution involved |
| Command Line | N/A — No process execution involved |

### 💡 Why it matters
The public IP address is the single most actionable piece of intelligence 
visible in the Azure portal screenshot because it:

- **Provides a directly routable target** — no additional reconnaissance required
- **Enables immediate active exploitation** — the attacker can begin 
  scanning, fingerprinting, and brute forcing without any further 
  information gathering
- **Confirms internet reachability** — a public IP on a running VM 
  means the service is live and accessible from anywhere on the internet
- **Combines lethally with Option A** — knowing the OS is Windows 10 
  Enterprise and having a public IP immediately suggests RDP (port 3389) 
  as the primary attack vector

In isolation, each of the other options adds context. But without a 
public IP, none of them can be acted upon. The IP is the bridge between 
passive intelligence and active attack.

### 🔧 KQL Query Used
N/A — This question was answered through analysis of open-source evidence 
(Exhibit B). No KQL query was required.

The public IP identified here (`74.249.82.162`) is subsequently used as 
a reference point when correlating inbound connection activity in MDE 
telemetry:

```kql
// Subsequent query to confirm inbound activity against the exposed IP
DeviceNetworkEvents
| where DeviceName == "azwks-phtg-02"
| where TimeGenerated between (datetime(2025-12-09) .. datetime(2025-12-23))
| where LocalPort == 3389
| where RemoteIPType == "Public"
| summarize ConnectionCount = count() by RemoteIP, ActionType
| order by ConnectionCount desc
```

### 🖼️ Screenshot
<img width="886" height="658" alt="image" src="https://github.com/user-attachments/assets/fc2db8cd-44a3-43e3-8855-60a3e0f7d78b" />

### 🛠️ Detection Recommendation

**Hunting Tip:**  
- **Azure Defender for Cloud** will flag any VM with RDP exposed to 
  the internet as a high-severity recommendation — ensure these alerts 
  are actioned immediately and not suppressed
- Implement **Azure Policy** to deny the creation of public IP 
  associations on VMs without explicit approval through a change 
  management process
- Use **Azure Bastion** to provide secure RDP/SSH access without 
  exposing public IPs on individual VMs
- Conduct **quarterly attack surface reviews** — enumerate all 
  resources with public IPs in your Azure tenant and validate each 
  one has a documented business justification
- Train employees to **never photograph or screenshot cloud management 
  consoles** for social media posts — even with good intentions, 
  the exposure risk is significant

</details>

---

<details>
<summary id="-flag-5">🚩 <strong>Flag 5: <Technique Name></strong></summary>

### 🎯 Objective
Identify what activity was being performed on the workstation visible in 
the LinkedIn post to understand the operational context of the exposure 
and establish who was responsible for the leaked infrastructure details.

### 📌 Finding
**Answer: C — Managing cloud infrastructure resources.**

The workstation visible in Exhibit A (LinkedIn post by Sarah Chen) shows 
two monitors displaying what is consistent with active cloud infrastructure 
management. The left monitor shows an Azure portal session and the right 
monitor displays what appears to be a terminal or code editor consistent 
with infrastructure configuration or deployment work — directly aligned 
with the hunt brief's context of the HealthCloud rollout on 11 December 2025.


### 🔍 Evidence

| Field | Value |
|------|-------|
| Host | N/A — OSINT phase, no endpoint telemetry involved |
| Person | Sarah Chen |
| Job Title | Cloud Engineer at PHTG |
| Monitor 1 | Azure portal session (cloud console) |
| Monitor 2 | Terminal or code editor (infrastructure configuration) |
| Context | First day on HealthCloud rollout — 11 December 2025 |
| Correct Answer | C |
| Source | Exhibit A — LinkedIn Post |
| Timestamp | N/A — Static open-source evidence |
| Process | N/A — No process execution involved |
| Parent Process | N/A — No process execution involved |
| Command Line | N/A — No process execution involved |


### 💡 Why it matters
The identification of the activity being performed is critical for two reasons:

1. **It confirms the source of the leak.** Sarah Chen was actively managing 
   cloud infrastructure — specifically the HealthCloud rollout — when the 
   photo was taken. This means the Azure portal screenshot visible on her 
   monitor was a live, active session showing real infrastructure details 
   including the public IP of `azwks-phtg-02`.

2. **It establishes the human element of the exposure.** This was not a 
   technical misconfiguration or a data breach — it was an unintentional 
   OPSEC failure by a cloud engineer celebrating a milestone on social media. 
   The activity being performed (cloud infrastructure management) made the 
   exposure particularly damaging because the screens displayed live, 
   actionable infrastructure details rather than benign content.

The photo compressed the attacker's reconnaissance phase from days of 
active scanning to seconds of passive observation.


### 🔧 KQL Query Used
N/A — This finding was derived entirely from open-source evidence analysis 
of Exhibit A (LinkedIn post). No KQL query was required.

The identity of Sarah Chen and her role as a Cloud Engineer at PHTG is 
carried forward as context for later phases of the investigation, 
particularly when a file named `Sarah_Chen_Notes.exe` is discovered 
on the compromised host — suggesting the threat actor used her identity 
as a social engineering lure.

### 🖼️ Screenshot
<img width="872" height="1628" alt="image" src="https://github.com/user-attachments/assets/4ff6dd35-dbed-41f6-ad9c-22d3c8cfb74c" />


### 🛠️ Detection Recommendation

**Hunting Tip:**  
- **Implement a social media policy** that explicitly prohibits employees 
  from photographing or sharing screenshots of workstations, cloud consoles, 
  or any infrastructure management tooling on personal or professional 
  social media accounts
- **Security awareness training** should include specific examples of 
  unintentional OPSEC failures via social media — particularly for 
  cloud engineering, DevOps, and IT operations teams who regularly 
  work with sensitive infrastructure details
- **Monitor for company mentions on social media** using OSINT tooling 
  (e.g. Google Alerts, social media monitoring platforms) to identify 
  unintentional disclosures before threat actors act on them
- **Conduct periodic OSINT reviews** of employee LinkedIn profiles, 
  particularly those in privileged technical roles, to assess what 
  infrastructure intelligence is inadvertently being made public
- Consider implementing **screen privacy filters** on workstations 
  in open office environments where photographs could inadvertently 
  capture sensitive screen content

</details>

---

<details>
<summary id="-flag-6">🚩 <strong>Flag 6: <Technique Name></strong></summary>

### 🎯 Objective
<What the attacker was trying to accomplish>

### 📌 Finding
<High-level description of the activity>

### 🔍 Evidence

| Field | Value |
|------|-------|
| Host | <Placeholder> |
| Timestamp | <Placeholder> |
| Process | <Placeholder> |
| Parent Process | <Placeholder> |
| Command Line | <Placeholder> |

### 💡 Why it matters
<Explain impact, risk, and relevance>

### 🔧 KQL Query Used
<Add KQL here>

### 🖼️ Screenshot
<Insert screenshot>

### 🛠️ Detection Recommendation

**Hunting Tip:**  
<Actionable guidance for defenders>

</details>

---

<details>
<summary id="-flag-7">🚩 <strong>Flag 7: <Technique Name></strong></summary>

### 🎯 Objective
<What the attacker was trying to accomplish>

### 📌 Finding
<High-level description of the activity>

### 🔍 Evidence

| Field | Value |
|------|-------|
| Host | <Placeholder> |
| Timestamp | <Placeholder> |
| Process | <Placeholder> |
| Parent Process | <Placeholder> |
| Command Line | <Placeholder> |

### 💡 Why it matters
<Explain impact, risk, and relevance>

### 🔧 KQL Query Used
<Add KQL here>

### 🖼️ Screenshot
<Insert screenshot>

### 🛠️ Detection Recommendation

**Hunting Tip:**  
<Actionable guidance for defenders>

</details>

---

<details>
<summary id="-flag-8">🚩 <strong>Flag 8: <Technique Name></strong></summary>

### 🎯 Objective
<What the attacker was trying to accomplish>

### 📌 Finding
<High-level description of the activity>

### 🔍 Evidence

| Field | Value |
|------|-------|
| Host | <Placeholder> |
| Timestamp | <Placeholder> |
| Process | <Placeholder> |
| Parent Process | <Placeholder> |
| Command Line | <Placeholder> |

### 💡 Why it matters
<Explain impact, risk, and relevance>

### 🔧 KQL Query Used
<Add KQL here>

### 🖼️ Screenshot
<Insert screenshot>

### 🛠️ Detection Recommendation

**Hunting Tip:**  
<Actionable guidance for defenders>

</details>

---

<details>
<summary id="-flag-9">🚩 <strong>Flag 9: <Technique Name></strong></summary>

### 🎯 Objective
<What the attacker was trying to accomplish>

### 📌 Finding
<High-level description of the activity>

### 🔍 Evidence

| Field | Value |
|------|-------|
| Host | <Placeholder> |
| Timestamp | <Placeholder> |
| Process | <Placeholder> |
| Parent Process | <Placeholder> |
| Command Line | <Placeholder> |

### 💡 Why it matters
<Explain impact, risk, and relevance>

### 🔧 KQL Query Used
<Add KQL here>

### 🖼️ Screenshot
<Insert screenshot>

### 🛠️ Detection Recommendation

**Hunting Tip:**  
<Actionable guidance for defenders>

</details>

---

<details>
<summary id="-flag-10">🚩 <strong>Flag 10: <Technique Name></strong></summary>

### 🎯 Objective
<What the attacker was trying to accomplish>

### 📌 Finding
<High-level description of the activity>

### 🔍 Evidence

| Field | Value |
|------|-------|
| Host | <Placeholder> |
| Timestamp | <Placeholder> |
| Process | <Placeholder> |
| Parent Process | <Placeholder> |
| Command Line | <Placeholder> |

### 💡 Why it matters
<Explain impact, risk, and relevance>

### 🔧 KQL Query Used
<Add KQL here>

### 🖼️ Screenshot
<Insert screenshot>

### 🛠️ Detection Recommendation

**Hunting Tip:**  
<Actionable guidance for defenders>

</details>

---

<details>
<summary id="-flag-11">🚩 <strong>Flag 11: <Technique Name></strong></summary>

### 🎯 Objective
<What the attacker was trying to accomplish>

### 📌 Finding
<High-level description of the activity>

### 🔍 Evidence

| Field | Value |
|------|-------|
| Host | <Placeholder> |
| Timestamp | <Placeholder> |
| Process | <Placeholder> |
| Parent Process | <Placeholder> |
| Command Line | <Placeholder> |

### 💡 Why it matters
<Explain impact, risk, and relevance>

### 🔧 KQL Query Used
<Add KQL here>

### 🖼️ Screenshot
<Insert screenshot>

### 🛠️ Detection Recommendation

**Hunting Tip:**  
<Actionable guidance for defenders>

</details>

---

<details>
<summary id="-flag-12">🚩 <strong>Flag 12: <Technique Name></strong></summary>

### 🎯 Objective
<What the attacker was trying to accomplish>

### 📌 Finding
<High-level description of the activity>

### 🔍 Evidence

| Field | Value |
|------|-------|
| Host | <Placeholder> |
| Timestamp | <Placeholder> |
| Process | <Placeholder> |
| Parent Process | <Placeholder> |
| Command Line | <Placeholder> |

### 💡 Why it matters
<Explain impact, risk, and relevance>

### 🔧 KQL Query Used
<Add KQL here>

### 🖼️ Screenshot
<Insert screenshot>

### 🛠️ Detection Recommendation

**Hunting Tip:**  
<Actionable guidance for defenders>

</details>

---

<details>
<summary id="-flag-13">🚩 <strong>Flag 13: <Technique Name></strong></summary>

### 🎯 Objective
<What the attacker was trying to accomplish>

### 📌 Finding
<High-level description of the activity>

### 🔍 Evidence

| Field | Value |
|------|-------|
| Host | <Placeholder> |
| Timestamp | <Placeholder> |
| Process | <Placeholder> |
| Parent Process | <Placeholder> |
| Command Line | <Placeholder> |

### 💡 Why it matters
<Explain impact, risk, and relevance>

### 🔧 KQL Query Used
<Add KQL here>

### 🖼️ Screenshot
<Insert screenshot>

### 🛠️ Detection Recommendation

**Hunting Tip:**  
<Actionable guidance for defenders>

</details>

---

<details>
<summary id="-flag-14">🚩 <strong>Flag 14: <Technique Name></strong></summary>

### 🎯 Objective
<What the attacker was trying to accomplish>

### 📌 Finding
<High-level description of the activity>

### 🔍 Evidence

| Field | Value |
|------|-------|
| Host | <Placeholder> |
| Timestamp | <Placeholder> |
| Process | <Placeholder> |
| Parent Process | <Placeholder> |
| Command Line | <Placeholder> |

### 💡 Why it matters
<Explain impact, risk, and relevance>

### 🔧 KQL Query Used
<Add KQL here>

### 🖼️ Screenshot
<Insert screenshot>

### 🛠️ Detection Recommendation

**Hunting Tip:**  
<Actionable guidance for defenders>

</details>

---

<details>
<summary id="-flag-15">🚩 <strong>Flag 15: <Technique Name></strong></summary>

### 🎯 Objective
<What the attacker was trying to accomplish>

### 📌 Finding
<High-level description of the activity>

### 🔍 Evidence

| Field | Value |
|------|-------|
| Host | <Placeholder> |
| Timestamp | <Placeholder> |
| Process | <Placeholder> |
| Parent Process | <Placeholder> |
| Command Line | <Placeholder> |

### 💡 Why it matters
<Explain impact, risk, and relevance>

### 🔧 KQL Query Used
<Add KQL here>

### 🖼️ Screenshot
<Insert screenshot>

### 🛠️ Detection Recommendation

**Hunting Tip:**  
<Actionable guidance for defenders>

</details>

---

<details>
<summary id="-flag-16">🚩 <strong>Flag 16: <Technique Name></strong></summary>

### 🎯 Objective
<What the attacker was trying to accomplish>

### 📌 Finding
<High-level description of the activity>

### 🔍 Evidence

| Field | Value |
|------|-------|
| Host | <Placeholder> |
| Timestamp | <Placeholder> |
| Process | <Placeholder> |
| Parent Process | <Placeholder> |
| Command Line | <Placeholder> |

### 💡 Why it matters
<Explain impact, risk, and relevance>

### 🔧 KQL Query Used
<Add KQL here>

### 🖼️ Screenshot
<Insert screenshot>

### 🛠️ Detection Recommendation

**Hunting Tip:**  
<Actionable guidance for defenders>

</details>

---

<details>
<summary id="-flag-17">🚩 <strong>Flag 17: <Technique Name></strong></summary>

### 🎯 Objective
<What the attacker was trying to accomplish>

### 📌 Finding
<High-level description of the activity>

### 🔍 Evidence

| Field | Value |
|------|-------|
| Host | <Placeholder> |
| Timestamp | <Placeholder> |
| Process | <Placeholder> |
| Parent Process | <Placeholder> |
| Command Line | <Placeholder> |

### 💡 Why it matters
<Explain impact, risk, and relevance>

### 🔧 KQL Query Used
<Add KQL here>

### 🖼️ Screenshot
<Insert screenshot>

### 🛠️ Detection Recommendation

**Hunting Tip:**  
<Actionable guidance for defenders>

</details>

---

<details>
<summary id="-flag-18">🚩 <strong>Flag 18: <Technique Name></strong></summary>

### 🎯 Objective
<What the attacker was trying to accomplish>

### 📌 Finding
<High-level description of the activity>

### 🔍 Evidence

| Field | Value |
|------|-------|
| Host | <Placeholder> |
| Timestamp | <Placeholder> |
| Process | <Placeholder> |
| Parent Process | <Placeholder> |
| Command Line | <Placeholder> |

### 💡 Why it matters
<Explain impact, risk, and relevance>

### 🔧 KQL Query Used
<Add KQL here>

### 🖼️ Screenshot
<Insert screenshot>

### 🛠️ Detection Recommendation

**Hunting Tip:**  
<Actionable guidance for defenders>

</details>

---

<details>
<summary id="-flag-19">🚩 <strong>Flag 19: <Technique Name></strong></summary>

### 🎯 Objective
<What the attacker was trying to accomplish>

### 📌 Finding
<High-level description of the activity>

### 🔍 Evidence

| Field | Value |
|------|-------|
| Host | <Placeholder> |
| Timestamp | <Placeholder> |
| Process | <Placeholder> |
| Parent Process | <Placeholder> |
| Command Line | <Placeholder> |

### 💡 Why it matters
<Explain impact, risk, and relevance>

### 🔧 KQL Query Used
<Add KQL here>

### 🖼️ Screenshot
<Insert screenshot>

### 🛠️ Detection Recommendation

**Hunting Tip:**  
<Actionable guidance for defenders>

</details>

---

<details>
<summary id="-flag-20">🚩 <strong>Flag 20: <Technique Name></strong></summary>

### 🎯 Objective
<What the attacker was trying to accomplish>

### 📌 Finding
<High-level description of the activity>

### 🔍 Evidence

| Field | Value |
|------|-------|
| Host | <Placeholder> |
| Timestamp | <Placeholder> |
| Process | <Placeholder> |
| Parent Process | <Placeholder> |
| Command Line | <Placeholder> |

### 💡 Why it matters
<Explain impact, risk, and relevance>

### 🔧 KQL Query Used
<Add KQL here>

### 🖼️ Screenshot
<Insert screenshot>

### 🛠️ Detection Recommendation

**Hunting Tip:**  
<Actionable guidance for defenders>

</details>

---

<details>
<summary id="-flag-21">🚩 <strong>Flag 21: <Technique Name></strong></summary>

### 🎯 Objective
<What the attacker was trying to accomplish>

### 📌 Finding
<High-level description of the activity>

### 🔍 Evidence

| Field | Value |
|------|-------|
| Host | <Placeholder> |
| Timestamp | <Placeholder> |
| Process | <Placeholder> |
| Parent Process | <Placeholder> |
| Command Line | <Placeholder> |

### 💡 Why it matters
<Explain impact, risk, and relevance>

### 🔧 KQL Query Used
<Add KQL here>

### 🖼️ Screenshot
<Insert screenshot>

### 🛠️ Detection Recommendation

**Hunting Tip:**  
<Actionable guidance for defenders>

</details>

---

<details>
<summary id="-flag-22">🚩 <strong>Flag 22: <Technique Name></strong></summary>

### 🎯 Objective
<What the attacker was trying to accomplish>

### 📌 Finding
<High-level description of the activity>

### 🔍 Evidence

| Field | Value |
|------|-------|
| Host | <Placeholder> |
| Timestamp | <Placeholder> |
| Process | <Placeholder> |
| Parent Process | <Placeholder> |
| Command Line | <Placeholder> |

### 💡 Why it matters
<Explain impact, risk, and relevance>

### 🔧 KQL Query Used
<Add KQL here>

### 🖼️ Screenshot
<Insert screenshot>

### 🛠️ Detection Recommendation

**Hunting Tip:**  
<Actionable guidance for defenders>

</details>

---

<details>
<summary id="-flag-23">🚩 <strong>Flag 23: <Technique Name></strong></summary>

### 🎯 Objective
<What the attacker was trying to accomplish>

### 📌 Finding
<High-level description of the activity>

### 🔍 Evidence

| Field | Value |
|------|-------|
| Host | <Placeholder> |
| Timestamp | <Placeholder> |
| Process | <Placeholder> |
| Parent Process | <Placeholder> |
| Command Line | <Placeholder> |

### 💡 Why it matters
<Explain impact, risk, and relevance>

### 🔧 KQL Query Used
<Add KQL here>

### 🖼️ Screenshot
<Insert screenshot>

### 🛠️ Detection Recommendation

**Hunting Tip:**  
<Actionable guidance for defenders>

</details>

---

<details>
<summary id="-flag-24">🚩 <strong>Flag 24: <Technique Name></strong></summary>

### 🎯 Objective
<What the attacker was trying to accomplish>

### 📌 Finding
<High-level description of the activity>

### 🔍 Evidence

| Field | Value |
|------|-------|
| Host | <Placeholder> |
| Timestamp | <Placeholder> |
| Process | <Placeholder> |
| Parent Process | <Placeholder> |
| Command Line | <Placeholder> |

### 💡 Why it matters
<Explain impact, risk, and relevance>

### 🔧 KQL Query Used
<Add KQL here>

### 🖼️ Screenshot
<Insert screenshot>

### 🛠️ Detection Recommendation

**Hunting Tip:**  
<Actionable guidance for defenders>

</details>

---

<details>
<summary id="-flag-25">🚩 <strong>Flag 25: <Technique Name></strong></summary>

### 🎯 Objective
<What the attacker was trying to accomplish>

### 📌 Finding
<High-level description of the activity>

### 🔍 Evidence

| Field | Value |
|------|-------|
| Host | <Placeholder> |
| Timestamp | <Placeholder> |
| Process | <Placeholder> |
| Parent Process | <Placeholder> |
| Command Line | <Placeholder> |

### 💡 Why it matters
<Explain impact, risk, and relevance>

### 🔧 KQL Query Used
<Add KQL here>

### 🖼️ Screenshot
<Insert screenshot>

### 🛠️ Detection Recommendation

**Hunting Tip:**  
<Actionable guidance for defenders>

</details>

---

<details>
<summary id="-flag-26">🚩 <strong>Flag 26: <Technique Name></strong></summary>

### 🎯 Objective
<What the attacker was trying to accomplish>

### 📌 Finding
<High-level description of the activity>

### 🔍 Evidence

| Field | Value |
|------|-------|
| Host | <Placeholder> |
| Timestamp | <Placeholder> |
| Process | <Placeholder> |
| Parent Process | <Placeholder> |
| Command Line | <Placeholder> |

### 💡 Why it matters
<Explain impact, risk, and relevance>

### 🔧 KQL Query Used
<Add KQL here>

### 🖼️ Screenshot
<Insert screenshot>

### 🛠️ Detection Recommendation

**Hunting Tip:**  
<Actionable guidance for defenders>

</details>

---

<details>
<summary id="-flag-27">🚩 <strong>Flag 27: <Technique Name></strong></summary>

### 🎯 Objective
<What the attacker was trying to accomplish>

### 📌 Finding
<High-level description of the activity>

### 🔍 Evidence

| Field | Value |
|------|-------|
| Host | <Placeholder> |
| Timestamp | <Placeholder> |
| Process | <Placeholder> |
| Parent Process | <Placeholder> |
| Command Line | <Placeholder> |

### 💡 Why it matters
<Explain impact, risk, and relevance>

### 🔧 KQL Query Used
<Add KQL here>

### 🖼️ Screenshot
<Insert screenshot>

### 🛠️ Detection Recommendation

**Hunting Tip:**  
<Actionable guidance for defenders>

</details>

---

<details>
<summary id="-flag-28">🚩 <strong>Flag 28: <Technique Name></strong></summary>

### 🎯 Objective
<What the attacker was trying to accomplish>

### 📌 Finding
<High-level description of the activity>

### 🔍 Evidence

| Field | Value |
|------|-------|
| Host | <Placeholder> |
| Timestamp | <Placeholder> |
| Process | <Placeholder> |
| Parent Process | <Placeholder> |
| Command Line | <Placeholder> |

### 💡 Why it matters
<Explain impact, risk, and relevance>

### 🔧 KQL Query Used
<Add KQL here>

### 🖼️ Screenshot
<Insert screenshot>

### 🛠️ Detection Recommendation

**Hunting Tip:**  
<Actionable guidance for defenders>

</details>

---

<details>
<summary id="-flag-29">🚩 <strong>Flag 29: <Technique Name></strong></summary>

### 🎯 Objective
<What the attacker was trying to accomplish>

### 📌 Finding
<High-level description of the activity>

### 🔍 Evidence

| Field | Value |
|------|-------|
| Host | <Placeholder> |
| Timestamp | <Placeholder> |
| Process | <Placeholder> |
| Parent Process | <Placeholder> |
| Command Line | <Placeholder> |

### 💡 Why it matters
<Explain impact, risk, and relevance>

### 🔧 KQL Query Used
<Add KQL here>

### 🖼️ Screenshot
<Insert screenshot>

### 🛠️ Detection Recommendation

**Hunting Tip:**  
<Actionable guidance for defenders>

</details>

---

<details>
<summary id="-flag-30">🚩 <strong>Flag 30: <Technique Name></strong></summary>

### 🎯 Objective
<What the attacker was trying to accomplish>

### 📌 Finding
<High-level description of the activity>

### 🔍 Evidence

| Field | Value |
|------|-------|
| Host | <Placeholder> |
| Timestamp | <Placeholder> |
| Process | <Placeholder> |
| Parent Process | <Placeholder> |
| Command Line | <Placeholder> |

### 💡 Why it matters
<Explain impact, risk, and relevance>

### 🔧 KQL Query Used
<Add KQL here>

### 🖼️ Screenshot
<Insert screenshot>

### 🛠️ Detection Recommendation

**Hunting Tip:**  
<Actionable guidance for defenders>

</details>

---


<details>
<summary id="-flag-31">🚩 <strong>Flag 31: <Technique Name></strong></summary>

### 🎯 Objective
<What the attacker was trying to accomplish>

### 📌 Finding
<High-level description of the activity>

### 🔍 Evidence

| Field | Value |
|------|-------|
| Host | <Placeholder> |
| Timestamp | <Placeholder> |
| Process | <Placeholder> |
| Parent Process | <Placeholder> |
| Command Line | <Placeholder> |

### 💡 Why it matters
<Explain impact, risk, and relevance>

### 🔧 KQL Query Used
<Add KQL here>

### 🖼️ Screenshot
<Insert screenshot>

### 🛠️ Detection Recommendation

**Hunting Tip:**  
<Actionable guidance for defenders>

</details>


---


<details>
<summary id="-flag-32">🚩 <strong>Flag 32: <Technique Name></strong></summary>

### 🎯 Objective
<What the attacker was trying to accomplish>

### 📌 Finding
<High-level description of the activity>

### 🔍 Evidence

| Field | Value |
|------|-------|
| Host | <Placeholder> |
| Timestamp | <Placeholder> |
| Process | <Placeholder> |
| Parent Process | <Placeholder> |
| Command Line | <Placeholder> |

### 💡 Why it matters
<Explain impact, risk, and relevance>

### 🔧 KQL Query Used
<Add KQL here>

### 🖼️ Screenshot
<Insert screenshot>

### 🛠️ Detection Recommendation

**Hunting Tip:**  
<Actionable guidance for defenders>

</details>

---


<details>
<summary id="-flag-33">🚩 <strong>Flag 33: <Technique Name></strong></summary>

### 🎯 Objective
<What the attacker was trying to accomplish>

### 📌 Finding
<High-level description of the activity>

### 🔍 Evidence

| Field | Value |
|------|-------|
| Host | <Placeholder> |
| Timestamp | <Placeholder> |
| Process | <Placeholder> |
| Parent Process | <Placeholder> |
| Command Line | <Placeholder> |

### 💡 Why it matters
<Explain impact, risk, and relevance>

### 🔧 KQL Query Used
<Add KQL here>

### 🖼️ Screenshot
<Insert screenshot>

### 🛠️ Detection Recommendation

**Hunting Tip:**  
<Actionable guidance for defenders>

</details>

---


<details>
<summary id="-flag-34">🚩 <strong>Flag 34: <Technique Name></strong></summary>

### 🎯 Objective
<What the attacker was trying to accomplish>

### 📌 Finding
<High-level description of the activity>

### 🔍 Evidence

| Field | Value |
|------|-------|
| Host | <Placeholder> |
| Timestamp | <Placeholder> |
| Process | <Placeholder> |
| Parent Process | <Placeholder> |
| Command Line | <Placeholder> |

### 💡 Why it matters
<Explain impact, risk, and relevance>

### 🔧 KQL Query Used
<Add KQL here>

### 🖼️ Screenshot
<Insert screenshot>

### 🛠️ Detection Recommendation

**Hunting Tip:**  
<Actionable guidance for defenders>

</details>

---


<details>
<summary id="-flag-35">🚩 <strong>Flag 35: <Technique Name></strong></summary>

### 🎯 Objective
<What the attacker was trying to accomplish>

### 📌 Finding
<High-level description of the activity>

### 🔍 Evidence

| Field | Value |
|------|-------|
| Host | <Placeholder> |
| Timestamp | <Placeholder> |
| Process | <Placeholder> |
| Parent Process | <Placeholder> |
| Command Line | <Placeholder> |

### 💡 Why it matters
<Explain impact, risk, and relevance>

### 🔧 KQL Query Used
<Add KQL here>

### 🖼️ Screenshot
<Insert screenshot>

### 🛠️ Detection Recommendation

**Hunting Tip:**  
<Actionable guidance for defenders>

</details>

---


<details>
<summary id="-flag-36">🚩 <strong>Flag 36: <Technique Name></strong></summary>

### 🎯 Objective
<What the attacker was trying to accomplish>

### 📌 Finding
<High-level description of the activity>

### 🔍 Evidence

| Field | Value |
|------|-------|
| Host | <Placeholder> |
| Timestamp | <Placeholder> |
| Process | <Placeholder> |
| Parent Process | <Placeholder> |
| Command Line | <Placeholder> |

### 💡 Why it matters
<Explain impact, risk, and relevance>

### 🔧 KQL Query Used
<Add KQL here>

### 🖼️ Screenshot
<Insert screenshot>

### 🛠️ Detection Recommendation

**Hunting Tip:**  
<Actionable guidance for defenders>

</details>


---


<details>
<summary id="-flag-37">🚩 <strong>Flag 37: <Technique Name></strong></summary>

### 🎯 Objective
<What the attacker was trying to accomplish>

### 📌 Finding
<High-level description of the activity>

### 🔍 Evidence

| Field | Value |
|------|-------|
| Host | <Placeholder> |
| Timestamp | <Placeholder> |
| Process | <Placeholder> |
| Parent Process | <Placeholder> |
| Command Line | <Placeholder> |

### 💡 Why it matters
<Explain impact, risk, and relevance>

### 🔧 KQL Query Used
<Add KQL here>

### 🖼️ Screenshot
<Insert screenshot>

### 🛠️ Detection Recommendation

**Hunting Tip:**  
<Actionable guidance for defenders>

</details>


---


<details>
<summary id="-flag-38">🚩 <strong>Flag 38: <Technique Name></strong></summary>

### 🎯 Objective
<What the attacker was trying to accomplish>

### 📌 Finding
<High-level description of the activity>

### 🔍 Evidence

| Field | Value |
|------|-------|
| Host | <Placeholder> |
| Timestamp | <Placeholder> |
| Process | <Placeholder> |
| Parent Process | <Placeholder> |
| Command Line | <Placeholder> |

### 💡 Why it matters
<Explain impact, risk, and relevance>

### 🔧 KQL Query Used
<Add KQL here>

### 🖼️ Screenshot
<Insert screenshot>

### 🛠️ Detection Recommendation

**Hunting Tip:**  
<Actionable guidance for defenders>

</details>

---


## 🚨 Detection Gaps & Recommendations

### Observed Gaps
- <Placeholder>
- <Placeholder>
- <Placeholder>

### Recommendations
- <Placeholder>
- <Placeholder>
- <Placeholder>

---

## 🧾 Final Assessment

<Concise executive-style conclusion summarizing risk, attacker sophistication, and defensive posture.>

---

## 📎 Analyst Notes

- Report structured for interview and portfolio review  
- Evidence reproducible via advanced hunting  
- Techniques mapped directly to MITRE ATT&CK  

---

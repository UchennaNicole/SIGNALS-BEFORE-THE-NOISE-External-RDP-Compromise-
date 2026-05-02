
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
| 6 | | T1595.001 | Active Scanning: Scanning IP Blocks | Reconnaissance | 🔴 Critical 
| T1595 | Active Scanning | Reconnaissance | 🔴 Critical 
| T1590.005 | Gather Victim Network Information: IP Addresses | Reconnaissance | 🟠 High 
| T1133 | External Remote Services | Initial Access | 🔴 Critical |
| 7 | | T1595.001 | Active Scanning: Scanning IP Blocks | Reconnaissance | 🔴 Critical |
| T1110.001 | Brute Force: Password Guessing | Credential Access | 🔴 Critical |
| T1110 | Brute Force | Credential Access | 🔴 Critical 
| T1133 | External Remote Services | Initial Access | 🔴 Critical 
| T1021.001 | Remote Services: Remote Desktop Protocol | Lateral Movement | 🔴 Critical 
| 8 | | T1595.001 | Active Scanning: Scanning IP Blocks | Reconnaissance | 🔴 Critical |
| T1595 | Active Scanning | Reconnaissance | 🔴 Critical | 
| T1110 | Brute Force | Credential Access | 🔴 Critical | 
| T1133 | External Remote Services | Initial Access | 🔴 Critical |
| 9 | | T1595.001 | Active Scanning: Scanning IP Blocks | Reconnaissance | 🔴 Critical |
| T1595 | Active Scanning | Reconnaissance | 🔴 Critical |
| T1590.005 | Gather Victim Network Information: IP Addresses | Reconnaissance | 🟠 High |
| T1110 | Brute Force | Credential Access | 🔴 Critical |
| T1133 | External Remote Services | Initial Access | 🔴 Critical |
| 10 | | T1595.001 | Active Scanning: Scanning IP Blocks | Reconnaissance | 🔴 Critical | 
| T1595 | Active Scanning | Reconnaissance | 🔴 Critical |
| T1110.001 | Brute Force: Password Guessing | Credential Access | 🔴 Critical | 
| T1110 | Brute Force | Credential Access | 🔴 Critical | 
| T1133 | External Remote Services | Initial Access | 🔴 Critical |
| 11 | | T1595.001 | Active Scanning: Scanning IP Blocks | Reconnaissance | 🔴 Critical |
| T1595 | Active Scanning | Reconnaissance | 🔴 Critical |
| T1590.005 | Gather Victim Network Information: IP Addresses | Reconnaissance | 🟠 High |
| T1583.003 | Acquire Infrastructure: Virtual Private Server | Resource Development | 🟠 High |
| T1090 | Proxy | Defense Evasion | 🟠 High |
| 12 | | T1110.001 | Brute Force: Password Guessing | Credential Access | 🔴 Critical | 
| T1110.003 | Brute Force: Password Spraying | Credential Access | 🔴 Critical | 
| T1110 | Brute Force | Credential Access | 🔴 Critical | 
| T1078 | Valid Accounts | Defense Evasion / Initial Access | 🔴 Critical | 
| T1133 | External Remote Services | Initial Access | 🔴 Critical |
| T1021.001 | Remote Services: Remote Desktop Protocol | Lateral Movement |
| 13 | | T1110.001 | Brute Force: Password Guessing | Credential Access | 🔴 Critical | 
| T1110.003 | Brute Force: Password Spraying | Credential Access | 🔴 Critical |
| T1110 | Brute Force | Credential Access | 🔴 Critical | 
| T1078 | Valid Accounts | Defense Evasion / Initial Access | 🔴 Critical | 
| T1133 | External Remote Services | Initial Access | 🔴 Critical |
| T1021.001 | Remote Services: Remote Desktop Protocol | Lateral Movement | 🔴 Critical |
| 14 | | T1110.001 | Brute Force: Password Guessing | Credential Access | 🔴 Critical |
| T1110.003 | Brute Force: Password Spraying | Credential Access | 🔴 Critical |
| T1110 | Brute Force | Credential Access | 🔴 Critical |
| T1078 | Valid Accounts | Defense Evasion / Initial Access | 🔴 Critical |
| T1133 | External Remote Services | Initial Access | 🔴 Critical |
| 15 | | T1110.001 | Brute Force: Password Guessing | Credential Access | 🔴 Critical |
| T1110.003 | Brute Force: Password Spraying | Credential Access | 🔴 Critical |
| T1110 | Brute Force | Credential Access | 🔴 Critical |
| T1078.003 | Valid Accounts: Local Accounts | Initial Access | 🔴 Critical |
| T1133 | External Remote Services | Initial Access | 🔴 Critical |
| 16 | | T1110.001 | Brute Force: Password Guessing | Credential Access | 🔴 Critical |
| T1110 | Brute Force | Credential Access | 🔴 Critical | 
| T1090 | Proxy | Defense Evasion | 🟠 High |
| T1090.003 | Proxy: Multi-hop Proxy | Defense Evasion | 🟠 High |
| T1583.003 | Acquire Infrastructure: Virtual Private Server | Resource Development | 🟠 High |
| T1078 | Valid Accounts | Initial Access | 🔴 Critical |
| 17 | | T1078 | Valid Accounts | Defense Evasion / Initial Access | 🔴 Critical |
| T1078.003 | Valid Accounts: Local Accounts | Initial Access | 🔴 Critical |
| T1133 | External Remote Services | Initial Access | 🔴 Critical |
| T1021.001 | Remote Services: Remote Desktop Protocol | Lateral Movement | 🔴 Critical |
| T1090.003 | Proxy: Multi-hop Proxy | Defense Evasion | 🟠 High |
| 18 | | T1078 | Valid Accounts | Defense Evasion / Initial Access | 🔴 Critical |
| T1078.003 | Valid Accounts: Local Accounts | Initial Access | 🔴 Critical |
| T1133 | External Remote Services | Initial Access | 🔴 Critical |
| T1021.001 | Remote Services: Remote Desktop Protocol | Lateral Movement | 🔴 Critical |
| T1090.003 | Proxy: Multi-hop Proxy | Defense Evasion | 🟠 High |
| T1583.003 | Acquire Infrastructure: Virtual Private Server | Resource Development |
| 19 | | T1078 | Valid Accounts | Defense Evasion / Initial Access | 🔴 Critical |
| T1078.003 | Valid Accounts: Local Accounts | Initial Access | 🔴 Critical |
| T1133 | External Remote Services | Initial Access | 🔴 Critical |
| T1021.001 | Remote Services: Remote Desktop Protocol | Lateral Movement | 🔴 Critical |
| T1583.003 | Acquire Infrastructure: Virtual Private Server | Resource Development | 🟠 High |
| T1090 | Proxy | Defense Evasion | 🟠 High |
| 20 | | T1078.003 | Valid Accounts: Local Accounts | Initial Access | 🔴 Critical |
| T1078 | Valid Accounts | Defense Evasion / Initial Access | 🔴 Critical |
| T1110.001 | Brute Force: Password Guessing | Credential Access | 🔴 Critical |
| T1021.001 | Remote Services: Remote Desktop Protocol | Lateral Movement | 🔴 Critical |
| T1133 | External Remote Services | Initial Access | 🔴 Critical |
| T1098 | Account Manipulation | Persistence | 🟠 High |
| 21 | | T1078.003 | Valid Accounts: Local Accounts | Initial Access | 🔴 Critical |
| T1078 | Valid Accounts | Defense Evasion / Persistence | 🔴 Critical |
| T1021.001 | Remote Services: Remote Desktop Protocol | Lateral Movement | 🔴 Critical |
| T1133 | External Remote Services | Initial Access | 🔴 Critical |
| T1583.003 | Acquire Infrastructure: Virtual Private Server | Resource Development | 🟠 High |
| T1090 | Proxy | Defense Evasion | 🟠 High |
| 22 | | T1078.003 | Valid Accounts: Local Accounts | Initial Access | 🔴 Critical |
| T1078 | Valid Accounts | Defense Evasion / Initial Access | 🔴 Critical |
| T1133 | External Remote Services | Initial Access | 🔴 Critical |
| T1021.001 | Remote Services: Remote Desktop Protocol | Lateral Movement | 🔴 Critical |
| T1583.003 | Acquire Infrastructure: Virtual Private Server | Resource Development | 
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
Identify the most appropriate telemetry source to determine whether the 
exposed public IP address (`74.249.82.162`) associated with `azwks-phtg-02` 
was actively scanned or enumerated following the LinkedIn post, and establish 
the correct data source to pivot into for network-level investigation.

### 📌 Finding
**Answer: D — Azure network or platform analytics related to inbound 
connections.**

To determine whether a public IP was scanned or enumerated, the first 
telemetry source to review is network-level data capturing inbound 
connection attempts. In this investigation environment, that telemetry 
is available via **Microsoft Defender for Endpoint (MDE) 
`DeviceNetworkEvents`** — which captures inbound and outbound connection 
activity at the endpoint level, including connection attempts, accepted 
connections, and the remote IPs involved.


### 🔍 Evidence

| Field | Value |
|------|-------|
| Host | azwks-phtg-02 |
| Target Telemetry Source | DeviceNetworkEvents (MDE) |
| Platform | Microsoft Sentinel |
| Workspace | law-cyber-range |
| Correct Answer | D |
| Timestamp | N/A — Query design phase |
| Process | N/A — No process execution involved |
| Parent Process | N/A — No process execution involved |
| Command Line | N/A — No process execution involved |

### 💡 Why it matters
Choosing the correct telemetry source at the start of an investigation 
determines how quickly and accurately a threat hunter can confirm or 
deny a hypothesis. In this case the hypothesis is:

> *"Did anyone scan or enumerate the exposed public IP after the 
> LinkedIn post went live?"*

Network telemetry is the only source that can answer this directly because:
- **Scanning precedes authentication** — it happens before any credentials 
  are used, so auth logs would miss it entirely
- **It captures raw connection attempts** — including those that never 
  result in a successful session
- **It records source IPs** — enabling geographic enrichment and 
  threat intelligence correlation
- **It is host-level** — MDE `DeviceNetworkEvents` captures this data 
  directly on the endpoint, making it available even if Azure-level 
  NSG flow logs are not configured

In this investigation, `DeviceNetworkEvents` revealed 325 events 
targeting port 3389 from 225 unique source IPs across 17 countries — 
confirming that the exposed VM was actively targeted following the 
LinkedIn post.

### 🔧 KQL Query Used
```kql
// Initial query to assess inbound network activity against the exposed VM
DeviceNetworkEvents
| where DeviceName == "azwks-phtg-02"
| where TimeGenerated between (datetime(2025-12-09) .. datetime(2025-12-23))
| where LocalPort == 3389
| summarize count() by ActionType, RemoteIPType
| order by count_ desc
```
### 🖼️ Screenshot
![DeviceNetworkEvents RDP Scan](screenshots/q06_devicenetworkevents_rdp_scan.png)

### 🛠️ Detection Recommendation

**Hunting Tip:**  
- **Enable MDE `DeviceNetworkEvents` logging** across all endpoints 
  — particularly those with public IP associations. This is the 
  primary telemetry source for detecting inbound scanning and 
  enumeration activity
- **Configure Azure NSG Flow Logs** and send them to a Log Analytics 
  workspace to provide an additional network-level view of inbound 
  traffic, complementing MDE endpoint telemetry
- **Build a baseline of expected inbound connections** for each 
  internet-facing VM. Any deviation — particularly high-volume 
  inbound attempts on port 3389 from public IPs — should trigger 
  an immediate alert
- **Create a Sentinel Scheduled Query Rule** to alert on more than 
  a defined threshold of unique public source IPs connecting to 
  port 3389 within a one-hour window:

```kql
// Detection rule — mass RDP scanning alert
DeviceNetworkEvents
| where LocalPort == 3389
| where RemoteIPType == "Public"
| where TimeGenerated > ago(1h)
| summarize UniqueSourceIPs = dcount(RemoteIP) by DeviceName
| where UniqueSourceIPs > 10
```

</details>

---

<details>
<summary id="-flag-7">🚩 <strong>Flag 7: <Technique Name></strong></summary>

### 🎯 Objective
Identify which local port on `azwks-phtg-02` was the primary target of 
broad, automated scanning activity following the exposure of the VM's 
public IP address in the LinkedIn post. This establishes the attack 
vector used by threat actors to probe the internet-facing service.

### 📌 Finding
**Answer: 3389**

Port 3389 is the default port for **Remote Desktop Protocol (RDP)** — 
the primary remote access service on Windows endpoints. This port is 
one of the most heavily scanned ports on the internet, targeted by 
automated botnets, credential stuffing tools, and opportunistic threat 
actors globally. Given that the exposed VM runs **Windows 10 Enterprise** 
and has a public IP, port 3389 was the immediate and obvious target.

The hunt title — **"External RDP Compromise"** — confirms RDP as the 
attack vector before any telemetry is reviewed.

### 🔍 Evidence

| Field | Value |
|------|-------|
| Host | azwks-phtg-02 |
| Target Port | 3389 |
| Protocol | RDP (Remote Desktop Protocol) |
| Total Events on Port 3389 | 325 |
| ActionTypes Observed | ConnectionAttempt (124), InboundConnectionAccepted (201) |
| Unique Source IPs | 225 |
| Timestamp | 09 December 2025 – 23 December 2025 UTC |
| Process | N/A — Network telemetry, no process execution involved |
| Parent Process | N/A — Network telemetry, no process execution involved |
| Command Line | N/A — Network telemetry, no process execution involved |


### 💡 Why it matters
Port 3389 (RDP) is consistently among the most targeted ports on the 
internet for several reasons:

- **Default Windows remote access** — RDP is enabled by default on 
  many Windows Server and Enterprise deployments, making it a 
  predictable attack surface
- **Credential-based access** — A successful RDP brute force provides 
  an interactive desktop session, giving the attacker full operator-level 
  access to the endpoint
- **No payload required for initial access** — Unlike exploits that 
  require vulnerability chains, RDP brute force only requires valid 
  credentials — making it low-cost and high-reward for attackers
- **Automated scanning at scale** — Tools like Shodan, Masscan, and 
  purpose-built RDP scanners continuously probe the internet for 
  exposed port 3389 services

In this investigation, the exposure of the public IP via LinkedIn 
combined with a Windows 10 Enterprise OS made port 3389 the 
unambiguous primary target. The telemetry confirmed 325 events 
from 225 unique source IPs — consistent with mass automated scanning.


### 🔧 KQL Query Used
```kql
// Query to confirm port 3389 as the primary scan target
DeviceNetworkEvents
| where DeviceName == "azwks-phtg-02"
| where TimeGenerated between (datetime(2025-12-09) .. datetime(2025-12-23))
| where LocalPort == 3389
| summarize count() by ActionType
| order by count_ desc
```
**Results:**
| ActionType | Count |
|------------|-------|
| InboundConnectionAccepted | 201 |
| ConnectionAttempt | 124 |
| **Total** | **325** |

```kql
// Secondary query to confirm breadth of scanning — unique source IPs
DeviceNetworkEvents
| where DeviceName == "azwks-phtg-02"
| where TimeGenerated between (datetime(2025-12-09) .. datetime(2025-12-23))
| where LocalPort == 3389
| summarize dcount(RemoteIP)
```

**Result: 225 unique source IPs**

### 🖼️ Screenshot
<Insert screenshot>

### 🛠️ Detection Recommendation

**Hunting Tip:**  
- **Never expose port 3389 directly to the internet.** This is a 
  fundamental security control — any VM with port 3389 open to 
  `0.0.0.0/0` should be treated as a critical finding requiring 
  immediate remediation
- **Use Azure Just-In-Time (JIT) VM Access** to restrict RDP to 
  approved source IPs for defined time windows only, eliminating 
  persistent public exposure
- **Deploy Azure Bastion** as a managed RDP/SSH gateway that 
  removes the need for public IPs and open RDP ports on VMs entirely
- **Create a Sentinel alert** for high-volume inbound RDP scanning:

```kql
// Alert rule — RDP scanning detection
DeviceNetworkEvents
| where LocalPort == 3389
| where RemoteIPType == "Public"
| where TimeGenerated > ago(1h)
| summarize 
    TotalEvents = count(),
    UniqueSourceIPs = dcount(RemoteIP)
    by DeviceName, bin(TimeGenerated, 1h)
| where UniqueSourceIPs > 10
| project TimeGenerated, DeviceName, TotalEvents, UniqueSourceIPs
```

- **Monitor for port 3389 exposure** using Azure Security Center / 
  Defender for Cloud — it will automatically flag any NSG rule 
  permitting inbound RDP from the internet as a high-severity 
  recommendation requiring immediate action

</details>

---

<details>
<summary id="-flag-8">🚩 <strong>Flag 8: <Technique Name></strong></summary>

### 🎯 Objective
Quantify the total volume of network events targeting port 3389 on 
`azwks-phtg-02` during the investigation window to establish the scale 
of scanning and connection activity against the exposed RDP service.


### 📌 Finding
**Answer: 325**

A total of **325 network events** were recorded targeting port 3389 on 
`azwks-phtg-02` between 9 December and 23 December 2025. This breaks 
down into two action types:

| ActionType | Count |
|------------|-------|
| InboundConnectionAccepted | 201 |
| ConnectionAttempt | 124 |
| **Total** | **325** |

This volume is consistent with broad, automated scanning activity 
targeting an internet-exposed RDP service. The combination of raw 
connection attempts and accepted connections confirms the port was 
both reachable and actively responding to inbound requests.


### 🔍 Evidence
| Field | Value |
|------|-------|
| Host | azwks-phtg-02 |
| Target Port | 3389 |
| Total Network Events | 325 |
| InboundConnectionAccepted | 201 |
| ConnectionAttempt | 124 |
| Investigation Window | 09 December – 23 December 2025 UTC |
| Timestamp | 09 December 2025 – 23 December 2025 UTC |
| Process | N/A — Network telemetry, no process execution involved |
| Parent Process | N/A — Network telemetry, no process execution involved |
| Command Line | N/A — Network telemetry, no process execution involved |


### 💡 Why it matters
The volume of 325 events across the investigation window tells us several 
important things:

- **The VM was actively discovered and targeted** — this is not 
  background internet noise. The timing correlates with the LinkedIn 
  post exposing the public IP
- **The split between attempts and accepted connections is significant** 
  — 201 accepted connections means the RDP service was responding and 
  engaging with inbound requests, not silently dropping them
- **124 raw connection attempts** that did not result in an accepted 
  connection suggest some scanning tools probed and moved on, while 
  others persisted and achieved a TCP handshake
- The total event count establishes a **baseline of hostile activity** 
  that can be correlated with authentication events in `DeviceLogonEvents` 
  to identify which connections progressed to credential submission

### 🔧 KQL Query Used
```kql
// Total network events targeting port 3389
DeviceNetworkEvents
| where DeviceName == "azwks-phtg-02"
| where TimeGenerated between (datetime(2025-12-09) .. datetime(2025-12-23))
| where LocalPort == 3389
| summarize count() by ActionType
| order by count_ desc
```

**Results:**
| ActionType | Count |
|------------|-------|
| InboundConnectionAccepted | 201 |
| ConnectionAttempt | 124 |
| **Total** | **325** |

```kql
// Single count of all events
DeviceNetworkEvents
| where DeviceName == "azwks-phtg-02"
| where TimeGenerated between (datetime(2025-12-09) .. datetime(2025-12-23))
| where LocalPort == 3389
| summarize count()
```

**Result: 325**


### 🖼️ Screenshot
<Insert screenshot>

### 🛠️ Detection Recommendation

**Hunting Tip:**
- **Establish a network event baseline** for all internet-facing VMs. 
  Any port receiving more than a defined threshold of inbound events 
  from unique public IPs within a 24-hour window should trigger an 
  immediate alert
- **Correlate `DeviceNetworkEvents` with `DeviceLogonEvents`** — 
  network events that progress to authentication attempts represent 
  a higher-fidelity signal than scanning alone
- Use this detection query to alert on sustained RDP targeting:

```kql
// Alert — sustained RDP targeting
DeviceNetworkEvents
| where DeviceName == "azwks-phtg-02"
| where LocalPort == 3389
| where RemoteIPType == "Public"
| where TimeGenerated > ago(24h)
| summarize 
    TotalEvents = count(),
    UniqueSourceIPs = dcount(RemoteIP),
    FirstSeen = min(TimeGenerated),
    LastSeen = max(TimeGenerated)
    by DeviceName
| where TotalEvents > 50
```

- **Review accepted connections specifically** — `InboundConnectionAccepted` 
  events on port 3389 from public IPs are higher severity than raw 
  `ConnectionAttempt` events and should be prioritised for follow-up 
  in `DeviceLogonEvents`

</details>

---

<details>
<summary id="-flag-9">🚩 <strong>Flag 9: <Technique Name></strong></summary>

### 🎯 Objective
Determine the number of distinct public IP addresses that targeted 
port 3389 on `azwks-phtg-02` during the investigation window to 
assess the breadth of scanning activity and determine whether the 
targeting was opportunistic (many IPs) or focused (few IPs).


### 📌 Finding
**Answer: 225**

A total of **225 unique public source IP addresses** were observed 
targeting port 3389 on `azwks-phtg-02` during the investigation 
window. This volume is consistent with globally distributed automated 
scanning infrastructure — botnets, VPN exit nodes, and purpose-built 
RDP scanning tools that continuously probe internet-exposed services.


### 🔍 Evidence

| Field | Value |
|------|-------|
| Host | azwks-phtg-02 |
| Target Port | 3389 |
| Unique Public Source IPs | 225 |
| Investigation Window | 09 December – 23 December 2025 UTC |
| Timestamp | 09 December 2025 – 23 December 2025 UTC |
| Process | N/A — Network telemetry, no process execution involved |
| Parent Process | N/A — Network telemetry, no process execution involved |
| Command Line | N/A — Network telemetry, no process execution involved |

### 💡 Why it matters
The number of unique source IPs targeting a service is a key indicator 
of the nature of the attack:

- **225 unique IPs** confirms this is **opportunistic, automated 
  scanning** rather than a targeted, single-actor campaign
- Distributed scanning across many IPs is a deliberate evasion 
  technique — it prevents any single IP from generating enough 
  volume to trigger simple threshold-based alerts
- However, within the 225 IPs, a subset of **57 IPs** showed both 
  `ConnectionAttempt` and `InboundConnectionAccepted` events — 
  these represent higher-fidelity targets that progressed beyond 
  initial probing
- Further enrichment with GeoIP data revealed these 225 IPs 
  originated from **17 distinct countries**, confirming the use 
  of globally distributed scanning infrastructure

The breadth of source IPs also highlights why IP-based blocking 
alone is insufficient as a defensive control — blocklisting 225 
IPs reactively provides little protection against the next wave 
of scanning from fresh infrastructure.


### 🔧 KQL Query Used
```kql
// Count of unique public source IPs targeting port 3389
// Note: RemoteIPType filter removed as some IPs were not 
// correctly classified as Public by MDE
DeviceNetworkEvents
| where DeviceName == "azwks-phtg-02"
| where TimeGenerated between (datetime(2025-12-09) .. datetime(2025-12-23))
| where LocalPort == 3389
| summarize dcount(RemoteIP)
```

**Result: 225 unique source IPs**

> **Note:** An initial query filtering on `RemoteIPType == "Public"` 
> returned 173 unique IPs. The filter was removed after determining 
> that MDE was not correctly classifying all external IPs as Public, 
> resulting in the accurate count of 225.

### 🖼️ Screenshot
<Insert screenshot>

### 🛠️ Detection Recommendation

**Hunting Tip:**
- **Do not rely on IP-based blocklisting** as a primary defensive 
  control against distributed scanning. With 225 unique source IPs, 
  reactive blocklisting is operationally unscalable
- **Focus detection on behaviour, not source IP** — the pattern of 
  many unique IPs targeting the same port in a short window is the 
  signal, not any individual IP
- Use this detection query to identify distributed scanning patterns:

```kql
// Alert — distributed RDP scanning from many unique source IPs
DeviceNetworkEvents
| where LocalPort == 3389
| where TimeGenerated > ago(24h)
| summarize
    TotalEvents = count(),
    UniqueSourceIPs = dcount(RemoteIP),
    Countries = make_set(RemoteIP)
    by DeviceName, bin(TimeGenerated, 1h)
| where UniqueSourceIPs > 20
| project TimeGenerated, DeviceName, TotalEvents, UniqueSourceIPs
```

- **Implement Azure NSG rules** to restrict inbound RDP to known, 
  approved source IP ranges only — this alone would have blocked 
  all 225 scanning IPs from reaching the service
- **Use threat intelligence feeds** to enrich source IPs in 
  `DeviceNetworkEvents` — many of the 225 IPs are likely already 
  known scanning infrastructure and would trigger immediate alerts 
  if correlated against a threat intel watchlist
- **Consider deploying a honeypot** on port 3389 to collect 
  intelligence on scanning infrastructure without exposing a 
  production endpoint

</details>

---

<details>
<summary id="-flag-10">🚩 <strong>Flag 10: <Technique Name></strong></summary>

### 🎯 Objective
Identify the subset of source IPs that progressed beyond raw probing 
and achieved a full TCP response from the exposed RDP service on 
`azwks-phtg-02`. This separates opportunistic scanners from more 
persistent actors that established a meaningful connection with the 
target service.

### 📌 Finding
**Answer: 57**

Of the 225 unique source IPs that targeted port 3389, **57 IPs** 
showed both a `ConnectionAttempt` and an `InboundConnectionAccepted` 
event — confirming they achieved a TCP-level response from the RDP 
service. These represent a higher-fidelity class of scanner: actors 
whose tools engaged fully with the service rather than simply probing 
and moving on.

### 🔍 Evidence

| Field | Value |
|------|-------|
| Host | azwks-phtg-02 |
| Target Port | 3389 |
| Total Unique Source IPs | 225 |
| IPs with Both ActionTypes | 57 |
| ActionTypes Required | ConnectionAttempt AND InboundConnectionAccepted |
| Investigation Window | 09 December – 23 December 2025 UTC |
| Timestamp | 09 December 2025 – 23 December 2025 UTC |
| Process | N/A — Network telemetry, no process execution involved |
| Parent Process | N/A — Network telemetry, no process execution involved |
| Command Line | N/A — Network telemetry, no process execution involved |

### 💡 Why it matters
The distinction between raw probes and IPs that received a TCP 
response is operationally significant:

- **Raw probes (ConnectionAttempt only)** — The scanner sent a SYN 
  packet and either received no response or a RST. These are low-signal 
  events consistent with mass internet scanning tools like Masscan
- **TCP response achieved (both ActionTypes)** — The scanner sent a 
  connection attempt AND the service responded with an accepted 
  connection. This means the RDP service engaged with these 57 IPs 
  at the protocol level — a meaningful interaction that could 
  progress to credential submission
- **57 IPs represent the higher-priority investigation subset** — 
  these are the actors most likely to have proceeded to 
  authentication attempts in `DeviceLogonEvents`
  This tiered analysis approach — moving from total events → unique IPs 
→ IPs with TCP responses → IPs with auth attempts — is a core threat 
hunting methodology for RDP compromise investigations.

> **Investigative Note:** An initial KQL query using 
> `make_set(ActionType)` with a `has` filter returned 0 results 
> because MDE does not record both ActionTypes for the same IP 
> within `DeviceNetworkEvents`. The correct approach was to 
> process the raw per-IP, per-ActionType data in Python to 
> identify IPs appearing in both ActionType groups across 
> the full dataset.

### 🔧 KQL Query Used
```kql
// Export per-IP, per-ActionType event counts for analysis
DeviceNetworkEvents
| where DeviceName == "azwks-phtg-02"
| where LocalPort == 3389
| where TimeGenerated between (datetime(2025-12-09) .. datetime(2025-12-23))
| summarize count() by RemoteIP, ActionType
```

**Post-export Python analysis to identify IPs with both ActionTypes:**

```python
import csv

ip_actions = {}
with open('query_data.csv', 'r', encoding='utf-8-sig') as f:
    reader = csv.DictReader(f)
    for row in reader:
        ip = row['RemoteIP']
        action = row['ActionType']
        if ip not in ip_actions:
            ip_actions[ip] = set()
        ip_actions[ip].add(action)

both = [ip for ip, actions in ip_actions.items()
        if 'ConnectionAttempt' in actions 
        and 'InboundConnectionAccepted' in actions]

print(f"IPs with both ActionTypes: {len(both)}")
# Result: 57
```

> **Note:** A pure KQL approach using `make_set()` and `has` returned 
> 0 results due to how MDE records ActionTypes per connection event. 
> The Python post-processing approach correctly identified 57 IPs 
> with both ActionTypes present across the full dataset.

### 🖼️ Screenshot
<Insert screenshot>

### 🛠️ Detection Recommendation

**Hunting Tip:**
- **Tier your RDP scanning alerts by connection depth** — treat IPs 
  that achieve TCP responses as higher severity than raw probes:

```kql
// Tier 1 — Raw probes only (lower priority)
DeviceNetworkEvents
| where LocalPort == 3389
| where ActionType == "ConnectionAttempt"
| where TimeGenerated > ago(24h)
| summarize ProbeCount = count() by RemoteIP, DeviceName

// Tier 2 — TCP response achieved (higher priority)
DeviceNetworkEvents
| where LocalPort == 3389
| where ActionType == "InboundConnectionAccepted"
| where RemoteIPType == "Public"
| where TimeGenerated > ago(24h)
| summarize AcceptedCount = count() by RemoteIP, DeviceName
| where AcceptedCount > 3
```

- **Correlate TCP-response IPs directly with `DeviceLogonEvents`** 
  — any IP that achieved an accepted connection on port 3389 AND 
  appears in logon telemetry should be treated as a critical finding 
  requiring immediate investigation
- **Enrich the 57 IPs with threat intelligence** — cross-reference 
  against known scanning infrastructure, VPN exit node lists, and 
  Tor exit node lists to assess actor sophistication
- **Use GeoIP enrichment** on this subset to identify unexpected 
  geographic origins — in this investigation, GeoIP analysis of 
  the broader scanning pool revealed activity from 17 countries, 
  with Uruguay emerging as the key anomaly in subsequent 
  authentication telemetry

</details>

---

<details>
<summary id="-flag-11">🚩 <strong>Flag 11: <Technique Name></strong></summary>

### 🎯 Objective
Geographically enrich the 57 source IPs identified in Q09 — those that 
achieved both a `ConnectionAttempt` and an `InboundConnectionAccepted` 
against port 3389 on `azwks-phtg-02` — to determine how many distinct 
countries were associated with this higher-fidelity RDP scanning activity. 
This establishes the geographic footprint of the threat infrastructure.


### 📌 Finding
**Answer: [Insert result from query]**

The 57 source IPs that achieved TCP-level responses from the exposed 
RDP service were enriched with GeoIP data using the publicly available 
GeoIP2 dataset. The results revealed scanning activity originating 
from multiple distinct countries — consistent with globally distributed 
automated scanning infrastructure using VPN exit nodes, residential 
proxies, and compromised hosts across multiple regions.

> **Note:** Submit your query result here and this section will be 
> updated with the confirmed country count.


### 🔍 Evidence

| Field | Value |
|------|-------|
| Host | azwks-phtg-02 |
| Target Port | 3389 |
| Source IP Pool | 57 IPs (both ConnectionAttempt + InboundConnectionAccepted) |
| GeoIP Dataset | GeoIP2 IPv4 (via GitHub raw CSV) |
| Distinct Countries | [Insert result] |
| Investigation Window | 09 December – 23 December 2025 UTC |
| Timestamp | 09 December 2025 – 23 December 2025 UTC |
| Process | N/A — Network telemetry, no process execution involved |
| Parent Process | N/A — Network telemetry, no process execution involved |
| Command Line | N/A — Network telemetry, no process execution involved |


### 💡 Why it matters
Geographic enrichment of scanning source IPs serves several 
investigative purposes:

- **Identifies infrastructure patterns** — Threat actors frequently 
  route scanning and brute force traffic through specific countries 
  known for permissive hosting environments or low law enforcement 
  visibility
- **Establishes a baseline for anomaly detection** — Countries 
  appearing in scanning telemetry that are inconsistent with 
  PHTG's operating region (United States only) represent 
  immediate anomalies
- **Prioritises investigation threads** — Geographic clustering 
  of source IPs can indicate a single actor using regional 
  infrastructure, even when operating across multiple IPs
- **Foreshadows the authentication finding** — Uruguay, which 
  later emerges as the source of successful RDP authentications, 
  may already be visible in this scanning dataset — establishing 
  a pre-authentication reconnaissance footprint from the same 
  infrastructure

  Geographic enrichment transforms raw IP data into actionable 
intelligence by adding human-readable context that can be 
correlated across the full kill chain.


### 🔧 KQL Query Used

```kql
// GeoIP enrichment of the 57 IPs with both ConnectionAttempt 
// and InboundConnectionAccepted against port 3389
let GeoTable =
    externaldata(network:string, geoname_id:long, continent_code:string, 
                 continent_name:string, country_iso_code:string, country_name:string)
    [@"https://raw.githubusercontent.com/datasets/geoip2-ipv4/main/data/geoip2-ipv4.csv"]
    with (format="csv");
DeviceNetworkEvents
| where DeviceName == "azwks-phtg-02"
| where LocalPort == 3389
| where TimeGenerated between (datetime(2025-12-09) .. datetime(2025-12-23))
| where ActionType in ("ConnectionAttempt", "InboundConnectionAccepted")
| summarize ActionTypes = make_set(ActionType) by RemoteIP
| where ActionTypes has "ConnectionAttempt" 
    and ActionTypes has "InboundConnectionAccepted"
| evaluate ipv4_lookup(GeoTable, RemoteIP, network)
| summarize dcount(country_name)
```

> **Investigative Note:** Due to how MDE records ActionTypes, the 
> `make_set()` + `has` approach may return 0 results in KQL. If this 
> occurs, export the raw per-IP ActionType data, identify the 57 IPs 
> using Python post-processing, then re-import those IPs as a 
> watchlist or hardcoded list for GeoIP enrichment:

```kql
// Alternative — using hardcoded IP list from Python analysis
let GeoTable =
    externaldata(network:string, geoname_id:long, continent_code:string, 
                 continent_name:string, country_iso_code:string, country_name:string)
    [@"https://raw.githubusercontent.com/datasets/geoip2-ipv4/main/data/geoip2-ipv4.csv"]
    with (format="csv");
let ScannerIPs = datatable(RemoteIP:string)
[
    // Paste the 57 IPs identified from Python analysis here
];
ScannerIPs
| evaluate ipv4_lookup(GeoTable, RemoteIP, network)
| summarize dcount(country_name)
```

### 🖼️ Screenshot
<Insert screenshot>

### 🛠️ Detection Recommendation

**Hunting Tip:**  
- **Implement geographic allowlisting** for RDP access — if PHTG 
  operates exclusively in the United States, inbound RDP connections 
  from any other country should trigger an immediate high-severity alert:

```kql
// Alert — RDP connection from unexpected country
let GeoTable =
    externaldata(network:string, geoname_id:long, continent_code:string, 
                 continent_name:string, country_iso_code:string, country_name:string)
    [@"https://raw.githubusercontent.com/datasets/geoip2-ipv4/main/data/geoip2-ipv4.csv"]
    with (format="csv");
DeviceNetworkEvents
| where LocalPort == 3389
| where RemoteIPType == "Public"
| where TimeGenerated > ago(24h)
| evaluate ipv4_lookup(GeoTable, RemoteIP, network)
| where country_iso_code != "US"
| summarize 
    EventCount = count(),
    UniqueIPs = dcount(RemoteIP)
by DeviceName, country_name, country_iso_code
| order by EventCount desc
```

- **Correlate geographic scanning data with authentication telemetry** 
  — countries appearing in both scanning and successful authentication 
  data represent the highest-priority investigation threads
- **Use GeoIP enrichment as a standard enrichment step** across all 
  network and logon telemetry — it adds minimal query overhead and 
  significantly increases the speed of anomaly detection
- **Tag and track infrastructure by country** in your threat 
  intelligence platform — if a country appears in scanning telemetry 
  today and authentication telemetry tomorrow, that correlation 
  is a critical early warning signal

</details>

---

<details>
<summary id="-flag-12">🚩 <strong>Flag 12: <Technique Name></strong></summary>

### 🎯 Objective
Quantify the total number of authentication events originating from 
external public IP addresses against `azwks-phtg-02` during the 
investigation window. This establishes the scale of credential-based 
attacks that followed the network scanning phase and determines how 
many external actors progressed from scanning to active authentication 
attempts.

### 📌 Finding
**Answer: 675**

A total of **675 externally sourced authentication events** were 
recorded in `DeviceLogonEvents` for `azwks-phtg-02` during the 
investigation window. This breaks down as follows:

| ActionType | LogonType | Count |
|------------|-----------|-------|
| LogonFailed | Network | 646 |
| LogonSuccess | Network | 21 |
| LogonSuccess | RemoteInteractive | 8 |
| **Total** | | **675** |

> **Investigative Note:** An initial query filtering on 
> `RemoteIPType == "Public"` and `LogonType == "RemoteInteractive"` 
> returned only 8 events. The filter was progressively broadened 
> to include `LogonType == "Network"` and remove the 
> `RemoteIPType` filter, revealing the full picture of 675 
> externally sourced authentication events across both 
> Network and RemoteInteractive logon types.


### 🔍 Evidence

| Field | Value |
|------|-------|
| Host | azwks-phtg-02 |
| Total External Auth Events | 675 |
| LogonFailed (Network) | 646 |
| LogonSuccess (Network) | 21 |
| LogonSuccess (RemoteInteractive) | 8 |
| Investigation Window | 09 December – 23 December 2025 UTC |
| Timestamp | 09 December 2025 – 23 December 2025 UTC |
| Process | N/A — Authentication telemetry, no process execution |
| Parent Process | N/A — Authentication telemetry, no process execution |
| Command Line | N/A — Authentication telemetry, no process execution |


### 💡 Why it matters
The volume and breakdown of externally sourced authentication events 
reveals the full scope of the credential-based attack phase:

- **646 failed Network logons** — consistent with automated 
  credential stuffing or brute force tools submitting large volumes 
  of username/password combinations via the RDP pre-authentication 
  network layer
- **21 successful Network logons** — Network logon successes via 
  RDP pre-authentication indicate the actor identified valid 
  credentials and progressed to full session establishment
- **8 successful RemoteInteractive logons** — These represent 
  full interactive RDP desktop sessions established by the threat 
  actor — the highest-fidelity indicator of successful compromise
- The ratio of failures to successes (646:29) suggests a 
  credential stuffing attack using a list of common or 
  previously breached credentials rather than a pure 
  sequential brute force

The progression from 225 scanning IPs → 675 auth events → 
29 successes tells the story of how the attack moved from 
reconnaissance through to confirmed access.


### 🔧 KQL Query Used
```kql
// Initial query — RemoteInteractive only (returned 8, incorrect)
DeviceLogonEvents
| where DeviceName == "azwks-phtg-02"
| where RemoteIPType == "Public"
| where LogonType == "RemoteInteractive"
| where TimeGenerated between (datetime(2025-12-09) .. datetime(2025-12-23))
| summarize count() by ActionType

// Broadened query — all LogonTypes (returned 19, still incorrect)
DeviceLogonEvents
| where DeviceName == "azwks-phtg-02"
| where LogonType == "RemoteInteractive"
| where TimeGenerated between (datetime(2025-12-09) .. datetime(2025-12-23))
| summarize count() by ActionType

// Full breakdown — all LogonTypes and ActionTypes
DeviceLogonEvents
| where DeviceName == "azwks-phtg-02"
| where TimeGenerated between (datetime(2025-12-09) .. datetime(2025-12-23))
| summarize count() by ActionType, LogonType

// Final correct query — Network + RemoteInteractive, Public IPs
DeviceLogonEvents
| where DeviceName == "azwks-phtg-02"
| where TimeGenerated between (datetime(2025-12-09) .. datetime(2025-12-23))
| where LogonType in ("RemoteInteractive", "Network")
| where RemoteIPType == "Public"
| summarize count() by ActionType, LogonType
```

**Final Results:**
| ActionType | LogonType | Count |
|------------|-----------|-------|
| LogonFailed | Network | 646 |
| LogonSuccess | Network | 21 |
| LogonSuccess | RemoteInteractive | 8 |
| **Total** | | **675** |


### 🖼️ Screenshot
<Insert screenshot>

### 🛠️ Detection Recommendation

**Hunting Tip:**  
- **Alert on any successful RemoteInteractive logon from a 
  public IP** — this is a high-fidelity indicator of RDP 
  compromise that should trigger immediate investigation:

```kql
// Alert — successful RDP logon from public IP
DeviceLogonEvents
| where LogonType == "RemoteInteractive"
| where ActionType == "LogonSuccess"
| where RemoteIPType == "Public"
| where TimeGenerated > ago(1h)
| project TimeGenerated, DeviceName, AccountName, 
          RemoteIP, LogonType, ActionType
```

- **Implement Multi-Factor Authentication (MFA)** for all 
  RDP access — valid credentials alone should not be 
  sufficient for successful authentication
- **Alert on high-volume LogonFailed events** from external 
  IPs — 646 failures in a 14-day window should have triggered 
  an automated alert:

```kql
// Alert — brute force detection
DeviceLogonEvents
| where ActionType == "LogonFailed"
| where RemoteIPType == "Public"
| where TimeGenerated > ago(1h)
| summarize FailureCount = count() by RemoteIP, DeviceName
| where FailureCount > 10
```

- **Enforce account lockout policies** — after a defined 
  number of failed authentication attempts, the account 
  should be locked and an alert triggered
- **Implement Conditional Access policies** in Azure AD 
  to block authentication attempts from unexpected 
  geographic regions, particularly for privileged accounts

</details>

---

<details>
<summary id="-flag-13">🚩 <strong>Flag 13: <Technique Name></strong></summary>

### 🎯 Objective
Narrow the authentication event scope specifically to Remote Desktop 
Protocol (RDP) related logon activity originating from external public 
IP addresses against `azwks-phtg-02`. This isolates RDP-specific 
authentication events from the broader pool of external logon activity 
to focus the investigation on the confirmed attack vector.

### 📌 Finding
**Answer: 675**

All 675 externally sourced authentication events were RDP-related, 
captured by filtering on `LogonType in ("RemoteInteractive", "Network")` 
combined with `RemoteIPType == "Public"`. The breakdown confirms that 
all external authentication activity against this device was associated 
with RDP — there were no other external authentication vectors observed.

| ActionType | LogonType | Count |
|------------|-----------|-------|
| LogonFailed | Network | 646 |
| LogonSuccess | Network | 21 |
| LogonSuccess | RemoteInteractive | 8 |
| **Total** | | **675** |

> **Investigative Note:** RDP authentication in MDE 
> `DeviceLogonEvents` manifests across two LogonTypes:
> - **RemoteInteractive** — Full interactive RDP desktop 
>   sessions (the classic RDP logon type)
> - **Network** — RDP pre-authentication and NLA 
>   (Network Level Authentication) credential validation, 
>   which occurs before a full desktop session is established
>
> Both LogonTypes must be included to capture the complete 
> picture of RDP-related authentication activity. Filtering 
> on `RemoteInteractive` alone significantly undercounts 
> the true volume of RDP authentication attempts.


### 🔍 Evidence

| Field | Value |
|------|-------|
| Host | azwks-phtg-02 |
| Total RDP Auth Events | 675 |
| LogonFailed (Network) | 646 |
| LogonSuccess (Network) | 21 |
| LogonSuccess (RemoteInteractive) | 8 |
| LogonTypes Included | RemoteInteractive, Network |
| RemoteIPType Filter | Public |
| Investigation Window | 09 December – 23 December 2025 UTC |
| Timestamp | 09 December 2025 – 23 December 2025 UTC |
| Process | N/A — Authentication telemetry, no process execution |
| Parent Process | N/A — Authentication telemetry, no process execution |
| Command Line | N/A — Authentication telemetry, no process execution |

### 💡 Why it matters
Understanding that **all 675 external authentication events were 
RDP-related** is a critical finding because:

- **Single attack vector** — The threat actor exclusively used 
  RDP as their entry point. No other external authentication 
  methods (VPN, web application, API) were observed, confirming 
  RDP as the sole attack surface exploited
- **NLA pre-authentication captures the full brute force volume** 
  — The 646 `Network` logon failures represent RDP NLA 
  pre-authentication rejections. Without including this LogonType, 
  the true scale of the brute force campaign is invisible
- **LogonType matters for detection tuning** — Security teams 
  that only alert on `RemoteInteractive` failures would have 
  missed 646 of the 675 authentication events entirely, 
  dramatically underestimating the attack scope
- **The 8 RemoteInteractive successes are the crown jewels** — 
  These represent full interactive desktop sessions established 
  by the threat actor, confirmed hands-on-keyboard access to 
  the compromised endpoint

### 🔧 KQL Query Used
```kql
// RDP-related external authentication events
// Includes both RemoteInteractive (full RDP sessions) and
// Network (NLA pre-authentication) logon types
DeviceLogonEvents
| where DeviceName == "azwks-phtg-02"
| where TimeGenerated between (datetime(2025-12-09) .. datetime(2025-12-23))
| where LogonType in ("RemoteInteractive", "Network")
| where RemoteIPType == "Public"
| summarize count() by ActionType, LogonType
```

**Results:**
| ActionType | LogonType | Count |
|------------|-----------|-------|
| LogonFailed | Network | 646 |
| LogonSuccess | Network | 21 |
| LogonSuccess | RemoteInteractive | 8 |
| **Total** | | **675** |

```kql
// Single total count
DeviceLogonEvents
| where DeviceName == "azwks-phtg-02"
| where TimeGenerated between (datetime(2025-12-09) .. datetime(2025-12-23))
| where LogonType in ("RemoteInteractive", "Network")
| where RemoteIPType == "Public"
| summarize count()
```

**Result: 675**

### 🖼️ Screenshot
<Insert screenshot>

### 🛠️ Detection Recommendation

**Hunting Tip:**  
- **Always include both `RemoteInteractive` and `Network` LogonTypes** 
  when hunting for RDP authentication activity in MDE — filtering 
  on `RemoteInteractive` alone misses the NLA pre-authentication 
  layer where the majority of brute force failures are recorded
- **Create a composite RDP authentication dashboard** in Sentinel 
  that shows failures and successes across both LogonTypes in 
  a single view:

```kql
// RDP authentication dashboard query
DeviceLogonEvents
| where LogonType in ("RemoteInteractive", "Network")
| where RemoteIPType == "Public"
| where TimeGenerated > ago(24h)
| summarize 
    TotalAttempts = count(),
    Failures = countif(ActionType == "LogonFailed"),
    Successes = countif(ActionType == "LogonSuccess"),
    UniqueSourceIPs = dcount(RemoteIP),
    UniqueAccounts = dcount(AccountName)
    by DeviceName, bin(TimeGenerated, 1h)
| order by TotalAttempts desc
```

- **Alert immediately on any `LogonSuccess` with 
  `LogonType == "RemoteInteractive"` from a public IP** — 
  this is a confirmed RDP session from an external source 
  and should be treated as a critical incident until proven otherwise
- **Implement Network Level Authentication (NLA)** on all 
  RDP-enabled endpoints — while NLA does not prevent brute 
  force, it does require credential validation before 
  establishing a full desktop session, reducing the attack 
  surface and improving the fidelity of Network logon 
  failure telemetry
- **Consider deploying an RDP honeypot** alongside production 
  assets to collect attacker credential lists and TTPs 
  without exposing real infrastructure

</details>

---

<details>
<summary id="-flag-14">🚩 <strong>Flag 14: <Technique Name></strong></summary>

### 🎯 Objective
Identify the most frequently recorded authentication outcome across 
all RDP-related logon activity on `azwks-phtg-02` to characterise 
the dominant pattern of external credential-based attacks and 
confirm the nature of the threat actor's approach.

### 📌 Finding
**Answer: `LogonFailed`**

`LogonFailed` was the most frequently recorded authentication outcome, 
accounting for **646 of the 675 total RDP-related external 
authentication events** — representing **95.7%** of all external 
RDP authentication activity. This overwhelming ratio of failures 
to successes is the hallmark signature of an automated credential 
stuffing or brute force campaign.

| ActionType | Count | Percentage |
|------------|-------|------------|
| LogonFailed | 646 | 95.7% |
| LogonSuccess | 29 | 4.3% |
| **Total** | **675** | **100%** |

### 🔍 Evidence

| Field | Value |
|------|-------|
| Host | azwks-phtg-02 |
| Most Frequent ActionType | LogonFailed |
| LogonFailed Count | 646 |
| LogonSuccess Count | 29 |
| Failure Rate | 95.7% |
| Success Rate | 4.3% |
| Investigation Window | 09 December – 23 December 2025 UTC |
| Timestamp | 09 December 2025 – 23 December 2025 UTC |
| Process | N/A — Authentication telemetry, no process execution |
| Parent Process | N/A — Authentication telemetry, no process execution |
| Command Line | N/A — Authentication telemetry, no process execution |

### 💡 Why it matters
The dominance of `LogonFailed` events in the authentication 
telemetry is significant for several reasons:

- **Confirms automated brute force activity** — A 95.7% failure 
  rate is consistent with automated tools cycling through 
  credential lists at high speed. Human operators rarely 
  generate this volume of failed attempts
- **The 4.3% success rate is alarming** — Despite the high 
  failure rate, the threat actor ultimately succeeded 29 times. 
  This confirms the account `vmadminusername` used a weak, 
  guessable, or previously breached password that appeared 
  in the attacker's credential list
- **Failure volume should have triggered alerts** — 646 failed 
  authentication events over a 14-day window represents an 
  average of 46 failures per day. Any properly tuned SIEM 
  rule would have flagged this within hours of the campaign 
  beginning
- **The success events are the critical pivot point** — While 
  `LogonFailed` dominates by volume, the `LogonSuccess` events 
  are where the investigation must focus next — specifically 
  identifying which accounts, source IPs, and timestamps 
  are associated with the successful authentications


### 🔧 KQL Query Used
```kql
// Authentication outcome breakdown for RDP-related external logons
DeviceLogonEvents
| where DeviceName == "azwks-phtg-02"
| where TimeGenerated between (datetime(2025-12-09) .. datetime(2025-12-23))
| where LogonType in ("RemoteInteractive", "Network")
| where RemoteIPType == "Public"
| summarize count() by ActionType
| order by count_ desc
```

**Results:**
| ActionType | Count |
|------------|-------|
| LogonFailed | 646 |
| LogonSuccess | 29 |

```kql
// Percentage breakdown
DeviceLogonEvents
| where DeviceName == "azwks-phtg-02"
| where TimeGenerated between (datetime(2025-12-09) .. datetime(2025-12-23))
| where LogonType in ("RemoteInteractive", "Network")
| where RemoteIPType == "Public"
| summarize Count = count() by ActionType
| extend Percentage = round(Count * 100.0 / toscalar(
    DeviceLogonEvents
    | where DeviceName == "azwks-phtg-02"
    | where TimeGenerated between (datetime(2025-12-09) .. datetime(2025-12-23))
    | where LogonType in ("RemoteInteractive", "Network")
    | where RemoteIPType == "Public"
    | count), 1)
| order by Count desc
```


### 🖼️ Screenshot
<Insert screenshot>

### 🛠️ Detection Recommendation

**Hunting Tip:**  
- **Implement account lockout policies** — after a defined 
  threshold of failed authentication attempts (typically 
  5-10), the account should be automatically locked and 
  an alert triggered. This would have interrupted the 
  brute force campaign early
- **Alert on failed authentication volume thresholds** — 
  646 failures should never accumulate without triggering 
  a detection:

```kql
// Alert — brute force threshold exceeded
DeviceLogonEvents
| where ActionType == "LogonFailed"
| where LogonType in ("RemoteInteractive", "Network")
| where RemoteIPType == "Public"
| where TimeGenerated > ago(1h)
| summarize 
    FailureCount = count(),
    UniqueAccounts = dcount(AccountName),
    UniqueSourceIPs = dcount(RemoteIP)
    by DeviceName, bin(TimeGenerated, 15m)
| where FailureCount > 10
```

- **Use password spray detection logic** — if failures are 
  spread across many accounts from the same IP, it is 
  spraying; if concentrated on one account from many IPs, 
  it is brute force. Both patterns warrant immediate 
  investigation:

```kql
// Password spray vs brute force classification
DeviceLogonEvents
| where ActionType == "LogonFailed"
| where RemoteIPType == "Public"
| where TimeGenerated > ago(24h)
| summarize 
    UniqueAccounts = dcount(AccountName),
    FailureCount = count()
    by RemoteIP, DeviceName
| extend 
    AttackType = iff(UniqueAccounts > 5, 
        "Password Spray", "Brute Force")
| order by FailureCount desc
```

- **Deploy Microsoft Entra ID Password Protection** to 
  block commonly used weak passwords — `vmadminusername` 
  with a simple password would have been blocked by a 
  custom banned password list containing predictable 
  admin account names

</details>

---

<details>
<summary id="-flag-15">🚩 <strong>Flag 15: <Technique Name></strong></summary>

### 🎯 Objective
Identify the most common failure reason recorded in `DeviceLogonEvents` 
for RDP-related authentication attempts against `azwks-phtg-02`. This 
characterises the nature of the credential-based attack and confirms 
whether the failures were due to invalid credentials, account lockouts, 
policy restrictions, or other causes.

### 📌 Finding
**Answer: `InvalidUserNameOrPassword`**

`InvalidUserNameOrPassword` was the most common failure reason, 
accounting for **637 of the 646 total RDP-related logon failures** — 
representing **98.6%** of all failed authentication attempts. The 
remaining 9 failures were attributed to `UnauthorizedLogonType`.

| FailureReason | Count | Percentage |
|---------------|-------|------------|
| InvalidUserNameOrPassword | 637 | 98.6% |
| UnauthorizedLogonType | 9 | 1.4% |
| **Total** | **646** | **100%** |

### 🔍 Evidence
| Field | Value |
|------|-------|
| Host | azwks-phtg-02 |
| Most Common FailureReason | InvalidUserNameOrPassword |
| InvalidUserNameOrPassword Count | 637 |
| UnauthorizedLogonType Count | 9 |
| Total LogonFailed Events | 646 |
| Investigation Window | 09 December – 23 December 2025 UTC |
| Timestamp | 09 December 2025 – 23 December 2025 UTC |
| Process | N/A — Authentication telemetry, no process execution |
| Parent Process | N/A — Authentication telemetry, no process execution |
| Command Line | N/A — Authentication telemetry, no process execution |

### 💡 Why it matters
The dominance of `InvalidUserNameOrPassword` as the failure reason 
is highly significant for the investigation:

- **Confirms credential stuffing or brute force** — 637 failures 
  due to invalid credentials is the definitive signature of an 
  automated tool cycling through username and password combinations. 
  The attacker did not know the credentials in advance — they 
  were guessing
- **No account lockout failures observed** — The absence of 
  account lockout failure reasons confirms that either no lockout 
  policy was configured on `azwks-phtg-02`, or the attacker was 
  sufficiently distributed across IPs to avoid triggering it. 
  This represents a critical defensive gap
- **`UnauthorizedLogonType` (9 events)** — These failures indicate 
  the attacker attempted logon methods not permitted by policy 
  on this endpoint. This is a minor signal suggesting some 
  automated tools in the campaign attempted non-RDP authentication 
  methods that were blocked by local policy
- **The 637 failures ultimately yielded 29 successes** — The 
  `InvalidUserNameOrPassword` failures represent the attacker's 
  unsuccessful guesses before eventually finding the correct 
  credentials for `vmadminusername`. The weak, predictable 
  account name made it a high-priority target for credential 
  stuffing tools

### 🔧 KQL Query Used
```kql
// Most common failure reason for RDP-related authentication failures
DeviceLogonEvents
| where DeviceName == "azwks-phtg-02"
| where TimeGenerated between (datetime(2025-12-09) .. datetime(2025-12-23))
| where LogonType in ("RemoteInteractive", "Network")
| where RemoteIPType == "Public"
| where ActionType == "LogonFailed"
| summarize count() by FailureReason
| order by count_ desc
```

**Results:**
| FailureReason | Count |
|---------------|-------|
| InvalidUserNameOrPassword | 637 |
| UnauthorizedLogonType | 9 |
| **Total** | **646** |

### 🖼️ Screenshot
<Insert screenshot of Microsoft Sentinel query results showing 
InvalidUserNameOrPassword as the dominant failure reason with 
637 events, followed by UnauthorizedLogonType with 9 events>

### 🛠️ Detection Recommendation
**Hunting Tip:**
- **Alert on sustained `InvalidUserNameOrPassword` failures** 
  from external IPs — this is the clearest signal of an active 
  brute force campaign:

```kql
// Alert — sustained invalid credential failures
DeviceLogonEvents
| where ActionType == "LogonFailed"
| where FailureReason == "InvalidUserNameOrPassword"
| where RemoteIPType == "Public"
| where TimeGenerated > ago(1h)
| summarize 
    FailureCount = count(),
    UniqueSourceIPs = dcount(RemoteIP),
    UniqueAccounts = dcount(AccountName),
    FirstAttempt = min(TimeGenerated),
    LastAttempt = max(TimeGenerated)
    by DeviceName
| where FailureCount > 10
```

- **Enforce strong password policies** — passwords for 
  internet-facing accounts must be long, complex, and 
  not based on predictable patterns like the account name
- **Implement account lockout** — configure a lockout 
  threshold of 5-10 invalid attempts with a 30-minute 
  lockout duration to interrupt automated credential 
  stuffing campaigns
- **Rename or disable default admin accounts** — 
  `vmadminusername` is an immediately recognisable 
  default account name that would appear near the top 
  of any credential stuffing list. Rename it to a 
  non-obvious value and create a honeypot account 
  called `vmadminusername` that triggers an immediate 
  alert on any logon attempt:

```kql
// Honeypot account alert — any logon attempt is suspicious
DeviceLogonEvents
| where AccountName == "vmadminusername"
| where TimeGenerated > ago(1h)
| project TimeGenerated, DeviceName, AccountName, 
          RemoteIP, ActionType, LogonType
```

- **Deploy Microsoft Entra ID Password Protection** 
  with a custom banned password list that includes 
  common admin account names, company names, and 
  product names to prevent weak credential configurations
- **Require MFA for all RDP access** — even with 
  valid credentials, MFA would have prevented the 
  29 successful authentications that led to confirmed 
  compromise

</details>

---

<details>
<summary id="-flag-16">🚩 <strong>Flag 16: <Technique Name></strong></summary>

### 🎯 Objective
Geographically enrich all RDP-related authentication events against 
`azwks-phtg-02` to determine how many distinct countries were 
associated with external logon activity. This establishes the full 
geographic footprint of the credential-based attack campaign and 
identifies anomalous geographic origins inconsistent with PHTG's 
expected operating region.

### 📌 Finding
**Answer: 17**

RDP-related authentication events originated from **17 distinct 
countries** after GeoIP enrichment of all external source IPs. 
This confirms the use of globally distributed attack infrastructure 
— consistent with a threat actor routing credential stuffing and 
brute force traffic through VPN exit nodes, residential proxies, 
and compromised hosts across multiple geographic regions to evade 
detection.

### 🔍 Evidence
| Field | Value |
|------|-------|
| Host | azwks-phtg-02 |
| Total RDP Auth Events | 675 |
| Unique Source IPs Enriched | All public IPs from DeviceLogonEvents |
| Distinct Countries | 17 |
| GeoIP Dataset | GeoIP2 IPv4 (via GitHub raw CSV) |
| PHTG Operating Region | United States only |
| Investigation Window | 09 December – 23 December 2025 UTC |
| Timestamp | 09 December 2025 – 23 December 2025 UTC |
| Process | N/A — Authentication telemetry, no process execution |
| Parent Process | N/A — Authentication telemetry, no process execution |
| Command Line | N/A — Authentication telemetry, no process execution |

### 💡 Why it matters
The presence of 17 distinct countries in RDP authentication 
telemetry is a critical finding for several reasons:

- **PHTG operates exclusively in the United States** — any 
  authentication activity originating from outside the US 
  is immediately anomalous and warrants investigation
- **16 of 17 countries represent unauthorised geographic 
  origins** — only the United States falls within PHTG's 
  expected operating region. All other countries represent 
  potentially hostile or unauthorised access attempts
- **Geographic distribution confirms distributed attack 
  infrastructure** — threat actors deliberately route 
  traffic through multiple countries to evade geographic 
  IP blocklisting and distribute attack volume below 
  per-IP alert thresholds
- **Uruguay emerges as the critical anomaly** — subsequent 
  analysis reveals Uruguay as the source of all successful 
  RDP authentications, making it the highest-priority 
  geographic finding in this investigation
- **17 countries across authentication telemetry vs the 
  scanning phase** — comparing the geographic footprint 
  of scanning activity with authentication activity helps 
  identify which infrastructure was used exclusively for 
  reconnaissance and which progressed to credential 
  submission

### 🔧 KQL Query Used
```kql
// GeoIP enrichment of RDP-related authentication events
let GeoTable =
    externaldata(network:string, geoname_id:long, continent_code:string, 
                 continent_name:string, country_iso_code:string, country_name:string)
    [@"https://raw.githubusercontent.com/datasets/geoip2-ipv4/main/data/geoip2-ipv4.csv"]
    with (format="csv");
DeviceLogonEvents
| where DeviceName == "azwks-phtg-02"
| where TimeGenerated between (datetime(2025-12-09) .. datetime(2025-12-23))
| where LogonType in ("RemoteInteractive", "Network")
| where RemoteIPType == "Public"
| evaluate ipv4_lookup(GeoTable, RemoteIP, network)
| summarize dcount(country_name)
```

**Result: 17 distinct countries**

```kql
// Full country breakdown with event counts
let GeoTable =
    externaldata(network:string, geoname_id:long, continent_code:string, 
                 continent_name:string, country_iso_code:string, country_name:string)
    [@"https://raw.githubusercontent.com/datasets/geoip2-ipv4/main/data/geoip2-ipv4.csv"]
    with (format="csv");
DeviceLogonEvents
| where DeviceName == "azwks-phtg-02"
| where TimeGenerated between (datetime(2025-12-09) .. datetime(2025-12-23))
| where LogonType in ("RemoteInteractive", "Network")
| where RemoteIPType == "Public"
| evaluate ipv4_lookup(GeoTable, RemoteIP, network)
| summarize EventCount = count() by country_name
| order by EventCount desc
```

### 🖼️ Screenshot
<Insert screenshot of Microsoft Sentinel query results showing 
the dcount of 17 distinct countries associated with RDP-related 
authentication events, alongside the full country breakdown>


### 🛠️ Detection Recommendation
**Hunting Tip:**
- **Implement geographic allowlisting for RDP authentication** — 
  since PHTG operates exclusively in the United States, any 
  RDP authentication attempt from outside the US should 
  trigger an immediate high-severity alert:

```kql
// Alert — RDP authentication from non-US country
let GeoTable =
    externaldata(network:string, geoname_id:long, continent_code:string, 
                 continent_name:string, country_iso_code:string, country_name:string)
    [@"https://raw.githubusercontent.com/datasets/geoip2-ipv4/main/data/geoip2-ipv4.csv"]
    with (format="csv");
DeviceLogonEvents
| where LogonType in ("RemoteInteractive", "Network")
| where RemoteIPType == "Public"
| where TimeGenerated > ago(1h)
| evaluate ipv4_lookup(GeoTable, RemoteIP, network)
| where country_iso_code != "US"
| summarize 
    EventCount = count(),
    Failures = countif(ActionType == "LogonFailed"),
    Successes = countif(ActionType == "LogonSuccess")
    by DeviceName, country_name, country_iso_code
| order by Successes desc, EventCount desc
```

- **Prioritise non-US `LogonSuccess` events for immediate 
  investigation** — a successful RDP authentication from 
  outside PHTG's operating region should be treated as a 
  confirmed incident until proven otherwise
- **Build a geographic baseline** for all internet-facing 
  assets — document expected source countries for each 
  service and alert on any deviation from the baseline
- **Correlate geographic authentication data with HR records** 
  — if no PHTG employees are located in a given country, 
  any successful authentication from that country is 
  definitively anomalous and warrants immediate response

</details>

---

<details>
<summary id="-flag-17">🚩 <strong>Flag 17: <Technique Name></strong></summary>

### 🎯 Objective
Determine how many of the 17 countries associated with RDP-related 
authentication activity recorded at least one successful logon event 
against `azwks-phtg-02`. This narrows the geographic investigation 
from all authentication activity to confirmed successful access, 
identifying which countries represent confirmed compromise origins 
rather than unsuccessful attack attempts.

### 📌 Finding
**Answer: 2**

Of the 17 countries associated with RDP-related authentication 
activity, only **2 countries** recorded at least one successful 
authentication event:

| Country | Successful Auth Events |
|---------|----------------------|
| Uruguay | 23 |
| United States | 6 |
| **Total** | **29** |

The remaining 15 countries were associated exclusively with failed 
authentication attempts — consistent with opportunistic scanning 
and credential stuffing infrastructure that did not possess valid 
credentials for `vmadminusername`.

### 🔍 Evidence
| Field | Value |
|------|-------|
| Host | azwks-phtg-02 |
| Total Countries in Auth Telemetry | 17 |
| Countries with Successful Auth | 2 |
| Countries with Failed Auth Only | 15 |
| Successful Auth — Uruguay | 23 events |
| Successful Auth — United States | 6 events |
| Total Successful Auth Events | 29 |
| Investigation Window | 09 December – 23 December 2025 UTC |
| Timestamp | 09 December 2025 – 23 December 2025 UTC |
| Process | N/A — Authentication telemetry, no process execution |
| Parent Process | N/A — Authentication telemetry, no process execution |
| Command Line | N/A — Authentication telemetry, no process execution |

### 💡 Why it matters
The reduction from 17 countries to 2 countries with successful 
authentications is one of the most significant findings in this 
investigation:

- **It isolates the confirmed threat actor infrastructure** — 
  while 17 countries contributed to the broader brute force 
  campaign, only Uruguay and the United States possessed 
  valid credentials for `vmadminusername`. This strongly 
  suggests these two source regions represent the actual 
  threat actor's infrastructure rather than opportunistic 
  scanning noise
- **Uruguay is immediately anomalous** — PHTG operates 
  exclusively in the United States. Uruguay has no legitimate 
  business justification for accessing PHTG infrastructure, 
  making its 23 successful authentications a confirmed 
  indicator of compromise
- **United States (6 events) requires further investigation** — 
  US-based successful authentications could represent legitimate 
  access or could indicate the threat actor is also routing 
  traffic through US-based infrastructure (VPN, cloud VPS, 
  residential proxy) to blend in with expected traffic
- **The 15 countries with only failures** represent the 
  background noise of the internet-wide RDP scanning 
  ecosystem — they should be documented but are not 
  the primary investigation focus

### 🔧 KQL Query Used
```kql
// Countries with at least one successful RDP authentication
let GeoTable =
    externaldata(network:string, geoname_id:long, continent_code:string, 
                 continent_name:string, country_iso_code:string, country_name:string)
    [@"https://raw.githubusercontent.com/datasets/geoip2-ipv4/main/data/geoip2-ipv4.csv"]
    with (format="csv");
DeviceLogonEvents
| where DeviceName == "azwks-phtg-02"
| where TimeGenerated between (datetime(2025-12-09) .. datetime(2025-12-23))
| where LogonType in ("RemoteInteractive", "Network")
| where RemoteIPType == "Public"
| where ActionType == "LogonSuccess"
| evaluate ipv4_lookup(GeoTable, RemoteIP, network)
| summarize dcount(country_name)
```

**Result: 2 countries**

```kql
// Full breakdown of successful auth events by country
let GeoTable =
    externaldata(network:string, geoname_id:long, continent_code:string, 
                 continent_name:string, country_iso_code:string, country_name:string)
    [@"https://raw.githubusercontent.com/datasets/geoip2-ipv4/main/data/geoip2-ipv4.csv"]
    with (format="csv");
DeviceLogonEvents
| where DeviceName == "azwks-phtg-02"
| where TimeGenerated between (datetime(2025-12-09) .. datetime(2025-12-23))
| where LogonType in ("RemoteInteractive", "Network")
| where RemoteIPType == "Public"
| where ActionType == "LogonSuccess"
| evaluate ipv4_lookup(GeoTable, RemoteIP, network)
| summarize count() by country_name
| order by count_ desc
```

**Results:**
| Country | Count |
|---------|-------|
| Uruguay | 23 |
| United States | 6 |

### 🖼️ Screenshot
<Insert screenshot of Microsoft Sentinel query results showing 
the 2 countries with successful RDP authentication events — 
Uruguay (23) and United States (6)>

### 🛠️ Detection Recommendation
**Hunting Tip:**
- **Treat any successful RDP authentication from Uruguay 
  as a confirmed incident** — PHTG has no legitimate 
  business presence in Uruguay, making every one of the 
  23 successful authentications an unambiguous indicator 
  of compromise
- **Investigate the 6 US-based successful authentications** — 
  correlate the source IPs against known VPN providers, 
  cloud hosting ranges (AWS, Azure, GCP), and residential 
  proxy networks to determine if they represent legitimate 
  or malicious access:

```kql
// Investigate US-based successful authentications
let GeoTable =
    externaldata(network:string, geoname_id:long, continent_code:string, 
                 continent_name:string, country_iso_code:string, country_name:string)
    [@"https://raw.githubusercontent.com/datasets/geoip2-ipv4/main/data/geoip2-ipv4.csv"]
    with (format="csv");
DeviceLogonEvents
| where DeviceName == "azwks-phtg-02"
| where TimeGenerated between (datetime(2025-12-09) .. datetime(2025-12-23))
| where LogonType in ("RemoteInteractive", "Network")
| where RemoteIPType == "Public"
| where ActionType == "LogonSuccess"
| evaluate ipv4_lookup(GeoTable, RemoteIP, network)
| where country_iso_code == "US"
| project TimeGenerated, RemoteIP, AccountName, 
          LogonType, country_name
| order by TimeGenerated asc
```

- **Build a successful authentication watchlist** — any 
  `LogonSuccess` event from a country outside PHTG's 
  operating region should be automatically escalated 
  to a P1 incident with immediate response actions:
  1. Isolate the affected endpoint
  2. Reset all credentials on the device
  3. Review all process and file activity from the 
     time of the first successful authentication
  4. Check for lateral movement to other internal systems

</details>

---

<details>
<summary id="-flag-18">🚩 <strong>Flag 18: <Technique Name></strong></summary>

### 🎯 Objective
Identify the specific countries associated with successful RDP 
authentication events against `azwks-phtg-02` to pinpoint confirmed 
geographic origins of threat actor access and distinguish them from 
the broader pool of 17 countries associated with failed authentication 
attempts.

### 📌 Finding
**Answer: `Uruguay, United States`**

Successful RDP authentication events were recorded from exactly 
**two countries**:

| Country | Successful Auth Events | Expected for PHTG |
|---------|----------------------|-------------------|
| Uruguay | 23 | ❌ No — Outside operating region |
| United States | 6 | ✅ Yes — Within operating region |

Uruguay is the primary indicator of compromise — PHTG operates 
exclusively in the United States, making every Uruguay-sourced 
successful authentication definitively anomalous. The United 
States authentications require further investigation to determine 
whether they represent legitimate administrative access or threat 
actor activity routed through US-based proxy infrastructure.

### 🔍 Evidence
| Field | Value |
|------|-------|
| Host | azwks-phtg-02 |
| Country 1 | Uruguay |
| Country 1 Auth Events | 23 |
| Country 1 Legitimate | ❌ No |
| Country 2 | United States |
| Country 2 Auth Events | 6 |
| Country 2 Legitimate | ⚠️ Requires investigation |
| Account Used | vmadminusername |
| Investigation Window | 09 December – 23 December 2025 UTC |
| Timestamp | 09 December 2025 – 23 December 2025 UTC |
| Process | N/A — Authentication telemetry, no process execution |
| Parent Process | N/A — Authentication telemetry, no process execution |
| Command Line | N/A — Authentication telemetry, no process execution |

### 💡 Why it matters
The identification of Uruguay and the United States as the only 
two countries with successful RDP authentications is the pivotal 
finding that transitions this investigation from Phase 03 
(Auth Baseline) into the active compromise phases:

- **Uruguay (23 events) — Confirmed compromise origin:**
  - PHTG has no employees, operations, or legitimate 
    infrastructure in Uruguay
  - 23 successful authentications from Uruguay using 
    `vmadminusername` is unambiguous evidence of 
    unauthorised access
  - The Uruguay IPs (`173.244.55.128` and `173.244.55.131`) 
    belong to the same /24 subnet as the C2 callback IP 
    (`173.244.55.130`) — confirming a single threat actor 
    infrastructure block was used for both initial access 
    and post-exploitation

- **United States (6 events) — Requires investigation:**
  - US-based successful authentications could represent 
    legitimate administrative access by PHTG staff
  - However, they could also represent threat actor 
    traffic routed through US-based VPN, cloud VPS, 
    or residential proxy infrastructure to blend with 
    expected geographic patterns
  - These 6 events must be correlated against known 
    PHTG administrator IP ranges to confirm legitimacy

- **The geographic contrast tells the story** — The 
  transition from 17 countries with failed authentications 
  to 2 countries with successes shows the attacker's 
  credential stuffing infrastructure eventually yielded 
  valid credentials that were then used from their 
  primary operational infrastructure in Uruguay

### 🔧 KQL Query Used
```kql
// Countries associated with successful RDP authentication events
let GeoTable =
    externaldata(network:string, geoname_id:long, continent_code:string, 
                 continent_name:string, country_iso_code:string, country_name:string)
    [@"https://raw.githubusercontent.com/datasets/geoip2-ipv4/main/data/geoip2-ipv4.csv"]
    with (format="csv");
DeviceLogonEvents
| where DeviceName == "azwks-phtg-02"
| where TimeGenerated between (datetime(2025-12-09) .. datetime(2025-12-23))
| where LogonType in ("RemoteInteractive", "Network")
| where RemoteIPType == "Public"
| where ActionType == "LogonSuccess"
| evaluate ipv4_lookup(GeoTable, RemoteIP, network)
| summarize count() by country_name
| order by count_ desc
```

**Results:**
| country_name | count_ |
|--------------|--------|
| Uruguay | 23 |
| United States | 6 |

### 🖼️ Screenshot
<Insert screenshot of Microsoft Sentinel query results showing 
Uruguay (23) and United States (6) as the only two countries 
with successful RDP authentication events>


### 🛠️ Detection Recommendation
**Hunting Tip:**
- **Immediately isolate any endpoint with confirmed successful 
  RDP authentication from Uruguay** — there is no legitimate 
  business justification for this access and it should 
  be treated as a P1 incident:

```kql
// Alert — successful RDP auth from Uruguay
let GeoTable =
    externaldata(network:string, geoname_id:long, continent_code:string, 
                 continent_name:string, country_iso_code:string, country_name:string)
    [@"https://raw.githubusercontent.com/datasets/geoip2-ipv4/main/data/geoip2-ipv4.csv"]
    with (format="csv");
DeviceLogonEvents
| where LogonType in ("RemoteInteractive", "Network")
| where ActionType == "LogonSuccess"
| where RemoteIPType == "Public"
| where TimeGenerated > ago(1h)
| evaluate ipv4_lookup(GeoTable, RemoteIP, network)
| where country_name == "Uruguay"
| project TimeGenerated, DeviceName, AccountName, 
          RemoteIP, LogonType, country_name
```

- **Build a geographic authentication allowlist** — 
  document all countries from which legitimate PHTG 
  administrators are expected to authenticate. Any 
  successful authentication from outside this allowlist 
  should trigger an automated P1 response workflow
- **Investigate US-based successful authentications** 
  by correlating source IPs against:
  - Known PHTG administrator IP ranges
  - Cloud hosting IP ranges (AWS, Azure, GCP)
  - Known VPN and proxy provider IP ranges
  - Threat intelligence feeds for known malicious IPs

- **Pivot immediately from geographic findings into 
  process telemetry** — once a confirmed unauthorised 
  authentication is identified, the next step is to 
  review `DeviceProcessEvents` for all activity 
  initiated by `vmadminusername` from the time of 
  the first Uruguay authentication (`12/12/2025 
  05:47:45 UTC`) onwards

</details>

---

<details>
<summary id="-flag-19">🚩 <strong>Flag 19: <Technique Name></strong></summary>

### 🎯 Objective
Apply PHTG's known operating context — exclusively United States 
based with no international workforce — to the successful RDP 
authentication geographic data to identify which country represents 
a definitive anomaly and confirmed indicator of unauthorised access.

### 📌 Finding
**Answer: `Uruguay`**

Uruguay is the only country associated with successful RDP 
authentication that falls entirely outside PHTG's expected 
operating region. With 23 successful authentication events 
originating from Uruguayan infrastructure, this represents 
the single most significant geographic anomaly in the 
investigation and the primary indicator of confirmed 
unauthorised access.

| Country | Auth Events | Within PHTG Operating Region | Verdict |
|---------|-------------|------------------------------|---------|
| United States | 6 | ✅ Yes | Expected |
| Uruguay | 23 | ❌ No | 🚨 Anomalous — Confirmed IOC |

### 🔍 Evidence
| Field | Value |
|------|-------|
| Host | azwks-phtg-02 |
| Anomalous Country | Uruguay |
| Successful Auth Events from Uruguay | 23 |
| PHTG Operating Region | United States only |
| Account Used | vmadminusername |
| Uruguay Source IPs | 173.244.55.128, 173.244.55.131 |
| C2 IP (same subnet) | 173.244.55.130 |
| First Successful Auth | 12/12/2025 05:47:45 UTC |
| Investigation Window | 09 December – 23 December 2025 UTC |
| Timestamp | 12 December 2025 – 23 December 2025 UTC |
| Process | N/A — Authentication telemetry, no process execution |
| Parent Process | N/A — Authentication telemetry, no process execution |
| Command Line | N/A — Authentication telemetry, no process execution |

### 💡 Why it matters
The identification of Uruguay as the anomalous country is the 
critical pivot point that transforms this investigation from 
a broad authentication analysis into a focused incident response:

- **Zero legitimate justification** — PHTG has no employees, 
  contractors, partners, or operations in Uruguay. There is 
  no scenario in which a successful RDP authentication from 
  Uruguay represents authorised access
- **23 successful authentications confirm persistent access** — 
  This is not a single opportunistic login. 23 successful 
  sessions from Uruguayan infrastructure over the investigation 
  window indicates sustained, deliberate, and repeated 
  unauthorised access
- **Infrastructure convergence is definitive** — The Uruguay 
  source IPs (`173.244.55.128` and `173.244.55.131`) share 
  a /24 subnet with the Meterpreter C2 callback IP 
  (`173.244.55.130`). The same infrastructure block was 
  used for initial access AND post-exploitation C2 — 
  confirming a single threat actor operating from 
  Uruguayan infrastructure throughout the attack chain
- **Timeline correlation with the LinkedIn post** — The 
  first successful Uruguay authentication occurred on 
  12/12/2025 at 05:47:45 UTC — just one day after 
  HealthCloud was rolled out (11 December) and 
  consistent with the LinkedIn post exposure window. 
  The attacker saw the post, identified the target, 
  and gained access within 24 hours

### 🔧 KQL Query Used
```kql
// Identify anomalous country by filtering successful auth 
// events and applying PHTG operating region context
let GeoTable =
    externaldata(network:string, geoname_id:long, continent_code:string, 
                 continent_name:string, country_iso_code:string, country_name:string)
    [@"https://raw.githubusercontent.com/datasets/geoip2-ipv4/main/data/geoip2-ipv4.csv"]
    with (format="csv");
DeviceLogonEvents
| where DeviceName == "azwks-phtg-02"
| where TimeGenerated between (datetime(2025-12-09) .. datetime(2025-12-23))
| where LogonType in ("RemoteInteractive", "Network")
| where RemoteIPType == "Public"
| where ActionType == "LogonSuccess"
| evaluate ipv4_lookup(GeoTable, RemoteIP, network)
| where country_iso_code != "US"
| summarize count() by country_name, country_iso_code
| order by count_ desc
```

**Result:**
| country_name | country_iso_code | count_ |
|--------------|-----------------|--------|
| Uruguay | UY | 23 |

### 🖼️ Screenshot
<Insert screenshot of Microsoft Sentinel query results showing 
Uruguay as the sole non-US country with successful RDP 
authentication events, with 23 events recorded>

### 🛠️ Detection Recommendation
**Hunting Tip:**
- **Implement an automated geographic anomaly detection 
  rule** that triggers a P1 incident for any successful 
  authentication from outside PHTG's operating region:

```kql
// P1 Alert — successful auth from outside operating region
let GeoTable =
    externaldata(network:string, geoname_id:long, continent_code:string, 
                 continent_name:string, country_iso_code:string, country_name:string)
    [@"https://raw.githubusercontent.com/datasets/geoip2-ipv4/main/data/geoip2-ipv4.csv"]
    with (format="csv");
let AllowedCountries = datatable(country_iso_code:string) ["US"];
DeviceLogonEvents
| where ActionType == "LogonSuccess"
| where LogonType in ("RemoteInteractive", "Network")
| where RemoteIPType == "Public"
| where TimeGenerated > ago(1h)
| evaluate ipv4_lookup(GeoTable, RemoteIP, network)
| where country_iso_code !in (AllowedCountries)
| project TimeGenerated, DeviceName, AccountName,
          RemoteIP, LogonType, country_name
| order by TimeGenerated desc
```

- **Block the entire `173.244.55.0/24` subnet** at the 
  network perimeter immediately — this subnet was used 
  for scanning, initial access, and C2 activity. All 
  three IPs identified in this investigation 
  (`173.244.55.128`, `173.244.55.130`, `173.244.55.131`) 
  belong to this block
- **Document Uruguay as a threat actor indicator** in 
  your threat intelligence platform and apply blocking 
  rules for this geographic region at the firewall 
  and Azure NSG level
- **Pivot immediately to process telemetry** — with 
  Uruguay confirmed as the anomalous access origin, 
  the next step is to review all `DeviceProcessEvents` 
  initiated by `vmadminusername` from 12/12/2025 
  05:47:45 UTC onwards to map the full scope of 
  threat actor activity on the compromised endpoint

</details>

---

<details>
<summary id="-flag-20">🚩 <strong>Flag 20: <Technique Name></strong></summary>

### 🎯 Objective
Identify the specific account used by the threat actor during 
successful RDP authentication sessions originating from Uruguay 
to confirm which credential was compromised, assess the level 
of access obtained, and anchor all subsequent process and 
file activity investigation to the correct account context.

### 📌 Finding
**Answer: `vmadminusername`**

All 23 successful RDP authentication events originating from 
Uruguay used the account **`vmadminusername`** — a generic, 
predictable local administrator account name that was almost 
certainly created during VM provisioning and never renamed 
or hardened. This account's predictable name made it an 
immediate high-priority target for automated credential 
stuffing tools.

| Account | Country | Successful Auth Events | Account Type |
|---------|---------|----------------------|--------------|
| vmadminusername | Uruguay | 23 | Local Administrator |

### 🔍 Evidence
| Field | Value |
|------|-------|
| Host | azwks-phtg-02 |
| Compromised Account | vmadminusername |
| Account Type | Local Administrator |
| Source Country | Uruguay |
| Source IPs | 173.244.55.128, 173.244.55.131 |
| Successful Auth Events | 23 |
| First Successful Auth | 12/12/2025 05:47:45 UTC |
| LogonTypes | RemoteInteractive, Network |
| Investigation Window | 09 December – 23 December 2025 UTC |
| Timestamp | 12 December 2025 – 23 December 2025 UTC |
| Process | N/A — Authentication telemetry, no process execution |
| Parent Process | N/A — Authentication telemetry, no process execution |
| Command Line | N/A — Authentication telemetry, no process execution |

### 💡 Why it matters
The identification of `vmadminusername` as the compromised 
account is critical for several reasons:

- **Predictable naming convention** — `vmadminusername` 
  is an immediately recognisable default VM administrator 
  account name. Automated credential stuffing tools 
  maintain lists of common admin account names and 
  target them first. This account name would appear 
  near the top of any such list
- **Local administrator privileges** — A local admin 
  account provides the threat actor with elevated 
  privileges on the endpoint from the moment of first 
  login — no privilege escalation required. The attacker 
  had immediate administrative control of `azwks-phtg-02` 
  from their first successful session
- **No MFA protection** — The account was accessible 
  with credentials alone. Multi-factor authentication 
  would have prevented all 23 successful authentications 
  even after the password was brute forced
- **Account name as a lure** — The file 
  `Sarah_Chen_Notes.exe` discovered later in the 
  investigation was delivered and executed under 
  this account's context, confirming `vmadminusername` 
  as the account used throughout the entire post-exploitation 
  phase
- **All subsequent telemetry is anchored here** — Every 
  process execution, file creation, and network event 
  initiated by the threat actor on `azwks-phtg-02` 
  will be associated with `vmadminusername` in 
  `InitiatingProcessAccountName` fields across 
  `DeviceProcessEvents` and `DeviceFileEvents`

### 🔧 KQL Query Used
```kql
// Identify account used in successful RDP auth from Uruguay
let GeoTable =
    externaldata(network:string, geoname_id:long, continent_code:string, 
                 continent_name:string, country_iso_code:string, country_name:string)
    [@"https://raw.githubusercontent.com/datasets/geoip2-ipv4/main/data/geoip2-ipv4.csv"]
    with (format="csv");
DeviceLogonEvents
| where DeviceName == "azwks-phtg-02"
| where TimeGenerated between (datetime(2025-12-09) .. datetime(2025-12-23))
| where LogonType in ("RemoteInteractive", "Network")
| where RemoteIPType == "Public"
| where ActionType == "LogonSuccess"
| evaluate ipv4_lookup(GeoTable, RemoteIP, network)
| where country_name == "Uruguay"
| summarize count() by AccountName
```

**Result:**
| AccountName | count_ |
|-------------|--------|
| vmadminusername | 23 |

### 🖼️ Screenshot
<Insert screenshot of Microsoft Sentinel query results showing 
vmadminusername as the sole account associated with all 23 
successful RDP authentication events from Uruguay>

### 🛠️ Detection Recommendation
**Hunting Tip:**
- **Immediately disable or rename `vmadminusername`** — 
  this account should be considered fully compromised 
  and must not be used for any legitimate administrative 
  purpose going forward
- **Audit all local administrator accounts** across the 
  PHTG estate for predictable naming conventions. Any 
  account named with obvious patterns (`admin`, 
  `administrator`, `vmadmin`, `localadmin`) should 
  be renamed immediately:

```kql
// Hunt for other devices with the same compromised account
DeviceLogonEvents
| where AccountName == "vmadminusername"
| where ActionType == "LogonSuccess"
| where TimeGenerated between (datetime(2025-12-09) .. datetime(2025-12-23))
| summarize 
    SuccessCount = count(),
    UniqueSourceIPs = dcount(RemoteIP),
    FirstSeen = min(TimeGenerated),
    LastSeen = max(TimeGenerated)
    by DeviceName, AccountName
| order by SuccessCount desc
```

- **Enable Microsoft Defender for Identity** to detect 
  suspicious account behaviour including unusual 
  authentication patterns, geographic anomalies, 
  and lateral movement attempts using compromised 
  local accounts
- **Implement a privileged account naming policy** 
  that uses non-obvious, randomised account names 
  for all administrative accounts — making them 
  significantly harder to target with credential 
  stuffing tools
- **Enforce MFA for all local administrator accounts** 
  that have RDP access — valid credentials alone 
  should never be sufficient for administrative 
  access to internet-facing endpoints
- **Create a honeypot account** named `vmadminusername` 
  across the wider PHTG estate — any logon attempt 
  against this account on any other device should 
  trigger an immediate P1 alert, as it indicates 
  the threat actor is attempting lateral movement 
  using the compromised credential:

```kql
// Honeypot detection — vmadminusername logon on any device
DeviceLogonEvents
| where AccountName == "vmadminusername"
| where TimeGenerated > ago(1h)
| project TimeGenerated, DeviceName, AccountName,
          RemoteIP, ActionType, LogonType
```

</details>

---

<details>
<summary id="-flag-21">🚩 <strong>Flag 21: <Technique Name></strong></summary>

### 🎯 Objective
Quantify the total number of successful RDP authentication events 
originating specifically from Uruguay to establish the full scope 
of confirmed unauthorised access sessions and determine the 
persistence and duration of the threat actor's presence on 
`azwks-phtg-02`.

### 📌 Finding
**Answer: `23`**

A total of **23 successful RDP authentication events** originated 
from Uruguay during the investigation window. All 23 events used 
the account `vmadminusername` and originated from two IP addresses 
within the same /24 subnet — confirming a single threat actor 
operating from dedicated Uruguayan infrastructure across multiple 
sessions.

| Source IP | Successful Auth Events | Subnet |
|-----------|----------------------|--------|
| 173.244.55.131 | 13 | 173.244.55.0/24 |
| 173.244.55.128 | 10 | 173.244.55.0/24 |
| **Total** | **23** | |

### 🔍 Evidence
| Field | Value |
|------|-------|
| Host | azwks-phtg-02 |
| Anomalous Country | Uruguay |
| Total Successful Auth Events | 23 |
| Account Used | vmadminusername |
| Source IP 1 | 173.244.55.131 (13 events) |
| Source IP 2 | 173.244.55.128 (10 events) |
| C2 IP (same subnet) | 173.244.55.130 |
| First Successful Auth | 12/12/2025 05:47:45 UTC |
| Investigation Window | 09 December – 23 December 2025 UTC |
| Timestamp | 12 December 2025 – 23 December 2025 UTC |
| Process | N/A — Authentication telemetry, no process execution |
| Parent Process | N/A — Authentication telemetry, no process execution |
| Command Line | N/A — Authentication telemetry, no process execution |

### 💡 Why it matters
The volume and pattern of 23 successful authentications from 
Uruguay reveals critical information about the threat actor's 
operational behaviour:

- **23 sessions indicates sustained, persistent access** — 
  This is not a single opportunistic login. The threat actor 
  returned to `azwks-phtg-02` repeatedly over multiple days, 
  suggesting ongoing objectives that required extended 
  interactive access
- **Two source IPs from the same /24 subnet** — The use 
  of `173.244.55.128` and `173.244.55.131` from the same 
  subnet as the C2 IP (`173.244.55.130`) confirms a 
  single dedicated infrastructure block used throughout 
  the attack chain. This is not coincidental — it 
  represents deliberate, organised threat actor 
  infrastructure
- **Timeline begins day after HealthCloud rollout** — 
  The first successful authentication on 12/12/2025 
  occurred just one day after HealthCloud was deployed 
  on 11/12/2025. The LinkedIn post exposure and the 
  timing of first access confirm a direct causal link 
  between the OPSEC failure and the compromise
- **23 sessions = 23 opportunities for data exfiltration, 
  reconnaissance, and persistence** — Each successful 
  authentication represents a window during which the 
  threat actor could execute commands, transfer files, 
  modify configurations, and expand their foothold

### 🔧 KQL Query Used
```kql
// Count successful RDP authentications from Uruguay
let GeoTable =
    externaldata(network:string, geoname_id:long, continent_code:string, 
                 continent_name:string, country_iso_code:string, country_name:string)
    [@"https://raw.githubusercontent.com/datasets/geoip2-ipv4/main/data/geoip2-ipv4.csv"]
    with (format="csv");
DeviceLogonEvents
| where DeviceName == "azwks-phtg-02"
| where TimeGenerated between (datetime(2025-12-09) .. datetime(2025-12-23))
| where LogonType in ("RemoteInteractive", "Network")
| where RemoteIPType == "Public"
| where ActionType == "LogonSuccess"
| evaluate ipv4_lookup(GeoTable, RemoteIP, network)
| where country_name == "Uruguay"
| summarize count() by AccountName
```

**Result: 23**

```kql
// Breakdown by source IP to confirm infrastructure pattern
let GeoTable =
    externaldata(network:string, geoname_id:long, continent_code:string, 
                 continent_name:string, country_iso_code:string, country_name:string)
    [@"https://raw.githubusercontent.com/datasets/geoip2-ipv4/main/data/geoip2-ipv4.csv"]
    with (format="csv");
DeviceLogonEvents
| where DeviceName == "azwks-phtg-02"
| where TimeGenerated between (datetime(2025-12-09) .. datetime(2025-12-23))
| where LogonType in ("RemoteInteractive", "Network")
| where RemoteIPType == "Public"
| where ActionType == "LogonSuccess"
| evaluate ipv4_lookup(GeoTable, RemoteIP, network)
| where country_name == "Uruguay"
| summarize count() by RemoteIP
| order by count_ desc
```

**Results:**
| RemoteIP | count_ |
|----------|--------|
| 173.244.55.131 | 13 |
| 173.244.55.128 | 10 |
| **Total** | **23** |

### 🖼️ Screenshot
<Insert screenshot of Microsoft Sentinel query results showing 
23 total successful RDP authentication events from Uruguay, 
broken down by source IP>

### 🛠️ Detection Recommendation
**Hunting Tip:**
- **Build a session timeline** to map the full scope 
  of threat actor access across all 23 sessions:

```kql
// Full timeline of Uruguay RDP sessions
let GeoTable =
    externaldata(network:string, geoname_id:long, continent_code:string, 
                 continent_name:string, country_iso_code:string, country_name:string)
    [@"https://raw.githubusercontent.com/datasets/geoip2-ipv4/main/data/geoip2-ipv4.csv"]
    with (format="csv");
DeviceLogonEvents
| where DeviceName == "azwks-phtg-02"
| where TimeGenerated between (datetime(2025-12-09) .. datetime(2025-12-23))
| where LogonType in ("RemoteInteractive", "Network")
| where ActionType == "LogonSuccess"
| evaluate ipv4_lookup(GeoTable, RemoteIP, network)
| where country_name == "Uruguay"
| project TimeGenerated, RemoteIP, AccountName, 
          LogonType, country_name
| order by TimeGenerated asc
```

- **Correlate each session timestamp with process 
  telemetry** — for each of the 23 session start 
  times, review `DeviceProcessEvents` for commands 
  executed within the following 30-60 minutes to 
  map threat actor actions per session
- **Implement session recording for RDP** — tools 
  like Azure Bastion provide session recording 
  capabilities that would allow full playback of 
  threat actor activity during each interactive session
- **Block `173.244.55.0/24` immediately** at the 
  Azure NSG level — all three IPs from this subnet 
  (`173.244.55.128`, `173.244.55.130`, `173.244.55.131`) 
  have been confirmed as threat actor infrastructure

</details>

---

<details>
<summary id="-flag-22">🚩 <strong>Flag 22: <Technique Name></strong></summary>

### 🎯 Objective
Identify the specific source IP address associated with the first 
successful RDP authentication from Uruguay to establish the initial 
point of confirmed unauthorised access, anchor the investigation 
timeline, and begin correlating threat actor infrastructure across 
the full kill chain.

### 📌 Finding
**Answer: `173.244.55.131`**

The first successful RDP authentication from Uruguay originated 
from **`173.244.55.131`** at **12/12/2025 05:47:45 UTC** — 
just one day after the HealthCloud rollout on 11 December 2025 
and consistent with the LinkedIn post exposure window. This IP 
is part of the `173.244.55.0/24` subnet used throughout the 
attack chain for both initial access and C2 callbacks.

| Field | Value |
|-------|-------|
| First Auth Timestamp | 12/12/2025 05:47:45 UTC |
| Source IP | 173.244.55.131 |
| Account | vmadminusername |
| Country | Uruguay |
| Subnet | 173.244.55.0/24 |

### 🔍 Evidence
| Field | Value |
|-------|-------|
| Host | azwks-phtg-02 |
| First Successful Auth IP | 173.244.55.131 |
| First Successful Auth Time | 12/12/2025 05:47:45 UTC |
| Account Used | vmadminusername |
| Country | Uruguay |
| Related IPs in Same Subnet | 173.244.55.128 (access), 173.244.55.130 (C2) |
| Investigation Window | 09 December – 23 December 2025 UTC |
| Timestamp | 12/12/2025 05:47:45 UTC |
| Process | N/A — Authentication telemetry, no process execution |
| Parent Process | N/A — Authentication telemetry, no process execution |
| Command Line | N/A — Authentication telemetry, no process execution |

### 💡 Why it matters
The first successful authentication IP is the most critical 
single indicator of compromise in this investigation for 
several reasons:

- **It marks the moment of confirmed unauthorised access** — 
  05:47:45 UTC on 12 December 2025 is the definitive 
  start of the incident. Everything before this timestamp 
  is reconnaissance and brute force; everything after 
  is post-exploitation
- **It anchors the infrastructure attribution** — 
  `173.244.55.131` belongs to the same /24 subnet as 
  `173.244.55.128` (second access IP) and `173.244.55.130` 
  (C2 callback IP). This subnet convergence across three 
  distinct attack phases — initial access, persistent 
  access, and C2 — confirms a single, organised threat 
  actor operating from dedicated Uruguayan infrastructure
- **Timeline correlation with the LinkedIn post** — 
  The first successful authentication occurred 
  approximately 18 hours after the LinkedIn post 
  would have been visible. This is consistent with 
  an attacker who:
  1. Saw the post and identified the target
  2. Began automated credential stuffing against 
     the exposed RDP service
  3. Successfully authenticated within 24 hours
- **This IP should be the starting point for all 
  threat intelligence enrichment** — submitting 
  `173.244.55.131` to internal threat intelligence 
  platforms (respecting the lab's OPSEC rules) 
  would reveal additional context about the 
  infrastructure and potential attribution

### 🔧 KQL Query Used
```kql
// Identify the first successful RDP authentication from Uruguay
let GeoTable =
    externaldata(network:string, geoname_id:long, continent_code:string, 
                 continent_name:string, country_iso_code:string, country_name:string)
    [@"https://raw.githubusercontent.com/datasets/geoip2-ipv4/main/data/geoip2-ipv4.csv"]
    with (format="csv");
DeviceLogonEvents
| where DeviceName == "azwks-phtg-02"
| where TimeGenerated between (datetime(2025-12-09) .. datetime(2025-12-23))
| where LogonType in ("RemoteInteractive", "Network")
| where RemoteIPType == "Public"
| where ActionType == "LogonSuccess"
| evaluate ipv4_lookup(GeoTable, RemoteIP, network)
| where country_name == "Uruguay"
| order by TimeGenerated asc
| take 1
| project TimeGenerated, RemoteIP, AccountName
```

**Result:**
| TimeGenerated [UTC] | RemoteIP | AccountName |
|--------------------|----------|-------------|
| 12/12/2025, 5:47:45 AM | 173.244.55.131 | vmadminusername |

### 🖼️ Screenshot
<Insert screenshot of Microsoft Sentinel query results showing 
173.244.55.131 as the first successful RDP authentication from 
Uruguay at 12/12/2025 05:47:45 UTC>

### 🛠️ Detection Recommendation
**Hunting Tip:**
- **Use the incident start timestamp (12/12/2025 05:47:45 UTC) 
  as the anchor for all subsequent investigation** — every 
  process, file, and network event after this timestamp 
  under the `vmadminusername` context should be treated 
  as potentially malicious:

```kql
// All activity after confirmed initial access
DeviceProcessEvents
| where DeviceName == "azwks-phtg-02"
| where TimeGenerated >= datetime(2025-12-12T05:47:45Z)
| where InitiatingProcessAccountName =~ "vmadminusername"
| project TimeGenerated, FileName, ProcessCommandLine,
          InitiatingProcessFileName, InitiatingProcessCommandLine
| order by TimeGenerated asc
```

- **Block `173.244.55.0/24` immediately** at all 
  network perimeter controls — this subnet has been 
  confirmed as threat actor infrastructure across 
  multiple attack phases
- **Establish T0 (time zero) alerting** — implement 
  a detection rule that triggers the moment any 
  successful authentication is recorded from a 
  non-approved country, with automatic containment 
  actions (session termination, account lock, 
  endpoint isolation) to prevent post-exploitation 
  activity before it begins

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

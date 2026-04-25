# 🛡️ SOC Operations: Threat Detection & Incident Response
<p align="center">
    <img src="https://github.com/alhemdrew/CyblackIntenship/blob/main/sprints/c.png" alt="CyBlack Logo" />
</p>
**Organization:** `Cyberinfiniti Ltd.`  
**Project:** SOC Enterprise Threat Analysis & Vulnerability Management  
**Report ID:** `SOC-TIV-2026-INT-001`  
**Date:** April 2026  
**Classification:** 🔴 Confidential / Internal Use  
**Frameworks:** `NIST SP 800-61r2` | `MITRE ATT&CK®`

---

## 📑 Table of Contents
- [1.0 Executive Summary](#10-executive-summary)
- [2.0 Detailed Analyst Contributions](#20-detailed-analyst-contributions)
- [3.0 Incident Overview & Attack Flow](#30-incident-overview--attack-flow)
- [4.0 MITRE ATT&CK® Mapping](#40-mitre-attck-mapping)
- [5.0 Technical Investigation (Malware & Phishing)](#50-technical-investigation-malware--phishing)
- [6.0 Containment & Remediation](#60-containment--remediation)
- [7.0 SOC Tooling & Appendices](#70-soc-tooling--appendices)

---
<p align="center">
    <img src="soc.png" alt="CyBlack Logo" />
</p>
## 1.0 Executive Summary
This report details the operational activities of the **Cyberinfiniti SOC** during the April 2026 assessment period. The team successfully detected, investigated, and neutralized a multi-stage phishing campaign that led to account compromise and attempted malware deployment.

### Key Outcomes:
- [x] **Rapid Detection:** Identified high-volume phishing targeting the finance department.
- [x] **Incident Containment:** Revoked compromised Entra ID tokens and isolated infected endpoints.
- [x] **Threat Intel:** Mapped adversary behavior to known threat actors using MITRE ATT&CK.
- [x] **Vulnerability Management:** Remediated critical gaps in mailbox forwarding rules.

---

## 2.0 Detailed Analyst Contributions
The SOC engagement was executed by a collaborative team of security analysts:

| Analyst | Core Functional Responsibility |
| :--- | :--- |
| **John Ofulue** | **Team Lead:** SOC management; threat hunting; final report compilation. |
| **Halimat O. Adepegba** | **Asst. Team Lead:** Data collection & analysis; executive reporting. |
| **Andrew Moses** | **Incident Responder:** Malware investigation; attack flow documentation; presentation design. |
| **Ikenna Emerole** | **Technical Reviewer:** Verification of MITRE mapping & incident timelines. |
| **Favour Obisike** | **Vulnerability Analyst:** Remediation tracking & technical documentation editing. |
| **Odunayo Balogun** | **Forensics Analyst:** Forensic analysis & attack flow diagramming. |
| **Ayodimeji Omole** | **SOC Reviewer:** Quality assurance of final report and technical findings. |
| **Blessing Ibe** | **Audit Lead:** Managed sprint timelines (Appendix B/C) & meeting coordination. |
| **Divine Ezewele** | **Reporting Analyst:** Documentation approach & cross-team communication. |

---

## 3.0 Incident Overview & Attack Flow
The incident involved a sophisticated phishing campaign utilizing **Typosquatting** and **Credential Harvesting**.

### 📉 Attack Flow Lifecycle:
1. **Initial Access:** Delivery of phishing email with a malicious URL.
2. **Execution:** User interacts with the URL, leading to a credential harvesting page.
3. **Persistence:** Unauthorized creation of mailbox forwarding rules.
4. **Impact:** Attempted lateral movement and financial data exfiltration.

---

## 4.0 MITRE ATT&CK® Mapping
The SOC team mapped the observed behaviors to the following tactics:

| Tactic | Technique ID | Technique Name | Observed Behavior |
| :--- | :--- | :--- | :--- |
| **Initial Access** | `T1566.002` | Phishing: Malicious Link | Spear-phishing link delivered via email. |
| **Credential Access** | `T1557` | Adversary-in-the-Middle | Proxying authentication to bypass MFA. |
| **Persistence** | `T1137.005` | Office Application Startup | Malicious mailbox forwarding rules. |
| **Exfiltration** | `T1041` | Exfiltration Over C2 | Data sent to a remote command & control server. |

---

## 5.0 Technical Investigation

### 📧 Phishing Analysis
* **Sender:** `hr-portal@cyberinfiniti-updates.com` (Typosquatted domain).
* **Payload:** Redirected to a credential harvester spoofing Microsoft 365.
* **Findings:** Identified a 15% click-rate among the targeted user group.

### 🧪 Malware Sandbox Detonation
> [!NOTE]
> **Static Analysis:** Hash `e3b0c442...` flagged by 45+ engines on VirusTotal.
> **Dynamic Analysis:** Malware attempted to disable Windows Defender and connect to `91.x.x.x` (C2).

---

## 6.0 Containment & Remediation

### Identity Containment (Entra ID)
- [x] Revoked all refresh tokens for compromised users.
- [x] Forced password resets and re-registration of MFA.
- [x] Audited and removed rogue OAuth app consents.

### Endpoint Containment (Defender for Endpoint)
- [x] Isolated 3 infected workstations from the network.
- [x] Ran full forensic investigation packages.
- [x] Pushed custom indicators (hashes/IPs) to prevent re-infection.

---

## 7.0 SOC Tooling & Appendices
The team utilized a robust stack of investigation and enrichment tools:

* **SIEM/EDR:** Microsoft Sentinel, Defender for Endpoint.
* **Analysis:** VirusTotal, Hybrid Analysis, ANY.RUN, urlscan.io.
* **DNS/Network:** MxToolbox, DigTrace, WannaBrowser.

---
**Owner:** `CyberInfiniti SOC`  
**Review Cadence:** Every 6 Months  
**Distribution:** SOC Team | IT Operations | Compliance  
**Project Status:** 🏁 Completed

# OpenCTI Threat Intelligence Sprint Assessment

**Report Title:** OpenCTI Threat Intelligence Sprint Assessment  
**Report ID:** TIR-CTI-2026-INT-001  
**Report Date:** January 2026  
**Classification:** Confidential / Internal Use  
**Analysts:** Andrew moses and 8 others 
**Report Version:** 1.0  
**Distribution:** CyBlack Team, Team 8 SOC Team, Executive Management  

---

## Table of Contents

1. [Executive Summary](#executive-summary)  
2. [Scenario Overview & Objectives](#scenario-overview--objectives)  
3. [Methodology & Intelligence Sources](#methodology--intelligence-sources)  
4. [OpenCTI Custom Deployment & Architecture](#opencti-custom-deployment--architecture)  
5. [Task 1: Industry Sector Focus & Threat Landscape](#task-1-industry-sector-focus--threat-landscape)  
6. [Task 2: National Threat Landscape Assessment](#task-2-national-threat-landscape-assessment)  
7. [Task 3: Victim Profile & Threat Mapping](#task-3-victim-profile--threat-mapping)  
8. [Detection & Mitigation Recommendations per Victim](#detection--mitigation-recommendations-per-victim)  
9. [Task 4: Politically Motivated Threat Group](#task-4-politically-motivated-threat-group)  
10. [Detection, Monitoring & Defensive Considerations](#detection-monitoring--defensive-considerations)  
11. [Executive Impact & Strategic Recommendations](#executive-impact--strategic-recommendations)  
12. [Lessons Learned](#lessons-learned)  
13. [References](#references)  
14. [Appendices](#appendices)  

---

## Executive Summary

This Threat Intelligence Report presents the results of a structured Cyber Threat Intelligence (CTI) sprint conducted using the OpenCTI platform in a Docker container, enriched with intelligence from the AlienVault Open Threat Exchange (OTX) Connector.  

The primary objective was to identify and assess sector-specific cyber threats, nation-state and criminal activity, targeted victim trends, and politically motivated threat actors relevant to the organization’s operating environment.  

Findings are correlated with established analytical frameworks, including the Diamond Model of Intrusion Analysis, Cyber Kill Chain, and MITRE ATT&CK, providing actionable intelligence to support executive decision-making, enhance detection and response capabilities, and strengthen overall cyber resilience.  

---

## Scenario Overview & Objectives

Cyberinfiniti Ltd, Team 8, operated as a dedicated threat intelligence function within a simulated organizational environment. The team leveraged OpenCTI as the central intelligence management platform, enriched with live, community-driven intelligence through AlienVault OTX.  

**Key Objectives:**
- Profile the cyber threat landscape affecting the IT sector.  
- Assess country-level cyber threats impacting headquarters and regional operations.  
- Identify recently targeted victims and analyze associated threat actors and campaigns.  
- Investigate politically motivated threat actors involved in high-impact activity.  
- Translate technical findings into executive-level intelligence for risk-based decisions.  

---

## Methodology & Intelligence Sources

The CTI effort followed a structured intelligence lifecycle:  

1. **Direction:** Defined intelligence requirements aligned with organizational risk and sector exposure.  
2. **Collection:** Aggregated threat data from OpenCTI and AlienVault OTX feeds.  
3. **Processing:** Normalized and enriched indicators, entities, and relationships within OpenCTI.  
4. **Analysis:** Applied the Diamond Model, Cyber Kill Chain, and timeline analysis to identify adversary behavior patterns.  
5. **Dissemination:** Produced analyst-ready and executive-level reporting focused on risk and defensive posture.  

**Primary Intelligence Sources:**
- OpenCTI Platform  
- AlienVault Open Threat Exchange (OTX)  
- Community-shared indicators, reports, and threat actor profiles  
- MITRE ATT&CK Framework  
- Open-source intelligence (OSINT)  

---

## OpenCTI Custom Deployment & Architecture

### Overview
OpenCTI was deployed in a secure AWS EC2 environment using Ubuntu Linux, Docker, and Docker Compose to enable scalable ingestion, correlation, and analysis of threat intelligence.

### AWS EC2 Environment Configuration
- **Instance Type:** t3.xlarge  
- **vCPU:** 4  
- **Memory:** 16 GB RAM  
- **OS:** Ubuntu Server 64-bit  
- **Deployment Model:** Single-node OpenCTI deployment using Docker  

### Network & Security
- EC2 instance placed in a VPC, secured with Security Groups  
- Restricted inbound access to analyst IP only  
- Exposed ports: SSH (22), HTTP (80), HTTPS (443), OpenCTI Web Interface (8080)  

### Secure Access & Administration
- SSH key-based authentication  
- Root access restricted; administrative actions via `sudo`  
- Encrypted communications and strong identity assurance  

### Docker & Containerization
1. **Setup Docker APT Repository**  
2. **Install Docker Engine & Compose Plugin**  
3. **Install supporting tools:** Git, Sublime Text  

### OpenCTI Installation & Configuration
- `.env` defines platform credentials, DB configuration, message queue parameters, connector authentication tokens  
- Validation enforced for secure authentication  

### Architecture & Data Flow
- **Host Ubuntu Machine → EC2 → Docker → OpenCTI Platform**  
- Components: OpenCTI API & frontend, Elasticsearch, Redis, MinIO, RabbitMQ, Graph Database, AlienVault OTX Connector  

### AlienVault OTX Connector Integration
- Authenticates via API token  
- Periodically queries OTX for IOCs, pulses, malware, and threat actor data  
- Data normalized into STIX, sent via RabbitMQ, ingested into OpenCTI  

### Operational Benefits
- Scalable, resilient, secure, realistic enterprise CTI simulation  

---

## Task 1: Industry Sector Focus & Threat Landscape

### Sector Identification
- **Sector:** Information Technology (IT)  
- **Exposure:** Privileged access to customer environments, sensitive IP, authentication systems, and security tooling  

### Sector Threat Landscape
1. **Ransomware Operations:** Double/triple extortion; T1078, T1486, T1567, T1041  
2. **State-Sponsored Intrusions (APT):** T1095, T1055, T1547, T1027  
3. **Data Exfiltration Campaigns:** T1213, T1114, T1039  
4. **Credential Compromise & Lateral Movement:** T1003, T1555, T1021, T1046  

### Key Threat Actors & Campaigns
- **Akira Ransomware:** RaaS, VPN compromise, lateral movement, exfiltration before encryption  
- **APT17:** China-based, spear-phishing, stealthy long-term espionage  
- **POLONIUM:** Lebanon-based, credential compromise, custom malware, stealth exfiltration  

### Common Tools & TTPs
- **Malware/Tools:** Akira, MiniKatz, LaZagne, PSExec, RClone, AdFind  
- **Techniques:** Phishing, credential theft, lateral movement, data exfiltration, final ransomware impact  

### Historical Incidents & Alerts
- Akira (2023–2024), APT17 (long-term), POLONIUM (2022–2024)  
- Alerts from CISA, Arctic Wolf, Microsoft, FireEye  

---

## Task 2: National Threat Landscape Assessment

### Headquarters Country: Nigeria

**Hilalrat / UNC788**
- Phishing, credential compromise, ransomware, data theft  
- Indicators: unusual traffic, ransomware file extensions  

**Hoplight / APT38 (Lazarus Group)**
- North Korea-linked, financial cyber operations  
- Techniques: spear-phishing, process injection, encrypted C2  
- Indicators: unauthorized banking transactions, known C2 infrastructure  

---

## Task 3: Victim Profile & Threat Mapping

### Victim Profile 1: Government Institutions
- High-value target: sensitive national data, transportation, citizen records  
- Threat Actor: Chafer  
- Tools: PSExec  
- Diamond Model: Credential harvesting, lateral movement, defense evasion  
- Kill Chain: Initial access via phishing, execution via PSExec  

*(Additional victim profiles for healthcare and defense sectors follow similar analysis)*  

---

## Detection & Mitigation Recommendations per Victim

- **Government:** Enhance phishing detection, network segmentation, MFA enforcement  
- **Healthcare:** Endpoint monitoring, secure remote access, malware sandboxing  
- **Defense:** Threat hunting, log analysis, privileged account auditing  

---

## Task 4: Politically Motivated Threat Group

- **Group:** Sandworm (APT44 / Seashell Blizzard)  
- **Analysis:** Diamond Model, Kill Chain, Campaign Review  
- **Targets:** Energy and government sectors  
- **Recommendation:** Continuous monitoring, threat intelligence sharing, ICS/SCADA defenses  

---

## Detection, Monitoring & Defensive Considerations

- Deploy multi-layer detection and correlation  
- Regularly update IoCs from OTX  
- Maintain network segmentation and endpoint hardening  
- Apply MITRE ATT&CK mapping for active threats  

---

## Executive Impact & Strategic Recommendations

- Use intelligence to inform executive decision-making  
- Prioritize defenses based on sector-specific threats  
- Maintain operational readiness for politically motivated actors  
- Continue investment in CTI infrastructure and analyst training  

---

## Lessons Learned

- Continuous enrichment from community feeds enhances detection  
- Dockerized OpenCTI ensures modularity and scalability  
- Network and access controls are critical for SOC-like operations  
- Realistic exercises improve cross-team collaboration and awareness  

---

## References

- MITRE ATT&CK Framework  
- OpenCTI Documentation  
- AlienVault OTX API Documentation  
- CISA and Arctic Wolf Threat Advisories  
- Microsoft & FireEye TTP Reports  

---

## Appendices

**Appendix A:** Sprint Timeline & Meetings  
**Appendix B:** Team Contributions  


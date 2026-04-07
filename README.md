# SOC Lab by Axis Security Solutions

**Free, browser-based SOC analyst training platform built for aspiring and early-career cybersecurity professionals.**

No installation. No account. No backend. No data collection. Open the link and start training.

🔗 **Live Platform:** (https://github.com/axissecuritylabs/axis-security-soc-lab)

---

## Overview

SOC Lab is a hands-on simulation environment designed to bridge the gap between cybersecurity certifications and real-world SOC work. Most entry-level candidates have completed Security+, taken a bootcamp, or watched hours of training content — but have never actually triaged an alert, enriched a log, or worked an IR case from containment to lessons learned. That gap is what this platform closes.

Built and maintained by Axis Security Solutions, SOC Lab puts you through the same decision-making process a working analyst faces every shift. Every alert requires you to read raw log data, enrich indicators, form a hypothesis, make a triage decision, and document your reasoning. The platform coaches you on every outcome — including when you're wrong.

Everything runs locally in your browser using localStorage. No data leaves your device. No account required. No tracking.

---

## Platform Architecture

Single HTML file. No framework. No build step. No dependencies. Drop it in a browser and it works.

State is managed entirely through localStorage — your alert decisions, case files, IR actions, lessons learned drafts, and portfolio data persist across sessions on your device. Clearing your browser storage resets the environment.

---

## Feature Breakdown

### Alert Queue
The core of the platform. 76+ realistic alerts spanning Tier 1 and Tier 2 categories. Each alert presents a raw log block mirroring what you would see in a real SIEM — Proofpoint, CrowdStrike Falcon, Azure AD, Zscaler, Sysmon, and more.

**Workflow per alert:**
- Read the raw log and correlated sim log timeline
- Fill in structured enrichment fields: source IP, destination, host, user, process, analyst notes
- Navigate four tabs: Triage, Investigation, MITRE + CTI, Detection Tuning
- Make a decision: Escalate, Investigating, False Positive, or Needs Monitoring
- Receive coaching on your decision with TP/FP rate context and technique explanation

**Alert categories include:**
- Phishing and BEC
- Credential attacks and identity anomalies
- Malware execution and encoded command lines
- Lateral movement and privilege escalation
- Domain controller attacks and credential dumping
- Ransomware and data destruction
- Insider threat and DLP violations
- Cloud misconfiguration and IAM abuse
- C2 beaconing and DNS anomalies
- Persistence mechanisms
- Threat intelligence and CTI-enriched scenarios

Each alert includes MITRE ATT&CK technique mapping, threat actor associations, enrichment tool guidance, and a structured investigation checklist.

---

### Interactive Investigation Checklist
Every alert has a task-gated investigation checklist. Steps cannot be marked complete by clicking a checkbox — you must write a substantive answer to a contextual question first. Minimum character count is enforced. Completing each step reveals a coaching panel explaining why that step matters operationally and what it reveals about the attack.

---

### File Viewer
Applicable alerts include an intercepted file tab that opens a simulated file viewer. DLP alerts show spreadsheet content with flagged columns highlighted by severity — CRITICAL for SSN fields, HIGH for salary data. Malware alerts show decoded PowerShell payloads with dangerous functions highlighted: `DownloadString`, `Invoke-Expression`, `Register-ScheduledTask`. DLP violation summaries appear below the file with per-finding explanations.

---

### Network Connection Maps
Applicable alerts include an SVG network diagram showing the full connection path: source endpoint → proxy → external destination, with threat labels, edge annotations, port/volume data, and a timestamped connection timeline. Used on geo-anomaly identity alerts, C2 beaconing cases, and lateral movement kill chains.

---

### Incident Response Console
Escalated alerts funnel into a full IR lifecycle simulation following the NIST SP 800-61 framework.

**Four phases, each gated by completion of the prior:**

**Containment** — Stop the spread. Isolate hosts, disable accounts, block IPs and domains, block hashes, revoke sessions, preserve evidence. Every action is logged with a timestamp. Six pre-built alert contexts provide recommended action sets with pre-populated targets pulled from the alert's IOC data.

**Eradication** — Remove the threat. Remove scheduled tasks, rotate KRBTGT (with correct double-reset guidance), reset credentials, apply blocks. Recommended eradication steps are alert-specific.

**Recovery** — Restore operations. All reversible containment actions (host isolation, account disables, IP/domain blocks, hash blocks) can be reversed individually from this phase with a single click. Each reversal is logged. Rebuild from image and patch actions available for affected hosts.

**Lessons Learned** — Formal post-incident documentation. Six required sections with enforced minimum word counts:
- Incident Timeline (50 words minimum)
- Root Cause Analysis (40 words)
- Detection Gap Assessment (40 words)
- Containment and Eradication Actions Taken (40 words)
- Deconfliction Notes (30 words — required field for documenting whether any legitimate or authorized activities were involved)
- Recommendations (40 words)

Every keystroke auto-saves the draft. Word counts update live. Submission is gated — all six sections must meet minimums. Submitted reports appear in the Portfolio Builder.

**Action log** — A running timestamped record of every action taken across all IR cases in the session, including reversals shown with strikethrough.

---

### Detection Engineering Lab
Three fully interactive guided demos plus independent practice tabs for writing and tuning rules.

**Demo 1: Office Macro Spawning PowerShell (T1059.001)**
Seven steps. Data source identification via multiple choice. Indicator type selection (static vs behavioral vs statistical). Office executable coverage via checkbox grid — all eight apps must be identified. TP/TN/FP scenario classification (five scenarios). Write-your-own Sigma rule textarea — minimum 30 characters required before the reference answer reveals. Reference answer includes design decision explanations. Tune and deploy phase with test results and FP tuning decisions.

**Demo 2: DNS-Based C2 Beaconing (Statistical Detection)**
Same interactive format. Multiple choice selects DNS security logs as primary source. Statistical indicator type selection with explanation of why IOC-based DNS blocking fails. Multi-select exercise identifying six beacon characteristics (timing regularity, after-hours activity, newly registered domain, single target, high-entropy subdomain, NXDOMAIN rotation). TP/TN/FP classification including OneDrive token refresh and developer test suite FP cases. Write-your-own SPL rule using stddev_interval, domain_age lookup, and allowlist logic.

**Demo 3: Persistence via Scheduled Task and Registry Run Key (T1053.005 / T1547.001)**
Same format. Event 4698 and Sysmon Event 13 data source selection. Path-based behavioral indicator type. Checkbox exercise identifying five user-writable suspicious paths vs System32/Program Files. TP/TN/FP classification including SCCM bulk deployment, Adobe Run key, and Chocolatey package manager cases. Write-your-own dual Sigma rule covering both task and registry persistence.

---

### Threat Hunt Lab
Five hunt categories: Credential Access, Lateral Movement, Persistence, Exfiltration, and C2. Each hunt presents a hypothesis, correlated log data with Sysmon event timelines, and structured questions requiring written answers. Validation hints reveal after each step.

---

### Forensics Lab
Seven tabs: Introduction, Memory Forensics, Log Analysis, YARA Rule Writing (eight exercises), Network Forensics, Cloud Forensics, and Automation. YARA exercises require writing functional rule syntax. Validation checks the structure before marking complete.

---

### Endpoint Activity Monitor
Eight endpoints drawn directly from the alert library: CORP-WKS-033, WKS-FINANCE-007, DC01, HR-WKS-012, EXEC-WKS-002, SALES-WKS-023, FILE-SVR-01, and LEGAL-WKS-031. Each card shows live status computed from current alert state — a COMPROMISED endpoint clears to CLEAN with a green resolved banner when all associated alerts are closed as false positive. Expandable cards show suspicious process lists, timestamped activity timelines, containment status, and direct links that open the associated alert modal.

---

### Identity Dashboard
47 user profiles across all departments. Risk scoring is computed live from alert state — profiles under active alert show ALERT status in red, profiles whose alerts have been resolved clear to NORMAL automatically. Department filter tabs (12 departments) compose with the search bar. Each card shows role, account type, MFA method, typical hours, risk indicators, analyst context notes, and clickable alert references. Alert count badges on card headers make the dashboard scannable before expanding.

---

### MITRE ATT&CK Navigator
Color-coded heatmap showing technique coverage across your triaged alerts. Each tactic column uses a distinct color. Covered techniques highlight in the tactic color. Total coverage count shown. Full technique detail view on the MITRE + CTI tab inside each alert modal.

---

### Workbench and Case Files
Four completed demo case files (two T1, two T2) showing what a fully documented investigation looks like — complete timeline, enrichment summary, IOC extraction, containment actions, and analyst notes. Your active cases populate below the demo cases as you work alerts.

---

### Portfolio Builder
Generates a formatted professional summary of your training activity: alerts triaged, MITRE techniques covered, false positive identification rate, case files documented, and a LinkedIn-ready paragraph you can adapt for your profile or use in interview prep conversations.

---

### Analyst Guide
SOC fundamentals reference covering triage methodology, escalation criteria, enrichment tool usage, the IR lifecycle, and common interview topics organized by domain.

---

## Alert Volume and Coverage

| Category | Count |
|---|---|
| Tier 1 alerts | 46 |
| Tier 2 alerts | 30 |
| Informational / benign | 5 |
| **Total** | **76+** |

MITRE ATT&CK techniques covered span Initial Access, Execution, Persistence, Privilege Escalation, Defense Evasion, Credential Access, Discovery, Lateral Movement, Collection, Command and Control, and Impact.

---

## Who This Is For

**Entry-level candidates** who have Security+ or equivalent but no professional SOC experience and need structured hands-on reps before interviews.

**Junior analysts** (0 to 2 years) who want deliberate practice outside work hours on alert types they do not see regularly in their current role.

**Career changers** entering cybersecurity from IT, networking, help desk, or adjacent fields who understand the concepts but need to build analyst instinct.

**Bootcamp graduates** who completed technical training but need to practice the documentation and decision-making layer that bootcamps often skip.

**Students** in cybersecurity programs who want something more realistic than a lab environment.

---

## What This Is Not

This is not a certification prep tool. It is not a substitute for real SOC experience. It does not simulate actual network traffic or live tooling. Alert logs are realistic but synthetic. The goal is to build decision-making instinct, documentation habits, and familiarity with analyst workflow — not to replicate any specific vendor product.

---

## Beta Status

This platform is in open beta. Core features are stable. If you encounter a broken button, rendering issue, or content error, open an issue on this repository with:
- What you were doing
- What browser and device you were using
- What you expected vs what happened

Feature requests and curriculum feedback are also welcome via issues.

---

## Built By

**Axis Security Solutions**

Cybersecurity consulting and career services firm delivering resume writing, LinkedIn optimization, interview preparation, workforce development training, and onboarding guidance to cybersecurity professionals from entry level through senior. Clients span SOC, GRC, IAM, DFIR, cloud, and IT fields.

Led by Ciera Stroman, a cybersecurity professional with 8+ years in the technical field, specializing in defensive and offensive security domains. The Axis Security Solutions team is comprised of seasoned cybersecurity professionals across multiple disciplines to bridge the gap for hands on cybersecurity training and development. Our instructors and consultants come from diverse backgrounds and hold numerous educational accolades. Our team prioritizes in-house training with legitimate resources that align with today's threat landscape. 

🌐 [axissecuritysolutions.com](https://axissecuritysolutions.com)
connec with Ciera here: [https://www.linkedin.com/in/cieracstroman/](url)

*"Axis Security Solutions" is not licensed under CC0 and may not be used to endorse derivative works or imply affiliation without written permission.*

---

## License

CC0 1.0 Universal — Public Domain Dedication

The SOC Lab platform code and curriculum content have been dedicated to the public domain under CC0 1.0. You may copy, modify, distribute, and use the work without asking permission.

The name **Axis Security Solutions** and associated branding are excluded from this dedication and remain the intellectual property of their owner.

See the LICENSE file for full legal text.

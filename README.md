# 🛡️ SOC-AI Journey  
AI-powered SOC Analyst Practice – Daily Log Analysis, Threat Detection Tasks, MITRE Mapping, KQL Queries, Python Automation, and Incident Response Notes.

This repository is my structured, day-by-day practice toward becoming a SOC Analyst.  
Each day contains:
- A realistic dataset (Windows/Linux logs)  
- Manual investigation + AI-assisted analysis  
- SOC-style findings and summary  
- Documentation stored inside **AI-Tasks/Day-X/**  

---

# 📅 Daily Progress (AI Tasks Only)

### ✔ Day 1 — Basic Log Observation  
- Introduced to simple login attempts  
- Identified normal vs failed patterns  
- Basic SOC-style summary  
📁 `AI-Tasks/Day-1/day1-analysis.md`

---

### ✔ Day 2 — Auth Log Parsing  
- Analyzed Linux `auth.log` sample  
- Identified failed logins, invalid users  
- Detected brute force activity  
📁 `AI-Tasks/Day-2/day2-analysis.md`

---

### ✔ Day 3 — Advanced Attack Pattern Detection  
- Multi-stage brute-force detection  
- Username rotation patterns  
- Correlated timestamps and attack sequences  
📁 `AI-Tasks/Day-3/day3-analysis.md`

---

### ✔ Day 4 — Windows Event Log Analysis  
- Analyzed Windows Event IDs (4624, 4625, 4672)  
- Identified internal & external brute-force attempts  
- Classified privileged logon behavior  
📁 `AI-Tasks/Day-4/day4-analysis.md`

---

### ✔ Day 5 — Cross-Platform Brute Force Investigation  
- Correlated Windows and Linux authentication logs  
- Identified successful brute-force attack  
- Detected privileged account compromise (Event ID 4672)  
- Mapped activity to MITRE ATT&CK (T1110, T1078)  
📁 `AI-Tasks/Day-5/day5-analysis.md`

---

### ✔ Day 6 — Detection Logic & Alert Threshold Analysis  
- Differentiated alert-worthy vs normal authentication behavior  
- Designed threshold-based detection rules  
- Focused on false-positive reduction  
- Applied SOC alert logic and MITRE mapping  
📁 `AI-Tasks/Day-6/day6-analysis.md`

---

### ✔ Day 7 — Privilege Escalation & Suspicious Command Analysis  
- Identified Linux and Windows privilege escalation techniques  
- Detected persistence via SUID and admin group modification  
- Analyzed encoded PowerShell abuse  
- Mapped post-exploitation activity to MITRE ATT&CK  
📁 `AI-Tasks/Day-7/day7-analysis.md`

---

### ✔ Day 8 — Suspicious Network Behavior & Early Attack Indicators  
- Detected external reconnaissance targeting SSH services  
- Identified suspicious internal east–west traffic  
- Analyzed early-stage attack indicators at the network layer  
- Mapped network activity to MITRE ATT&CK techniques  
📁 `AI-Tasks/Day-8/day8-analysis.md`

---

# 🎯 Purpose of This Repository  
This repo simulates **daily SOC analyst work**, including:

### 🔹 Log Analysis  
Identifying suspicious behavior from Windows & Linux logs  
(4625 failed logons, SSH brute-force, service account abuse)

### 🔹 Threat Detection  
Recognizing brute force, reconnaissance, privilege escalation, and lateral movement attempts.

### 🔹 MITRE ATT&CK Mapping  
Understanding attacker techniques and TTP alignment.

### 🔹 SIEM & KQL Preparation  
Early practice for Azure Sentinel and ELK-style workflows.

### 🔹 Python for SOC Automation  
Future scripts for log filtering, enrichment, correlation, etc.

### 🔹 Incident Response Notes  
Writing professional SOC reports and summaries.

---

# 🚀 Upcoming Work (Day 9–Day 60)  
- Advanced Linux/Windows hybrid analysis  
- Detection engineering rules (network, brute force, privilege abuse)  
- MITRE ATT&CK tagging at scale  
- KQL query library  
- Python enrichment scripts  
- Full SOC report templates  
- Alert → Investigation → Summary workflow

---

# ⭐ Learning in Public  
This repo is a growing timeline of my SOC journey — every day builds toward becoming a job-ready SOC Analyst.

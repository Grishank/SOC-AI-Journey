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

# 📁 Repository Structure
SOC-AI-Journey/
│
├── AI-Tasks/
│ ├── Day-1/
│ ├── Day-2/
│ ├── Day-3/
│ ├── Day-4/
│ └── Day-X/ (future)
│
├── SOC-Theory/
│ ├── SOC-Basics.md
│ ├── Types-of-Logs.md
│ ├── Threat-Intel-Notes.md
│ └── MITRE-ATTACK.md
│
├── KQL-Queries/
│ └── README.md
│
├── Python-Automation/
│ └── README.md
│
└── Incident-Reports/
└── README.md

---

# 🎯 Purpose of This Repository  
This repo simulates **daily SOC analyst work**, including:

### 🔹 Log Analysis  
Identifying suspicious behavior from Windows & Linux logs  
(4625 failed logons, SSH brute-force, service account abuse)

### 🔹 Threat Detection  
Recognizing brute force, reconnaissance, and privilege escalation attempts.

### 🔹 MITRE ATT&CK Mapping  
Understanding attacker techniques and TTP alignment.

### 🔹 SIEM & KQL Preparation  
Early practice for Azure Sentinel and ELK-style workflows.

### 🔹 Python for SOC Automation  
Future scripts for log filtering, enrichment, correlation, etc.

### 🔹 Incident Response Notes  
Writing professional SOC reports and summaries.

---

# 🚀 Upcoming Work (Day 5–Day 60)  
- Day 5: Windows Event Correlation + Failed Logon Heatmaps  
- Day 6: Brute Force Detection Engineering  
- Day 7–10: Linux/Windows hybrid analysis  
- MITRE ATT&CK tagging  
- KQL query library  
- Python enrichment scripts  
- Full SOC report templates  
- Alert → Investigation → Summary workflow

---

# ⭐ Learning in Public  
This repo is a growing timeline of my SOC journey — every day builds toward becoming a job-ready SOC Analyst.




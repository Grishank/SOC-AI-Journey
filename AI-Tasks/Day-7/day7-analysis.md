# 🔍 Day 7 — Privilege Escalation & Suspicious Command Analysis (Linux + Windows)

---

## **1. Observed High-Risk Linux Activity**

### **Linux Command & Authentication Logs**

| Timestamp | User | Command | Risk |
|---------|------|---------|------|
| 11:02:11 | john | `sudo su` | Privilege escalation attempt |
| 11:02:13 | john → root | `/bin/su` | Switched to root |
| 11:02:15 | root | `cat /etc/shadow` | Credential access |
| 11:15:44 | john | `chmod +s /bin/bash` | Persistent privilege escalation |
| 11:15:46 | john | `/bin/bash -p` | Root shell execution |

**Interpretation:**  
These commands indicate **successful privilege escalation** followed by **credential access** and **persistence creation** using the SUID bit.

---

## **2. Observed High-Risk Windows Activity**

### **Windows Process Creation Events (Event ID 4688)**

| Timestamp | Account | Process | Command | Risk |
|---------|---------|---------|---------|------|
| 11:05:21 | john | powershell.exe | `powershell -enc SQBFAFgA...` | Obfuscated execution |
| 11:05:25 | john | cmd.exe | `whoami /priv` | Privilege enumeration |
| 11:05:29 | john | net.exe | `net localgroup administrators john /add` | Privilege escalation |

**Interpretation:**  
The user executed **encoded PowerShell**, enumerated privileges, and added themselves to the **Administrators group**, confirming escalation on Windows.

---

## **3. Privilege Escalation Indicators**

### **Linux**
- Use of `sudo` and `su`
- Reading `/etc/shadow`
- Setting **SUID bit** on `/bin/bash`
- Launching privileged shell (`bash -p`)

### **Windows**
- Encoded PowerShell execution (`-enc`)
- Privilege enumeration
- Group membership modification

---

## **4. Highest-Risk Event Identified**

### 🚨 Critical Event
chmod +s /bin/bash

**Why this is critical:**
- Grants root access to any user
- Establishes persistence
- Survives reboot
- Often overlooked without integrity monitoring

**SOC Severity:** **CRITICAL**

---

## **5. MITRE ATT&CK Mapping**

### **Linux**
- **T1548** — Abuse Elevation Control Mechanism  
- **T1059.004** — Unix Shell  
- **T1547** — Persistence  

### **Windows**
- **T1059.001** — PowerShell  
- **T1136** — Modify Account Privileges  
- **T1078** — Valid Accounts  

---

## **6. SOC Risk Assessment**

This activity represents a **post-exploitation phase** with:
- Confirmed privilege escalation
- Credential access
- Persistence mechanisms
- Cross-platform impact (Linux + Windows)

This is **not reconnaissance** — it is **active system compromise**.

---

## **7. Recommended SOC Response Actions**

1. **Immediately isolate affected hosts** (Linux and Windows)  
2. **Remove persistence mechanisms**
   - Remove SUID bit from `/bin/bash`
   - Remove user from Administrators group  
3. **Reset compromised credentials**  
4. **Conduct forensic analysis** for additional backdoors  
5. **Consider system rebuild** if integrity cannot be assured  

---

## 🔐 **SOC Summary**

A confirmed privilege escalation event was detected involving both Linux and Windows systems.  
The attacker successfully escalated privileges, accessed sensitive credential files, and established persistence.

The use of **SUID backdoors**, **encoded PowerShell**, and **administrator group modification** indicates a **high-confidence compromise** requiring immediate incident response.

This scenario demonstrates real-world **post-exploitation detection and response** responsibilities of a SOC analyst.

---

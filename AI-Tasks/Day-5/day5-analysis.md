# 🔍 Day 5 — Cross-Platform Brute Force Investigation (Windows + Linux)

---

## **1. Observed Authentication Failures**

### **Windows Security Events**
Multiple failed login attempts were observed against a privileged account before a successful login.

| Timestamp | Event ID | Account | Source IP | Notes |
|----------|----------|---------|-----------|-------|
| 09:12:11 | 4625 | admin | 192.168.1.45 | Failed login (Bad password) |
| 09:12:18 | 4625 | admin | 192.168.1.45 | Failed login |
| 09:12:25 | 4625 | admin | 192.168.1.45 | Failed login |
| 09:12:33 | 4625 | admin | 192.168.1.45 | Failed login |
| 09:12:41 | 4625 | admin | 192.168.1.45 | Failed login |

---

### **Linux SSH Authentication Failures**
The same source IP targeted the Linux server via SSH using the root account.

| Timestamp | Account | Source IP | Result |
|---------|---------|-----------|--------|
| 09:10:01 | root | 192.168.1.45 | Failed password |
| 09:10:05 | root | 192.168.1.45 | Failed password |
| 09:10:09 | root | 192.168.1.45 | Failed password |
| 09:10:14 | root | 192.168.1.45 | Failed password |

---

## **2. Successful Authentication Detected**

### **Windows**
| Timestamp | Event ID | Account | Source IP | Notes |
|----------|----------|---------|-----------|-------|
| 09:12:55 | **4624** | admin | 192.168.1.45 | Successful login |

### **Linux**
| Timestamp | Account | Source IP | Result |
|---------|---------|-----------|--------|
| 09:10:19 | root | 192.168.1.45 | **Accepted password** |

**Interpretation:**  
Repeated authentication failures followed by a successful login indicate a **successful brute-force attack**.

---

## **3. Privileged Activity Identified**

| Timestamp | Event ID | Account | Details |
|----------|----------|---------|---------|
| 09:13:02 | **4672** | admin | Special privileges assigned (SeDebugPrivilege, SeTcbPrivilege) |

**Interpretation:**  
Event ID **4672** confirms that the compromised Windows account has **high-level administrative privileges**, significantly increasing impact.

---

## **4. Cross-Platform Correlation**

- Same source IP: **192.168.1.45**
- Same attack pattern:  
  - Multiple failed attempts  
  - Eventual successful authentication  
- Targets:
  - Windows → `admin`
  - Linux → `root`

**Conclusion:**  
This is a **coordinated brute-force attack** across multiple operating systems using high-value accounts.

---

## **5. Attack Classification**

### **Attack Type**
- Brute Force Authentication Attack

### **MITRE ATT&CK Mapping**
- **T1110 — Brute Force**
- **T1110.001 — Password Guessing**
- **T1078 — Valid Accounts** (post-compromise)

---

## **6. SOC Risk Assessment**

This activity is **high risk** because:
- A brute-force attempt **succeeded**
- The compromised account holds **administrative privileges**
- Both **Windows and Linux systems** were accessed
- Root and admin accounts were targeted

This indicates a **confirmed account compromise**, not a misconfiguration or user error.

---

## **7. Recommended SOC Response Actions**

1. **Immediately escalate** to Incident Response due to privileged account compromise  
2. **Isolate or block source IP** `192.168.1.45`  
3. **Force password resets** for affected accounts  
4. **Review lateral movement and persistence indicators**  
5. **Enable account lockout and brute-force detection rules**

---

## 🔐 **SOC Summary**

A coordinated brute-force attack originating from **192.168.1.45** targeted privileged accounts on both Windows and Linux systems.  
Repeated authentication failures were followed by successful logins, confirming account compromise.

The presence of **Event ID 4672** confirms elevated privileges on the Windows host, increasing the severity and potential impact.

Immediate incident response actions are required to contain the threat, remediate compromised credentials, and prevent further exploitation.

---

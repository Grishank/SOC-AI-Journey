# 🔍 Day 6 — Detection Logic & Alert Threshold Analysis (Windows + Linux)

---

## **1. Observed Authentication Activity**

### **Windows Security Events**
Multiple failed login attempts were observed against a privileged account from a single internal IP.

| Timestamp | Event ID | Account | Source IP | Notes |
|----------|----------|---------|-----------|-------|
| 10:01:11 | 4625 | admin | 10.0.0.45 | Failed login (Bad password) |
| 10:01:18 | 4625 | admin | 10.0.0.45 | Failed login |
| 10:01:25 | 4625 | admin | 10.0.0.45 | Failed login |
| 10:01:33 | 4625 | admin | 10.0.0.45 | Failed login |
| 10:01:41 | 4625 | admin | 10.0.0.45 | Failed login |

---

### **Linux SSH Authentication Activity**
The same source IP attempted repeated SSH logins using a privileged account.

| Timestamp | Account | Source IP | Result |
|---------|---------|-----------|--------|
| 10:02:01 | root | 10.0.0.45 | Failed password |
| 10:02:05 | root | 10.0.0.45 | Failed password |
| 10:02:09 | root | 10.0.0.45 | Failed password |
| 10:02:14 | root | 10.0.0.45 | Failed password |

---

### **Normal User Activity**
A separate user shows typical authentication behavior.

| Timestamp | Event ID | Account | Source IP | Notes |
|----------|----------|---------|-----------|-------|
| 10:05:12 | 4625 | john | 10.0.0.12 | Single failed attempt |
| 10:05:55 | 4624 | john | 10.0.0.12 | Successful login |

**Interpretation:**  
User `john` demonstrates normal login behavior (mistyped password followed by success).

---

## **2. Alert vs Non-Alert Classification**

### **Alert-Worthy Activity**
- Account: `admin`
- Source IP: `10.0.0.45`
- Pattern:
  - Multiple failed logins
  - Short time window
  - Privileged account
  - Cross-platform targeting (Windows + Linux)

**Conclusion:**  
This activity should trigger a **SOC alert**.

---

### **Non-Alert Activity**
- Account: `john`
- Pattern:
  - Single failure
  - Successful login shortly after
  - No repetition

**Conclusion:**  
This activity should be logged and monitored, but **not alerted**.

---

## **3. Detection Threshold Logic**

### **Windows Brute-Force Detection Rule**
Trigger an alert if:
- **≥ 5 failed logon events (Event ID 4625)**
- From the **same IP**
- Targeting the **same account**
- Within **5 minutes**

Increase severity if:
- Target account is **admin or service account**

---

### **Linux SSH Brute-Force Detection Rule**
Trigger an alert if:
- **≥ 4 SSH failed password attempts**
- From the **same IP**
- Within **2–3 minutes**
- Targeting `root` or privileged users

---

## **4. Attack Classification**

### **Attack Type**
- Brute Force Authentication Attempt

### **MITRE ATT&CK Mapping**
- **T1110 — Brute Force**
- **T1110.001 — Password Guessing**
- **T1078 — Valid Accounts** *(if access is later gained)*

---

## **5. SOC Risk Assessment**

This activity is **high risk** because:
- Privileged accounts are targeted
- Repeated failures indicate automation
- Same IP targets multiple platforms
- Pattern matches known brute-force behavior

This represents an **attempted compromise**, requiring immediate detection and response.

---

## **6. False Positive Considerations**

Before enabling alerts in production, consider:
- Users mistyping passwords
- Admin scripts using outdated credentials
- Services retrying after password changes
- IT troubleshooting from known admin IPs

**Mitigation:**
- Apply thresholds
- Use time-window correlation
- Exclude trusted IP ranges

---

## **7. Recommended SOC Actions**

1. Trigger a **high-severity alert** for privileged account brute-force attempts  
2. **Escalate** to senior SOC / IR team if threshold is met  
3. Temporarily **block or rate-limit source IP**  
4. Review authentication logs for lateral movement  
5. Enforce account lockout policies

---

## 🔐 **SOC Summary**

A detection-worthy brute-force pattern was identified targeting the privileged account `admin` from IP **10.0.0.45** across both Windows and Linux systems.  
Threshold-based correlation confirms malicious intent rather than user error.

This task demonstrates the importance of **alert logic, thresholds, and false-positive reduction** in real-world SOC environments.

---

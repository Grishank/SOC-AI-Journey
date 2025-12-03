# 🔍 Day 4 — Windows Event Log Analysis (Failed Logons + Privileged Activity)

---

## **1. Failed Login Attempts (Per IP)**

| Source IP         | Attempts | Target Users           | Notes                              |
|-------------------|----------|------------------------|------------------------------------|
| **192.168.1.45**  | 3        | guest                  | Internal brute forcing             |
| **185.66.12.9**   | 4        | admin                  | External brute force attack        |
| **192.168.1.200** | 2        | backup                 | Internal failed attempts           |
| **89.44.12.18**   | 3        | svc_system             | External targeting service account |

---

## **2. Brute Force Clusters Identified**

These IPs attempted repeated failed logins in short intervals:

- **192.168.1.45** → guest  
- **185.66.12.9** → admin  
- **89.44.12.18** → svc_system  

Each shows rapid failures → **automated/scripted brute force activity**.

---

## **3. Account-Level Observations**

### **Suspicious Accounts**
| Username         | Reason                                                    |
|------------------|-----------------------------------------------------------|
| **guest**        | Repeated failures; common brute-force target              |
| **admin**        | External brute-force attempts                             |
| **svc_system**   | Service account targeted by external IP                   |

### **Possibly Normal**
| Username   | Reason                                                          |
|------------|-----------------------------------------------------------------|
| **backup** | One successful login + later failures → may be misconfiguration |

### **Legitimate Accounts**
- **grishank** → 2 successful logons, no failures  
- **Administrator** → Privileged local login (expected behavior)

---

## **4. Event ID Breakdown**

| Event ID | Meaning                              | Count | Notes                                |
|----------|--------------------------------------|-------|------------------------------------- |
| **4625** | Failed logon                         | 12    | Used in brute-force attempts         |
| **4624** | Successful logon                     | 3     | Normal system/user logons            |
| **4672** | Privileged logon                     | 1     | Administrator with elevated rights   |

**Interpretation:**  
Heavy failed-logon activity (4625) alongside normal successful logons.

---

## **5. Internal vs External IP Behavior**

### **Internal IPs**
- `192.168.1.45` → guest brute force  
- `192.168.1.99` → successful login for backup  
- `192.168.1.200` → failed attempts on backup  
- `10.0.0.55` → RDP-style login by grishank  
- `127.0.0.1` → Administrator local privileged login  

**Interpretation:** Mostly normal internal traffic except repeated failures on guest.

---

### **External IPs**
- `185.66.12.9` → 4 failed attempts on admin  
- `89.44.12.18` → 3 failed attempts on svc_system  

**Interpretation:** Both show patterns of **active brute-force attacks** from outside the network.

---

## **6. Normal vs Suspicious Logon Behavior**

### **Normal**
- **Administrator** → Privileged login from localhost  
- **grishank** → Consistent successful logons, no anomalies  

### **Suspicious**
- **guest** → Internal repeated failures  
- **admin** → External brute force  
- **svc_system** → External targeting  
- **backup** → Mixed behavior → monitor

---

# 🔐 **7. SOC Summary**

Multiple unauthorized login attempts were detected across internal and external IPs.  
External IPs **185.66.12.9** and **89.44.12.18** attempted brute-force attacks on *admin* and *svc_system*, indicating targeted external threat activity.  
Internal IP **192.168.1.45** repeatedly attempted to access the *guest* account, suggesting internal probing or misuse.

A privileged logon (4672) by **Administrator** occurred from localhost and appears legitimate.  
User **grishank** shows normal, successful logon behavior with no failed attempts.

While no unauthorized access succeeded, the failed sequences indicate **active brute-force reconnaissance**.  
Recommended actions: block malicious IPs, enable account lockout policies, and monitor service accounts closely.

---

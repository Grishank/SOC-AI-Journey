
## 🔍 Day 3 — Advanced SOC Log Analysis (Pattern + Correlation)

### **1. Failed Login Attempts (Per IP)**

| IP Address         | Attempts | Notes                      |
|--------------------|----------|-----------------------------|
| **203.0.113.56**   | 6        | Multi-stage brute force     |
| **198.51.100.22**  | 5        | Invalid user + root attack  |
| **203.0.113.140**  | 4        | Alternating admin/root      |

---

### **2. Brute Force Clusters Identified**
These IPs attempted ≥3 failed logins in a short time window:

- **203.0.113.56**
- **198.51.100.22**
- **203.0.113.140**

---

### **3. Multi-Stage Attacks**
Attackers changing usernames = escalation behavior.

- **203.0.113.56**  
  - 3× failed as *admin*  
  - then 3× failed as *root*  
  → **Credential escalation attempt**

- **198.51.100.22**  
  - 2× failed as *invalid user “backup”*  
  - then 3× failed as *root*  
  → **Recon → root attack**

- **203.0.113.140**  
  - 2× failed as *root*  
  - 2× failed as *admin*  
  → **Automated username rotation**

---

### **4. Suspicious Usernames**
| Username              | Reason                               |
|----------------------|----------------------------------------|
| **root**             | High-value target                      |
| **admin**            | Common brute-force target              |
| **invalid user backup** | Attackers scanning for weak accounts |

**Legitimate users:**  
- `dev` (valid password login)  
- `developer` (valid publickey login)

---

### **5. Legitimate System Activity**
- **Accepted password** for `dev` → 192.168.1.22  
- **sudo command** by admin → installing apache2  
- **Accepted publickey** for `developer` → 192.168.1.50  

No malicious activity from internal IPs.

---

### **6. Time-Based Correlation**
- Multiple attacks happened within **seconds** → automated tools.
- All attempts reused the **same ports** → single attacking script.
- Attackers returned after short gaps → persistent targeting.
- Final cluster (198.51.100.22) failed 3 times within **5 seconds**.

---

## 🔐 **7. SOC Summary**

Multiple coordinated brute-force attempts were detected from three external IPs.  
IP **203.0.113.56** performed a clear multi-stage attack, first targeting *admin* and then escalating to *root*.  
IP **198.51.100.22** attempted access using an invalid user (“backup”), followed by repeated root attacks, indicating reconnaissance followed by escalation.  
IP **203.0.113.140** alternated between admin and root, consistent with automated username-rotation scripts.  

All brute-force sequences occurred within seconds or minutes, using the same ports, confirming the presence of automated attack tools.  
Legitimate activity was observed only from internal users (`dev`, `developer`, sudo activity).  
No unauthorized access succeeded, but the event is classified as **High-Risk Brute Force Activity**, requiring IP blocking and additional monitoring.


# 🔍 Day 9 — Reconnaissance & Network Scanning Detection

---

## **1. Observed Network Activity**

### **Normal User Traffic**

| Timestamp | Source IP | Destination | Port | Action | Notes |
|--------|-----------|-------------|------|--------|------|
| 09:14:01 | 192.168.1.50 | 10.0.0.5 | 80 | ALLOW | Normal web traffic |
| 09:14:02 | 192.168.1.50 | 10.0.0.5 | 443 | ALLOW | Normal HTTPS browsing |

**Interpretation:**  
The IP `192.168.1.50` accessed standard web ports (80, 443) with limited frequency, which is consistent with normal user browsing behavior.

---

## **2. External Reconnaissance Activity**

### **Firewall Denied Connections**

| Timestamp | Source IP | Destination | Port | Action |
|--------|-----------|-------------|------|--------|
| 09:15:10 | 203.0.113.45 | 10.0.0.5 | 21 | DENY |
| 09:15:11 | 203.0.113.45 | 10.0.0.5 | 22 | DENY |
| 09:15:12 | 203.0.113.45 | 10.0.0.5 | 23 | DENY |
| 09:15:13 | 203.0.113.45 | 10.0.0.5 | 25 | DENY |
| 09:15:14 | 203.0.113.45 | 10.0.0.5 | 53 | DENY |
| 09:15:15 | 203.0.113.45 | 10.0.0.5 | 80 | DENY |
| 09:15:16 | 203.0.113.45 | 10.0.0.5 | 110 | DENY |
| 09:15:17 | 203.0.113.45 | 10.0.0.5 | 139 | DENY |
| 09:15:18 | 203.0.113.45 | 10.0.0.5 | 445 | DENY |
| 09:15:19 | 203.0.113.45 | 10.0.0.5 | 3389 | DENY |

**Interpretation:**  
The external IP `203.0.113.45` attempted connections to multiple ports in rapid succession.  
This pattern indicates **horizontal port scanning**, a common reconnaissance technique used to identify exposed services.

---

## **3. IDS Detection**

IDS ALERT — TCP Port Scan Detected
Source: 203.0.113.45
Destination: 10.0.0.5

**Interpretation:**  
Even though the firewall blocked the traffic, the IDS alert is significant because it confirms **malicious intent**.  
IDS systems help SOC teams detect attacker behavior early, before any successful compromise.

---

## **4. Suspicious Internal Network Activity**

### **East–West Traffic**

| Timestamp | Source | Destination | Port | Service |
|--------|--------|-------------|------|--------|
| 09:20:21 | 10.0.0.12 | 10.0.0.20 | 445 | SMB |
| 09:20:22 | 10.0.0.12 | 10.0.0.20 | 3389 | RDP |

**Interpretation:**  
Internal traffic accessing administrative ports (SMB and RDP) shortly after external reconnaissance is **suspicious** and requires investigation.  
While internal traffic is not automatically malicious, the timing and port selection raise concerns about possible lateral movement.

---

## **5. Targeted Systems Analysis**

The attacker targeted ports commonly associated with **Windows systems**:

- **445** — SMB (file sharing)
- **139** — NetBIOS
- **3389** — RDP (remote desktop)

This suggests the reconnaissance was focused on discovering **Windows-based services**.

---

## **6. MITRE ATT&CK Mapping**

- **T1046 — Network Service Scanning**  
- **T1021 — Remote Services (Potential)**  
- **T1110 — Brute Force (Possible Follow-Up)**  

MITRE ATT&CK helps classify attacker behavior and understand their position in the attack lifecycle.

---

## **7. SOC Alerting Decision**

| Activity | SOC Action | Reason |
|------|-----------|--------|
| External port scanning | Alert (Medium) | Reconnaissance activity detected |
| IDS scan alert | Alert | Confirms malicious intent |
| Internal admin port access | Investigate / Escalate | Possible lateral movement |

---

## 🔐 **SOC Summary**

This investigation identified external reconnaissance activity originating from `203.0.113.45`, consistent with a horizontal port scan targeting Windows services.  
Although the firewall successfully blocked the attempts, the IDS alert confirms hostile intent.

Subsequent internal traffic involving administrative ports (SMB and RDP) raises suspicion of possible post-reconnaissance activity and warrants further investigation.

Early detection at the network layer allows the SOC team to respond proactively before system compromise occurs.

---

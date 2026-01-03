# 🔍 Day 8 — Suspicious Network Behavior & Early Attack Indicators

---

## **1. Observed External Network Activity**

### **Firewall / IDS Logs**

| Timestamp | Source IP | Destination | Protocol | Port | Action |
|--------|-----------|-------------|----------|------|--------|
| 09:01:11 | 185.203.44.19 | 10.0.0.5 | TCP | 22 | DENY |
| 09:01:14 | 185.203.44.19 | 10.0.0.5 | TCP | 22 | DENY |
| 09:01:17 | 185.203.44.19 | 10.0.0.5 | TCP | 22 | DENY |
| 09:01:21 | 185.203.44.19 | 10.0.0.5 | TCP | 22 | DENY |
| 09:01:25 | 185.203.44.19 | 10.0.0.5 | TCP | 22 | DENY |

**Interpretation:**  
Repeated access attempts from the same external IP targeting **SSH (port 22)** indicate reconnaissance or an attempted initial access. This behavior is consistent with automated scanning or brute-force preparation.

---

## **2. Server-Level Network Interaction**

### **SSH Connection Attempts**

| Timestamp | Source IP | Service | Observation |
|--------|-----------|---------|-------------|
| 09:02:03 | 185.203.44.19 | SSH | Connection attempt |
| 09:02:07 | 185.203.44.19 | SSH | Repeated connection |
| 09:02:11 | 185.203.44.19 | SSH | Continued probing |

**Interpretation:**  
Even without successful authentication, repeated SSH connection attempts indicate an **initial access attempt** and should be monitored closely.

---

## **3. Suspicious Internal Network Traffic**

### **East–West Traffic Analysis**

| Timestamp | Source | Destination | Protocol | Port | Service |
|--------|--------|-------------|----------|------|---------|
| 09:10:01 | 10.0.0.15 | 10.0.0.20 | TCP | 445 | SMB |
| 09:10:04 | 10.0.0.15 | 10.0.0.20 | TCP | 3389 | RDP |
| 09:10:07 | 10.0.0.15 | 10.0.0.20 | TCP | 135 | RPC |

**Interpretation:**  
Multiple administrative service ports accessed between internal hosts in a short time window suggest **lateral movement or internal reconnaissance**, not normal user activity.

---

## **4. Attack Stage Classification**

- **External activity:** Reconnaissance / Initial Access Attempt  
- **Internal activity:** Lateral Movement / Service Discovery  

This indicates progression along the attack lifecycle.

---

## **5. MITRE ATT&CK Mapping**

### **External Activity**
- **T1046 — Network Service Scanning**
- **T1110 — Brute Force (Potential)**

### **Internal Activity**
- **T1021 — Remote Services**
- **T1087 — Account Discovery (Possible)**

---

## **6. Alerting Decision**

| Activity | Action | Reason |
|-------|--------|--------|
| External SSH attempts | Alert (Medium) | Repeated probing of sensitive service |
| Internal admin port access | Alert (High) | Indicates possible lateral movement |

Internal suspicious behavior carries **higher risk** than external scanning.

---

## **7. Recommended Preventive Controls**

1. Restrict SSH exposure (no public access, key-based auth)  
2. Implement network segmentation to limit lateral movement  
3. Enable IDS/IPS for early detection  
4. Monitor east–west traffic continuously  

---

## 🔐 **SOC Summary**

This analysis identified early-stage attack indicators involving external SSH probing followed by suspicious internal network activity.  
The combination of repeated perimeter access attempts and internal administrative port scanning strongly suggests reconnaissance progressing toward lateral movement.

Early detection at the network layer provides the opportunity to contain threats **before system compromise occurs**.

---

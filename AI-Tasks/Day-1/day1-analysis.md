## 🔍 Day 1 — Introductory Log Review (Basic Observations)

This was the first AI-based SOC task of the journey.  
The goal was to understand how logs look and identify very simple patterns.

---

### **1. What was done**
- Observed a sample Linux `auth.log`
- Identified basic log structure: timestamp, service, PID, message
- Differentiated between:
  - Successful login
  - Failed login
  - System activity

---

### **2. Key Learnings**
- Log files follow consistent formatting  
- SSH logs include user, IP, port, and authentication method  
- Failed login messages always include the username and source IP  
- Repeated failures usually indicate brute-force attempts

---

### **3. Simple Findings**
- Identified failed vs accepted login attempts  
- Identified source IP in logs  
- Understood the concept of “events” vs “noise”  

(No major attack patterns were present since this was an introductory session.)

---

### **4. SOC Summary**

Day 1 introduced core log analysis concepts.  
Reviewed basic SSH authentication logs, observed failed and successful login patterns, and understood how attackers can be identified by repeated failures. This laid the foundation for deeper log analysis on Day 2 and Day 3.


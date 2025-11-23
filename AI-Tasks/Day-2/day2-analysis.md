🔍 Day 2 — Log Analysis (Basic Anomaly Detection)
1. Total Failed Login Attempts

15 failed attempts

2. IPs with Failed Attempts
IP Address	Attempts	Notes
45.77.23.18	3	Brute force pattern
185.244.25.9	2	Probable scanning
103.145.12.7	4	Strong brute force
176.119.1.55	3	Brute force threshold met
3. Brute Force IPs Identified

45.77.23.18 → 3 attempts

103.145.12.7 → 4 attempts

176.119.1.55 → 3 attempts

Rule used:
3 or more failed SSH attempts = brute force

4. Suspicious Users
User	Why
root	Target of brute force attempts
invalid user test	Default/weak account scanning
admin	Multiple failed attempts

Legitimate Users:

admin (accepted login from 192.168.1.10)

dev (accepted login from 192.168.1.22)

5. SOC Summary

Multiple brute-force attempts were detected against the system within a short time window. A total of 15 failed SSH login attempts originated from four external IPs. IPs 103.145.12.7, 45.77.23.18, and 176.119.1.55 exhibited brute-force behavior (≥3 attempts). Attackers targeted both root and admin, as well as an invalid user, indicating scanning activity. No unauthorized access succeeded; only legitimate internal logins were observed. System experienced active external attack attempts but remained uncompromised.

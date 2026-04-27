# Enterprise Network Penetration Lab

## Overview

This project simulates an enterprise network penetration test with a focus on **service-level exploitation, lateral movement, and privilege escalation**.

The lab demonstrates how attackers leverage misconfigured services and known vulnerabilities to gain initial access, escalate privileges, and pivot across systems.

---

## Objectives

- Perform structured network reconnaissance and service enumeration  
- Identify vulnerabilities in exposed network services  
- Exploit real-world CVEs and misconfigurations  
- Achieve privilege escalation on compromised systems  
- Demonstrate **multi-service attack chaining and pivoting**  
- Produce a professional **Vulnerability Assessment & Penetration Testing (VAPT) report**  

---

## Lab Environment

| Role     | System           | IP Address      |
|----------|----------------|-----------------|
| Attacker | Kali Linux      | 192.168.109.131 |
| Target 1 | Metasploitable2 | 192.168.109.130 |
| Target 2 | Windows XP      | 192.168.109.132 |

> ⚠️ This lab is intentionally vulnerable and designed for controlled security testing.

<img width="660" height="523" alt="net_diagram" src="https://github.com/user-attachments/assets/554e1730-2e02-481b-aa6d-b83dd26c1a10" />


---

## Methodology

The assessment follows a standard penetration testing lifecycle:

1. Reconnaissance  
2. Service Enumeration  
3. Vulnerability Identification  
4. Exploitation  
5. Privilege Escalation  
6. Post-Exploitation  
7. Reporting  

---

## Attack Surface Overview

Initial reconnaissance identified multiple exposed services:

- FTP (Port 21)  
- SSH (Port 22)  
- RPC/NFS (Port 111)  
- SMB (Port 445)  

These services formed the basis for exploitation and lateral movement.

---

## Exploitation Details

### FTP — Remote Code Execution

- **Service:** vsFTPd 2.3.4  
- **CVE:** CVE-2011-2523  
- **Issue:** Backdoored service allowing unauthenticated access  
- **Impact:** Remote shell access without credentials  

---

### SMB — EternalBlue Exploit

- **Vulnerability:** MS17-010  
- **CVE:** CVE-2017-0144  
- **Issue:** SMBv1 remote code execution vulnerability  
- **Impact:** SYSTEM-level access on Windows target  

---

### SSH — Credential Brute Force & Privilege Escalation

- **Technique:** Password brute-force attack  
- **Post-Exploitation:** Sudo misconfiguration exploited  
- **Impact:** Full root access  

---

### RPC / NFS — Misconfiguration Abuse

- **Issue:** Root directory (`/`) exported to all hosts  
- **Impact:** Unauthenticated filesystem access  
- **Result:** Credential extraction and sensitive data exposure  

---

## Attack Chain & Lateral Movement

This lab demonstrates realistic attacker workflows:


FTP → Initial Access → Credential Extraction
SMB → SYSTEM Compromise → Persistence
SSH → Brute Force → Privilege Escalation
NFS → Filesystem Mount → Credential Dump → Pivoting


### Key Insight

The compromise was not due to a single vulnerability, but due to:

- Multiple exposed services  
- Weak authentication  
- Lack of segmentation  
- Poor configuration practices  

---

## Impact Assessment

- Full compromise of Linux and Windows systems  
- Credential reuse across services  
- Persistent access establishment  
- High potential for lateral movement  

**Overall Risk Rating: CRITICAL**

---

## Mitigation & Defensive Measures

- Apply regular patch management (e.g., MS17-010)  
- Disable deprecated protocols (SMBv1)  
- Enforce strong authentication policies  
- Restrict service exposure (least privilege)  
- Implement network segmentation  
- Monitor traffic and detect anomalies  

---

## Tools Used

- Nmap (Reconnaissance & Enumeration)  
- Metasploit Framework (Exploitation)  
- Hydra / Ncrack (Credential Attacks)  
- Netcat (Shell Handling)  
- John the Ripper (Password Cracking)  

---

## Key Takeaways

- Real-world attacks rely on **chaining multiple weaknesses**, not isolated exploits  
- Misconfigurations are often more critical than software vulnerabilities  
- Network segmentation plays a key role in limiting attack spread  
- Understanding **service behavior** is essential for effective penetration testing  

---

## Deliverables

- Full VAPT report (including CVE and CVSS mapping)  
- Exploitation walkthrough and documentation  
- Attack chain analysis  

---

## Disclaimer

This project was conducted in a controlled lab environment for educational purposes only.  
Do not attempt these techniques on systems without proper authorization.

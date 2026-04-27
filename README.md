# Network Service Exploitation Lab (VAPT Project)

## Overview

This project demonstrates a **full network penetration testing workflow**, focusing on the exploitation of common network services in a controlled lab environment.

The objective was to simulate real-world attack scenarios by identifying vulnerabilities, exploiting them, and chaining multiple services to achieve **full system compromise**.

---

## Objectives

* Perform structured network reconnaissance and enumeration
* Identify vulnerabilities across exposed services
* Exploit misconfigurations and known CVEs
* Achieve privilege escalation and system compromise
* Demonstrate **multi-service attack chaining**
* Produce a professional **Vulnerability Assessment & Penetration Testing (VAPT) report**

---

## Key Highlights

*  Unauthenticated Remote Code Execution (FTP backdoor)
*  SMB exploitation using EternalBlue (MS17-010)
*  SSH brute-force and privilege escalation
*  Full filesystem access via misconfigured NFS (RPC)
*  Attack chaining across multiple services
*  Detailed VAPT report with CVE & CVSS mapping

---

## Lab Environment

| Role     | System           | IP Address      |
| -------- | ---------------- | --------------- |
| Attacker | Kali Linux       | 192.168.109.131 |
| Target 1 | Metasploitable 2 | 192.168.109.130 |
| Target 2 | Windows XP       | 192.168.109.132 |

>  This environment is intentionally vulnerable and designed for learning and demonstration purposes.

---

##  Methodology

The assessment followed a standard penetration testing lifecycle:

1. Reconnaissance
2. Service Enumeration
3. Vulnerability Identification
4. Exploitation
5. Privilege Escalation
6. Post-Exploitation
7. Reporting

---

##  Services Exploited

###  FTP (Port 21)

* Vulnerable version: vsFTPd 2.3.4
* CVE: CVE-2011-2523
* Impact: Unauthenticated remote shell access

---

###  SMB (Port 445)

* Vulnerability: MS17-010 (EternalBlue)
* CVE: CVE-2017-0144
* Impact: Remote code execution as SYSTEM

---

###  SSH (Port 22)

* Weak credentials exploited via brute force
* Privilege escalation via sudo misconfiguration
* Impact: Full root access

---

###  RPC / NFS (Port 111)

* Misconfiguration: Root directory (`/`) exported to all hosts
* Impact: Full filesystem access without authentication

---

##  Attack Chain Summary

The project demonstrates realistic attack paths:

```
FTP → Root Access → Credential Extraction  
SMB → SYSTEM Access → Persistence  
SSH → Brute Force → Privilege Escalation  
RPC/NFS → Filesystem Mount → Credential Dump  
```

> These chains reflect how attackers pivot across services in real environments.

---

##  Impact

* Full system compromise (Linux & Windows)
* Credential disclosure and reuse
* Persistent access creation
* Potential lateral movement

**Overall Risk:  CRITICAL**

---

##  Mitigation Overview

Key defensive measures include:

* Patch management and software updates
* Disabling deprecated protocols (SMBv1)
* Strong authentication policies
* Network segmentation and firewalling
* Monitoring and intrusion detection

> Detailed remediation strategies are included in the full report.


##  Tools Used

* Nmap
* Metasploit Framework
* Hydra / Ncrack
* Netcat
* John the Ripper


##  Learning Outcomes

* Understanding of network service vulnerabilities
* Hands-on exploitation of real CVEs
* Development of attacker mindset
* Ability to write professional pentest reports
* Exposure to multi-service attack chaining

---

##  Disclaimer

This project was conducted in a controlled lab environment for educational purposes only.
Do not attempt these techniques on systems without proper authorization.

---


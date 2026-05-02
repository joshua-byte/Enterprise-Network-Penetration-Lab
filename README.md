# Internal Network Penetration Test Report

## Overview

This project simulates a real-world internal network penetration test conducted in a controlled lab environment. The objective is to identify vulnerabilities, exploit weaknesses across multiple services, and assess the overall security posture of the network.

The assessment demonstrates how attackers leverage misconfigured services, weak authentication, deprecated cryptographic configurations, and known vulnerabilities to gain initial access, escalate privileges, establish persistence, and move laterally across systems.

---

## Objectives

* Perform structured network reconnaissance and service enumeration
* Identify vulnerabilities in exposed network services
* Exploit real-world CVEs and misconfigurations
* Achieve privilege escalation on compromised systems
* Demonstrate multi-stage attack chaining and lateral movement
* Produce a professional Vulnerability Assessment & Penetration Testing (VAPT) report

---

##  Lab Environment

| Role     | System          | IP Address      |
| -------- | --------------- | --------------- |
| Attacker | Kali Linux      | 192.168.109.131 |
| Target 1 | Metasploitable2 | 192.168.109.139 |
| Target 2 | Windows XP      | 192.168.109.132 |

>  This lab is intentionally vulnerable and used for authorized testing only.

---

## ⚔️ Methodology

Reconnaissance → Enumeration → Vulnerability Identification → Exploitation → Privilege Escalation → Post-Exploitation → Reporting

---

## Attack Surface Overview

* FTP (Port 21)
* SSH (Port 22)
* RPC/NFS (Port 111)
* SMB (Port 445)

---

## Findings

---

### FTP Backdoor (vsFTPd 2.3.4)

* **Severity:** Critical
* **CVE:** CVE-2011-2523
* **Description:** Backdoored FTP service allowing unauthenticated remote command execution
* **Impact:** Immediate root shell access

**Post-Exploitation:**

* Upgraded basic shell to Meterpreter session

**Proof:**

* FTP exploit → shell
<img width="1257" height="658" alt="meterpreter_shell" src="https://github.com/user-attachments/assets/bdc446f5-a50f-4274-8e97-466f24c459c0" />
<img width="1267" height="757" alt="exploiting_vuln_escalation" src="https://github.com/user-attachments/assets/f3f980d2-95c2-49d6-8af0-2b4cc0783490" />


**Remediation:**

* Remove vulnerable service
* Apply patch management

---

### SMB Remote Code Execution (EternalBlue)

* **Severity:** Critical
* **CVE:** CVE-2017-0144
* **Description:** SMBv1 vulnerability enabling remote code execution
* **Impact:** SYSTEM-level access on Windows machine

**Post-Exploitation (Persistence):**

* Created new administrative user
* Maintained persistent access

**Proof:**

* `getuid → NT AUTHORITY\SYSTEM`
* `net user hacker Pass@123 /add`
* `net localgroup administrators hacker /add`
<img width="923" height="493" alt="smb_user" src="https://github.com/user-attachments/assets/612ed66d-18e2-4930-b5e8-60f5bacbce30" />
<img width="923" height="790" alt="admin_user" src="https://github.com/user-attachments/assets/c94c9dc5-7dc7-406c-bec4-f0e63076d5a0" />
<img width="923" height="502" alt="add_user" src="https://github.com/user-attachments/assets/0e28f4d5-88d5-42bf-8fe4-4fb78a6b6c7e" />


**Remediation:**

* Apply MS17-010 patch
* Disable SMBv1

---

### Weak SSH Credentials & Legacy Crypto Configuration

* **Severity:** High
* **Description:** Weak password authentication combined with deprecated cryptographic algorithms enabled unauthorized access
* **Impact:** Authenticated system access and privilege escalation

**Technical Weakness:**

* Supports outdated algorithms:

  * `diffie-hellman-group1-sha1`
  * `hmac-sha1`
  * `ssh-rsa`

**Proof:**

* Successful brute-force attack
* SSH login as `msfadmin`
* `sudo su → root`
<img width="1116" height="687" alt="ssh_access" src="https://github.com/user-attachments/assets/14866c48-4680-42c0-aab4-7cec27321a73" />
<img width="497" height="257" alt="ncrack_bruteforce" src="https://github.com/user-attachments/assets/5280bc9d-43e8-4910-bc50-212119eb9dfb" />


**Remediation:**

* Disable password authentication
* Enforce key-based login
* Remove legacy cryptographic support

---

### NFS Misconfiguration

* **Severity:** Critical
* **Description:** Root filesystem exported without access restrictions
* **Impact:** Full filesystem access and credential exposure

**Proof:**

* `showmount -e` reveals `/` exported
* Mounted root filesystem remotely
* Accessed `/etc/shadow`
<img width="1234" height="248" alt="rpc_Access" src="https://github.com/user-attachments/assets/7aa1b409-7c40-48c3-ba68-f52e3be79185" />
<img width="1045" height="652" alt="passwd_rpc" src="https://github.com/user-attachments/assets/999c2460-c6ea-48a9-b6d1-5c7763051f96" />


**Remediation:**

* Restrict NFS exports
* Enforce authentication controls

---

## Attack Chain

```id="attackchain"
Reconnaissance
   ↓
FTP Exploit → Root Access → Meterpreter Session
   ↓
Credential Extraction
   ↓
SSH Access → Privilege Escalation
   ↓
SMB Exploit → SYSTEM Access → Persistence (Admin User)
   ↓
NFS Mount → Sensitive Data Access → Lateral Movement Potential
```

---

## Impact Assessment

* Full compromise of Linux and Windows systems
* Credential reuse across services
* Persistent administrative access established
* High potential for lateral movement

**Business Impact:**
An attacker can gain complete control over internal systems, extract sensitive data, maintain long-term access, and pivot across the network.

**Overall Risk Rating:** **CRITICAL**

---

## Mitigation & Defensive Measures

* Apply regular patch management
* Disable deprecated protocols (SMBv1)
* Enforce strong authentication mechanisms
* Remove legacy cryptographic configurations
* Restrict unnecessary service exposure
* Implement network segmentation
* Monitor logs and detect anomalies

---

## Tools Used

* Nmap
* Metasploit Framework
* Ncrack

---

## Key Takeaways

* Real-world attacks rely on chaining multiple vulnerabilities
* Misconfigurations are often more dangerous than software flaws
* Weak authentication enables rapid compromise
* Legacy cryptographic support increases attack surface
* Post-exploitation techniques enable persistence and control
* Network segmentation is critical for limiting attack spread

---

## Executive Summary

The internal network is critically vulnerable due to exposed services, weak authentication, legacy cryptographic configurations, and misconfigurations. An attacker can achieve full compromise with minimal effort by chaining these weaknesses and maintaining persistent access.

---

## Conclusion

This assessment demonstrates how attackers can exploit internal network weaknesses to gain unauthorized access, escalate privileges, establish persistence, and move laterally across systems. Proper hardening, patching, and network controls are essential to mitigate these risks.

---

## Disclaimer

This project was conducted in a controlled lab environment for educational purposes only. Unauthorized testing is strictly prohibited.

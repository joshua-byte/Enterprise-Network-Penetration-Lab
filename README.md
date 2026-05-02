# Internal Network Penetration Test Report

## 📌 Overview

This project simulates a real-world internal network penetration test conducted in a controlled lab environment. The objective is to identify vulnerabilities, exploit weaknesses across multiple services, and assess the overall security posture of the network.

The assessment demonstrates how attackers leverage misconfigured services, weak authentication, and known vulnerabilities to gain access, escalate privileges, and move laterally across systems.

---

## 🎯 Objectives

* Perform structured network reconnaissance and service enumeration
* Identify vulnerabilities in exposed network services
* Exploit real-world CVEs and misconfigurations
* Achieve privilege escalation on compromised systems
* Demonstrate multi-stage attack chaining and lateral movement
* Produce a professional Vulnerability Assessment & Penetration Testing (VAPT) report

---

## 🧱 Lab Environment

| Role     | System          | IP Address      |
| -------- | --------------- | --------------- |
| Attacker | Kali Linux      | 192.168.109.131 |
| Target 1 | Metasploitable2 | 192.168.109.130 |
| Target 2 | Windows XP      | 192.168.109.132 |

> ⚠️ This lab is intentionally vulnerable and designed for controlled security testing.

![Network Diagram](https://github.com/user-attachments/assets/554e1730-2e02-481b-aa6d-b83dd26c1a10)

---

## ⚔️ Methodology

The assessment follows a structured penetration testing lifecycle:

1. Reconnaissance
2. Service Enumeration
3. Vulnerability Identification
4. Exploitation
5. Privilege Escalation
6. Post-Exploitation
7. Reporting

---

## 🔍 Attack Surface Overview

Initial reconnaissance identified the following exposed services:

* FTP (Port 21)
* SSH (Port 22)
* RPC/NFS (Port 111)
* SMB (Port 445)

These services formed the primary attack surface.

---

## 🔍 Findings

### 🔴 FTP Backdoor (vsFTPd 2.3.4)

* **Severity:** Critical
* **CVE:** CVE-2011-2523
* **Description:** The FTP service contains a backdoor that allows unauthenticated remote command execution.
* **Impact:** Immediate shell access without credentials, enabling full system compromise.
* **Remediation:** Upgrade or replace the vulnerable FTP service.

**Proof of Exploitation:**
*(Add screenshot: FTP exploit + shell access here)*

---

### 🔴 SMB Remote Code Execution (EternalBlue)

* **Severity:** Critical
* **CVE:** CVE-2017-0144
* **Description:** SMBv1 vulnerability enabling remote code execution.
* **Impact:** SYSTEM-level access on the Windows machine.
* **Remediation:** Apply MS17-010 patch and disable SMBv1.

**Proof of Exploitation:**
*(Add screenshot: Metasploit exploit success + SYSTEM shell)*

---

### 🟠 Weak SSH Credentials & Privilege Escalation

* **Severity:** High
* **Description:** Weak passwords allowed brute-force access, followed by privilege escalation via sudo misconfiguration.
* **Impact:** Full root access to the system.
* **Remediation:** Enforce strong password policies and restrict sudo privileges.

**Proof of Exploitation:**
*(Add screenshot: Hydra attack + root shell)*

---

### 🔴 NFS Misconfiguration

* **Severity:** Critical
* **Description:** Root directory (`/`) exported without proper restrictions.
* **Impact:** Unauthorized file access, credential exposure, and potential lateral movement.
* **Remediation:** Restrict exports and enforce proper authentication controls.

**Proof of Exploitation:**
*(Add screenshot: NFS mount + file access)*

---

## 🔗 Attack Chain & Lateral Movement

The attack demonstrates a realistic multi-stage compromise:

```
[Reconnaissance]
      ↓
[FTP Exploit → Initial Shell]
      ↓
[Credential Extraction]
      ↓
[SSH Access → Privilege Escalation]
      ↓
[SMB Exploit → SYSTEM Access]
      ↓
[NFS Mount → Data Exfiltration → Pivoting]
```

### Key Insight

The compromise was achieved by chaining multiple weaknesses:

* Exposed services
* Weak authentication
* Lack of segmentation
* Misconfigured network resources

---

## 📊 Impact Assessment

* Full compromise of Linux and Windows systems
* Credential reuse across services
* Persistent access established
* High potential for lateral movement

**Business Impact:**
An attacker could access sensitive enterprise data, maintain persistent access, and move laterally across internal systems, leading to full network compromise.

**Overall Risk Rating:** **CRITICAL**

---

## 🛠️ Mitigation & Defensive Measures

* Apply regular patch management (e.g., MS17-010)
* Disable deprecated protocols (SMBv1)
* Enforce strong authentication policies
* Restrict unnecessary service exposure
* Implement network segmentation
* Monitor logs and detect anomalies

---

## 🛠️ Tools Used

* Nmap (Reconnaissance & Enumeration)
* Metasploit Framework (Exploitation)
* Hydra / Ncrack (Credential Attacks)
* Netcat (Shell Handling)
* John the Ripper (Password Cracking)

---

## 📊 Key Takeaways

* Real-world attacks rely on chaining multiple vulnerabilities
* Misconfigurations often pose greater risks than software flaws
* Weak authentication leads to rapid compromise
* Network segmentation is critical for limiting attack spread

---

## 🧾 Executive Summary

The internal network is critically vulnerable due to multiple high-risk services, weak authentication, and lack of segmentation. An attacker can achieve full compromise with minimal effort by chaining these weaknesses.

---

## 📄 Conclusion

This assessment demonstrates how attackers can exploit internal network weaknesses to gain unauthorized access, escalate privileges, and move laterally across systems. Proper security controls, patch management, and network segmentation are essential to mitigate these risks.

---

## ⚠️ Disclaimer

This project was conducted in a controlled lab environment for educational purposes only.
Do not attempt these techniques on systems without proper authorization.

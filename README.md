# 🧃 TryHackMe: Juicy Details

**Category**: Blue Team / Log Analysis  
**Platform**: [TryHackMe](https://tryhackme.com/room/juicydetails)

---

## 🎯 Objective

The objective of this project is to simulate a real-world web application breach against the OWASP Juice Shop. As a blue team analyst, the goal is to:

- Investigate attacker activities through log analysis.
- Identify the sequence of tools and techniques used by the attacker.
- Assess and document the impact of the cyberattack on organizational information security.
- Develop a defense strategy to prevent future attacks on the organization's networks and systems.

---

## 🛠️ Skills Learned

- **Log Analysis**: Parsing and interpreting logs (`access.log`, `vsftpd.log`, `auth.log`) to trace attacker activity.
- **Threat Intelligence**: Identifying attacker tools and techniques like `nmap`, `hydra`, `sqlmap`, `curl`, `feroxbuster`.
- **Vulnerability Assessment**: Recognizing exploits such as brute-force login and SQL injection.
- **Incident Response**: Documenting data exposure and crafting security recommendations.
- **Report Writing**: Producing a formal incident report with recommendations.

---

## 🧪 Tools Used

- **Log Files**:
  - `access.log`: User-agent & URL analysis
  - `vsftpd.log`: FTP file download tracking
  - `auth.log`: SSH login verification
- **Analysis Utilities**:
  - `grep`, `awk`, `sed`
  - `whois`, `nslookup`

---

## 🧾 Tasks Completed

### 🔹 Task 1: Access Log Analysis
- Traced tool-based scans and brute-force attempts
- Detected patterns indicative of enumeration and SQL injection

### 🔹 Task 2: Vulnerability Discovery
- Discovered brute-force login and SQL injection
- Detected insecure backup and credential files

### 🔹 Task 3: Data Exfiltration Techniques
- Found evidence of FTP downloads and successful SSH login

### 🔹 Task 4: Documentation & Recommendations
- Created detailed [Incident Report](juicy-details-incident-report.md) covering:
  - Attack vector
  - Exploited vulnerabilities
  - Data accessed
  - Actionable remediation advice

---

## 🧠 Lessons Learned

- Logs are essential for uncovering attack timelines.
- Misconfigurations (e.g., anonymous FTP) can lead to major breaches.
- Hardcoded or poorly managed credentials can compromise an entire system.
- Documentation is critical for communicating risk and informing future security strategy.

---

## 📁 Repository Structure

```
juicy-details/
├── access.log
├── vsftpd.log
├── auth.log
├── juicy-details-incident-report.md
└── README.md
```

---

## 📌 Note

This repository is a practical SOC analysis and reporting task based on the TryHackMe "Juicy Details" room and reflects real-world defensive cybersecurity scenarios.

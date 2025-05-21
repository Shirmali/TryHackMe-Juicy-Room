# 🛡️ Incident Report: TryHackMe – Juicy Details

## 📌 Report Title:
**Security Breach Analysis of Juice Shop Web Application**

## 📅 Date of Analysis:
May 21, 2025

## 🧑‍💻 Analyst:
Shirley Mali

---

## 📄 Executive Summary

The OWASP Juice Shop application was compromised by an external threat actor using publicly accessible vulnerabilities and weak access controls. The attacker conducted reconnaissance, exploited SQL injection vulnerabilities, leveraged unsecured FTP access, and ultimately gained remote shell access via SSH using stolen credentials.

This report provides a detailed analysis of the attack vector, exploited vulnerabilities, impacted assets, and recommendations for remediation.

---

## 🔍 Technical Overview

### 1. **Initial Reconnaissance**
The attacker began their activity by scanning the environment using automated tools:

| Tool         | Evidence (User-Agent / Behavior) |
|--------------|-----------------------------------|
| `nmap`       | Scan patterns in `access.log`     |
| `feroxbuster`| Multiple rapid directory requests |
| `hydra`      | Numerous POST requests to login API with varying credentials |

#### Indicators:
- High frequency of requests to `/rest/user/login`
- Sequential and recursive attempts to access hidden resources

---

### 2. **Exploitation Phase**

#### A. **Brute-force Login**
- **Endpoint**: `/rest/user/login`
- **Method**: Repeated POST requests with different credentials
- **Outcome**: Successful login to a user account (`jim@juice-sh.op`)

#### B. **SQL Injection**
- **Vulnerable Parameter**: `q` in `/rest/products/search?q=`
- **Method**: SQL payloads injected via GET requests
- **Outcome**: Database enumeration and potential data extraction

#### C. **Sensitive File Discovery via FTP**
- **FTP Access**: Anonymous login enabled
- **Files Accessed**:
  - `backup.zip`: Extracted backup containing credentials
  - `credentials.txt`: Contained hardcoded SSH credentials

#### D. **SSH Access**
- **Username**: Reused from backup file
- **IP**: Internal host accessed via SSH (evidenced in `auth.log`)
- **Outcome**: Full system access achieved

---

## 🧾 Summary of Exploited Vulnerabilities

| Vulnerability            | CVE/Reference                  | Risk Level | Exploitation Evidence                   |
|--------------------------|-------------------------------|------------|-----------------------------------------|
| Weak login protection    | OWASP A2: Broken Authentication | High       | Hydra-based brute force via login form  |
| SQL Injection            | OWASP A1: Injection             | High       | Payloads in query parameter `q`         |
| Insecure FTP             | Misconfigured Service           | High       | Anonymous access allowed                |
| Hardcoded credentials    | OWASP A3: Sensitive Data Exposure | High    | Credentials found in `backup.zip`       |
| SSH with reused creds    | Poor Credential Hygiene         | Critical   | Root-level shell via credential reuse   |

---

## 📦 Data Accessed

- **User credentials** (via login brute force and backup file)
- **Database information** (via SQLi)
- **System-level access via SSH**
- **Internal logs and potentially sensitive files on host**

---

## 🛡️ Recommendations

| Issue                             | Recommended Remediation                                            |
|----------------------------------|--------------------------------------------------------------------|
| Brute-force login                | Implement rate limiting, account lockout, and MFA                 |
| SQL Injection                    | Use parameterized queries or ORM frameworks                       |
| Anonymous FTP Access             | Disable anonymous login, monitor FTP logs                         |
| Backup File Security             | Store backups outside of web or FTP root directories              |
| Credential Management            | Avoid hardcoded credentials; use password vaults                  |
| SSH Access Control               | Enforce key-based authentication, audit logins                    |
| Log Monitoring                   | Set up SIEM alerts for brute-force patterns and SQLi attempts     |

---

## 🔚 Conclusion

This simulated breach highlights the ease with which a misconfigured and vulnerable system can be compromised. Organizations must implement defense-in-depth strategies, routinely audit services, and ensure sensitive data is protected at all levels.

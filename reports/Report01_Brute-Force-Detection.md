## 🛡️ **Security Incident Report**

### **Incident Title**: Brute Force Attack Detection on Windows System

**Date**: May 28, 2025
**Time Detected**: 11:24 AM (UTC)
**Detected by**: Wazuh SIEM + Sysmon Integration
**Severity Level**: High (Level 10)
**Agent**: windows11 (IP: 192.168.1.7)
**Manager**: wazuh-server
**Event ID**: 4625 (Failed Logon Attempt)

---

### 📌 **Description**:

Wazuh detected a **brute force attack** targeting the Windows system at `192.168.1.7`. The attacker repeatedly attempted to log in using the username **admin** with incorrect credentials. The source IP address of the failed attempts was **192.168.1.5**. The attack was detected based on **76 failed login attempts** in a short timeframe, indicating a brute-force pattern.

---

### 🔎 **Technical Details**:

| Field                      | Value                                                                                                 |
| -------------------------- | ----------------------------------------------------------------------------------------------------- |
| **Target Username**        | `admin`                                                                                               |
| **Domain**                 | `WINDOWS11`                                                                                           |
| **Source IP**              | `192.168.1.5`                                                                                         |
| **Workstation**            | `WINDOWS11`                                                                                           |
| **Logon Type**             | 10 (Remote/Remote Desktop)                                                                            |
| **Authentication Package** | `Negotiate`                                                                                           |
| **Failure Reason**         | `0xC000006A` (Unknown user name or bad password)                                                      |
| **Rule Description**       | Brute force attack detected - multiple failed login attempts from 192.168.1.5 targeting user 'admin'. |
| **Detection Method**       | Windows Event ID 4625 + Rule Fired 76 Times                                                           |

---

### 📁 **Sysmon & Windows Event Correlation**:

* **Sysmon Provider GUID**: `{54849625-5478-4994-a5ba-3e3b0328c30d}`
* **Security Event Channel**: Microsoft-Windows-Security-Auditing
* **Decoder Used**: `windows_eventchannel`
* **Wazuh Rule ID**: `18100`
* **Fired Times**: `76`

---

### 🚨 **Impact**:

* Potential unauthorized access attempts to a privileged account.
* High risk of credential compromise if the attack succeeded.
* System stability and user data integrity at risk.

---

### 🛠️ **Mitigation Steps Taken**:

* Blocked IP `192.168.1.5` at the firewall.
* Enabled account lockout policy after 5 failed attempts.
* Audited admin account for any successful logins.
* Alert sent to security operations team for further investigation.
* Increased logging level for all authentication events.

---

### 📝 **Recommendations**:

* Enforce multi-factor authentication (MFA) on all administrative accounts.
* Apply stricter lockout and rate-limiting policies.
* Monitor suspicious login patterns from remote IPs.
* Rotate passwords for sensitive accounts.
* Regularly update threat detection rules and signatures.

---

### ✅ **Status**:

> **Containment Completed**. No successful logins were detected. System integrity is intact.


# Detection Rules

## Purpose

This document summarizes the detection rules implemented in the Home SOC Lab. Each detection was validated by simulating the corresponding attack and verifying that Elastic Security generated an alert.

---

# Detection Summary

| Detection | Status | MITRE ATT&CK |
|------------|--------|--------------|
| SSH Brute Force | ✅ | T1110 |
| Windows Brute Force | ✅ | T1110 |
| PowerShell Execution | ✅ | T1059.001 |
| Credential Dumping (LSASS) | ✅ | T1003.001 |
| Kerberoasting | ✅ | T1558.003 |
| Windows Event Log Cleared | ✅ | T1070 |
| Backdoor User Account | ✅ | T1136 |
| Pass-the-Hash | ✅ | T1550.002 |
| Windows Defender Malware Detection | ✅ | T1204 |
| LOLBins (CertUtil) | ✅ | T1218 |
| RDP Lateral Movement | ✅ | T1021.001 |
| DCSync | ✅ | T1003.006 |
| Golden Ticket | ✅ | T1558.001 |

---

# Detection Workflow

```

Attacker
│
▼
Attack Execution
│
▼
Elastic Agent
│
▼
Fleet Server
│
▼
Elasticsearch
│
▼
Detection Rule
│
▼
Security Alert
│
▼
Investigation
│
▼
osTicket Automation

```

---

# Investigation

Alerts were investigated using:

- Kibana Security
- Discover
- Timeline
- Event Details
- Host Information

Important fields collected during investigations included:

- Timestamp
- Source IP
- Destination Host
- Username
- Event ID
- Severity
- Rule Name

---

# Validation

Each detection rule was validated by:

- Executing the attack
- Confirming event collection
- Verifying Elastic Security alerts
- Investigating the alert in Kibana

---

# Related Documentation

- [06 - Mythic C2](06-mythic-c2.md)
- [07 - osTicket](07-osticket.md)
- [09 - Automation](09-automation.md)

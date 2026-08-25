# Splunk SIEM Investigation: Suspicious Authentication Activity

## 📌 Project Overview

This project demonstrates the use of Splunk SIEM to analyze simulated Windows authentication events and identify suspicious login activity.

The investigation focuses on failed and successful authentication events to identify patterns that may indicate brute-force attempts, suspicious account activity, or potential account compromise.

The analysis was performed using a simulated Windows security log dataset and Splunk queries to investigate authentication behavior and document relevant findings.

---

## 🎯 Project Objective

The objective of this project was to:

- Analyze simulated Windows authentication events using Splunk
- Identify repeated failed login attempts
- Investigate successful logons following failed authentication activity
- Analyze targeted user accounts
- Identify potentially suspicious authentication patterns
- Classify observed activity based on severity
- Recommend appropriate mitigation and detection measures

---

## 🛠️ Lab Environment & Tools

| Component | Details |
|---|---|
| SIEM Platform | Splunk |
| Log Source | Simulated Windows Security Events |
| Dataset | `brute_force_pattern_logs.txt` |
| Environment | Controlled Lab |
| Analysis Focus | Authentication Activity |

---

## 📂 Log Events Analyzed

The investigation focused on the following Windows Security Event IDs:

| Event ID | Description |
|---|---|
| **4625** | Failed logon attempt |
| **4624** | Successful logon |
| **4634** | Logoff event |

These events were analyzed to understand authentication behavior and identify potentially suspicious patterns.

---

# 🔍 Investigation Methodology

The simulated Windows authentication log dataset was ingested into Splunk for analysis.

The investigation involved:

1. Searching for failed authentication events.
2. Identifying accounts with repeated failed login attempts.
3. Reviewing successful authentication events.
4. Comparing failed and successful activity associated with the same accounts.
5. Investigating authentication patterns that could indicate suspicious activity.
6. Assessing the severity of the observed events.
7. Documenting recommended security improvements.

---

# 🔎 Splunk Queries

## 1. Search for Failed Logons

```spl
index=* source="brute_force_pattern_logs.txt" EventCode=4625

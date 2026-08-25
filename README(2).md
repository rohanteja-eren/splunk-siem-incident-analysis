# Splunk SIEM Investigation: Suspicious Authentication Activity

## Project Overview

This project demonstrates the use of Splunk SIEM to investigate simulated Windows authentication events and identify suspicious login activity.

The investigation focuses on analyzing failed and successful authentication events to identify patterns that may indicate brute-force attempts, suspicious account activity, or potential credential compromise.

Using Splunk, authentication events were searched, filtered, and analyzed to identify repeated failed logon attempts, targeted accounts, and successful logons that occurred following previous authentication failures.

---

## Project Objective

The objective of this project was to investigate simulated Windows authentication events using Splunk and identify potentially suspicious authentication patterns.

The investigation focused on:

- Identifying failed authentication attempts
- Analyzing successful logon events
- Identifying accounts targeted by repeated login failures
- Investigating successful logons following failed authentication attempts
- Detecting potential brute-force or password-spraying activity
- Assessing the severity of suspicious authentication events
- Recommending appropriate security and mitigation measures

---

## Lab Environment and Tools

| Component | Details |
|---|---|
| SIEM Platform | Splunk |
| Log Source | Simulated Windows Security Events |
| Dataset | `brute_force_pattern_logs.txt` |
| Environment | Controlled Lab |
| Analysis Focus | Windows Authentication Activity |

---

## Log Events Analyzed

The investigation focused primarily on Windows authentication events.

| Event ID | Description |
|---|---|
| 4625 | Failed logon attempt |
| 4624 | Successful logon |
| 4634 | Logoff event |

These events were analyzed to understand authentication behavior and identify potentially suspicious patterns.

---

# Investigation Methodology

The simulated Windows authentication log dataset was ingested into Splunk for analysis.

The investigation followed the steps below:

1. Ingested the authentication log dataset into Splunk.
2. Searched for failed authentication events.
3. Identified accounts associated with repeated failed login attempts.
4. Reviewed successful authentication events.
5. Compared failed and successful authentication activity.
6. Investigated accounts that showed suspicious authentication patterns.
7. Assessed the severity of the observed activity.
8. Documented findings and recommended security improvements.

---

# Splunk Queries

## 1. Search for Failed Logons

```spl
index=* source="brute_force_pattern_logs.txt" EventCode=4625
```

This query was used to identify failed authentication attempts in the dataset.

---

## 2. Search for Successful Logons

```spl
index=* source="brute_force_pattern_logs.txt" EventCode=4624
```

This query was used to review successful authentication events.

---

## 3. Identify Failed Logons by Account

```spl
index=* source="brute_force_pattern_logs.txt" EventCode=4625
| stats count by Account
| sort -count
```

This query identifies accounts with failed authentication attempts and helps determine which accounts were targeted most frequently.

---

## 4. Analyze Authentication Activity

```spl
index=* source="brute_force_pattern_logs.txt"
(EventCode=4624 OR EventCode=4625)
| stats count by Account, EventCode
```

This query provides a summary of successful and failed authentication events associated with each account.

---

## 5. Identify Accounts with Both Failed and Successful Logons

```spl
index=* source="brute_force_pattern_logs.txt"
(EventCode=4624 OR EventCode=4625)
| stats values(EventCode) as EventCodes by Account
```

This query can be used to identify accounts that experienced both failed and successful authentication events and may require additional investigation.

---

## 6. Investigate a Specific Account

```spl
index=* source="brute_force_pattern_logs.txt" Account="Administrator"
```

This query was used to review authentication activity associated with a specific account.

---

# Investigation Findings

The analysis identified multiple failed and successful authentication events within the simulated Windows security log dataset.

The investigation focused on identifying:

- Repeated failed login attempts
- Authentication activity targeting multiple user accounts
- Activity involving administrative accounts
- Successful logons occurring after previous authentication failures
- Authentication patterns that may require further investigation

These patterns can indicate suspicious activity such as password guessing, brute-force attempts, password spraying, or unauthorized account access. However, authentication events alone do not confirm a successful compromise and should be validated using additional context.

Additional investigation could include reviewing source information, endpoint activity, authentication history, user behavior, and other relevant security events.

---

# Severity Assessment

| Activity | Description | Severity |
|---|---|---|
| Repeated Failed Logons | Multiple failed authentication attempts against an account | High |
| Failed Authentication Followed by Successful Logon | Successful authentication observed after previous failures | High |
| Multiple Accounts Targeted | Authentication failures involving several account names | Medium |
| Isolated Failed Logon | Single failed authentication event with no additional suspicious context | Low |

Severity should be validated using additional contextual information during a real-world investigation.

---

# Security Recommendations

## Immediate Actions

- Investigate accounts showing repeated authentication failures.
- Review successful logons that occur after suspicious failed attempts.
- Validate whether successful authentication was performed by an authorized user.
- Reset credentials if account compromise is suspected.
- Review activity associated with privileged and administrative accounts.

## Preventive Measures

- Implement Multi-Factor Authentication for privileged and sensitive accounts.
- Configure account lockout or authentication throttling policies where appropriate.
- Monitor excessive Windows Event ID 4625 activity.
- Create Splunk detection rules for repeated failed authentication attempts.
- Establish baselines for normal authentication behavior.
- Monitor successful logons following multiple authentication failures.
- Regularly review privileged account activity.

---

# Skills Demonstrated

- Splunk SIEM
- Security Log Analysis
- Windows Event Log Analysis
- Authentication Monitoring
- SPL Query Development
- Brute-Force Detection
- Password-Spraying Detection
- Security Event Correlation
- Incident Investigation
- Incident Severity Assessment

---

# Repository Structure

```text
splunk-siem-incident-analysis/
│
├── README.md
│
├── data/
│   └── brute_force_pattern_logs.txt
│
├── screenshots/
│   ├── failed-logons.png
│   └── successful-logons.png
│
└── queries/
    └── splunk-queries.md
```

---

# Lab Disclaimer

This project was conducted in a controlled lab environment using simulated Windows authentication logs.

The analysis was performed for educational and cybersecurity portfolio purposes. No production systems, real user accounts, or unauthorized systems were targeted.

---

# Conclusion

This project demonstrates a SIEM-based investigation workflow using Splunk to analyze Windows authentication events.

By examining failed and successful logons, identifying suspicious authentication patterns, and reviewing accounts associated with repeated login failures, the investigation demonstrates core SOC analyst skills including log analysis, event correlation, SPL query development, incident assessment, and security recommendations.

The project highlights the importance of continuous authentication monitoring and demonstrates how SIEM platforms can assist security analysts in identifying and investigating potentially suspicious activity.

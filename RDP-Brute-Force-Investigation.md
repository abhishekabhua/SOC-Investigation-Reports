INVESTIGATION REPORT
====================

Date: May 31, 2026  
Alert Name: SOC176 – RDP Brute Force Detected  
Severity: Medium

ALERT SUMMARY
-------------

Multiple Remote Desktop Protocol (RDP) authentication failures were detected from a single external IP address targeting multiple user accounts on a Windows endpoint. Following the failed login attempts, a successful authentication was observed, indicating a potential brute-force compromise attempt.

TIMELINE
--------

- 11:44 AM – Alert Generated
- 11:44 AM – First Failed Login Detected
- 11:44 AM – Last Failed Login Detected
- 04:00 PM – Investigation Started
- 07:19 PM – Investigation Completed

AFFECTED ASSETS
---------------

- Hostname: Matthew
- Destination IP: 172.16.17.148
- Operating System: Windows 10
- Targeted Usernames: Matthew, sysadmin, guest, admin

ATTACK DETAILS
--------------

- Source IP: 218.92.0.56
- Source Country: China
- Failed Login Attempts: 14
- Successful Login Attempts: 1
- Observed Event IDs: 4625 (Failed Logon), 4624 (Successful Logon)
- Log Source: Operating System Security Logs

THREAT INTELLIGENCE
-------------------

- VirusTotal: 8/91 security vendors identified the IP as malicious.
- AbuseIPDB: 453,051 abuse reports associated with the IP address.
- LetsDefend Threat Intelligence: Classified as malicious.

INVESTIGATION FINDINGS
----------------------

- Multiple authentication failures were observed within a one-minute period.
- The attacker attempted access using multiple usernames, indicating username enumeration activity.
- A successful RDP authentication (Event ID 4624) occurred after two failed login attempts.
- No evidence of lateral movement was identified during the investigation.
- No additional suspicious processes, persistence mechanisms, or post-compromise activities were observed on the affected host.

VERDICT
--------

- Classification: True Positive
- Escalation Required: Yes
- Host Contained: Yes

REASON FOR VERDICT
------------------

The investigation confirmed a brute-force attack against the RDP service. The source IP generated multiple failed authentication attempts (Event ID 4625) against several user accounts within a short timeframe, followed by a successful login event (Event ID 4624). Additionally, the source IP is associated with known malicious activity according to multiple threat intelligence platforms. Based on these findings, the alert has been classified as a True Positive and escalated for further incident response actions.

RECOMMENDED ACTIONS
-------------------

1. Block source IP address 218.92.0.56 at perimeter security controls.
2. Reset credentials for the compromised account.
3. Review all activities performed during the successful RDP session.
4. Enable Multi-Factor Authentication (MFA) for remote access services.
5. Lock or disable affected accounts until verification is completed.
6. Review RDP exposure and restrict access through firewall rules or VPN.
7. Continue monitoring for additional authentication attempts and related malicious activity.
8. Escalate to Tier 2/Incident Response team for further forensic analysis.

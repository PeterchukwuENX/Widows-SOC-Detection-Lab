Incident 001 — Suspicious Authentication Activity
Summary
This investigation was created to practice analyzing Windows authentication activity from the perspective of a SOC analyst.
A controlled series of failed login attempts was generated against the local Windows account, followed by a successful login.
The investigation focused on correlating Windows Security Event IDs **4625** and **4624** and determining whether the activity represented suspicious remote authentication or normal local activity.

Investigation Objective
Determine:
- Which account was targeted
- Whether the login attempts were successful or failed
- What type of logon occurred
- Where the authentication originated
- Whether the activity appeared suspicious
- Whether additional investigation was required

Evidence Collected
Event ID 4625 — Failed Logon
The Security log recorded failed authentication attempts for:

```text
Target User: kenny
Target Domain: WINDOWS-SOC-LAB
Logon Type: 2
Workstation: WINDOWS-SOC-LAB
Source IP: 127.0.0.1
Process: C:\Windows\System32\svchost.exe

The failure status indicated that the supplied credentials were not valid.
Event ID 4624 — Successful Logon
A successful authentication event was also identified for:
Target User: kenny
Target Domain: WINDOWS-SOC-LAB
Logon Type: 2
Workstation: WINDOWS-SOC-LAB

Timeline
The controlled activity followed this pattern:
Failed Logon
      ↓
Failed Logon
      ↓
Failed Logon
      ↓
Successful Logon

The failed and successful events were correlated using the Windows Security log.
Analysis
The repeated failed logons initially resemble a possible password attack pattern.
However, further analysis showed important context:
- The account involved was the local kenny account.
- The logon type was 2 (Interactive).
- The source address was 127.0.0.1, indicating the local machine.
- The workstation name matched the Windows SOC lab machine.
- The activity was intentionally generated as part of this controlled investigation.
Because the authentication originated locally rather than from an external source, the available evidence does not support classifying this as a confirmed remote brute-force attack.
Finding
Classification: Benign / Controlled Lab Activity
The events successfully demonstrated how Windows records failed and successful authentication attempts.
The investigation also demonstrated why a SOC analyst should not classify an alert based only on the number of failed logins.
Additional context such as:
- Logon Type
- Source IP
- Account
- Workstation
- Timestamp
- Related endpoint activity
is required before determining whether authentication activity is malicious.
SOC Lessons
This investigation reinforced several practical SOC concepts:
1. Event ID 4625 can indicate a failed authentication attempt.
2. Event ID 4624 records a successful authentication.
3. Logon Type provides important context about how authentication occurred.
4. Source IP information helps determine whether authentication was local or remote.
5. Multiple failed logons do not automatically mean brute force.
6. Security events should be correlated and investigated in context rather than analyzed individually.
Tools Used
- Windows 10
- Windows Event Viewer
- Windows Security Logs
- VirtualBox
Status
Investigation completed

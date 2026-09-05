# Day 5 — Detection Engineering & Incident Investigation

## Objective

Develop and validate basic detection logic using Windows Security logs, PowerShell Script Block Logging, and Sysmon telemetry. Simulate an authentication attack and investigate the resulting account lockout.

## Activities Completed

### 1. Simulated Authentication Attack

- Generated five consecutive incorrect password attempts against the `FREDDYS\Alice.Martin` account from WS-01.
- The attempts occurred within approximately 25 seconds.
- The activity triggered the configured domain account lockout threshold.

### 2. Account Lockout Detection

- Verified Event ID 4740 on AD-DC01.
- Confirmed that `alice.martin` was locked out.
- Confirmed WS-01 as the caller computer.

### 3. Failed Authentication Investigation

- Investigated Event ID 4625 on WS-01.
- Confirmed five failed authentication events involving Alice.Martin.
- Extracted the affected account from the event data rather than relying on a hard-coded username.

### 4. Failed Logon Threshold Detection

- Developed PowerShell detection logic to group Event ID 4625 events by account.
- Established a threshold of five failed logons within 30 minutes.
- Successfully identified Alice.Martin after the threshold was reached.

### 5. PowerShell Detection

- Verified Event ID 4104 Script Block Logging.
- Generated a controlled `Invoke-Expression` test using harmless `Write-Output` activity.
- Confirmed that the full PowerShell command was captured in Event ID 4104.
- Demonstrated how potentially suspicious PowerShell constructs can be identified through script-block telemetry.

### 6. Process Execution Detection

- Used Sysmon Event ID 1 to investigate parent-child process relationships.
- Identified PowerShell launching `runas.exe`.
- Correlated the process execution with the authentication activity used during the simulated attack.

## Incident Timeline

1. WS-01 initiated repeated authentication attempts against `Alice.Martin`.
2. Five Event ID 4625 failures were generated within approximately 25 seconds.
3. Sysmon recorded `powershell.exe` launching `runas.exe`.
4. The domain account lockout threshold was reached.
5. AD-DC01 generated Event ID 4740.
6. The 4740 event identified WS-01 as the caller computer.
7. The threshold detection identified Alice.Martin with five failed logons.

## Detection Logic

### Failed Authentication Threshold

**Data Source:** Windows Security Event Log

**Event ID:** 4625

**Condition:**
- Group failed authentication events by account.
- Evaluate events within a 30-minute window.
- Alert when an account reaches five or more failures.

**Purpose:**
Identify potential password spraying, brute-force activity, or repeated authentication failures requiring investigation.

### Suspicious PowerShell Activity

**Data Source:** Microsoft-Windows-PowerShell/Operational

**Event ID:** 4104

**Condition:**
Identify potentially suspicious PowerShell constructs within captured script blocks.

**Test Pattern:**
`Invoke-Expression`

**Purpose:**
Provide visibility into PowerShell script execution for further investigation.

### Suspicious Process Chain

**Data Source:** Microsoft-Windows-Sysmon/Operational

**Event ID:** 1

**Condition:**
Monitor parent-child process relationships and command-line execution.

**Observed Test Chain:**
`powershell.exe → runas.exe`

**Purpose:**
Identify unusual process execution chains that may indicate malicious activity.

## Screenshots

- `57-ADDC01-Account-Lockout-Event.png`
- `58-WS01-Failed-Logon-Detection-Count.png`
- `59-WS01-Repeated-Failed-Logon-Detection.png`
- `60-WS01-Suspicious-PowerShell-4104-Detection.png`
- `61-WS01-Sysmon-Suspicious-Process-Chain.png`
- `62-WS01-Failed-Logon-Incident-Timeline.png`
- `63-WS01-Automated-Failed-Logon-Detection.png`

## SOC Relevance

This exercise demonstrates the transition from raw security telemetry to actionable detection logic.

The simulated attack produced multiple telemetry sources that could be correlated during an investigation:

- Event ID 4625 — failed authentication
- Event ID 4740 — account lockout
- Event ID 4104 — PowerShell script-block activity
- Sysmon Event ID 1 — process creation

The investigation established the affected account, originating workstation, authentication failures, process execution chain, and account-lockout response.

## Day 5 Outcome

Detection logic was successfully developed and tested against controlled attack activity. The lab can now identify repeated failed authentication attempts, inspect PowerShell script-block activity, analyze process execution chains, and correlate multiple Windows security events during an incident investigation.
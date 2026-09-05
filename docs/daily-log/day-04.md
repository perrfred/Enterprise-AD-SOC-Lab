# Day 4 — Logging & Telemetry

## Objective

Validate Windows security telemetry across the domain workstation and domain controller, generate controlled authentication activity, verify PowerShell logging, and deploy Sysmon for enhanced endpoint telemetry.

## Activities Completed

### 1. WS-01 Security Event Logging
- Verified the Windows Security Event Log was enabled.
- Confirmed approximately 25,000+ Security events were present.
- Confirmed the Security log maximum size was configured to 100 MB.

### 2. Controlled Authentication Failure
- Generated controlled failed authentication attempts against the `Alice.Martin` domain account.
- Verified Windows Security Event ID 4625.
- Confirmed telemetry captured:
  - Account name and domain
  - Failure reason
  - Status and substatus codes
  - Logon type
  - Workstation name
  - Source network address
  - Authentication process

### 3. PowerShell Telemetry
- Verified PowerShell Script Block Logging.
- Confirmed Event ID 4104 events were being generated in the PowerShell Operational log.

### 4. Sysmon Deployment
- Installed Microsoft Sysmon on WS-01.
- Verified the `Sysmon64` service was running.
- Confirmed Sysmon was generating Process Create (Event ID 1) and Process Terminated (Event ID 5) events.

### 5. Controlled Process Monitoring
- Executed `notepad.exe` manually on WS-01.
- Verified Sysmon captured the execution as Event ID 1.
- Observed process path, command line, user, integrity level, SHA256 hash, and parent process information.

### 6. AD-DC01 Telemetry
- Verified the Security Event Log was enabled and actively collecting events.
- Confirmed successful authentication events (Event ID 4624).
- Verified Kerberos authentication activity on the domain controller.

## Screenshots

- `49-WS01-Security-Event-Log-Verification.png`
- `50-WS01-Failed-Logon-Events.png`
- `51-WS01-Failed-Logon-Event-Details.png`
- `52-WS01-PowerShell-Script-Block-Events.png`
- `53-WS01-Sysmon-Process-Creation-Event.png`
- `54-WS01-Sysmon-Controlled-Process-Event.png`
- `55-ADDC01-Security-Event-Log-Verification.png`
- `56-ADDC01-Successful-Kerberos-Logon.png`

## SOC Relevance

The lab now produces multiple sources of Windows security telemetry that can be used for detection and investigation.

Event ID 4625 provides failed authentication context, while Event ID 4624 provides successful authentication information. PowerShell Event ID 4104 provides visibility into script block activity. Sysmon Event ID 1 adds detailed process execution telemetry, including command-line arguments, hashes, users, and parent-child process relationships.

These telemetry sources establish the foundation for future detection engineering and incident investigation exercises.

## Day 4 Outcome

Logging and telemetry were successfully validated on both WS-01 and AD-DC01. Sysmon was deployed and confirmed operational, and controlled activity was successfully captured for SOC analysis.
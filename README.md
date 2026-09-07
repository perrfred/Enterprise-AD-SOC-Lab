# Enterprise Active Directory SOC Lab

A hands-on enterprise Active Directory security lab designed to demonstrate Windows infrastructure administration, Active Directory security, security logging, detection engineering, threat hunting, and SOC incident response.

The lab simulates a small enterprise Windows environment and demonstrates the complete workflow from infrastructure deployment and security hardening through attack simulation, detection, investigation, containment, remediation, and recovery.

---

## Project Objectives

- Deploy and configure an enterprise-style Windows Server environment
- Build and configure an Active Directory domain
- Implement baseline security controls
- Configure enterprise users, groups, organizational units, and Group Policy
- Configure Windows security auditing and security telemetry
- Implement Sysmon and PowerShell logging
- Develop SOC detection queries
- Simulate controlled authentication attack activity
- Investigate security incidents
- Perform account containment and credential remediation
- Validate recovery and post-incident activity
- Map security activity to MITRE ATT&CK concepts
- Document findings, evidence, and response actions

---

## Lab Environment

| Component | Configuration |
|---|---|
| Hypervisor | VMware Workstation Pro |
| Host OS | Windows 11 |
| Domain Controller | AD-DC01 |
| Server OS | Windows Server 2022 Standard Evaluation |
| Workstation | WS-01 |
| Workstation OS | Windows 10 |
| Active Directory Domain | corp.freddys.local |
| NetBIOS Domain | FREDDYS |
| Network | VMware NAT (VMnet8) |
| Lab Subnet | 192.168.64.0/24 |
| Domain Controller IP | 192.168.64.10 |

---

## Active Directory Environment

The lab contains a functional Active Directory environment with:

- Active Directory Domain Services (AD DS)
- DNS
- Global Catalog
- Group Policy Management
- Organizational Units (OUs)
- Enterprise user accounts
- Security groups
- Domain-joined Windows workstation
- PowerShell-based administration

The domain structure includes departmental organizational units for:

- Finance
- HR
- IT
- Security
- Workstations

Test user accounts were created and assigned to corresponding security groups to simulate a small enterprise environment.

---

## Security Configuration

The environment includes several Windows security controls and logging configurations.

### Group Policy

A workstation security baseline was implemented using:

`GPO-Workstation-Security-Baseline`

Security configuration included:

- Account lockout policy
- Windows Defender Firewall
- Advanced Audit Policy
- Security event logging
- PowerShell logging

### Account Lockout Policy

The domain account lockout policy was configured with:

- Lockout threshold: 5 failed attempts
- Lockout duration: 15 minutes
- Observation window: 15 minutes

### Windows Defender Firewall

The workstation Domain Profile was configured with:

- Firewall: Enabled
- Inbound connections: Block
- Outbound connections: Allow

---

## Security Telemetry

The lab was configured to generate and investigate Windows security telemetry.

### Windows Security Events

The investigation process used Windows Security Event IDs including:

- **4624** — Successful logon
- **4625** — Failed logon
- **4740** — User account locked out
- **4776** — Domain controller credential validation

### PowerShell Logging

PowerShell telemetry was enabled through:

- Script Block Logging
- Script Block Invocation Logging
- Module Logging

PowerShell Event IDs **4103** and **4104** were verified and used during detection activities.

### Sysmon

Sysmon was deployed to the Windows workstation to provide additional process-level telemetry.

Sysmon Event ID **1** (Process Creation) was used to investigate:

- Process execution
- Command lines
- Parent-child process relationships
- User context
- Integrity levels
- Process hashes

---

## Detection Engineering

Detection activities focused on identifying suspicious authentication and process activity.

Examples included:

- Detecting repeated Windows Event ID 4625 failures
- Grouping failed authentication events by affected account
- Identifying accounts exceeding a failed-logon threshold
- Detecting account lockout events through Event ID 4740
- Searching PowerShell Event ID 4104 for suspicious script patterns
- Investigating Sysmon process creation events
- Correlating parent and child process relationships
- Building an incident timeline from multiple telemetry sources

---

## Threat Hunting & Incident Investigation

A controlled authentication attack simulation was performed against the `Alice.Martin` domain account.

Five incorrect authentication attempts were generated from `WS-01`, producing:

- Five Event ID 4625 failed-logon events
- An Event ID 4740 account-lockout event
- A lockout attributed to `WS-01`
- Supporting Sysmon process telemetry
- PowerShell telemetry

The investigation followed a SOC-style workflow:

**Detect → Hunt → Correlate → Scope → Investigate → Contain → Remediate → Recover → Validate**

The investigation determined that:

- The activity affected a single domain account
- The activity originated from `WS-01`
- The account was automatically locked after five failures
- No successful Alice.Martin authentication was identified during the investigated period
- The account was disabled as a containment measure
- The account password was reset
- The account was re-enabled after remediation
- No new failed-logon activity was detected following recovery

The activity was a controlled lab simulation and did not represent a real-world compromise.

---

## Incident Response

Incident `INC-2026-001` documents the simulated authentication attack and response process.

Response actions included:

1. Validate failed authentication evidence
2. Confirm account lockout
3. Determine incident scope
4. Check for successful authentication
5. Disable the affected account
6. Reset the account password
7. Re-enable the account after remediation
8. Verify the account was no longer locked
9. Monitor for additional failed authentication activity
10. Document the final incident disposition

**Final Disposition: Closed — No Evidence of Successful Compromise**

---

## MITRE ATT&CK Relevance

The lab provides practical exposure to techniques associated with authentication attacks and credential access.

Relevant concepts include:

- **T1110 — Brute Force**
- Authentication failure monitoring
- Account lockout detection
- Credential validation telemetry
- Process execution analysis
- PowerShell activity monitoring

The project focuses on understanding how security telemetry can be used to detect, investigate, and respond to suspicious authentication behavior.

---

## Project Progress

| Day | Focus | Status |
|---|---|---|
| Day 1 | Initial VM setup and Windows Server deployment | ✅ Complete |
| Day 2 | Windows Server baseline and Active Directory deployment | ✅ Complete |
| Day 3 | Enterprise domain configuration | ✅ Complete |
| Day 4 | Security logging and telemetry | ✅ Complete |
| Day 5 | Detection engineering and attack simulation | ✅ Complete |
| Day 6 | Threat hunting and incident investigation | ✅ Complete |
| Day 7 | Final validation and documentation | ✅ Complete |

---

## Project Outcomes

This project demonstrates the ability to:

- Deploy and administer a Windows Server environment
- Configure and manage Active Directory
- Implement Windows security controls
- Configure Group Policy
- Configure Windows security auditing
- Deploy Sysmon for endpoint telemetry
- Investigate Windows authentication events
- Develop basic SOC detection logic
- Correlate telemetry across multiple Windows event sources
- Perform targeted threat hunting
- Build an incident timeline
- Determine incident scope and severity
- Execute account containment and remediation
- Validate post-incident recovery
- Produce professional incident documentation

---

## Documentation

Project documentation is organized by function and daily activity.

```text
docs/
├── architecture/
│   └── active-directory-design.md
│
├── deployment/
│   └── server-baseline.md
│
├── daily-log/
│   ├── day-01.md
│   ├── day-02.md
│   ├── day-03.md
│   ├── day-04.md
│   ├── day-05.md
│   └── day-06.md
│
└── incidents/
    └── INC-2026-001.md

---

## Evidence

The `Screenshots/` directory contains documented evidence from the lab, including:

- Active Directory configuration
- Organizational Units and users
- Group Policy configuration
- Security logging
- Failed authentication events
- PowerShell telemetry
- Sysmon process telemetry
- Account lockout detection
- Detection engineering
- Incident investigation
- Containment and recovery

---

## Key Technologies

### Infrastructure

- Windows Server 2022
- Windows 10
- Active Directory Domain Services
- DNS
- Group Policy
- VMware Workstation Pro
- PowerShell

### Security Operations

- Windows Security Event Logs
- Advanced Audit Policy
- Sysmon
- PowerShell Script Block Logging
- PowerShell Module Logging
- Windows Defender Firewall
- Detection Engineering
- Threat Hunting
- Incident Response
- MITRE ATT&CK

---

## Project Status

**Completed — September 2026**

This project was built as a controlled cybersecurity laboratory environment for learning, detection engineering, SOC investigation, and incident response.

All attack activity performed within the lab was intentionally simulated and conducted in an isolated environment.

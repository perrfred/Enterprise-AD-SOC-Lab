# Day 3 — Active Directory Workstation Configuration

## Objectives

* Create and organize Active Directory users and security groups
* Join a Windows 10 workstation to the domain
* Create and apply a workstation security baseline GPO
* Configure Windows security auditing and PowerShell logging
* Verify domain connectivity and policy application

## Work Completed

### Active Directory Users and Groups

* Created departmental test users:

  * Alice Martin — Finance
  * Bob Tremblay — HR
  * Charlie Nguyen — IT
  * Diana Roy — Security
* Created departmental security groups:

  * GG-Finance-Users
  * GG-HR-Users
  * GG-IT-Users
  * GG-Security-Users
* Added each test user to the appropriate security group.
* Verified the OU, user, and group structure.

### Windows 10 Domain Workstation

* Configured the Windows 10 VM to use `192.168.64.10` as its DNS server.
* Verified DNS resolution for `corp.freddys.local`.
* Verified connectivity to `AD-DC01.corp.freddys.local`.
* Joined the Windows 10 VM to the `corp.freddys.local` domain.
* Moved the workstation computer account into the `Workstations` OU.
* Renamed the workstation to `WS-01`.
* Verified domain membership after the rename.

### Security Baseline GPO

Created and linked:

`GPO-Workstation-Security-Baseline`

Configured:

* Windows Defender Firewall

  * Domain Firewall: Enabled
  * Inbound: Block
  * Outbound: Allow
* Account lockout policy

  * Threshold: 5 failed attempts
  * Lockout duration: 15 minutes
  * Observation window: 15 minutes
* Advanced Audit Policy

  * Logon
  * Logoff
  * Credential Validation
  * User Account Management
  * Process Creation
  * File System
  * Audit Policy Change
* PowerShell Script Block Logging
* PowerShell Script Block Invocation Logging
* PowerShell Module Logging
* Security Event Log maximum size: 100 MB

### Verification

Verified that `WS-01` successfully receives:

* GPO-Workstation-Security-Baseline
* Default Domain Policy

Verified PowerShell telemetry:

* Event ID 4104 — Script Block Logging
* Event ID 4103 — Module Logging

Verified that the configured audit policies remained active after renaming the workstation.

## Screenshots

* #33 — AD OU Structure
* #34 — AD Nested OU Structure
* #35 — AD Users and Groups
* #36 — AD User/Group Verification
* #37 — Workstation Computer Account
* #38 — Workstation Security Baseline GPO
* #39 — Account Lockout Policy
* #40 — Windows Firewall Baseline
* #41 — Windows Security/System Event Logging
* #42 — Advanced Audit Policy
* #43 — PowerShell Script Block Logging
* #44 — PowerShell Module Logging
* #45 — Security Event Log Retention
* #46 — Workstation GPO Baseline Applied
* #47 — WS-01 Domain Membership
* #48 — WS-01 Security Baseline Verification

## Day 3 Result

The Windows 10 workstation is now fully integrated into the Active Directory environment as `WS-01`, organized within the `Workstations` OU, and receiving a dedicated security baseline. The workstation is generating security and PowerShell telemetry that will be used for SOC monitoring and detection engineering in later project stages.

# Enterprise Active Directory SOC Lab

A hands-on enterprise Active Directory security lab designed to demonstrate Windows infrastructure administration, Active Directory security, detection engineering, logging, threat hunting, and incident response.

The environment simulates a small enterprise network and will progressively be expanded to generate realistic security telemetry and support SOC investigations.

---

## Project Objectives

- Deploy and configure an enterprise-style Windows Server environment
- Build and configure an Active Directory domain
- Implement baseline security controls
- Configure enterprise users, groups, and policies
- Generate and collect Windows security telemetry
- Develop SOC detection rules and queries
- Simulate realistic attack activity
- Investigate security incidents
- Map activity to MITRE ATT&CK techniques
- Document findings and remediation actions

---

## Lab Environment

| Component | Configuration |
|---|---|
| Hypervisor | VMware Workstation Pro |
| Host OS | Windows 11 |
| Server OS | Windows Server 2022 Standard Evaluation |
| Domain Controller | AD-DC01 |
| Active Directory Domain | corp.freddys.local |
| NetBIOS Domain | FREDDYS |
| Network | VMware NAT (VMnet8) |
| Lab Subnet | 192.168.64.0/24 |
| Domain Controller IP | 192.168.64.10 |

---

## Current Architecture

The lab currently contains a Windows Server 2022 domain controller providing:

- Active Directory Domain Services (AD DS)
- DNS
- Global Catalog
- Group Policy Management
- Active Directory management tools
- PowerShell-based administration

Additional endpoints, logging infrastructure, and security tooling will be added as the project progresses.

---

## Technologies

### Infrastructure

- Windows Server 2022
- Active Directory Domain Services
- DNS
- Group Policy
- VMware Workstation Pro
- PowerShell

### Security Operations

Planned security capabilities include:

- Windows Security Event Logging
- Sysmon
- SIEM / log aggregation
- Detection engineering
- Threat hunting
- PowerShell-based investigation
- Incident response
- MITRE ATT&CK mapping

---

## Project Progress

| Day | Focus | Status |
|---|---|---|
| Day 1 | Initial VM setup and Windows Server deployment | ✅ Complete |
| Day 2 | Windows Server baseline and Active Directory deployment | ✅ Complete |
| Day 3 | Enterprise domain configuration | ✅ Complete |
| Day 4 | Security logging and telemetry | ✅ Complete |
| Day 5 | Detection engineering and attack simulation | 🔲 Planned |
| Day 6 | Threat hunting and incident investigation | 🔲 Planned |
| Day 7 | Final validation and documentation | 🔲 Planned |

---

## Documentation

Project documentation is organized by function and daily activity.

```text
docs/
├── architecture/
│   └── active-directory-design.md
├── deployment/
│   └── server-baseline.md
└── daily-log/
    ├── daily-01.md
    └── daily-02.md
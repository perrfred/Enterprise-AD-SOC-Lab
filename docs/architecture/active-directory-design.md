# Active Directory Design

## Organization

The laboratory simulates a fictional organization named **Freddys Security**.

The organization is intentionally separate from the author's real-world
company and is used exclusively for the cybersecurity laboratory.

## Domain Architecture

| Component | Configuration |
|---|---|
| Organization | Freddys Security |
| Forest | corp.freddys.local |
| Domain | corp.freddys.local |
| NetBIOS Name | FREDDYS |
| Domain Controller | AD-DC01 |
| Domain Controller IP | 192.168.64.10 |
| DNS | AD-DC01 |
| Network | VMware VMnet8 |
| Network CIDR | 192.168.64.0/24 |

## Design Goals

The Active Directory environment is designed to simulate a small enterprise
identity infrastructure suitable for SOC monitoring, detection engineering,
threat hunting, incident response, and purple-team exercises.

The environment will provide centralized authentication, DNS,
organizational structure, Group Policy, Windows security logging,
and telemetry for Wazuh.

## Initial Services

AD-DC01 will initially provide:

- Active Directory Domain Services (AD DS)
- Active Directory-integrated DNS

DHCP will be evaluated separately to avoid unnecessarily concentrating
additional infrastructure roles on the Domain Controller.

## Planned Organizational Structure

The initial OU structure will include:

- Users
- Workstations
- Servers
- Groups
- Service Accounts
- Security
- Administrative accounts

The OU structure will be expanded as the laboratory develops.

## Security Objectives

The domain will eventually support:

- Centralized Windows authentication
- Group Policy security controls
- Advanced Windows auditing
- Sysmon telemetry
- Wazuh monitoring
- Detection engineering
- Threat hunting
- Incident response exercises
- Purple-team attack simulations
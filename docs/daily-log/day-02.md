# Day 2 – Windows Server Baseline & Active Directory Deployment

## Objective

Prepare the Windows Server 2022 environment and deploy the first Active Directory domain controller for the Freddys Security enterprise SOC lab.

## Environment

- Hypervisor: VMware Workstation Pro
- Host OS: Windows 11
- Server OS: Windows Server 2022 Standard Evaluation
- Virtual Machine: AD-DC01
- CPU: 2 vCPU
- Memory: 4 GB RAM
- Storage: 60 GB virtual disk
- Network: VMware NAT (VMnet8)
- Lab subnet: 192.168.64.0/24
- Server IP: 192.168.64.10
- Domain: corp.freddys.local
- NetBIOS domain: FREDDYS

## Windows Server Baseline

Completed the initial Windows Server baseline configuration and verification.

### Network Configuration

- Confirmed VMware NAT connectivity.
- Configured AD-DC01 with a static IPv4 address.
- Configured the server to use itself as the preferred DNS server.
- Verified network connectivity and DNS configuration.

### System Configuration

- Confirmed hostname: `AD-DC01`
- Confirmed Windows Server 2022 Standard Evaluation.
- Verified system storage and available resources.
- Confirmed Windows Firewall profiles are enabled.
- Verified Microsoft Defender Antivirus and real-time protection are enabled.
- Verified Windows Time service configuration.

### Updates

Windows Update was checked and available updates were installed where possible. Several update-related events remained in the system logs, but they did not prevent the Active Directory deployment or domain controller health checks from passing.

## Active Directory Domain Services Deployment

Installed the following Windows Server roles and management components:

- Active Directory Domain Services (AD DS)
- DNS Server
- Group Policy Management
- Active Directory management tools
- Active Directory PowerShell module

## New Forest Deployment

Configured AD-DC01 as the first domain controller in a new forest.

### Domain Configuration

- Root domain: `corp.freddys.local`
- NetBIOS domain name: `FREDDYS`
- Forest functional level: Windows Server 2016
- Domain functional level: Windows Server 2016
- Global Catalog: Enabled
- DNS Server: Enabled
- Read-Only Domain Controller: Disabled
- DNS delegation: Not created because this is an isolated lab environment.

### Active Directory Paths

Default AD DS paths were retained:

- Database: `C:\Windows\NTDS`
- Log files: `C:\Windows\NTDS`
- SYSVOL: `C:\Windows\SYSVOL`

## Domain Controller Verification

After the AD DS promotion and reboot, the domain controller was verified using PowerShell.

### Domain Verification

`Get-ADDomain` confirmed:

- DNS root: `corp.freddys.local`
- NetBIOS name: `FREDDYS`
- Forest: `corp.freddys.local`
- Domain controller: `AD-DC01.corp.freddys.local`

### Domain Controller Verification

`Get-ADDomainController` confirmed:

- Domain: `corp.freddys.local`
- Host name: `AD-DC01.corp.freddys.local`
- IPv4 address: `192.168.64.10`
- Global Catalog: Enabled
- Read-only status: False

### DNS Verification

`Get-DnsServerZone` was used to verify that DNS zones were created and available following the domain controller promotion.

### Service Verification

The following critical services were confirmed to be running automatically:

- NTDS
- DNS
- Netlogon

### AD Health Checks

`dcdiag` was used to validate the domain controller.

The following tests passed successfully:

- Connectivity
- Advertising
- NetLogons

The forest and domain partition tests also completed successfully.

## Documentation & Evidence

Day 2 evidence was captured in the following screenshots:

- `31-AD-Domain-Controller-DNS-Verification.png`
- `32-AD-Health-Check-Advertising-NetLogons.png`

## Snapshot

A VMware snapshot was created after successful AD DS deployment and verification.

**Snapshot:** `Day 2 - AD DS Deployment Complete`

## Day 2 Result

AD DS was successfully deployed and configured on AD-DC01.

The `corp.freddys.local` Active Directory forest is operational, DNS is functioning, and the domain controller successfully passed the required connectivity, advertising, and NetLogon health checks.

The environment is ready for the next phase of the Enterprise AD SOC Lab.
# Windows Server Baseline

## 1. Purpose

This document records the initial configuration and security baseline of
AD-DC01 before Active Directory Domain Services (AD DS) deployment.

The objective is to establish a known-good operating system, network, and
security baseline before introducing Active Directory infrastructure.

---

## 2. Server Specifications

| Component | Configuration |
|---|---|
| Hostname | AD-DC01 |
| Operating System | Windows Server 2022 Standard Evaluation |
| OS Build | 20348 |
| vCPU | 2 |
| RAM | 4 GB |
| Virtual Disk | 60 GB |
| Hypervisor | VMware Workstation Pro |
| Network Type | VMware NAT / VMnet8 |

---

## 3. Network Configuration

| Parameter | Configuration |
|---|---|
| Network | VMnet8 |
| Network Type | NAT |
| Subnet | 192.168.64.0/24 |
| AD-DC01 IP | 192.168.64.10 |
| Subnet Mask | 255.255.255.0 |
| Default Gateway | 192.168.64.2 |
| Temporary DNS | 192.168.64.2 |
| DHCP Range | 192.168.64.128 - 192.168.64.254 |

The server was initially configured using DHCP to identify the VMware
NAT network parameters. A static IPv4 address was subsequently assigned
to provide predictable addressing for future Active Directory services.

---

## 4. Network Validation

The following connectivity tests were successfully completed:

- VMware NAT gateway connectivity
- External IP connectivity
- DNS resolution
- Hostname-based connectivity

The server was confirmed to have functional network connectivity before
continuing with the Active Directory deployment.

---

## 5. Time Synchronization

Windows Time synchronization was verified using `w32tm`.

The system reported a successful synchronization with the configured
Windows time service.

Time synchronization is particularly important for Active Directory
because Kerberos authentication relies on synchronized system clocks.

---

## 6. Windows Firewall

Windows Defender Firewall was confirmed to be enabled for:

- Domain profile
- Private profile
- Public profile

No firewall profiles were disabled during the baseline process.

Detailed firewall configuration will be revisited after AD DS deployment
when Active Directory-specific network requirements are introduced.

---

## 7. Microsoft Defender

Microsoft Defender status was checked before AD DS deployment.

The following protections were enabled:

- Antimalware service
- Antivirus
- Antispyware
- Real-time protection
- Behavior monitoring
- IOAV protection

---

## 8. Windows Update

Windows Update was initiated during the initial server baseline.

Security and cumulative updates were downloaded and installation/reboot
cycles were performed. Some updates remained pending due to installation
issues encountered during the lab setup.

The project therefore records the patching state as a known baseline
limitation rather than treating the system as fully patched.

---

## 9. VMware Tools

VMware Tools was installed to provide proper guest integration and virtual
display functionality.

The installation corrected the initial low-resolution display behavior
and allowed the Windows Server guest to use an appropriate display
resolution.

---

## 10. Security Considerations

The server is currently an isolated laboratory system running on the
VMware NAT network.

No Internet-facing services are exposed directly from the VM.

The server has not yet been promoted to a Domain Controller and does not
currently provide Active Directory, DNS, or DHCP services.

---

## 11. Baseline Evidence

Relevant screenshots are stored under:

`Screenshots/02-Windows-Server-Baseline/`

Evidence includes:

- Windows Server installation
- Hostname verification
- Network configuration
- VMware VMnet8 configuration
- DHCP range
- Static IP configuration
- Connectivity testing
- Windows Update state
- Time synchronization
- Windows Firewall status
- Microsoft Defender status
- System configuration

---

## 12. Next Phase

The next stage is deployment of:

1. Active Directory Domain Services
2. DNS Server
3. Active Directory forest
4. Domain Controller configuration

The server will then become the central identity and authentication
component of the enterprise SOC laboratory.
# Day 6 — SOC Incident Investigation & Response

## Objective

Use the detection and telemetry collected during Day 5 to investigate a simulated authentication security incident as a SOC analyst.

The investigation focused on validating the incident, determining its scope and severity, establishing an incident timeline, performing containment and credential remediation, and verifying recovery.

---

## Incident Investigated

**Incident ID:** `INC-2026-001`

**Incident Type:** Suspected Brute-Force Authentication Attempt

**Affected Account:** `Alice.Martin`

**Source Workstation:** `WS-01`

**Domain Controller:** `AD-DC01`

**Severity:** Medium

**Final Status:** Closed — No Evidence of Successful Compromise

---

## 1. Incident Evidence Validation

The investigation began by reviewing Windows Security Event ID 4625 records on `WS-01`.

Five failed authentication attempts targeting `Alice.Martin` were confirmed within approximately 25 seconds.

The observed events occurred at:

| Time | Event |
|---|---|
| 18:36:05 | 4625 — Failed logon |
| 18:36:11 | 4625 — Failed logon |
| 18:36:17 | 4625 — Failed logon |
| 18:36:26 | 4625 — Failed logon |
| 18:36:30 | 4625 — Failed logon |

**Evidence:** `64-WS01-Incident-Evidence-4625.png`

---

## 2. Account Lockout Investigation

The domain controller was then investigated for the resulting account lockout.

AD-DC01 generated Windows Security Event ID 4740 at approximately 18:36:30.

The event identified:

- Locked account: `alice.martin`
- Caller computer: `WS-01`
- Domain: `FREDDYS`

This established the relationship between the repeated authentication failures on `WS-01` and the account lockout recorded by the domain controller.

**Evidence:** `65-ADDC01-Incident-Account-Lockout.png`

A detailed review of the Event ID 4740 record confirmed the affected account and originating workstation.

**Evidence:** `66-ADDC01-Incident-Lockout-Details.png`

---

## 3. Successful Authentication Verification

The investigation checked AD-DC01 for Windows Security Event ID 4624 records associated with `Alice.Martin` between 18:30 and 18:40 on September 5, 2026.

**Result:** No successful logon was found for `Alice.Martin` during the investigation window.

This provided no evidence of successful authentication during the simulated attack.

**Evidence:** `67-ADDC01-No-Successful-Logon-Detected.png`

---

## 4. Incident Scope Analysis

The failed authentication events were grouped by affected account during the investigation window.

The results showed:

| Account | Failed Attempts |
|---|---:|
| Alice.Martin | 5 |

No other accounts were identified as targets during the investigation window.

The incident was therefore assessed as limited to a single domain account and one workstation.

**Evidence:** `68-WS01-Incident-Scope-Single-Account.png`

---

## 5. Account Containment

As an additional containment measure, the affected domain account was disabled using Active Directory administrative controls.

Verification confirmed:

```text
alice.martin    False
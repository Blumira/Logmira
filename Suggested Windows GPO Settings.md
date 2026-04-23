# Suggested Windows GPO Settings

Logmira is provided to help people quickly enable suitable logging for Windows systems. The settings below reflect the current Logmira GPO policy, aligned to CIS Benchmark Level 1 (L1) recommendations.

If you would like to create your own policy instead, refer to the documentation below.

---

### Enable Advanced Auditing
* `Computer Configuration > Policies > Windows Settings > Security Settings > Local Policies > Security Options`
  * Enable **Force audit policy subcategory settings** (Windows Vista or later) to override audit policy category settings
* [Enable command-line logging](https://github.com/Blumira/Logmira/blob/master/Advanced%20Microsoft%20Commandline%20Logging%20via%20GPO.md)
* Event Log Sizes
  * `Computer Configuration > Policies > Windows Settings > Security Settings > Event Log`
  * Set the following values from the table below:

| Property | Value |
|:---|:---|
| Application Log Size | 16,384 KB (16 MB minimum) |
| Security Log Size | 2,048,000 KB (2 GB minimum recommended) |
| System Log Size | 16,384 KB (16 MB minimum) |

---

### Advanced Audit Policy Settings

Configure Advanced Audit Policies at:
`Computer Configuration > Policies > Windows Settings > Security Settings > Advanced Audit Policy Configuration > Audit Policies`

| Account Logon | Suggested Values |
|:---|:---|
| Credential Validation | Success and Failure |
| Kerberos Authentication Service | Success and Failure |
| Kerberos Service Ticket Operations | Success and Failure |
| Other Account Logon Events | Success and Failure |

| Account Management | Suggested Values |
|:---|:---|
| Application Group Management | Success and Failure |
| Computer Account Management | Success and Failure |
| Distribution Group Management | Success and Failure |
| Other Account Management Events | Success and Failure |
| Security Group Management | Success and Failure |
| User Account Management | Success and Failure |

| Detailed Tracking | Suggested Values |
|:---|:---|
| DPAPI Activity | No Auditing |
| PNP (Plug and Play) | Success |
| Process Creation | Success |
| Process Termination | No Auditing |
| RPC Events | Success and Failure |
| Token Right Adjusted | Success |

| DS Access | Suggested Values |
|:---|:---|
| Detailed Directory Service Replication | No Auditing |
| Directory Service Access | Success and Failure |
| Directory Service Changes | Success and Failure |
| Directory Service Replication | No Auditing |

| Logon/Logoff | Suggested Values |
|:---|:---|
| Account Lockout | Success and Failure |
| Group Membership | Success |
| IPsec Extended Mode | No Auditing |
| IPsec Main Mode | No Auditing |
| IPsec Quick Mode | No Auditing |
| Logoff | Success |
| Logon | Success and Failure |
| Network Policy Server | Success and Failure |
| Other Logon/Logoff Events | Success and Failure |
| Special Logon | Success and Failure |
| User / Device Claims | No Auditing |

| Object Access | Suggested Values |
|:---|:---|
| Application Generated | Success and Failure |
| Central Access Policy Staging | No Auditing |
| Certification Services | Success and Failure |
| Detailed File Share | Failure |
| File Share | Success and Failure |
| File System | No Auditing |
| Filtering Platform Connection | No Auditing |
| Filtering Platform Packet Drop | No Auditing |
| Handle Manipulation | No Auditing |
| Kernel Object | No Auditing |
| Other Object Access Events | Success and Failure |
| Registry | No Auditing |
| Removable Storage | Success and Failure |
| SAM | Success |

| Policy Change | Suggested Values |
|:---|:---|
| Audit Policy Change | Success and Failure |
| Authentication Policy Change | Success and Failure |
| Authorization Policy Change | Success and Failure |
| Filtering Platform Policy Change | Success |
| MPSSVC Rule-Level Policy Change | Success and Failure |
| Other Policy Change Events | Success and Failure |

| Privilege Use | Suggested Values |
|:---|:---|
| Non Sensitive Privilege Use | No Auditing |
| Other Privilege Use Events | No Auditing |
| Sensitive Privilege Use | Success and Failure |

| System | Suggested Values |
|:---|:---|
| IPsec Driver | Success and Failure |
| Other System Events | Success and Failure |
| Security State Change | Success and Failure |
| Security System Extension | Success and Failure |
| System Integrity | Success and Failure |

| Global Object Access Auditing | Suggested Values |
|:---|:---|
| File System | No Auditing |
| Registry | No Auditing |

---

### Enable PowerShell Logging

PowerShell logging must be configured under **Computer Configuration** to ensure it applies to all users on the machine, including local accounts. Configuring it under User Configuration alone is insufficient for CIS L1 compliance.

**Computer Configuration** (required — applies to all users on the machine):
`Computer Configuration > Policies > Administrative Templates > Windows Components > Windows PowerShell`

| PowerShell Logging | Suggested Values |
|:---|:---|
| Turn on Module Logging | Enabled |
| Module Names | * |
| Turn on PowerShell Script Block Logging | Enabled |
| Log script block invocation start / stop | Enabled |

**User Configuration** (supplemental — applies per-user GPO scope):
`User Configuration > Policies > Administrative Templates > Windows Components > Windows PowerShell`

| PowerShell Logging | Suggested Values |
|:---|:---|
| Turn on Module Logging | Enabled |
| Module Names | * |
| Turn on PowerShell Script Block Logging | Enabled |
| Log script block invocation start / stop | Enabled |

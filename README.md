# Logmira GPO — Overview and Deployment Guidance

The Logmira GPO is a **logging and auditing baseline** for Windows environments. It enables the audit categories, PowerShell logging, and event log sizes that Blumira recommends for meaningful security visibility. It is aligned to CIS Benchmark Level 1 (L1) recommendations.

This GPO is intentionally scoped to *what to record* — not how to respond, restrict, or harden the system. Password policy, account lockout thresholds, user rights assignments, firewall rules, and other enforcement settings are outside its scope and should be managed separately based on your environment's requirements.

---

## What This GPO Configures

- **Advanced Audit Policy subcategories** — specific Success/Failure logging for ~42 subcategories across Account Logon, Account Management, DS Access, Logon/Logoff, Object Access, Policy Change, Privilege Use, and System categories
- **PowerShell Module Logging and Script Block Logging** — under both Computer Configuration and User Configuration
- **Process creation command-line logging** — records full command-line arguments in Event ID 4688
- **Event log sizes** — Security log set to 2 GB minimum; Application and System to 16 MB minimum
- **Force audit subcategory override** — ensures advanced audit policy subcategory settings take precedence over legacy category-level settings (`SCENoApplyLegacyAuditPolicy`)

---

## What This GPO Does Not Configure

- Password complexity, length, or expiration policy
- Account lockout thresholds
- User rights assignments (e.g., logon rights, privilege grants)
- Windows Firewall rules
- BitLocker, AppLocker, or application control policies
- Any settings that restrict or block behavior

These are environment-specific and require separate, intentional configuration.

---

## Policy Ordering and Precedence

Windows processes GPOs in **Local → Site → Domain → OU** order. OU-linked GPOs have the highest precedence and will override settings from GPOs applied at higher (broader) scopes. Within the same level, GPO link order determines precedence — lower link order numbers win.

**Recommended deployment approach:**

Apply Logmira at the **domain level or a broad OU** as a baseline. Any more specific or restrictive audit policies you define at a lower OU level will override it for machines in that OU. This lets you tune logging up or down for specific machine groups without modifying the baseline.

If two GPOs configure the same audit subcategory, the GPO with higher precedence wins for that specific setting. Logmira is designed to be a floor, not a ceiling — it sets minimum recommended values. A higher-precedence GPO that enables `Success and Failure` where Logmira only requires `Success` is additive and compatible.

**The `Force audit policy subcategory settings` option** (`SCENoApplyLegacyAuditPolicy`) is enabled in this GPO. This ensures subcategory-level settings (like those in this GPO) are not silently overridden by older category-level audit policy settings that some legacy GPOs or tools may write. If you have existing category-level audit policies in your environment, this setting is required for subcategory settings to take effect.

## Conflict Resolution Between GPOs

If this GPO conflicts with an existing GPO in your environment, the resolution depends on which has higher precedence (see above). Common scenarios:

| Scenario | Outcome |
|:---|:---|
| Existing GPO sets a subcategory to `Success and Failure`; Logmira sets it to `Success` | Existing GPO wins if it has higher precedence — no regression |
| Existing GPO sets a subcategory to `No Auditing`; Logmira sets it to `Success and Failure` | Whichever has higher precedence wins — review intentionally |
| Existing GPO uses legacy category-level audit settings | `SCENoApplyLegacyAuditPolicy` in Logmira ensures subcategory settings win regardless |
| No existing audit GPO | Logmira settings apply as configured |

Before deploying, you may run `gpresult /h gpresult.html` on a representative machine to identify any existing audit policy GPOs.

---

## Deploying the GPO

1. In Group Policy Management Console, Right-Click on **Group Policy Objects** and choose "New"
2. Right-Click on the new policy you created and choose **Import Settings**
3. Click **Next** twice, then browse to the folder where Logmira was unzipped and select "Logmira", then proceed to **Finish**
4. Afterwards, link the imported GPO to the desired scope (domain, site, or OU).
5. Set the **Security Filtering** to Domain Computers, Domain Controllers, and Domain Users.

---

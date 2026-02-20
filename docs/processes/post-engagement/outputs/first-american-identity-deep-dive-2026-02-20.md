# Post-Engagement Summary — Identity Deep-Dive with First American

## Whiteboard Discovery Record

| Field | Value |
|---|---|
| File name | `Identity Deep-dive with First American @Microsoft Irvine.png` |
| Location | `docs/processes/post-engagement/Whiteboards/` |
| Last modified | 2026-02-20 10:45 AM |
| Analysis method | Option B — Visual analysis of exported whiteboard image |

---

## Summary

### 1. Core Themes

- **Current identity architecture** — Hybrid AD/Entra environment with heavy reliance on legacy protocols (NTLM/LDAPS), Silverlight dependencies, and a mix of on-prem and cloud identity surfaces.
- **Future state direction** — Full Entra ID as the primary identity plane, elimination of AD over time, OAuth as the authentication standard, and a passwordless end-user experience.
- **Non-human identity gap** — Service Principal Names (SPNs) and Service Accounts flagged as a critical area requiring Agent ID / Non-human Identity coverage.
- **Legacy protocol risk** — NTLM/LDAP persists in the future state (highlighted in red) as a hard dependency for apps and servers (RDP, SQL, etc.), and is the key blocker to full modernization.
- **Privileged access and token control** — Detailed work around GSAC, Continuous Access Evaluation (CAE), and Access Token Revocation to harden privileged and remote access paths.

---

### 2. Key Decisions

| Decision | Detail |
|---|---|
| **Entra ID as primary IdP** | Replacing AD as the authoritative identity source going forward |
| **No AD in the future** | Explicitly marked with ✗ — AD is targeted for elimination |
| **OAuth as the standard** | Replacing legacy auth protocols wherever possible |
| **Passwordless target** | WHFB (Windows Hello for Business) + Touch ID for macOS; Entra Joined devices |
| **DWB deprecated** | Desktop Workplace Join (DWB) crossed out in the future-state diagram |
| **MDA left in Audit mode** | Microsoft Defender for Cloud Apps currently in audit mode only (asterisked) |
| **Silverlight is a blocker** | Circled as a legacy dependency on AD Forest CORP — needs remediation path |
| **PHS retained** | Password Hash Sync kept in both current and future state as a fallback |

---

### 3. Action Items

| # | Action | Area |
|---|---|---|
| 1 | Define remediation path for **Silverlight** dependency on AD Forest | App Modernization |
| 2 | Inventory and classify all **SPNs and Service Accounts** (Non-human Identities) | NHI / Agent ID |
| 3 | Plan **NTLM/LDAP elimination** for apps, RDP, and SQL workloads — or wrap with GSAC/CAE controls | Legacy Protocol |
| 4 | Move **MDA from Audit mode to enforcement** after baselining alerts | Security |
| 5 | Finalize **Provisioning Engine** design (WorkDay → Prov. Engine → Entra/AD path) | IGA |
| 6 | Scope **App Segmentation** (VNET / DC Sites) for server FQDN access (LS1, S27) | Network / Zero Trust |
| 7 | Define **CAE + GSAC** policy scope for RDP/NTLM/3389 and CDAP/SQL Mgt Studio access | PAM / Privileged Access |
| 8 | Validate **EIA + EPA** (Enterprise Integration / Privileged Access) alignment to GSAC | Architecture |
| 9 | Confirm **B2B/B2C** use cases and ownership within Entra External ID | Identity |
| 10 | Evaluate **SailPoint integration** role in the future state (currently feeds Exch Relay) | IGA |

---

### 4. Technical Details

#### Current State
- **AD:** Multi-forest topology (Forest + AD Forest CORP); central identity plane
- **Entra:** Connected via PHS; handling B2B, B2C, SSPR, GWB, PWB
- **Auth protocols:** NTLM/LDAPS actively in use (circled); Palo Alto ZTNA + CA + ZTNA overlay present
- **Devices:** Windows 11 (Hybrid Joined + Entra Joined), managed via SCCM + Intune; Intune + Compliance enforced; 11 MDE deployed
- **IGA:** SailPoint integrated; feeds Exchange Relay + Sailpoint relay
- **Email:** Exchange Hybrid + Email Gateway
- **Legacy app:** Silverlight running on AD Forest CORP — no modern auth
- **Access control:** Conditional Access (CA) gating SSO → MFA → Azure/AWS/SaaS; MFA supports Auth passkeys + FIDO2
- **Servers:** S1 on-prem; MDA in Audit mode

#### Future State
- **Identity plane:** Entra ID primary; AD retained as a transitional sync source only, targeted for removal
- **Provisioning:** WorkDay → Provisioning Engine → AD (interim) → Entra
- **Devices:** Windows 11 + macOS; WHFB + Touch ID (Passwordless); Entra Joined
- **Auth:** OAuth standard; PWB, GWB retained; DWB removed
- **MFA + SSO:** Entra-native MFA and SSO; CA enforced
- **Legacy path (red):** NTLM/LDAP still flows to Apps/Servers (RDP, SQL, MS services) — not yet eliminated
- **Privileged access stack:**
  - GSAC as the gateway for RDP/NTLM/3389 and CDAP/SQL Mgt Studio
  - Trusted CA → MFA
  - CAE + GSAC for continuous access enforcement
  - Access Token Revocation capability
  - EIA + EPA policies in scope
- **Network:** VNET ↔ App Segmentation (DC Sites); server access via FQDN (LS1, S27)
- **Apps in scope:** Browser, Outlook, Cache PSTs, OneDrive
- **Cloud targets:** Azure VMs, SaaS

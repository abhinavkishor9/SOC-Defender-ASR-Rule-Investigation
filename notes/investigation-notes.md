# Investigation Notes

## Scenario

The SOC team receives an alert indicating that Microsoft Defender configuration has changed on a workstation.

The analyst must determine:

- Was a security feature enabled?
- Was Defender tampered with?
- Was the change expected?
- Does it reduce or increase endpoint security?

---

# Initial Verification

Microsoft Defender health was verified using:

```powershell
Get-MpComputerStatus
```

Result:

- Defender Running
- Real-Time Protection Enabled
- Antivirus Enabled

No issues observed.

---

# ASR Configuration Review

Existing ASR configuration was reviewed.

Command:

```powershell
Get-MpPreference | Select AttackSurfaceReductionRules_Ids, AttackSurfaceReductionRules_Actions
```

The ASR rule was not previously configured.

---

# Configuration Change

Enabled ASR Rule:

```
Block executable files from running unless they meet a prevalence, age, or trusted list criterion
```

GUID

```
01443614-CD74-433A-B99E-2ECDC07BFC25
```

---

# Validation

PowerShell confirmed the rule was successfully added.

---

# Event Viewer Investigation

Location

Applications and Services Logs

Microsoft

Windows

Windows Defender

Operational

---

Observed Event

Event ID:

5007

Meaning:

Microsoft Defender configuration changed.

The event contained the newly added ASR Rule GUID.

---

# Timeline

08:xx

Defender health verified

↓

Existing ASR configuration reviewed

↓

ASR Rule enabled

↓

PowerShell confirmed configuration

↓

Event ID 5007 generated

↓

SOC investigation completed

↓

ASR Rule removed

---

# SOC Assessment

The configuration change was expected.

No indicators of malicious activity were identified.

No Defender tampering observed.

The change successfully increased endpoint protection.

---

# MITRE ATT&CK

T1204

User Execution

T1562.001

Impair Defenses (Configuration Monitoring)

T1059

Command & Scripting Interpreter

---

# Conclusion

The Defender configuration change was legitimate and administrator initiated.

The generated Event ID 5007 can be used by SOC teams to monitor unauthorized Defender configuration changes.

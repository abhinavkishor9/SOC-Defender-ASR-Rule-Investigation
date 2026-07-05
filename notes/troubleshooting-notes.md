# Troubleshooting Notes

## Problem

ASR rule does not appear after enabling.

### Solution

Verify using

```powershell
Get-MpPreference
```

---

## Problem

Permission denied

### Solution

Open PowerShell as Administrator.

---

## Problem

Event ID 5007 not generated

### Solution

Refresh Event Viewer.

Wait 30–60 seconds.

Review the Defender Operational log again.

---

## Problem

Multiple ASR Rules Displayed

This is expected.

Microsoft Defender supports multiple Attack Surface Reduction rules simultaneously.

---

## Problem

Rule Removal Failed

Run:

```powershell
Remove-MpPreference -AttackSurfaceReductionRules_Ids 01443614-CD74-433A-B99E-2ECDC07BFC25
```

Then verify:

```powershell
Get-MpPreference | Select AttackSurfaceReductionRules_Ids
```

---

## Problem

Event Viewer does not show Defender Operational log

Verify that Microsoft Defender Antivirus is enabled.

Run:

```powershell
Get-MpComputerStatus
```

Confirm:

- AntivirusEnabled = True
- RealTimeProtectionEnabled = True

---

## Lessons Learned

- Event ID 5007 records Defender configuration changes.
- PowerShell provides reliable validation of ASR configuration.
- Defender Operational logs should always be reviewed after security configuration changes.
- ASR rules help reduce endpoint attack surface and should be monitored by SOC analysts.

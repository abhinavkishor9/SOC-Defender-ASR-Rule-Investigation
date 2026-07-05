# SOC-Defender-ASR-Rule-Investigation
## Overview

This lab demonstrates how a SOC analyst can investigate Microsoft Defender Attack Surface Reduction (ASR) rule configuration changes.

The objective is to:

- Verify Microsoft Defender health
- Enable an ASR rule
- Validate Defender configuration
- Investigate Windows Defender Operational logs
- Correlate PowerShell and Event Viewer evidence
- Map findings to MITRE ATT&CK
- Remove the ASR rule after validation

---

## Lab Objectives

- Verify Microsoft Defender status
- Review existing ASR configuration
- Enable an Attack Surface Reduction rule
- Validate configuration using PowerShell
- Review Windows Defender Operational logs
- Investigate Defender Event ID 5007
- Perform SOC analysis
- Remove the ASR rule after investigation

---

## Tools Used

- Windows Security
- Microsoft Defender Antivirus
- Windows Event Viewer
- PowerShell
- Microsoft Defender Operational Log

---

## Commands Used

Verify Defender

```powershell
Get-MpComputerStatus
```

View existing ASR rules

```powershell
Get-MpPreference | Select AttackSurfaceReductionRules_Ids, AttackSurfaceReductionRules_Actions
```

Enable ASR Rule

```powershell
Add-MpPreference -AttackSurfaceReductionRules_Ids 01443614-CD74-433A-B99E-2ECDC07BFC25 -AttackSurfaceReductionRules_Actions Enabled
```

Verify configuration

```powershell
Get-MpPreference | Select AttackSurfaceReductionRules_Ids, AttackSurfaceReductionRules_Actions
```

Review Defender logs

```powershell
Get-WinEvent -LogName "Microsoft-Windows-Windows Defender/Operational" -MaxEvents 30
```

Remove ASR Rule

```powershell
Remove-MpPreference -AttackSurfaceReductionRules_Ids 01443614-CD74-433A-B99E-2ECDC07BFC25
```

---

## Findings

The Defender Operational log generated **Event ID 5007**, confirming that Microsoft Defender configuration changed after enabling the ASR rule.

PowerShell verification confirmed the ASR rule was successfully added.

Cleanup successfully removed the ASR rule.

---

# MITRE ATT&CK Mapping

| Technique | Description |
|-----------|-------------|
| T1204 | User Execution |
| T1562.001 | Impair Defenses (Configuration Changes) |
| T1059 | Command and Scripting Interpreter |
| T1105 | Ingress Tool Transfer |
| T1566 | Phishing |

---

## Skills Demonstrated

- Microsoft Defender
- Windows Security
- Attack Surface Reduction
- PowerShell
- Event Viewer
- Security Investigation
- Detection Validation
- SOC Analysis
- Windows Endpoint Security

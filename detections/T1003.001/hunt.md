# Hunt: LSASS Memory Access (T1003.001)

## Hypothesis
Adversaries are dumping LSASS memory to extract credentials.

## ATT&CK Information
- **Tactic:** Credential Access (TA0006)
- **Technique:** OS Credential Dumping: LSASS Memory (T1003.001)

## Required Data Sources
- Sysmon Event ID 10 (ProcessAccess)
- Windows Security Event ID 4656 (A handle to an object was requested)

## Attack Behavior
Tools like Mimikatz or procdump request specific access rights (e.g., 0x1010 or 0x143a) to the `lsass.exe` process to read its memory contents. 

## Expected False Positives and Tuning
- Endpoint Detection and Response (EDR) agents may routinely access LSASS.
- System processes like `taskmgr.exe` may request access if a user manually creates a dump.
- **Tuning:** Exclude known good processes by paths and signatures.

## Triage
1. Identify the SourceImage (the process requesting access).
2. Check if the SourceImage is a known, approved administrative or security tool.
3. Review related events for the SourceImage (e.g., process creation, network connections).

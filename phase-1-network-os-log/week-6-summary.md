# Phase 1 - Week 6 - Summary
Date: 07/04/2026
Focus: Windows Security Auditing & Anti-Forensics

##  Topic covered
- Windows Authentication Logs (4624 & 4625)
- Account Management (4720, 4722, 4732)
- Windows Service & Scheduled Tasks (7045 & 4698)
- Anti-Forensics (Detecting Log Tampering)

## Technical understanding 

### Windows Authentication
- Event ID 4624 (Success) & 4625 (Failure)
- The importance of Logon Type:
    + Type 2: Interactive (Direct access)
    + Type 3: Network (SMB, Shared folders)
    + Type 10: RemoteInteractive (RDP)
- Use Source Network Address to identify the attacker's location

### Account Management (Subject vs Target)
- Subject: The user who performed the action (The attacker)
- Target: The account that was modified (The victim/new user)
- Privilege Escalation: Detected when SubjectUserName is the same as TargetUserName in Event 4732

### Persistence Mechanisms
- Event ID 7045 (New Service): Monitor ImagePath for suspicious locations like \Temp, \Public, \AppData
- Event ID 4698 (New Task): Monitor for LOLBins (bitsadmin.exe, certutil.exe) downloading payloads

### Anti-Forensics (Log Tampering)
- Event ID 1102: Security Log was cleared (Critical Alert)
- Event ID 104: System Log was cleared
- Event ID 4719: Audit Policy was changed (Attackers disable logging to hide their tracks)

## Detection Thinking practice
**IF** Event ID == 4732
**AND** GroupName == "Administrators"
**AND** SubjectUserName == TargetUserName
**THEN** Alert: Possible Privilege Escalation attack

**IF** Event ID == 7045
**AND** ImagePath CONTAINS ("Temp" OR "Public" OR "AppData")
**THEN** Alert: Persistence via Suspicious Service Path

## Skill Improved
- Mastering Windows Event ID correlation
- Understanding the lifecycle of an attack (Access -> Privilege -> Persistence -> Cleanup)

## Improvement area
- Need more practice with Regex to filter ImagePath more accurately

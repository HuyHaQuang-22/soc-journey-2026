# Phase 1 - Week 9 - Summary
Date: 27/04/2026
Focus: Incident Response (NIST SP 800-61) & Threat Hunting

## Topic covered
- NIST SP 800-61 Incident Response Lifecycle (Preparation, Detection, Containment, Eradication, Recovery)
- Incident Response Methodologies: Containment tactics, Order of Volatility
- Recovery Strategies: Re-imaging vs Patching vs Restore from Backup
- Threat Hunting: Hypothesis-driven hunting & LOLBins detection
- Persistence Mechanisms Analysis: Registry/Run keys, Scheduled Tasks
- Incident Reporting & Stakeholder Communication

## Technical understanding 

### NIST Incident Response Lifecycle
- IR Workflow: Understanding the critical order of Containment -> Eradication -> Recovery to minimize damage
- Order of Volatility: Prioritizing RAM acquisition (volatile evidence) before disk imaging to avoid data loss

### Containment & Recovery Strategy
- Containment Tactics: Differentiating between Logical Isolation (VLAN/Firewall) and Physical Isolation based on incident severity
- Remediation Decision Making:
  - Re-imaging: System integrity restoration via "Golden Images"
  - Patching: Addressing CVEs to eliminate root cause
  - Restoration: Secure data recovery from verified backups

### Threat Hunting Principles
- Proactive Hunt: Shifting from reactive alerting to hypothesis-driven scanning
- LOLBins Detection: Monitoring abuse of native binaries (`powershell.exe`, `certutil.exe`) using anomalous arguments (e.g., `-EncodedCommand`, `-w hidden`)
- Persistence Identification: Auditing unauthorized entries in autostart locations to uncover deep-seated threats

## Incident Response & Hunting practice
**IF** Host_Anomaly_Detected
**THEN** Step 1: Contain (Isolate via Network/Account Lock)
**THEN** Step 2: Acquire (Snapshot RAM/Disk)
**THEN** Step 3: Eradicate (Re-image or Patch)

**IF** Hunting_Hypothesis == "LOLBins_Abuse"
**AND** Command_Line contains ("-enc" OR "-w hidden")
**THEN** Alert: Suspicious PowerShell Execution (Threat Hunting)

**IF** Persistence_Found == "Scheduled_Task"
**THEN** Action: Extract_Metadata AND Analyze_Payload AND Eradicate

## Skill Improved
- Proficiency in executing the NIST-standard Incident Response lifecycle
- Strategic decision-making skills: Choosing between Clean/Patch vs. Re-image
- Development of a proactive "Threat Hunter" mindset for identifying hidden persistence
- Technical documentation: Translating technical IR logs into executive/business-oriented summaries
- Advanced recursion & backtracking logic in C++ for algorithmic optimization

## Improvement area
- Automating IR playbooks (SOAR) to reduce Time to Containment (TTC)
- Expanding Threat Hunting hypotheses for Active Directory lateral movement detection
- Deepening knowledge in forensic artifact analysis during the eradication phase

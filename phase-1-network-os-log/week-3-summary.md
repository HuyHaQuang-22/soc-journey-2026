# Phase 1 - Week 3 - Summary
Date: 16/03/2026
Focus: attack -> detection

## Topic covered
- attack -> artifact -> log -> detection
- analyzing key fields in a log entry
- normal vs suspicious log behaviour
- detection rule basis

## Technical understanding

### Attack-to-Detection Workflow
- after an attack occurs, it usually leaves traces (artifacts)
- these artifacts are recorded in system logs
- soc analysts analyze those logs and create detection rules to identify attacks

### Normal vs Suspicious log behaviour
- normal log behaviour matches an user's usual activity pattern
- suspicious log behaviour is differtent from the user's usual behaviour or contains signs of attack
- soc analysts have to use context, pattern, baseline behaviour - not just a single log line

###  Detection rule basis
- formula:
    **IF** suspicious condtions
    **THEN** trigger an alert
 - a strong detection rule includes enough relevant conditions directly related to the attack behavior
## Detection thinking practice
- scenario:
there is an ip try to login fail many different user from 1 server within 10 minutes
- detection rule:
    **IF** one source ip fails login for 5 or more distinct usernames within 10 minutes
    **AND** each username has fewer then 5 failed login attempts
    **AND** followed by a successful login within 10 minutes
    **THEN** possible successful password spraying leading to account compromise

## Skills improved
- improved detection rule writing
- stronger attack-to-detection thinking

## Improvement area
- need more hands-on labs
- need more practice with real log patterns

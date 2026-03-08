# Phase 1 – Week 2 Summary
Date: 08/03/2026
Focus: Log & SIEM Foundation

## Topics Covered
- Log pipeline
- Brute force Detection logic
- IOC (Indicator of Compromise)
- SOC Detection

## Technical Understanding

### Brute force
- Understand the attack pattern
- Observe Brute force attack by Youtube

### IOC
- Indicator show the server maybe compromised (IP, domain, hash, ...)
- IOC can be found in log

### Detection Logic
- Rule/Logic that used to recognize attack based on IOC or behaviour
- SOC Detection include:
  + IOC-based Detection
  + Rule-based Detection
  + Behaviour-based Detection
- SOC alert flow : Log -> SIEM -> Detection Rule -> Alert -> SOC investigation

## Detection Thinking Practice
Scenario:
There is a failed login from other country different with your normal location.

Detection Logic:
- IF login location ≠ user's normal location
- THEN trigger suspicious login alert

## Skills Improved
- Basic brute force attack pattern recognition
- Know how to check the IOC

## Improvement Areas
- Need deeper understanding of Windows Event Logs

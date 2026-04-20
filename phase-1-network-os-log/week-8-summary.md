# Phase 1 - Week 8 - Summary
Date: 20/04/2026
Focus: SOC Analysis, Centralized Logging & Detection Engineering

## Topic covered
- SIEM Architecture & ELK Stack (Winlogbeat, Logstash, Elasticsearch, Kibana)
- Log Lifecycle: Generation, Forwarding, Normalization & Enrichment
- Kibana Query Language (KQL) & Splunk Processing Language (SPL)
- Detection Engineering & Correlation Rules
- Log Integrity & Anti-Tampering (EventID 1102)

## Technical understanding 

### SIEM Architecture & Log Flow
- Understanding the pipeline: Endpoints (Raw Log) -> Winlogbeat (Agent) -> Logstash (Enrichment) -> Elasticsearch (Indexing/Storage) -> Kibana (Visualization).
- Log Forwarding: Importance of real-time log forwarding to secure SIEM servers before potential tampering/clearing by attackers.
- Data Structure: Converting raw binary Windows events (`.evtx`) to structured JSON using ECS (Elastic Common Schema).

### KQL vs SPL
- KQL (Kibana): Used for investigation/searching within the Elastic stack.
- SPL (Splunk): Used for complex searching, statistical analysis, and manipulation (pipes/functions).
- Core Concept: Querying is not about "reading the log file" but "raiding the indexed database".

### Correlation & Detection Engineering
- Detection Thinking: Identifying malicious patterns by correlating multiple events (e.g., Failed Logons followed by Success).
- Event ID Analysis: Focusing on critical security events (4625 - Failed Logon, 4624 - Success, 1102 - Log Cleared).

## Detection Thinking practice
**IF** EventID == 4625
**AND** Count(EventID:4625) > 5 **WITHIN** 1 minute
**AND** Source_User == Same_User
**THEN** Alert: Potential Brute Force Attack Detected

**IF** EventID == 1102 OR EventID == 104
**THEN** Alert: Critical - Security Log Cleared (Possible Tampering)

**IF** EventID == 4624 (Success)
**AND** EventID == 7045 (Service Install) **WITHIN** 5 minutes
**AND** Source_User == Same_User
**THEN** Alert: Potential Lateral Movement Detected

## Skill Improved
- Ability to design and manage a centralized logging infrastructure (ELK).
- Expertise in creating automated detection rules (Correlation Logic).
- Proficiency in using KQL for incident investigation.
- Understanding of attacker behavior regarding log tampering and how to detect it.

## Improvement area
- Fine-tuning detection rules to minimize False Positives in a noisy environment.
- Exploring deeper SPL functions for advanced statistical threat hunting in Splunk.
- Practicing incident response workflows directly within Kibana Cases.

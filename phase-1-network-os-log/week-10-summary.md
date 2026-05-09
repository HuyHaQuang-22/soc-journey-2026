# Phase 1 Milestone: BOTS v1 Investigation
**Date:** 2026-05-09  
**Focus:** Splunk Enterprise & Real-world Threat Hunting  
**Status:** Phase 1 Milestone Completed 

---

## Lab Overview: Boss of the SOC (v1)
This milestone marks the completion of the **BOTS v1** investigation. Unlike theoretical exercises, this lab required high-level telemetry correlation and hypothesis-driven analysis

*   **Platform:** Splunk Enterprise
*   **Dataset:** Boss of the SOC (v1)
*   **Mission:** Reconstruct the attack timeline by correlating HTTP traffic, IDS alerts, and Firewall logs

---

## 🛠️ Technical Deep-Dive

### 📡 Traffic Analysis (HTTP/DNS)
*   **POST vs. GET Analysis:** Differentiated between resource retrieval (GET) and malicious data submission/file uploads (POST)
*   **Webshell Detection:** Identified suspicious behavior by monitoring access to newly uploaded `.php` files
*   **Scanner Identification:** Uncovered automated reconnaissance activity by analyzing `User-Agent` strings and request frequency

### 🔗 Telemetry Correlation
Learned to pivot across multiple data sources to validate IOCs:
*   **Suricata IDS**: Initial alert triggering
*   **stream:http**: Payload and header inspection
*   **Fortigate Logs**: Mapping external connection attempts

---

## 💻 Featured SPL Queries

### 1. Hunting Malicious Web Shell Uploads
Searching for POST requests containing executable extensions in the form data
index=botsv1 sourcetype=stream:http http_method=POST
| search form_data="*.php*" OR form_data="*.exe*"
| table _time, src_ip, dest_ip, http_user_agent, form_data

### 2. Brute Force Pattern Detection
Identifying high-frequency authentication attempts to uncover potential account compromise
index=botsv1 sourcetype=stream:http http_method=POST
| search form_data="*password*" OR form_data="*username*"
| stats count by src_ip
| where count > 50
| sort - count

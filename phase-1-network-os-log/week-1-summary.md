# Phase 1 – Week 1 Summary
Date: 01/03/2026
Focus: Network & OS Fundamentals

## Topics Covered
- TCP/IP & OSI model
- DNS & DHCP
- HTTP/HTTPS
- Linux authentication & SSH logs

## Technical Understanding

### DNS
- Query/Response structure
- Observed DNS traffic using Wireshark
- Understood how DNS resolution appears in network captures

### Linux Authentication Logs
- SSH login events stored in /var/log/auth.log
- Failed login attempts can indicate brute force behavior

## Detection Thinking Practice
Scenario:
Multiple failed SSH login attempts within short time frame.

Possible causes:
- Brute force attack
- Automated scanning
- Misconfigured monitoring system

## Skills Improved
- Packet inspection (Wireshark)
- Log location awareness in Linux
- Basic security pattern recognition

## Improvement Areas
- Need deeper understanding of Windows Event Logs

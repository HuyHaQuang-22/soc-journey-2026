# Phase 1 - Week 7 - Summary
Date: 12/04/2026
Focus: Network Traffic Analysis (NTA) & Protocol Deep Dive

## Topic covered
- OSI Model & Encapsulation Fundamentals
- Wireshark Mastery (Filters & Packet Analysis)
- TCP Three-Way Handshake & Connection States
- Protocol Analysis (DNS, ICMP, HTTP/HTTPS)
- Network Reconnaissance & Scanning Detection

## Technical understanding 

### OSI Model & Encapsulation
- Focused on L2 (Data Link), L3 (Network), and L4 (Transport).
- Encapsulation: Understanding how data is wrapped from L7 down to L2 (Data -> Segment -> Packet -> Frame).
- Concept: IP Address (Logical) for global routing vs. MAC Address (Physical) for local identification.

### Wireshark & Traffic Filtering
- Using Wireshark as a "Network Microscope" to dissect packets.
- Difference between Filters:
    + Capture Filters: `host 192.168.1.1` (Filtering before capturing to save resources).
    + Display Filters: `ip.addr == ...`, `http.request.method == "POST"` (Analyzing specific traffic).

### TCP Handshake & Connection Analysis
- Three-Way Handshake: SYN -> SYN/ACK -> ACK.
- Connection Termination: FIN (Graceful) vs. RST (Abrupt).
- Attack Signature (SYN Flood): Attacker sends multiple SYN packets without ever sending an ACK to exhaust server resources.

### Protocol Deep Dive (Abuse & Exfiltration)
- DNS: Analyzing queries for "DNS Tunneling" (hiding data in DNS requests).
- ICMP: Analyzing ping packets for "ICMP Exfiltration" (stashing data in the Data field).
- HTTP: Analyzing GET/POST methods, User-Agents, and Cookies to identify malicious web activity.

### Reconnaissance Detection
- Nmap Analysis: Differentiating between Full Connect Scan (Complete handshake) and Stealth Scan (Half-open/SYN scan).
- Identifying Port Scanning: One source IP hitting multiple ports in a very short timeframe.

## Detection Thinking practice
**IF** Protocol == TCP
**AND** TCP.Flags.SYN == 1 **AND** TCP.Flags.ACK == 0
**AND** Count(Unique Destination Ports) > 100 **WITHIN** 1 second
**THEN** Alert: Potential Port Scanning Detected

**IF** Protocol == ICMP
**AND** PacketSize > 128 bytes
**AND** Payload CONTAINS ("suspicious_strings" OR EncodedData)
**THEN** Alert: Possible ICMP Data Exfiltration

## Skill Improved
- Proficiency in Wireshark for deep packet inspection.
- Ability to analyze network protocols to find hidden malicious artifacts.
- Understanding connection-oriented (TCP) vs connectionless (UDP/ICMP) traffic.

## Improvement area
- Need to practice decrypting TLS/HTTPS traffic using RSA keys or SSLKEYLOGFILE.
- Improve skills in analyzing complex multi-stage malware traffic from .pcap files.

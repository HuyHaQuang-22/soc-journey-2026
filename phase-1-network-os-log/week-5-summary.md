# Phase 1 - Week 5 - Summary
Date: 30/03/2026
Focus: Process Monitoring & Command Line Analysis

##  Topic covered
- What is parent-child process?
- How to recognize suspicious behaviour?
- What is Sysmon?
- Network Connections and Event ID 3

## Technical understanding 

### Parent-child process 
- Every process (child) always created by a parent process
- Analize Parent-Child helps SOC know the origin of the command behaviour

### The importance of Sysmon 
- Sysmon is a Microsoft Sysinternals tool that provides advanced system monitoring beyond native Windows logs
- Event 1 in Sysmon is very important
    + Meaning: there is a new process was created
    + It's noted a command line very detail
 
### Methods to analize a command line
- Analize the parent-child process: If parent are Office or Webserver and they spawn cmd / powershell processes
- Analyze Deception (Checking for Stealth or Bypassing Controls):
    + -enc / EncodedCommand: Encodes keywords (to obfuscate the actual command content) 
    + -w hidden / -WindowStyle hidden: Hidden execution (runs the command without opening a visible window)
    + -ep bypass / -ExecutionPolicy bypass: Bypasses Windows security policies (allows scripts to run without being blocked by the system)
- Analyze Actions (Determining System Impact):
    + Monitor for suspicious behaviors such as:
    + Connecting to URLs (http, https)
    + Connecting to suspicious or unknown IP addresses
    + Initiating file downloads to the system

  ### Network Connection & Event ID 3
- Event ID 3: A command that note everything happened
- Three most important fields in Event ID 3:
    + Image : Process Name
    + Destination IP
    + Destination Port: Hackers love port 80 or 443 or 8080 ...
- Alway remember this 3 plots:
    + Non-network process initiating network connections: If some app like (notepad.exe, calc.exe, mspaint.exe connect to the Internet -> Process Injection)
    + Network tools are abused (lolbins): certutil.exe, bitsadmin.exe, rundll32.exe connects to some websites that contain files (like Github, PasteBin)
    + Office applications: Winword.exe, Excel.exe connects to the Internet
 
  ## Detection Thinking practice
  **IF** Event ID == 3
  **AND** Image in (notepad.exe, calc.exe, mspaint.exe)
  **AND** Destination port == 443
  **THEN** Alert: Network connection from suspicious Non-network Process

  ## Skill Imporved
  - Improved command line analysis ability
 
  ## Improvement area
  - Need more hand-on lab

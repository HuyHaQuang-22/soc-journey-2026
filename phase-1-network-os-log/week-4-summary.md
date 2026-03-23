# Phase 1 - Week 4 - Summary
Date: 23/03/2026
Focus: Windows Logs & Event ID Foundation

## Topic covered
- What is Windows Event Logs?
- Know the 3 most important logs in Windows : Security, System, Application
- Know about Event ID and how a SOC analyst uses it 
- Understand a basic Event ID

## Technical understanding

### Windows Event Logs
- This is Windows' system diary, where all events in the computer are recorded
- For example, Linux has /var/log/auth.log or /var/log/syslog so Windows has Event Viewer or Windows Event Logs

### Three most important logs for SOC 
- Security Log: 
  + It covers events related to log in / log out, failed / success login, created / deleted an account, change the password, ....
  + SOC use Security Log to hunt for brute force or password spraying or suspicious login ...
- System Log:
  + It contains events such as start / stop the computer, service start / stop, error driver / disk, changes of network interface, ...
  + The System log tracks system-level changes and service operations
- Application Log: It records event from application, downloaded software, database client / server, office, ...

### Event ID
- A identification code for an event in Windows Logs
- SOC use Event ID to know what kind of event instead of reading all the log line
- Event ID = "tag" -> easier to write rule

### Process Execution Visibility (4688 vs. Sysmon 1)
- Event ID 4688 (Native) = A new process has been created 
- Sysmon event ID 1 better than 4688 : it has more detailed command line, parent process, hashes, GUID

### Persistence Techniques 
- Windows Service : 
  + Attackers install malicious services to execute code with SYSTEM-level privileges 
  + This allows malware to run automatically in the background without user interaction
- Scheduled Task  : 
  + Attackers register scheduled tasks to re-execute malware during system boot, user logon, or at specific intervals.
  + This technique ensures the threat can survive reboots and maintain a long-term foothold

## Detection thinking practice 
- Scenario : 
there is an event id = 106 that use powershell to do something
- Detection rule :
  **IF** Event ID = 106
  **AND** 
(action contains "powershell.exe -enc" **OR** "powershell.exe -w hidden" **OR** "mshta.exe" **OR** "rundll32.exe"
  **OR** 
TaskContent contain "C:\Users\Public" **OR** "C:\ProgramData" **OR** "Temp")
  **THEN** alert possible persistence via scheduled task

## Skills improved 
- Improved windows detection rule thinking

## Improvement are
- Need more hand-on lab

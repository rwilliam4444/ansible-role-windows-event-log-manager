# Role Name:
- ansible-role-windows-event-log-manager

# Description:
The windows event log mngr role will check the server's drives (C, D, E, & F),
at the root level, for a directory called eventlogs.   If none are found then
a folder will be created on the C: drive called c:\\eventlogs.   The role
will also ensure that the necessary ZIP utility file is on the server.  The
role will then export the system, security and application event logs to a CSV
file inside the noted folder previously mentioned.   It will then ZIP up the
CSV files and then clear the system, security and application event logs.  The
role will remove the CSV files and it will delete any zipped files older than
the noted number_days_before_deletion variable.   The default value for this
variable is 270 days.

# Requirements
Windows Ansible related pre-requisites

# Role Variables:
# Defaults file for ansible-role-windows-event-log-manager

Parameter | Choices/Defaults|Comments
----------|-----------------|--------
__zip_path__  (string)| "C:\\Scripts\\Sec_Log_Archive\\7z" | default zip path
__number_days_before_deletion__ (number) | 270 | # of days before it will delete


# Results from execution

Return Code | Success of execution| effect on target machine | Comments
----------|-----------------|--------|---------
0 | True | True | event log manager on __affected_host__  was successful.
0 | True | False | event log manager on  __affected_host__ took no action.
3000 | False | False | could not find or create the eventlogs folder.
3001 | False | False | could not find the zip_path folder and executable.


# Example Playbook:
---
 - hosts: [win]
   roles:
   - ansible-role-windows-event-log-manager


# Author Information:
Richard M. Williams (williamsitv@yahoo.com)

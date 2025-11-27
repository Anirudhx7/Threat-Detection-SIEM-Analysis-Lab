# Threat-Detection-SIEM-Analysis-Lab



## Objective
The RDP protocol is a primary attack vector for ransomware groups. This project simulates an identity-based attack to engineer detection rules using Splunk.

## Architecture
[Insert that Network Diagram we made earlier]

## The Attack (Red Team)
Simulated a brute force attack using Hydra on Kali Linux targeting the Windows Administrator account.
[Insert Screenshot 1: Kali Terminal with Hydra running]

## The Defense (Blue Team)
Ingested logs via Splunk Universal Forwarder. Configured Sysmon to capture Event ID 4625.

### The Query
I used the following SPL to identify anomalies based on login velocity:
`index=security EventCode=4625 | stats count by IpAddress | where count > 10`

### The Result
Successfully identified the threat actor IP (10.0.2.x) with 500+ failed attempts.
[Insert Screenshot 3: Splunk Statistics Table]

## Conclusion
This rule allows for the automated detection of brute-force attempts before a valid session is established.

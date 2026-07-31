# Brute-Force Detection Lab

SOC Analyst portfolio project focused on manual analysis of authentication logs to detect SSH brute-force attacks.

## Project Objective
Analyze a sample authentication log, identify malicious activity, map it to the MITRE ATT&CK framework, and document findings in a professional format suitable for a Security Operations Center (SOC).

## Method
- Manual log analysis (no automated tools or scripts used)
- Identification of failed vs successful logins
- Source IP correlation and username targeting analysis
- MITRE ATT&CK mapping

## Sample Log
The file `sample-auth.log` contains realistic SSH authentication events, including both legitimate successful logins and a clear brute-force attack.

## Findings

**Alert Title:** Possible SSH Brute-Force Attack

**Source IP:** 203.0.113.45

**Target:** webserver (SSH)

**Time Window:** Jul 28 08:01:12 – 08:15:11

**Activity Summary:**  
The source IP 203.0.113.45 performed 16 failed SSH login attempts against the host “webserver” within a 14-minute window. The attacker primarily targeted the root account (10 attempts) and also tried several other common usernames. No successful authentication from this IP was observed.

**Key Observations:**
- Total failed attempts from this IP: 16
- Most targeted username: root (10 times)
- Other usernames tried: admin, ubuntu, test, oracle
- Successful logins during the same period came only from internal-looking IPs (10.0.0.x range)
- Attacks occurred in two main bursts (around 08:01 and 08:15)

**MITRE ATT&CK:**
- Tactic: Credential Access
- Technique: T1110 – Brute Force
- Sub-technique: T1110.001 – Password Guessing

**Recommended Actions:**
- Block the IP 203.0.113.45 at the firewall / perimeter
- Review SSH configuration (disable root login, enforce key-based authentication, consider fail2ban or equivalent)
- Confirm there were no successful logins from this IP (none present in this log)
- Monitor for similar activity from other external IPs

**Analyst Notes:**  
The attempt to log in with the username “ubuntu” is common in automated brute-force activity and does not reliably indicate the attacker’s operating system. Many tools simply try a list of frequent usernames (root, admin, ubuntu, etc.).

## How to Reproduce
1. Download or view `sample-auth.log`
2. Open the file in any text editor
3. Manually count failed vs successful logins
4. Group failed attempts by source IP and username
5. Document findings using the structure above

## Skills Demonstrated
- Log analysis
- Threat identification
- MITRE ATT&CK mapping
- Clear and professional documentation
- SOC-style alert triage and reporting

## Future Improvements
- Add detection logic with a simple script
- Expand the dataset with more attack types
- Integrate with a free SIEM (Wazuh / Elastic / Splunk Free)

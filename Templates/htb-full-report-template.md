<%*
/* HTB Full Report — Fixed Version (Templater v2 safe) */

let box = await tp.system.prompt("Box name (e.g., Stone)");
let ip = await tp.system.prompt("Target IP or hostname");
let date = tp.date.now("YYYY-MM-DD");
let difficulty = await tp.system.prompt("Difficulty (Easy/Medium/Hard)");
let author = await tp.system.prompt("Author (your name / handle)");
let os = await tp.system.prompt("Target OS (Linux/Windows)");
let scope = await tp.system.prompt("Scope / Allowed actions (e.g., Only the lab machine)");
let execSummary = await tp.system.prompt("Executive summary (1-3 sentences)");

tR += `
---
box: ${box}
ip: ${ip}
date: ${date}
difficulty: ${difficulty}
author: ${author}
os: ${os}
scope: ${scope}
exec_summary: ${execSummary}
---

# ${box} — Full Report (${difficulty})

**Author:** ${author}  
**IP:** ${ip}  
**OS:** ${os}  
**Date:** ${date}  

---

## Table of Contents
1. [Executive Summary](#executive-summary)
2. [Objective & Scope](#objective--scope)
3. [Environment & Assumptions](#environment--assumptions)
4. [Tools Used](#tools-used)
5. [Enumeration](#enumeration)
6. [Vulnerability Analysis](#vulnerability-analysis)
7. [Exploitation Initial Access](#exploitation-initial-access)
8. [Post-exploitation Low-priv](#post-exploitation-low-priv)
9. [Privilege Escalation](#privilege-escalation)
10. [Evidence Appendix](#evidence-appendix)
11. [Remediation & Recommendations](#remediation--recommendations)
12. [Lessons Learned](#lessons-learned)
13. [Appendix: Raw outputs / scripts](#appendix-raw-outputs--scripts)

---

## Executive Summary
${execSummary}

---

## Objective & Scope
- **Target:** ${ip}  
- **Scope / Allowed actions:** ${scope}

---

## Environment & Assumptions
- **Attacker:** Kali/Debian  
- **Notes / Assumptions:** (no lateral movement, lab only)

---

## Tools Used
- nmap, gobuster, feroxbuster, burpsuite, nikto, linPEAS/winPEAS, netcat, python3, metasploit (if used), custom scripts

---

## Enumeration
### Nmap
**Command:**  
\`\`\`bash
nmap -sC -sV -oN nmap_full.txt ${ip}
\`\`\`

**Summary of findings:**  
- Port / Service / Version — notes

### Web & Directory Discovery
**Command example:**  
\`\`\`bash
gobuster dir -u http://${ip} -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -o gobuster.txt
\`\`\`

**Findings:**  
- /admin — login page  
- /uploads — interesting files

### Service-specific Enumeration
- SMB / FTP / SQL notes

---

## Vulnerability Analysis
- **Finding 1:** Service X (version Y) — impact, evidence, CVE/reference if any  
- **Finding 2:** Misconfiguration Z — evidence & risk

---

## Exploitation Initial Access
**Goal:** Gain low-priv shell.  
**Steps & Commands:**  
\`\`\`bash
# Exploit steps here
\`\`\`

**Proof (user):**  
\`\`\`
whoami
user
\`\`\`

**Screenshot:** Attach at: Attachments/${box}/initial_shell.png

---

## Post-exploitation Low-priv
**Enumeration:**  
\`\`\`bash
id
pwd
ls -la
ps aux
sudo -l
\`\`\`

**Findings:**  
- Config files / credentials found  

---

## Privilege Escalation
**Enumeration for escalation:**  
\`\`\`bash
sudo -l
find / -perm -4000 -type f 2>/dev/null
\`\`\`

**Escalation steps:**  
\`\`\`bash
# steps to escalate privileges
\`\`\`

**Proof (root):**  
\`\`\`
whoami
root
\`\`\`

**Screenshot:** Attach at: Attachments/${box}/root.png

---

## Evidence Appendix
- Figure 1: Nmap output (nmap_full.txt)  
- Figure 2: Initial shell screenshot (initial_shell.png)  
- Figure 3: Root proof (root.png)  
- Save all raw outputs in Attachments/${box}/

---

## Remediation & Recommendations
- Patch vulnerable services  
- Enforce least-privilege permissions  
- Disable unnecessary ports/services  
- Monitor logs for unusual access

---

## Lessons Learned
- What worked:  
- What to improve next time:

---

## Appendix: Raw outputs / scripts
- nmap_full.txt  
- gobuster.txt  
- linpeas.txt / winPEAS.txt  
- exploit scripts

---

*End of full report — attach artifacts in Attachments/${box}/*
`
%>

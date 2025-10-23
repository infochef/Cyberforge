<%*
let Box = await tp.system.prompt("Box name (e.g., Stone)");
let Ip = await tp.system.prompt("Target IP or hostname");
let Date = tp.date.now("YYYY-MM-DD");
let Difficulty = await tp.system.prompt("Difficulty (Easy/Medium/Hard)");
let Short = await tp.system.prompt("One-line summary (quick)");

tR += `---
Box: ${Box}
Ip: ${Ip}
Date: ${Date}
Difficulty: ${Difficulty}
Summary: ${Short}
---

# ${Box} — Quick Note

**IP:** ${Ip}  
**Date:** ${Date}  
**Difficulty:** ${Difficulty}

## One-line summary
${Short}

## Recon
- Nmap: \`nmap -sC -sV -oN nmap.txt ${Ip}\`
- Key ports:

## Key Findings
- 

## Initial Access
- Exploit / vuln:
- Commands:
  - 

**Proof (user):** \`whoami\` -> 

## Privilege Escalation
- Steps:
  - \`sudo -l\` -> 
  - find SUIDs -> 

**Proof (root):** \`whoami\` -> root

## Artifacts
- nmap.txt, gobuster.txt, linpeas.txt (save to Attachments/${Box}/)

## Quick notes / lessons
- 
`
%>

<%*
let box = await tp.system.prompt("Box name (e.g., Stone)");
let ip = await tp.system.prompt("Target IP or hostname");
let date = tp.date.now("YYYY-MM-DD");
let difficulty = await tp.system.prompt("Difficulty (Easy/Medium/Hard)");
let short = await tp.system.prompt("One-line summary (quick)");

tR += `---
box: ${box}
ip: ${ip}
date: ${date}
difficulty: ${difficulty}
summary: ${short}
---

# ${box} — Quick Note

**IP:** ${ip}  
**Date:** ${date}  
**Difficulty:** ${difficulty}

## One-line summary
${short}

## Recon
- Nmap: \`nmap -sC -sV -oN nmap.txt ${ip}\`
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
- nmap.txt, gobuster.txt, linpeas.txt (save to Attachments/${box}/)

## Quick notes / lessons
- 
`
%>

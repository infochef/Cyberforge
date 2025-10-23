<%*
let Box = await tp.system.prompt("Box name (e.g., Stone)");
let Ip = await tp.system.prompt("Target IP or hostname");
let Date = tp.date.now("YYYY-MM-DD");
let Difficulty = await tp.system.prompt("Difficulty (Easy/Medium/Hard)");
let Author = await tp.system.prompt("Your handle/author name");
let Os = await tp.system.prompt("Target OS (Linux/Windows)");
let Summary = await tp.system.prompt("One-line summary for header");

tR += `---
Box: ${Box}
Ip: ${Ip}
Date: ${Date}
Difficulty: ${Difficulty}
Author: ${Author}
Os: ${Os}
Summary: ${Summary}
---

# ${Box} — ${Difficulty}

**Author:** ${Author}  
**IP:** ${Ip}  
**OS:** ${Os}  
**Date:** ${Date}  

## Summary
${Summary}

---

## Enumeration
**Nmap command:**  
\\\`\\\`\\\`bash
nmap -sC -sV -oN nmap_initial.txt ${Ip}
\\\`\\\`\\\`

**Key ports / services:**  
- 80/HTTP —  
- 22/SSH —

**Web discovery (gobuster/ferox):**  
- \`/admin\` — note

---

## Initial Access
**Vector / vuln:**  
- Explanation of the vulnerability.

**Commands used / exploit:**  
\\\`\\\`\\\`bash
# example commands/payloads used
\\\`\\\`\\\`

**Proof (user):**  
\\\`\\\`
whoami
user
\\\`\\\`

**Screenshot:** \`Attachments/${Box}/initial_shell.png\`

---

## Privilege Escalation
**Method:** (SUID / sudo misconfig / creds / kernel exploit)  
**Commands & steps:**  
\\\`\\\`\\\`bash
sudo -l
find / -perm -4000 -type f 2>/dev/null
\\\`\\\`\\\`

**Proof (root):**  
\\\`\\\`
whoami
root
\\\`\\\`

**Screenshot:** \`Attachments/${Box}/root.png\`

---

## Mitigation
- Bullet points to fix the vulnerabilities discovered.

## Takeaways / Notes
- Short learning points and next steps.

## Artifacts
- Raw outputs: \`nmap_initial.txt\`, \`gobuster.txt\`, \`linpeas.txt\`
- Attachments folder: \`Attachments/${Box}/\`
`
%>

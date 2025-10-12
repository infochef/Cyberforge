<%*
let box = await tp.system.prompt("Box name (e.g., Stone)");
let ip = await tp.system.prompt("Target IP or hostname");
let date = tp.date.now("YYYY-MM-DD");
let difficulty = await tp.system.prompt("Difficulty (Easy/Medium/Hard)");
let author = await tp.system.prompt("Your handle/author name");
let os = await tp.system.prompt("Target OS (Linux/Windows)");
let summary = await tp.system.prompt("One-line summary for header");

tR += `---
box: ${box}
ip: ${ip}
date: ${date}
difficulty: ${difficulty}
author: ${author}
os: ${os}
summary: ${summary}
---

# ${box} — ${difficulty}

**Author:** ${author}  
**IP:** ${ip}  
**OS:** ${os}  
**Date:** ${date}  

## Summary
${summary}

---

## Enumeration
**Nmap command:**  
\`\`\`bash
nmap -sC -sV -oN nmap_initial.txt ${ip}
\`\`\`

**Key ports / services:**  
- 80/HTTP —  
- 22/SSH —

**Web discovery (gobuster/ferox):**  
- `/admin` — note

---

## Initial Access
**Vector / vuln:**  
- Explanation of the vulnerability.

**Commands used / exploit:**  
\`\`\`bash
# example commands/payloads used
\`\`\`

**Proof (user):**  
\`\`\`
whoami
user
\`\`\`

**Screenshot:** `Attachments/${box}/initial_shell.png`

---

## Privilege Escalation
**Method:** (SUID / sudo misconfig / creds / kernel exploit)  
**Commands & steps:**  
\`\`\`bash
sudo -l
find / -perm -4000 -type f 2>/dev/null
\`\`\`

**Proof (root):**  
\`\`\`
whoami
root
\`\`\`

**Screenshot:** `Attachments/${box}/root.png`

---

## Mitigation
- Bullet points to fix the vulnerabilities discovered.

## Takeaways / Notes
- Short learning points and next steps.

## Artifacts
- Raw outputs: `nmap_initial.txt`, `gobuster.txt`, `linpeas.txt`
- Attachments folder: `Attachments/${box}/`
`
%>

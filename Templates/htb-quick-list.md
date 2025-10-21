<%*
/* HTB Quick Checklist — Templater v2 compatible */
let box = await tp.system.prompt("Box name (e.g., Stone)");
tR += `---

## 🧩 HTB Quick Checklist — ${box}

- [ ] Create **Quick Note** using Templater  
- [ ] Run **nmap** (\`-sC -sV -oN nmap.txt\`)  
- [ ] Run **gobuster / feroxbuster** for web enumeration  
- [ ] Enumerate other services (**SMB / FTP / SQL**, etc.)  
- [ ] Search for **credentials**, **config files**, or sensitive data  
- [ ] Attempt **common exploits / web shells** (manual or scripted)  
- [ ] Gain **low-privilege shell** → save user proof (\`whoami\`)  
- [ ] Run **linPEAS / winPEAS** for privilege escalation checks  
- [ ] Check **sudo -l**, **SUIDs**, **cron jobs**, and discovered creds  
- [ ] Escalate privileges to **root/admin** → save root proof  
- [ ] Save **raw outputs** and **screenshots** to \`Attachments/${box}/\`  
- [ ] Convert **Quick Note → Medium** (for public write-up) or **→ Full Report** (for OSCP-style documentation)
`
%>

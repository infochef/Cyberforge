<%*
let box = await tp.system.prompt("Box / Topic name (e.g., Stone)");
let date = tp.date.now("YYYY-MM-DD");

tR += `---
box: ${box}
date: ${date}
---

# ${box} — Quick Note

**Date:** ${date}

## Commands
- 

## Quick notes / lessons
- 
`
%>

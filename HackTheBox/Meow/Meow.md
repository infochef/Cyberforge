
---
Title: Meow
Created: 2025-10-06
Time: 22:50

=======================================================================
Step 1 - Check basic reachability
	Command - ping {TARGET_IP} - ping  10.129.251.148 or ping -c 4 10.129.251.148
		Explanation - `-c 4` tells `ping` to send **4 ICMP echo requests** and then stop. On Linux/macOS `-c` = **count**. Without it `ping` runs until you interrupt it (Ctrl+C).
		
 .        Output - ![[Pasted image 20251006231232.png]]
 
	Interpretation - The host at 10.129.251.148 responds to ICMP. This confirms
	 network reachability and that the machine is online; proceed to basic 
	 TCP/UDP port enumeration.
	
	Next step - Run TCP port scan (e.g., nmap) against common ports to identify
	 services.
	
	Notes - Ping may be blocked by some machines — lack of response does not 
	always indicate host is down.

Step 2 - Enumeration
		Explanation - Enumeration is the active information‑gathering phase after initial discovery. It’s the process of probing systems, services, and applications to extract detailed, actionable information (users, shares, services, software versions, configuration, open ports, DNS records, etc.) that can be used to plan exploitation or lateral movement.
		Every server uses ports in order to serve data to other clients. The first steps in the Enumeration phase involve scanning these open ports to see the purpose of the target on the network and what potential vulnerabilities might appear from the services running on it. In order to quickly scan for ports, we can use a tool called nmap , which we will detail more in the Enumeration chapter of this write-up.
		
	Command - nmap -sV 10.129.251.148 (nmap stands for Network Mapper) or
			sudo nmap -sS -sV -p- -T4 --version-all -oA full-scan 10.129.251.148
			
		**Explanation** - nmap - the network scanner programm
					  -sV - service/version detection map probes open ports to 
					  identify the running service (e.g., `ssh`, `http`,`mysql`) 
					  and attempts to determine the service product and version 
					  (for example `OpenSSH 7.9p1` or `Apache httpd 2.4.29`)
					  -p- — scan **all** 65535 TCP ports (instead of top 1000).
					 -sS — force SYN scan (faster/stealthier when privileged).
					  -A — enable OS detection, version detection, script 
					  scanning, and traceroute (more noisy).
					  --version-all — attempt every version probe (more thorough
					   / slower / noisier).
					--version-intensity <0-9> — reduce/increase the 
					aggressiveness of version probes (default 7).
					-T4 — faster timing (useful on reliable networks).
					-oA <basename> — save output in all formats (`.nmap`, 
					`.xml`, `.gnmap`).
					
   .      Output -  ![[Pasted image 20251007185723.png]]

	Interpretation - The command `nmap -sV 10.129.251.148` performs active 
	service/version detection against the target. Nmap probes the target’s open 
	TCP ports (default: top 1000) and attempts to identify running services and
	their software versions, providing actionable information for vulnerability 
	mapping and follow‑up testing.
	
	Next step - If `-sV` reports open services, run targeted follow‑up scans and
	 service‑specific probes (e.g., `sudo nmap -sS -sV --top-ports 1000 -T4 -oA 
	 nmap/top-1000 10.129.251.148` to confirm, then `sudo nmap -sS -sV -p- --
	 version-all -T4 -oA nmap/full-tcp 10.129.251.148` for a full port/version 
	 sweep). For discovered services, use protocol tool. 
	 (curl/telnet/ssh/smbclient/ldapsearch/snmpwalk) to validate banners and 
	 enumerate further.
	
    Notes - `-sV` is an active and potentially noisy scan: it can trigger 
    IDS/IPS and generate service logs. By default it scans TCP (top 1000 ports);
     run with elevated privileges for SYN scans and `-p-` to scan all ports. UDP 
     enumeration is separate (`-sU`) and slower. Absence of a version string does 
     not imply absence of vulnerability (banners can be hidden/proxied); always 
     corroborate with manual probes and respect rules of engagement.

Step 3 - telnet service ping
	**Explanation** - **telnet** is an old service used for remote management of other hosts on the network. Since the target is running this service, it can receive telnet connection requests from other hosts in the network (such as ourselves). Usually, connection requests through telnet are configured with username/password combinations for increased security.
	
    **Command** - telnet 10.129.251.148
    
   Output -  ![[Pasted image 20251007192120.png]]

	Interpretation - The command `telnet <target_ip>` opens a raw TCP 
	connection from your machine to the specified IP address and port. It is 
	commonly used for quick manual banner grabbing, basic protocol interaction
	 (e.g., issuing an HTTP `GET`, SMTP `HELO`, or SMTP `VRFY`), and testing 
	 whether a specific TCP service accepts connections. Example: `telnet 
	 10.129.251.148 80` connects to TCP port 80 on the target.
	
	Next step - Use `telnet` to manually validate an open port and capture the 
	service banner or perform simple protocol exchanges.
	
    Notes - `telnet` creates an unencrypted, plaintext TCP session and is 
    primarily a diagnostic/manual tool. It may not be installed by default on 
    modern systems. `telnet` is noisy and will generate logs on the target 
    (connection attempts and commands). Many services do not display full 
    version strings via plain banner or may block simple probes; `telnet` can 
    show connectivity but is not a replacement for protocol‑aware enumeration 
    tools. Use alternatives when appropriate: `nc`/`ncat` for scripted/raw TCP 
    tests, `curl`/`wget` for HTTP(s), and `openssl s_client -connect ip:port` 
    for TLS‑wrapped services. Always operate within authorization/scope and avoid
     sending sensitive commands while testing.
 
Step 4 - Foothold
	Explanation - **Gaining initial access to a target system or network**, typically through an exploited vulnerability, misconfiguration, or exposed credentials — giving the attacker (or pentester) a limited presence or control inside the environment.
	Sometimes, due to configuration mistakes, some important accounts can be left with blank passwords for the sake of accessibility. This is a significant issue with some network devices or hosts, leaving them open to simple brute-forcing attacks, where the attacker can try logging in sequentially, using a list of usernames with no password input. Some typical important accounts have self-explanatory names, such as: admin, administrator, root

	 Command - admin, administrator, root

   Output - ![[Pasted image 20251007195030.png]]
	![[Pasted image 20251007195110.png]]
	
	Interpretation - The host at `10.129.251.148` accepted authentication for the
	 **root** account, providing a direct foothold on the system. This confirms 
	 successful credential‑based access to the target with full administrative 
	 privileges, allowing immediate local enumeration and access to sensitive 
	 system configuration and data.
	
	Next step - Perform controlled, non‑destructive post‑access enumeration to 
	validate the foothold, collect evidence, and identify possible avenues for 
	lateral movement and privilege abuse. Run `ls -la` to view files and 
	`ls | wc -l` to count the number of files in the directory. If `flag.txt` is 
	present, display its contents with `cat flag.txt` (or `less flag.txt` for 
	paging). Capture the file contents (screenshot and saved output with 
	command, user, and timestamp) and submit the flag on Hack The Box to 
	complete the challenge.
	
	Notes - ICMP traffic is frequently restricted at the host or network 
	perimeter. If a host does not respond to ping, verify reachability using 
	additional methods (for example, TCP probes against expected service ports)
	 before concluding the system is offline.
 

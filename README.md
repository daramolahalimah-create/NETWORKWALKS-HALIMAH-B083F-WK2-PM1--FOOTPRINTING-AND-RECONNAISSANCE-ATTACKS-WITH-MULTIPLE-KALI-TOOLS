# PENETRATION TESTING REPORT
## FOOTPRINTING & NETWORK SCANNING PHASES
### W2-PM-FINAL | CYBERSECURITY | NETWORKWALKS



|Field  | Details |
|---|---
|Pentester name| Halimah Daramola|
| Program/Batch | B083F-Networkwalks |
| Date | 30 September 2026 |
| Modules completed | W2-PM1 ( Multiple Kali Tools) & W2-PM5 (Zenmap Scanning) |
| Client/Target |  Networkwalks (secured written permission) & My own local LAN Network |
| Permission secured from client | Yes |
| Phases covered | 1. Reconnaissance & Footprinting  2. Scanning & Network Discovery 3-5 In progress

---


# 1. Liability Disclaimer
   
I have performed these activities only on the systems & devices where I had secured written permission or the devices/systems that I own myself. All these materials are for education and research purpose only. Do not use anything from here to break the law. The instructor, the authors and Networkwalks are not responsible for what you do with this knowledge. Every action you take is your own responsibility. Misuse can lead to criminal charges, heavy fines, loss of your job and a permanent record. In most countries unauthorised access is a crime even when nothing is damaged

---
# 2. Introduction

This report documents footprinting the networkwalks.com domain using multiple Kali Linux tools (W2-PM1) and scanning my own local network with Zenmap (W2-PM5). The first module shows the footprinting phase and the second shows the scanning phase, so they both show how an attacker moves from gathering public information to mapping live hosts on a network. It is my week 2 part of my ongoing internship program at Networkwalks. 
All commands were run in Kali Linux (footprinting) and on a Windows PC with Zenmap installed (scanning). Every step below includes the exact command used, the result I observed, a screenshot as evidence, and a short note on why the finding matters from an attacker's point of view.

# 3. Tools Used 
|Tools | Purpose| 
|---|---|
|Kali Linux & windows | Operating systems used for footprinting|
| WHOIS| Reveal domain registration details (owner, dates, name servers)|
| whatweb | Fingerprint web technologies (server, CMS, plugins, IP) |
| nslookup | Resolve the domain name to its IP address using DNS |
| curl -I | Read the HTTP response headers of the website |
| wafw00f | Detect whether a Web Application Firewall protects the site |
| dnsrecon | List all DNS records |
| Zenmap (Nmap GUI) | Scan all local subnet to find live hosts, IPs and MAC addresses |
| Windows CMD | Identify local IP and MAC addresses |

# 4. Activities Conducted 
## 4.1 Footprinting & Reconnaissance 
- I used **WHOIS** to collect publicly available domain registration information and determine the domain's servers name. The results provided information about the domain registration and hosting infrastructure.
- Then i used **WhatWeb** to identify technologies used by the website. The results identified WordPress 7.0.4 and WP Download Manager 3.3.58, along with other information exposed by the website.
- Using **Nslookup**, I resolved the domain name to its IP address. The provided result identified **192.232.216.135**.
- I used **Curl** with the **-I** option to inspect the HTTP response headers. This provided additional information about the web application and exposed the WordPress REST API endpoint /wp-json/.
- Next, I used **Wafw00f** to determine whether a Web Application Firewall was protecting the website. The result identified **ModSecurity (SpiderLabs)**.
- Finally, I used **DNSRecon** to enumerate DNS records. The results provided information relating to name servers, mail servers, SPF/TXT records, service records and DNS software information

---









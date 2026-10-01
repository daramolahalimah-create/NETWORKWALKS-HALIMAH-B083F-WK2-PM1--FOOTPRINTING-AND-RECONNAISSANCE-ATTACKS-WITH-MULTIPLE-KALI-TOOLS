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

## 4.2 Network Scanning with Zenmap 

- I used the windows **ipconfig** command to identify my local IP address and LAN subnet.
- I then entered the subnet into Zenmap and selected **Ping Scan** to identify active hosts. I discovered 3 live hosts ( 192.168.100.1 , 192,168.100.13, 192.168.100.15 , it also included their MAC addresses)
- I opened the topology the **Topology** section in Zenmap, enabled the legend and saved the network topology in PDF format as required by the practical task.

---

# 5. Risk Analysis / Impact

Based on the information collected during the footprinting and network scanning activities, I identified the following potential risks.

| # | Risk | Evidence | Potential Impact | Risk Level |
|---|---|---|---|---|
| 1 | Web technology information exposed | WhatWeb identified WordPress and WP Download Manager |	Attackers may use exposed technology/version information to identify software requiring further security review |	● Medium |
| 2 |	Server IP address identifiable |	Nslookup resolved the domain to 192.232.216.135 |	Provides information about the network location of the web service | ● Low |
| 3 |	HTTP technical information exposed	| Curl returned HTTP response headers and exposed /wp-json/ |	May assist technology fingerprinting and further enumeration |	● Low |
| 4 |	WAF technology identifiable | Wafw00f identified ModSecurity (SpiderLabs) |	Reveals information about the web application’s security architecture |	● Low |
| 5 | DNS infrastructure information exposed |	DNSRecon identified DNS, mail and service-related records |	DNS information can help build a broader infrastructure profile | ● Medium |
| 6 | Multiple live hosts visible on local network | Zenmap identified four live hosts in the example network | Unknown or unauthorized devices may potentially be present on a network	| ● Medium |

Risk level key:  ● Critical  ● Medium  ● Low
The risks above are observations from the footprinting and scanning exercises, not confirmed vulnerabilities.
The practical exercises primarily involved information gathering and host discovery. No exploitation or vulnerability validation was performed as part of these two modules.
Therefore, the presence of information such as a software version, IP address or DNS record does not by itself mean that the system is vulnerable. Further authorized security testing would be required to confirm any actual vulnerability.

----

# 6. Recommendations

Based on the observations from these activities, I recommend the following security improvements:
1.	**Review publicly exposed technology information**
Organizations should regularly review what information about their web technologies, CMS and plugins is publicly visible.
2.	**Keep software updated**
CMS platforms, plugins and other web technologies should be regularly updated and reviewed against current security advisories.
3.	**Review HTTP headers**
HTTP response headers should be reviewed to determine whether unnecessary technical information is being exposed.
4.	**Review DNS records regularly**
DNS records should be checked periodically to ensure that only required information and services are publicly exposed.
5.	**Properly configure and monitor the WAF**
Keep the WAF (ModSecurity) enabled and tuned, since it already blocks naive attacks.
6.	**Perform regular internal network discovery**
Organizations should periodically scan their own networks to identify active devices.
7.	**Investigate unknown devices**
Any unexpected device discovered during network scanning should be investigated and verified.
8.	**Maintain network documentation**
Network topology and device information should be documented and updated regularly.
9.	**Perform security testing with authorization**
Reconnaissance and scanning should only be performed against systems and networks where appropriate authorization has been provided.

---
  
# 7. Conclusion

During Week 2 of my Cybersecurity & Ethical Hacking internship, I completed practical activities covering footprinting, reconnaissance and network scanning.
In the footprinting activity, I used six Kali Linux tools to collect information about the target domain. I learned how WHOIS can provide domain information, WhatWeb can identify web technologies, Nslookup can resolve domain names, Curl can inspect HTTP headers, Wafw00f can identify a WAF, and DNSRecon can provide additional DNS information.
In the network scanning activity, I used Zenmap to identify my local network configuration and discover active hosts. I also collected IP and MAC address information and created a network topology.
The exercises showed me that information gathering is an important part of cybersecurity. Even before attempting to exploit a system, a security professional can learn a significant amount about an environment by carefully analyzing publicly available information and network responses.
I also learned that technical findings should be documented clearly. A good cybersecurity report should explain what was performed, what was discovered, what the observation means, what risk it may create, and what can be done to reduce that risk.
Finally, I learned that reconnaissance and scanning must always be performed within an authorized scope. These activities were completed as part of the assigned educational cybersecurity lab.

---

# 8. Evidences Collected

<img width="1920" height="891" alt="Screenshot_2026-09-29_07_22_20" src="https://github.com/user-attachments/assets/4ec70b99-5ef9-43d4-8f3f-a00959d2975d" />

<img width="1920" height="891" alt="Screenshot_2026-09-29_08_17_27" src="https://github.com/user-attachments/assets/024f6eab-ef0e-46cc-9c4a-802835ab6063" />

<img width="1920" height="891" alt="Screenshot_2026-09-29_14_31_36" src="https://github.com/user-attachments/assets/8a03d3af-1b0b-4176-a385-e994cbdd34da" />

<img width="1920" height="891" alt="Screenshot_2026-09-29_14_40_32" src="https://github.com/user-attachments/assets/2c7452c9-e67e-4b38-81f8-f91948c0ece5" />

<img width="1920" height="891" alt="Screenshot_2026-09-29_14_48_58" src="https://github.com/user-attachments/assets/024f41d1-733b-4379-8788-6a432ae3dec2" />

<img width="1920" height="891" alt="Screenshot_2026-09-29_19_04_12" src="https://github.com/user-attachments/assets/22948514-1bfb-4361-ad75-f21d69bb0ec4" />

<img width="1878" height="989" alt="Screenshot 2026-09-29 213107" src="https://github.com/user-attachments/assets/b66afdd4-4ec8-4f41-a06c-6665b1e32d41" />

<img width="1191" height="572" alt="Screenshot 2026-09-30 153748" src="https://github.com/user-attachments/assets/d17f0df2-23a9-4ced-9da3-53b5a3619c86" /> 

<img width="1887" height="990" alt="Screenshot 2026-09-30 154252" src="https://github.com/user-attachments/assets/2ec60423-bfc3-4913-ac1c-ab1426316c50" />

<img width="1905" height="1002" alt="Screenshot 2026-09-30 155248" src="https://github.com/user-attachments/assets/e4fc8d45-b886-4834-af74-5aab1c571be8" />

-End-

**Author**
**Halimah Daramola**
Cybersecurity Professional B082
Linkedln: https://www.linkedin.com/in/halimah-daramola-63663a194?utm_source=share_via&utm_content=profile&utm_medium=member_ios

---
- Project Information
  Program Name : Cybersecurity program at Networkwalks | Week:2 |

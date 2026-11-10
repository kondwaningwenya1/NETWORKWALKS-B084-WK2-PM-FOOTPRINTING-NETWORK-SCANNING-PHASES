# NETWORKWALKS-B084-WK2-PM-FOOTPRINTING-NETWORK-SCANNING-PHASES
# PENETRATION TESTING REPORT
### FOOTPRINTING & NETWORK SCANNING PHASES
### W2-PM-FINAL | CYBERSECURITY | NETWORKWALKS

| Pentester Name<br>(Cybersecurity Professional) | Kondwani Ngwenya |
| :--- | :--- |
| **Program/Batch** | B084-Networkwalks |
| **Date** | 09 November 2026 |
| **Modules completed** | W2-PM1 (Multiple Kali Tools)<br>W2-PM5 (Zenmap Scanning) |
| **Client/Target** | 1. Networkwalks (secured written permission already)<br>2. My own local LAN Network |
| **Permission secured from client?** | Yes |
| **Phases covered** | Phase 1: Reconnaissance & Footprinting<br>Phase 2: Scanning & Network Discovery |

---

### 1. Liability Disclaimer
I performed these activities for educational and research purposes, using systems and networks that I own or for which appropriate authorization was provided. The practical exercises were intended to develop my understanding of cybersecurity, footprinting, reconnaissance and network scanning.

These activities should only be conducted within an authorized scope. Unauthorized access or testing of computer systems and networks may violate applicable laws. The instructor, authors and Networkwalks are not responsible for any misuse of the knowledge presented in this report.


### 2. Introduction
This report covers footprinting and reconnaissance of the networkwalks.com domain using multiple Kali Linux tools, as well as network scanning of my own local LAN network using Nmap.

The first activity involved gathering publicly available information about the target domain, including its IP address, domain registration details, DNS records, web technologies and security mechanisms.

The second activity involved scanning my local network to identify active hosts, their IP and MAC addresses, and the open ports and services running on the discovered devices.

All commands were executed in Kali Linux. The results obtained from each activity were analyzed and documented, with screenshots serving as evidence of the practical work performed.

---

### 3. Tools Used
The following tools were used during the practical exercises:

| Tool | Purpose |
| :--- | :--- |
| **Kali Linux** | Operating system used for cybersecurity and reconnaissance activities. |
| **WHOIS** | Obtaining domain registration information, registrar details and name servers. |
| **WhatWeb** | Identifying web technologies and server information. |
| **NSLookup** | Resolving domain names into IP addresses. |
| **Curl (-I)** | Inspecting HTTP response headers from the target website. |
| **WafW00f** | Identifying whether a Web Application Firewall protects the website. |
| **Dmitry** | Enumerating DNS records, including NS, MX, TXT and SRV records. |
| **Nmap** | Discovering live hosts and identifying open ports and services on the local network. |
| **Windows CMD** | Identifying local network configuration and MAC addresses. |

---

### 4. Activities Performed

#### 4.1 Footprinting & Reconnaissance
I performed footprinting and reconnaissance against the networkwalks.com domain using six Kali Linux tools: WHOIS, WhatWeb, NSLookup, Curl, WafW00f and Dmitry.

Each tool was used to collect a different category of information about the target.

First, I used the WHOIS command to obtain domain registration information. The results showed that the domain was registered through GoDaddy.com, LLC, with a creation date of 6 November 2019 and an expiry date of 6 November 2027. The domain uses two Hostgator name servers: ://ns6135.hostgator.com and ://ns6136.hostgator.com.

Next, I used WhatWeb to identify technologies and information exposed by the website. The results identified Apache as the web server, the server IP address as 192.232.216.135 and a cookie named `wpdm_client`. The website also returned HTTP redirects before reaching its lowercase HTTPS address.

Using NSLookup, I resolved the domain name to its corresponding IP address. The result confirmed 192.232.216.135.

I then used Curl with the `-I` option to inspect the HTTP response headers. The website returned an `HTTP/2 200 OK` response, indicating a successful response to the request. The results also exposed information such as the Apache server, content type, security-related headers and the WordPress REST API endpoint (`/wp-json/`).

After that, I used WafW00f to identify whether a Web Application Firewall was protecting the website. The result indicated that the website was behind ModSecurity (SpiderLabs) WAF. 

Finally, I used dnsrecon to enumerate DNS records associated with the domain. The results identified the following information:
* **SOA record:** ://ns6135.hostgator.com
* **Name servers:** ://ns6135.hostgator.com and ://ns6136.hostgator.com
* **Mail server:** ://mail.networkwalks.com
* **A IP address:** 192.232.216.135
* **TXT records:** SPF information and Google site verification.
* **SRV records:** Autodiscover services associated with cPanel email discovery.

Dnsrecon also returned an error stating that there was no answer for the DNSSEC query. However, the tool continued with the enumeration and successfully collected other DNS records.

Overall, the footprinting activity provided information about the domain's registration, hosting infrastructure, web server, DNS configuration and security mechanisms.

#### 4.2 Network Scanning with Nmap
For the second activity, I used Nmap to perform network discovery on my local network. The practical required me to identify active hosts, their IP addresses, MAC addresses and open ports.

I scanned the local subnet, `192.168.1.0/24`, to identify devices that were active on the network. The scan completed successfully and identified three live hosts:
* `192.168.1.1`
* `192.168.1.101`
* `192.168.1.188`

The scan also identified several open ports and their associated services.

##### Live Hosts and MAC Addresses
The following table summarizes the discovered devices:

| IP Address | MAC Address | Identification |
| :--- | :--- | :--- |
| 192.168.1.1 | 98:A9:42:57:4E:43 | Router |
| 192.168.1.101 | E4:A4:71:58:75:64 | DESKTOP-EH27S8P |
| 192.168.1.188 | 5C:C5:D4:6F:92:F3 | Host on local network |

The scan identified three live hosts on the subnet, including my PC.

After completing the scan, I documented the discovered devices and their network information and completed the network topology task.



### 5. Risk Analysis / Impact
Based on the information collected during the footprinting and network scanning activities, I identified the following potential security risks:

| # | Risk / Finding | Evidence / Observation | Potential Impact | Risk Level |
| :--- | :--- | :--- | :--- | :--- |
| 1 | Web technology information exposed | WhatWeb identified Apache and other web-related information. | Attackers may use exposed technology information to identify potential vulnerabilities requiring further investigation. | Medium |
| 2 | Server IP address identifiable | NSLookup resolved the domain to 192.232.216.135. | Provides information about the network location of the web service. | Low |
| 3 | HTTP technical information exposed | Curl returned HTTP response headers and exposed the `/wp-json/` endpoint. | May assist technology fingerprinting and further reconnaissance. | Low |
| 4 | WAF technology identifiable | WafW00f identified ModSecurity(SpiderLabs). | Reveals information about the website's security architecture. | Low |
| 5 | DNS infrastructure information exposed | Dnsrecon identified DNS, mail, TXT and service records. | DNS information may help attackers build a broader infrastructure profile. | Medium |
| 6 | Multiple live hosts visible on local network | Nmap identified three live hosts. | Unknown or unauthorized devices may potentially be present on the network. | Medium |
| 7 | Multiple open ports identified | Nmap identified services such as DNS, HTTP, HTTPS, SMB, RDP and MySQL. | Exposed services may increase the attack surface if they are unnecessary or improperly configured. | Medium |

**Risk Level Key:** Critical | High | Medium | Low

The risks identified above are observations from the footprinting and scanning exercises, not confirmed vulnerabilities.

The practical activities primarily involved information gathering and host discovery. No exploitation or vulnerability validation was performed.

Therefore, the presence of an exposed service, IP address, DNS record or web technology does not automatically mean that a system is vulnerable. Further authorized security testing would be required to confirm any actual vulnerability.



### 6. Recommendations
Based on the observations from these activities, I recommend the following security improvements:

#### 1. Review publicly exposed technology information
Organizations should regularly review information about their web technologies, servers and applications that is publicly accessible.

#### 2. Keep software updated
Web servers, CMS platforms, plugins and other technologies should be regularly updated to address known security weaknesses.

#### 3. Review HTTP response headers
HTTP response headers should be reviewed to ensure that unnecessary technical information is not exposed.

#### 4. Review DNS records regularly
DNS records should be checked periodically to ensure that only necessary information and services are publicly exposed.

#### 5. Properly configure and monitor the WAF
The Web Application Firewall should remain enabled and properly configured to help detect and block malicious web traffic.

#### 6. Perform regular internal network discovery
Network administrators should periodically scan their networks to identify active devices and block malicious web requests.

#### 7. Investigate unknown devices
Any unexpected device discovered during network scanning should be investigated to determine whether it is authorized to access the network.

#### 8. Secure unnecessary open ports
Unnecessary services and ports should be disabled or restricted to reduce the network's attack surface.

#### 9. Maintain network documentation
Network topology, device IP addresses and MAC addresses should be documented and updated regularly.

#### 10. Perform security testing with authorization
Reconnaissance and scanning activities should only be conducted against systems and networks where appropriate authorization has been provided.

### 7. Conclusion
During the practical exercises, I completed activities covering footprinting, reconnaissance and network scanning using different cybersecurity tools.
In the footprinting activity, I used six Kali Linux tools to collect information about the networkwalks.com domain. I learned how WHOIS provides domain registration information, WhatWeb identifies web technologies, Nslookup resolves domain names, Curl inspects HTTP response headers, Wafw00f identifies Web Application Firewalls and DNSRecon enumerates DNS records.
In the network scanning activity, I used Nmap to discover active devices on my local network. The scan identified three live hosts and provided information about their IP addresses, MAC addresses, open ports and associated services. I also completed the network topology task.
These exercises demonstrated the importance of reconnaissance and network discovery in cybersecurity. They showed how publicly available information and network responses can help security professionals understand a target's infrastructure and identify areas that may require further security assessment.
I also learned that proper documentation is an important part of cybersecurity testing. Findings should be clearly presented, their potential impact explained and appropriate recommendations provided.
Finally, I learned that footprinting and network scanning must always be conducted within an authorized scope.


### 8. Evidences Collected
   
<img width="1366" height="768" alt="Whois Results" src="https://github.com/user-attachments/assets/d352f1c9-9634-4774-bc55-2cfdd89d44d1" />
Figure 8.0 WHOIS domain registration results.


 <img width="1366" height="768" alt="Whatweb results" src="https://github.com/user-attachments/assets/ecd713fb-bd85-4ea7-8e9a-9b59ae6c257f" />
Figure 8.1 WhatWeb website fingerprinting results.


<img width="1366" height="768" alt="nslookup results" src="https://github.com/user-attachments/assets/26553ef4-9966-4f9f-af79-8b2f2802786a" />
Figure 8.3 Nslookup domain resolution results.


<img width="1366" height="768" alt="Curl results" src="https://github.com/user-attachments/assets/6094348f-8376-40fa-8bc9-dcb25fad64ae" />
Figure 8.4 Curl HTTP response headers.


<img width="1366" height="768" alt="wafw00f results" src="https://github.com/user-attachments/assets/7efe0eeb-20b9-44ef-ac0d-77eec5461e7d" />
Figure 8.5 Wafw00f WAF detection results.


<img width="1366" height="768" alt="dnsrecon results" src="https://github.com/user-attachments/assets/6ae53453-ba71-4234-a790-788c65d6f42b" />
Figure 8.6 DNSRecon DNS enumeration results.


 <img width="1366" height="768" alt="Screenshot (695)" src="https://github.com/user-attachments/assets/e55df9ae-35a1-46fd-9473-b1a30e28810d" />
Figure 8.7. Nmap network scanning results showing the three live hosts.


<img width="1366" height="768" alt="topology graph" src="https://github.com/user-attachments/assets/b4384a29-8b1f-41fd-bb20-fd5a5c6e0033" />
Figure 8.8 network topology screenshot.


👤 Author
Waqas Karim CCIE
Cybersecurity Professional B084
LinkedIn: https://www.linkedin.com/in/waqaskarim/

📌 Project Information
Program Name: Cybersecurity program at Networkwalks | Week: 02 | Repository: GitHub



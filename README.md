# PENETRATION TESTING REPORT

## FOOTPRINTING & NETWORK SCANNING PHASES

**W2-PM-FINAL | CYBERSECURITY | NETWORKWALKS**

### Report Details

| Field | Details |
|---|---|
| **Pentester Name** | Oyetunde Al-Ameen Akorede (Cybersecurity Professional) |
| **Program/Batch** | B084-Networkwalks |
| **Date** | 13 September 2026 |
| **Modules Completed** | W2-PM1 (Multiple Kali Tools); W2-PM5 (Zenmap Scanning) |
| **Client/Target** | 1. Networkwalks (written permission secured)<br>2. My own local LAN |
| **Permission secured from client?** | Yes |
| **Phases covered** | Phase 1: Reconnaissance & Footprinting<br>Phase 2: Scanning & Network Discovery<br>Phases 3–5: In Progress |

## 1. Liability Disclaimer

I performed these activities only on systems and devices for which I had written permission or that I own. This report is for educational and research purposes. The knowledge and techniques described here must not be used unlawfully.

The instructor, authors and Networkwalks are not responsible for how others use this information. Anyone who misuses it is responsible for their actions. In many countries, unauthorized access is a crime, even if no damage is caused, and may result in criminal charges, fines, or other serious consequences.

## 2. Introduction

This report documents two Week 2 internship activities: footprinting the **networkwalks.com** domain using Kali Linux tools (W2-PM1), and scanning my own local network with Zenmap (W2-PM5). Together, these exercises introduced the process of collecting publicly available information about a domain and identifying active devices on a network.

I ran the footprinting commands in Kali Linux and used Zenmap on a Windows PC for the network scan. The report summarizes the tools used, the observations recorded, and why those observations may matter during a security assessment. Screenshots and exact command outputs should be included as evidence in the final submission.

## 3. Tools Used

| Tool | Purpose |
|---|---|
| Kali Linux and Windows | Operating systems used during the reconnaissance activities |
| WHOIS | Collect publicly available domain registration details, such as registration dates and name servers |
| WhatWeb | Identify web technologies, including servers, content management systems and plugins |
| Nslookup | Resolve a domain name to its IP address using DNS |
| `curl -I` | Inspect a website’s HTTP response headers |
| Wafw00f | Check whether a web application firewall may be present |
| DNSRecon | Gather DNS information, including name servers, mail servers, SPF/TXT and SRV records |
| Zenmap (Nmap GUI) | Scan a local subnet to discover live hosts and view network information |
| Windows CMD | Identify the local IP address and related network configuration |

## 4. Activities Performed

### 4.1 Footprinting & Reconnaissance

I used six Kali Linux tools to gather different types of publicly available information about **networkwalks.com**: WHOIS, WhatWeb, Nslookup, Curl, Wafw00f and DNSRecon.

WHOIS provided domain registration details and information about the domain’s name servers. I then ran WhatWeb to identify technologies associated with the website. The recorded results included WordPress 7.0.4 and WP Download Manager 3.3.58, along with other information exposed by the site.

Next, I used Nslookup to resolve the domain name. The recorded result was **192.232.216.135**. I used Curl with the `-I` option to view the site’s HTTP response headers. The results included technical information about the web application and an exposed WordPress REST API endpoint at `/wp-json/`.

Wafw00f identified **ModSecurity (SpiderLabs)** as the web application firewall. Finally, DNSRecon gathered DNS-related information, including details about name servers, mail servers, SPF/TXT records, service records and DNS software.

### 4.2 Network Scanning with Zenmap

For the second activity, I used Zenmap to discover devices on my local network. The practical exercise called for identifying the local IP address and subnet, finding active hosts, recording their IP and MAC addresses, and generating a network topology.

I began by using the Windows `ipconfig` command to check my local network configuration. I then entered the subnet into Zenmap and selected **Ping Scan** to identify active hosts.

The practical example listed one live host:

- `10.0.0.10`

After the scan, I opened Zenmap’s **Topology** view, enabled the legend and saved the topology as a PDF, as required by the exercise.

**Before submitting:** The host address above is from the example results provided in the practical. Replace it with the results from your own network, including your actual subnet and the number of hosts discovered. Add your scan evidence and topology PDF as applicable.

## 5. Risk Analysis / Impact

The observations below describe information gathered during the exercises. They do not confirm that a vulnerability exists.

| # | Risk / Finding | Evidence / Observation | Potential Impact | Risk Level |
|---|---|---|---|---|
| 1 | Web technology information is visible | WhatWeb identified WordPress and WP Download Manager | Technology and version details may help someone decide what further security checks to conduct | Medium |
| 2 | The server IP address is identifiable | Nslookup resolved the domain to `192.232.216.135` | The address gives additional information about where the web service is hosted | Low |
| 3 | HTTP technical information is available | Curl returned response headers and showed the `/wp-json/` endpoint | This information may assist with technology fingerprinting and further enumeration | Low |
| 4 | WAF technology is identifiable | Wafw00f identified ModSecurity (SpiderLabs) | Identifying the WAF provides information about the site’s security setup | Low |
| 5 | DNS infrastructure information is available | DNSRecon returned DNS, mail and service-related records | These records can help build a broader picture of the organization’s infrastructure | Medium |
| 6 | Live devices were visible on the local network | The practical’s example results listed a live host at `10.0.0.10` | Network discovery can help identify devices that should be checked and accounted for | Medium |

**Risk-level key:** Critical · Medium · Low

These are observations from footprinting and network discovery, not confirmed vulnerabilities. The exercises focused on information gathering and identifying hosts; no exploitation or vulnerability validation was performed. A software version, IP address or DNS record alone does not prove that a system is vulnerable. Further testing within an authorized scope would be needed to confirm any security issue.

## 6. Recommendations

1. **Review publicly visible technology information.** Regularly check what details about web technologies, the CMS and plugins are exposed.

2. **Keep software current.** Update CMS platforms, plugins and other web technologies, and review relevant security advisories.

3. **Review HTTP response headers.** Check whether the site’s headers expose technical details that are not needed.

4. **Review DNS records.** Periodically confirm that public DNS records and services are still required.

5. **Configure and monitor the WAF.** Keep ModSecurity enabled, review its configuration and monitor its alerts.

6. **Perform regular internal network discovery.** Scan authorized networks periodically to maintain an accurate view of active devices.

7. **Investigate unfamiliar devices.** Verify unexpected devices found during a scan and determine whether they belong on the network.

8. **Maintain network documentation.** Keep network topology and device records accurate and up to date.

9. **Work within an authorized scope.** Perform reconnaissance and scanning only on systems and networks for which permission has been granted.

## 7. Conclusion

During Week 2 of my Cybersecurity and Ethical Hacking internship, I completed practical activities in footprinting, reconnaissance and network scanning.

For the footprinting exercise, I used six Kali Linux tools to gather information about **networkwalks.com**. I learned how WHOIS can reveal domain registration information, WhatWeb can identify web technologies, Nslookup can resolve a domain name, Curl can display HTTP headers, Wafw00f can check for a WAF, and DNSRecon can collect DNS information.

For the network scanning exercise, I used Zenmap to discover active hosts on a local network. I also worked with local network configuration and the topology view. The example host details in this draft should be replaced with the results from my own network before submission.

These exercises showed me how security professionals can use public information and network responses to understand an environment. They also helped me see why findings need to be documented clearly: a report should explain what was done, what was observed, why it may matter and what steps could help reduce risk.

All reconnaissance and scanning described in this report were conducted as part of an educational program and within an authorized scope.

### Author

**Oyetunde Al-Ameen Akorede**  
Cybersecurity Intern at NetworkWalks B084  
LinkedIn: AL AMEEN

### Project Information

**Program Name:** Cybersecurity Program at Networkwalks  
**Week:** 02  
**Repository:** GitHub

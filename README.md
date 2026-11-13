
<div align="center">

# 🔍 Footprinting, OSINT & Network Scanning
### Reconnaissance and discovery practicals using Kali Linux tools, Maltego, theHarvester and Zenmap

[![Skill](https://img.shields.io/badge/Skill-Cybersecurity-red?style=for-the-badge&logo=shield&logoColor=white)](https://github.com)
[![Kali Linux](https://img.shields.io/badge/Kali_Linux-Recon_Tools-orange?style=for-the-badge&logo=kalilinux&logoColor=white)](https://github.com)
[![Maltego](https://img.shields.io/badge/Maltego-v4.14.0-green?style=for-the-badge&logo=maltego&logoColor=white)](https://github.com)
[![theHarvester](https://img.shields.io/badge/theHarvester-v4.11.1-blue?style=for-the-badge&logo=hackthebox&logoColor=white)](https://github.com)
[![Nmap](https://img.shields.io/badge/Nmap%20%2F%20Zenmap-v7.99-teal?style=for-the-badge&logo=cisco&logoColor=white)](https://github.com)
[![Phase](https://img.shields.io/badge/Phase-Recon_%26_Scanning-black?style=for-the-badge&logo=letsencrypt&logoColor=white)](https://github.com)
[![Ethical Hacking](https://img.shields.io/badge/Ethical_Hacking-Practice-darkred?style=for-the-badge&logo=hackthebox&logoColor=white)](https://github.com)
[![NetworkWalks](https://img.shields.io/badge/NetworkWalks-orange?style=for-the-badge&logo=network-wired&logoColor=white)](https://github.com)
[![GitHub](https://img.shields.io/badge/GitHub-Repository-blue?style=for-the-badge&logo=github&logoColor=white)](https://github.com)

</div>

---

## 📌 Project Overview
This project documents the Week 2 practicals of the Networkwalks Cybersecurity Program (Batch B084). It follows the way an attacker moves through the first two phases of a penetration test: collecting public information about a target without touching it, correlating that information into a relationship graph, harvesting more data from public search engines, and finally discovering live hosts on a network segment.

Two practicals were completed:

| Module | Practical | Target / Scope |
| :--- | :--- | :--- |
| **W2-PM1** | Footprinting with six Kali Linux tools | `networkwalks.com` (written permission secured) |
| **W2-PM5** | Host discovery with Zenmap | My own local LAN (`10.0.1.0/24`) |

```mermaid
graph TD
    A["W2-PM1: Fingerprinting"] -->B
 B[W2-PM5: Host Discovery with Zenmap"]
```

---

## 🎯 Objectives
- Collect domain registration, DNS, web-technology and perimeter-defence information about a target using six Kali Linux tools.
- Correlate a single domain into a graph of e-mail addresses, subdomains, mail servers and websites with Maltego.
- Harvest hostnames, IPs and email addresses from public sources with theHarvester.
- Identify the local subnet, discover live hosts, and capture IP and MAC addresses with Zenmap.
- Interpret every finding from an attacker's point of view and rate its risk.
- Recommend practical defensive improvements.
- Document commands, results, problems and lessons learned.

---

## 🛡️ Purpose of the Lab
These exercises build the skills used in the **Reconnaissance & Footprinting** and **Scanning & Network Discovery** phases of a penetration test.

Key capabilities practised:
- WHOIS and DNS intelligence gathering
- Web technology and WAF fingerprinting
- HTTP header analysis
- Passive reconnaissance through search engines
- ARP/ICMP-based host discovery and topology mapping

---

## ⚙️ Environment & Tools

| 🧩 Component | ⚙️ Details |
| :--- | :--- |
| 🐉 Recon workstation | Kali Linux (`pentest-serv01`) |
| 🪟 Link analysis / scanning | Windows PC with Maltego Graph Desktop and Zenmap |
| 🔎 WHOIS | Domain registration data |
| 🌐 WhatWeb | Web technology fingerprinting |
| 📡 nslookup | DNS resolution (via 8.8.8.8) |
| 📥 curl | HTTP header inspection |
| 🧱 wafw00f v2.4.2 | WAF detection |
| 🗺️ dnsrecon | DNS enumeration |
| 🛰️ Zenmap / Nmap 7.99 | Host discovery and topology |

---

## 4. Practical Execution and Findings

### 4.1 WHOIS — Domain Registration Information

**Command:**
```bash
whois networkwalks.com
```

**Purpose:**

WHOIS was used to retrieve publicly available registration information about the target domain.

**Information examined:**
- Domain registrar.
- Domain creation and expiration dates.
- Domain status.
- Name servers.
- Registration privacy information.

**Findings and Analysis:**

The WHOIS lookup provided information about the domain's registration, registrar, name servers and registration status. This information helps establish the ownership and administrative details associated with a domain.

**Evidence:**

![WHOIS output 1/3](screenshots/1-Footprinting-whois-1.png)
![WHOIS output 2/3](screenshots/2-footprinting-whois-2.png)
![WHOIS output 2/3](screenshots/3-footprinting-whois-3.png)
![WHOIS output 2/3](screenshots/4-footprinting-whois-3.png)

**Command:**
```bash
whatweb networkwalks.com
```

**Purpose:**

WhatWeb was used to identify the technologies and software components running on the target website.

**Information examined:**
- Web server.
- Content Management System (CMS).
- JavaScript libraries.
- Website plugins.
- Server IP address.

**Findings and Analysis:**

The scan provided information about the website's underlying technologies and software components. Technology fingerprinting can help security professionals identify outdated software and understand the technologies used by a website.

**Evidence:**

![WhatWeb Screenshot](screenshots/5-footprinting-whatweb.png)

---

### 4.3 nslookup — DNS Information Gathering

**Command:**
```bash
nslookup networkwalks.com
```

**Purpose:**

nslookup was used to query the Domain Name System (DNS) and determine the IP address associated with the target domain.

**Information examined:**
- Domain name.
- Resolved IP address.
- DNS server used for the query.

**Findings and Analysis:**

The lookup returned the IP address associated with the domain. DNS information is useful during reconnaissance because it helps establish the relationship between domain names and their corresponding network addresses.

**Evidence:**

![nslookup Output](screenshots/6-footprinting-nslookup.png)

---

### 4.4 curl — HTTP Header Inspection

**Command:**
```bash
curl -i networkwalks.com
```

**Purpose:**

curl was used to send an HTTP request and inspect the response returned by the target web server.

**Information examined:**
- HTTP response status.
- Server information.
- Redirect behaviour.
- Security-related HTTP headers.

**Findings and Analysis:**

The response provided information about how the web server handled the request, including its HTTP status and response headers. These headers can reveal details about the server configuration and security controls.

**Evidence:**

![curl Output](screenshots/7-footprinting-curl.png)

---

### 4.5 wafw00f — Web Application Firewall Detection

**Command:**
```bash
wafw00f networkwalks.com
```

**Purpose:**

wafw00f was used to identify whether a Web Application Firewall (WAF) was protecting the target website.

**Information examined:**
- Presence of a WAF.
- Identified WAF technology.
- Detection response.

**Findings and Analysis:**

The tool examined the website's responses to determine whether a Web Application Firewall was present. Identifying a WAF helps security professionals understand the defensive technologies protecting a web application.

**Evidence:**

![wafw00f Output](screenshots/8-footprinting-wafw00f.png)

---

### 4.6 dnsrecon — DNS Enumeration

**Command:**
```bash
dnsrecon -d networkwalks.com
```

**Purpose:**

dnsrecon was used to gather additional DNS information about the target domain.

**Information examined:**
- A records.
- MX records.
- NS records.
- SOA records.
- TXT records.
- Other available DNS information.

**Findings and Analysis:**

The enumeration provided additional information about the domain's DNS configuration and associated infrastructure. This information helps security professionals understand how a domain's DNS services are organised.

**Evidence:**

![dnsrecon Output](screeshots/9-footprinting-dnsrecon.png)

| Tool | Information Obtained |
|---|---|
| WHOIS | Domain registration information |
| WhatWeb | Website technologies |
| nslookup | Domain-to-IP resolution |
| curl | HTTP response and headers |
| wafw00f | WAF identification |
| dnsrecon | DNS records and infrastructure |

The results demonstrate how multiple reconnaissance tools can be combined to develop a better understanding of a domain's publicly exposed information.

---

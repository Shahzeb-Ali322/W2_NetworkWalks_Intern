# Week 2: Footprinting, Reconnaissance & Network Scanning

**Cybersecurity & Ethical Hacking Internship | Networkwalks | Batch B082**
**Author:** Shahzeb Ali | [LinkedIn](https://www.linkedin.com/in/shahzeb-ali-5aab89299/)
**Date:** 13 November 2026

---

## Overview

This repository holds my Week 2 submission. The work covers two modules:

- **W2-M1 / PM1: Footprinting & Reconnaissance** of `networkwalks.com`, using six Kali Linux tools.
- **W2-M5: Zenmap Network Scanning (Practice Lab):** installing Nmap/Zenmap and running host discovery on a local lab network.

> **Authorization:** The reconnaissance on `networkwalks.com` was done with Networkwalks' permission, as an assigned internship task. It was information gathering only. No exploitation or vulnerability validation was performed. The host discovery was run on my own local network.

---

## Repository Structure

```
Week 2/
├── W2_PM_Final Report.pdf        # Full penetration testing report (Phase 1: Recon)
├── W2_M1/                        # Footprinting & Reconnaissance
│   ├── reconbywhois.txt
│   ├── reconbywhatweb.txt
│   ├── reconbynslookup.txt
│   ├── reconbycurl.txt
│   ├── reconbywafw00f.txt
│   └── *.png                     # Screenshots as evidence
└── W2_M5/                        # Zenmap / Nmap network scanning
    ├── Installing & upgrading nmap(Zen_map).png
    ├── Finding IP & Subnet.png
    ├── Host Discovery.png
    ├── Zen_Map Host Discovery.png
    ├── zenmap topology.pdf
    └── Screenshot From 2026-11-13 07-39-35.png   # Lab completion (100%)
```

---

## Module 1: Footprinting & Reconnaissance (`W2_M1`)

**Target:** `networkwalks.com`  |  **Environment:** Kali Linux

| Tool | Command | Purpose |
|------|---------|---------|
| WHOIS | `whois networkwalks.com > reconbywhois.txt` | Domain registration details |
| WhatWeb | `whatweb networkwalks.com > reconbywhatweb.txt` | Web technology fingerprinting |
| Nslookup | `nslookup networkwalks.com > reconbynslookup.txt` | DNS resolution to IP |
| Curl | `curl -I networkwalks.com > reconbycurl.txt` | HTTP response header analysis |
| Wafw00f | `wafw00f networkwalks.com > reconbywafw00f.txt` | Web Application Firewall detection |
| DNSRecon | `sudo dnsrecon -d networkwalks.com` | DNS record enumeration |

### Key Findings

- **Registration:** Registered with GoDaddy. Privacy protection (Domains By Proxy) and all four client locks are enabled. DNSSEC is unsigned.
- **Technology stack:** Apache, WordPress, WordPress Download Manager and jQuery, behind an nginx/Endurance caching layer.
- **Hosting:** Hosted in the United States and resolving to a single IP. Name servers are HostGator.
- **WAF:** ModSecurity (SpiderLabs) detected.
- **DNS:** BIND version disclosed on both name servers. The SPF record uses soft fail (`~all`).

### Risk Summary

| # | Observation | Risk |
|---|-------------|------|
| 1 | Web technology and version information exposed | Medium |
| 2 | DNS software (BIND) version disclosed | Medium |
| 3 | Server IP address identifiable | Low |
| 4 | HTTP technical headers exposed | Low |
| 5 | WAF technology identifiable | Low |
| 6 | SPF record uses soft fail (`~all`) | Low |
| 7 | DNSSEC not enabled | Low |
| 8 | Public email address exposed | Low |
| 9 | Different name server sets listed (registry vs registrar) | Low |

> These are **observations, not confirmed vulnerabilities**. Seeing a version number, IP address or DNS record does not mean a system is vulnerable. Further authorized testing would be needed to confirm any issue.

### Positive Security Observations

- Domain privacy and registrar locks enabled
- HTTP redirects to HTTPS
- ModSecurity WAF in place
- `HttpOnly` flag on the session cookie
- Apache `Server` header does not reveal a version number

### Recommendations (summary)

1. Reduce exposed CMS, plugin and library version information.
2. Keep WordPress and all plugins updated.
3. Hide the DNS software version.
4. Review HTTP headers that expose technical detail.
5. Strengthen email authentication (stricter SPF, DKIM and DMARC).
6. Consider enabling DNSSEC.
7. Review DNS records and clarify the mixed name server sets.
8. Keep the WAF enabled, tuned and monitored.
9. Only test systems with written authorization.

The full write-up, with evidence for each step, is in **`W2_PM_Final Report.pdf`**.

---

## Module 5: Zenmap Network Scanning (`W2_M5`)

Practice lab on host discovery with Nmap and its GUI, Zenmap, on a local network.

| Step | Command / Action | Evidence |
|------|------------------|----------|
| Install / upgrade Nmap | `sudo apt install \|\| upgrade nmap` | `Installing & upgrading nmap(Zen_map).png` |
| Find IP and subnet | `ifconfig` | `Finding IP & Subnet.png` |
| Host discovery (CLI) | `sudo nmap -sn 192.168.1.0/24` | `Host Discovery.png` |
| Host discovery (Zenmap) | Ping scan profile on `192.168.1.0/24` | `Zen_Map Host Discovery.png` |
| Network topology | Zenmap Topology tab | `zenmap topology.pdf` |

**Results:** The ping scan (`-sn`) covered 256 IP addresses and found a handful of live hosts, including the gateway router. Nmap reported hosts with their IPs, latency and MAC vendors, and Zenmap showed them in its host list and topology view.

**Outcome:** Completed the *Zenmap Network Scanning (Practice Lab)* quiz with a score of **100%**.

---

## Skills Practiced

- Passive and active footprinting
- DNS, WHOIS and HTTP header analysis
- Web technology and WAF fingerprinting
- Host discovery and network mapping with Nmap/Zenmap
- Risk rating and professional security reporting
- Working within an authorized scope

---

## Disclaimer

All activities were performed only on systems where I had permission, for educational purposes as part of the Networkwalks internship program. Do not use anything here to break the law. Unauthorized access to systems is a crime in most countries. The author and Networkwalks are not responsible for misuse of this material.

---

**Shahzeb Ali** | Cybersecurity & Ethical Hacking Intern | Networkwalks B082

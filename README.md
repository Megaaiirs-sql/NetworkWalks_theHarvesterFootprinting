# NetworkTalks_theHarvesterFootprinting

Week 2 project for the NetworkTalks Cybersecurity Internship — Footprinting & Reconnaissance with theHarvester (Project Module 4).

## Overview

This project documents a passive OSINT (Open Source Intelligence) footprinting exercise using theHarvester, a tool that gathers publicly available information about a target domain — emails, subdomains, hosts, and IP addresses — entirely from public sources, without ever directly contacting or scanning the target's systems.

Target domain: microsoft.com (used per the lab's instructions, as a large, well-known public domain).

## Objective

Learn to use theHarvester to gather email addresses, subdomains, and hosts associated with a target organization, compare results across a single data source vs. multiple combined sources, and understand how passive reconnaissance reveals an organization's public attack surface.


## Methodology

### Task 1 - Single source (Baidu)

Command used: theHarvester -d microsoft.com -l 1000 -b baidu

Searches exclusively through Baidu (a Chinese search engine), limited to 1000 results.

### Task 2 - All sources

Command used: theHarvester -d microsoft.com -l 50 -b all

Searches across every data source theHarvester supports, limited to 50 results per source. Sources requiring a paid API key (Shodan, VirusTotal, SecurityTrails, etc.) are automatically skipped with a warning; free/open sources (crt.sh, DNS records, DuckDuckGo, Wayback Archive, Hudson Rock, etc.) are used.

## Results

Task 1 (Baidu only): 0 emails, 0 hosts/subdomains, 0 IPs found.

Task 2 (All sources): 3 emails, 9,972 hosts/subdomains, 172 IPs, 6 ASNs found.

Emails discovered (Task 2):
- dotnet-docker-bot@microsoft.com
- opencode@microsoft.com
- secure@microsoft.com

Full raw output saved in task1_output.json / task1_output.xml and task2_output.json / task2_output.xml.

## Key Takeaways

Single-source searches can be highly misleading. Baidu alone returned zero results for microsoft.com, not because the domain has no public footprint, but because Baidu's index has minimal coverage of large Western corporate domains. Relying on one source in a real assessment would produce a dangerously incomplete picture.

Combining sources reveals the true scale of an attack surface. The all-sources scan surfaced nearly 10,000 subdomains, many following naming patterns suggesting internal, staging, or pre-production environments (ppe, test, dev, uat) - exactly the kind of forgotten or under-monitored systems that expand an organization's real attack surface.

theHarvester is entirely passive. It never sends traffic to the target's own infrastructure - everything it returns was already indexed by public search engines, certificate transparency logs, and similar open sources. This is why footprinting is so hard to detect: the target has no way of knowing it's being studied.

API key limitations are a real constraint. Many of theHarvester's most powerful sources (Shodan, VirusTotal, SecurityTrails) require paid API access. A professional assessment with those keys configured would likely surface significantly more data than this exercise captured.

## Disclaimer

This exercise used only passive, publicly available OSINT techniques against a public domain, as instructed in the NetworkTalks lab materials. No systems were accessed, scanned, or interacted with directly. This is standard, legal reconnaissance methodology taught across cybersecurity certifications (CEH, OSCP, etc.) - the same principle a defender would use to audit their own organization's public exposure.

## Author

Built as part of the NetworkTalks Cybersecurity Internship (Week 2, Project Module 4: Footprinting & Reconnaissance with theHarvester).

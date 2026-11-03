---
title: "Threat Intelligence: Pyramid of Pain"
excerpt: "Confirmed a malicious file hash with VirusTotal and mapped its indicators of compromise to the Pyramid of Pain."
category_slug: risk-threat
order: 8
skills: ["Threat Intelligence", "VirusTotal", "IoCs", "Malware Analysis"]
project_url: "https://drive.google.com/file/d/14uNWu5Z62rkdF2jP16HYd5qZN_cXlbCA/view?usp=sharing"
---

## Overview
A SOC analyst exercise investigating a suspicious file hash.

## Key findings
- **Verdict: malicious.** 47 of 65 vendors flagged the file, with a community score of -293. It was identified as a trojan from the FlagPro family, commonly linked to the BlackTech threat group.
- Extracted indicators (hash values, IP addresses, domain names, network and host artifacts, tools and TTPs) and mapped each to its level on the Pyramid of Pain.

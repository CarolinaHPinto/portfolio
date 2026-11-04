---
title: "Incident Report: DNS Resolution Failure"
excerpt: "Analyzed a tcpdump capture to diagnose why customers couldn't reach a website, and proposed a fix."
category_slug: incident-response
order: 11
skills: ["tcpdump", "DNS", "UDP / ICMP", "Network Troubleshooting"]
deliverable: "/assets/projects/dns-incident.pdf"
deliverable_pages: 1
preview: "/assets/images/projects/dns-incident.jpg"
project_url: "https://drive.google.com/file/d/1g2S-gMPjmbWYGgF1vBgzLj8VmxBTibiT/view?usp=sharing"
---

## Overview
Customers reported they couldn't load a client's website.

## What I did
- Read the tcpdump log: repeated DNS queries over UDP were answered with ICMP "udp port 53 unreachable" errors.
- Identified the affected protocols and the likely cause on the DNS server.
- Documented the analysis and recommended a solution.

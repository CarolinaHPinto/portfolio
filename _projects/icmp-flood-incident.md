---
title: "Incident Report: ICMP Flood DoS"
excerpt: "Analyzed a two-hour outage caused by an ICMP flood and documented it across the NIST CSF functions."
category_slug: incident-response
order: 9
featured: true
skills: ["NIST CSF", "DoS Analysis", "Firewall Rules", "IDS/IPS", "Incident Documentation"]
project_url: "https://drive.google.com/file/d/1VIEJvGct89KvTzloB_TJZpq6q832Fjlq/view?usp=sharing"
---

## Overview
All network services stopped responding for two hours after an ICMP packet flood passed through an unconfigured edge firewall.

## What I did
- **Identify:** pinpointed the attack type (ICMP ping flood), the vulnerability (unfiltered incoming ICMP) and the affected systems.
- **Protect / Detect / Respond / Recover:** documented containment (blocking ICMP, taking non-critical services offline) and follow-up controls: new firewall rules, source IP verification, network monitoring and an IDS/IPS.

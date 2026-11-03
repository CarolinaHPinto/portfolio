---
title: "Incident Report: SYN Flood on a Sales Web Server"
excerpt: "Used Wireshark logs to identify a SYN flood from a single IP and explain why the company website was timing out."
category_slug: incident-response
order: 10
skills: ["Wireshark", "TCP Handshake", "DoS vs DDoS", "Traffic Analysis"]
project_url: "https://drive.google.com/file/d/1l_ntSamF4qztjJrwwAsNHhKce0SiQj1N/view?usp=sharing"
---

## Overview
Customers were getting connection timeout errors on the company's sales website.

## What I did
- Found an abnormally large number of TCP SYN packets from a single external IP in the Wireshark logs.
- Classified it as a DoS (single source) rather than a DDoS, and specifically a SYN flood, because the attacker never completed the TCP handshake.
- Explained how the flood exhausted the server's resources and caused the timeouts.

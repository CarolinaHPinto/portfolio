---
title: "Scanning & Enumeration Lab"
excerpt: "Mapped a lab network with Nmap, SMB, WMI, LDAP and ffuf, and verified the results before and after remediation."
category_slug: network-security
order: 14
skills: ["Nmap / Zenmap", "SMB Enumeration", "WMI", "LDAP", "ffuf"]
deliverable: "/assets/projects/scanning-enumeration.pdf"
deliverable_pages: 3
preview: "/assets/images/projects/scanning-enumeration.jpg"
deliverable_extra: "/assets/projects/scanning-enumeration.xlsx"
deliverable_extra_label: "Download the spreadsheet (.xlsx)"
project_url: "https://docs.google.com/spreadsheets/d/1IQu6KAqTtfwqnyxUTeSFPst_GSQCAwgRZUE9ivPKx4s/view"
---

## Overview
A hands-on scanning and enumeration lab against a test network.

## What I did
- Ran Nmap and Zenmap scans: ping, aggressive, service and version detection, and script scans.
- Enumerated SMB (nmblookup, nbtscan, smb-os-discovery, smb-enum-shares), WMI and LDAP user objects.
- Discovered web content with ffuf, and compared web banners and SMB versions before and after fixes.

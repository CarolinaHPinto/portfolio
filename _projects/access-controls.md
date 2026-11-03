---
title: "Access Controls Review: Unauthorized Payroll Entry"
excerpt: "Traced an unauthorized payroll transaction to a contractor account that was never deactivated, and recommended access control fixes."
category_slug: grc
order: 4
skills: ["Access Control", "Least Privilege", "Account Lifecycle", "Log Review"]
project_url: "https://drive.google.com/file/d/1PqrK8qCFQ1LfpeIDr9pq2YzoBlj7SEbc/view?usp=sharing"
---

## Overview
Investigated an unauthorized payroll entry posted under an administrator account.

## Key findings
- The event log tied the entry to the IP address of a legal contractor whose access had ended almost four years earlier, but whose account was never deactivated.
- Every user in the directory, including part-time, seasonal and contract staff, held broader access than their role required.
- Recommended authorization and authentication fixes, including timely account deprovisioning and least-privilege access.

---
title: "Data Leak Analysis: Least Privilege"
excerpt: "Analyzed how internal product files were accidentally shared publicly and recommended controls to prevent it from happening again."
category_slug: grc
order: 5
skills: ["Least Privilege", "Data Protection", "Control Analysis"]
project_url: "https://drive.google.com/file/d/1u0R89TAfGV3qiW4z2J82JHxkTCS1_9aV/view?usp=sharing"
---

## Overview
A sales representative accidentally shared a link to an internal folder (unreleased product files, customer analytics) instead of approved promotional materials. A business partner then posted the link publicly.

## What I did
- Identified where the least privilege control broke down: access to the internal folder was never revoked after the meeting.
- Documented the issue and recommended changes to prevent similar leaks.

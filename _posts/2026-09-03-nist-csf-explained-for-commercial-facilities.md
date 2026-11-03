---
title: "The NIST Cybersecurity Framework, Explained Simply (For Anyone Running a Commercial Facility)"
date: 2026-09-03
categories: [GRC & Frameworks]
tags: [nist csf, cisa, risk management, supply chain]
excerpt: "A plain-English summary of CISA's framework guidance for commercial facilities: the threats, the three building blocks, and the seven-step cycle."
---

*This is a simplified summary of the Commercial Facilities Sector Cybersecurity Framework Implementation Guidance, published by the Cybersecurity and Infrastructure Security Agency (CISA), U.S. Department of Homeland Security, May 2020. It's meant as an accessible starting point — not a replacement for the original guidance — for anyone new to security work who wants to understand the basics before diving into the full document.*

If you manage a building, a stadium, a shopping center, or really any kind of commercial facility, "cybersecurity" probably feels like someone else's job — the IT department's problem, not yours. But here's the thing: badge readers, HVAC controls, payment systems, parking gates, and building management software are all computers now. And computers can be attacked.

That's where the NIST Cybersecurity Framework comes in — and CISA (the Cybersecurity and Infrastructure Security Agency) put together a whole guide just for the Commercial Facilities Sector on how to actually use it. Here's what you need to know, without the jargon overload.

## Why This Exists

Back in 2014, the government passed a law (the Cybersecurity Enhancement Act) asking NIST to build a voluntary framework that any organization could use to get a handle on cyber risk. It's now on Version 1.1, and it wasn't built for tech companies — it was built to be flexible enough for anyone, including facilities that never thought of themselves as "tech" businesses.

The core idea: cyber risk is just another business risk, like fire risk or financial risk. You don't need to eliminate it — you need to understand it, manage it, and keep improving.

## The Threats You're Actually Defending Against

Before diving into the framework itself, it helps to know what you're up against. The common ones:

- **Ransomware** — malware that locks up your data until you pay
- **Phishing** — fake emails/texts trying to trick employees into handing over access
- **DDoS attacks** — flooding a website or system with traffic until it crashes
- **Man-in-the-middle attacks** — someone secretly intercepting data mid-transaction
- **Trojan horses & viruses** — malicious programs disguised as legitimate software
- **Spear phishing** — a phishing attempt that's been custom-tailored to a specific person, making it far more convincing
- **Pharming** — quietly redirecting someone from a legitimate website to a fake one, without them noticing
- **SQL injection** — malicious code slipped into a system to trick a server into leaking private data
- **Watering hole attacks** — compromising a website your employees already trust and visit often, so the infection spreads through normal browsing

None of these require a Hollywood-level hacker. Most start with something boring, like a weak password or an unpatched system. Which is why CISA's basics list is refreshingly unglamorous: change default passwords, keep software patched, lock down unused ports, train your staff, and revoke access the moment someone leaves the company. Boring, but it's where most breaches actually start.

## The Framework's Three Building Blocks

The whole thing boils down to three pieces working together:

### 1. The Framework Core

A menu of cybersecurity activities, organized into five plain-English "Functions":

- **Identify** — know what you have and what could go wrong
- **Protect** — put safeguards in place
- **Detect** — notice when something's off
- **Respond** — act when there's an incident
- **Recover** — get back to normal afterward

Think of these as the five verbs of cybersecurity. Everything else in the framework is just detail underneath these.

Each Function then breaks down into **Categories** (more specific groupings) and **Subcategories** (concrete, checkable outcomes). It sounds bureaucratic, but it's actually the most useful part once you dig in — because it turns vague advice like "be secure" into specific, answerable questions. A few examples of what that looks like in practice:

- **Identify → Asset Management:** "Are all your physical devices and software inventoried?" "Do you know which of your systems are actually critical to the business?"
- **Protect → Identity Management and Access Control:** "Is remote access managed and logged?" "Do people only have the access they actually need (least privilege)?"
- **Detect → Anomalies and Events:** "Do you have a baseline for what 'normal' network activity looks like, so you'd notice when something's off?"
- **Respond → Communications:** "Does everyone know their role and who to notify when an incident happens?"
- **Recover → Improvements:** "Do you actually update your recovery plan based on lessons learned, or does it just sit in a drawer?"

Each Subcategory also comes with **Informative References** — pointers to existing standards (like NIST SP 800-53 or ISO 27001) that show how to actually achieve that outcome. So you're not reinventing anything; you're mapping what you already do (or should do) to a recognized standard.

There are over 20 Categories and 100+ Subcategories total across the five Functions — you're not meant to tackle all of them at once. That's exactly what the Profile and Tiers are for: deciding which ones matter most to your organization right now.

### 2. The Framework Profile

This is where you get honest about where you are (your "Current Profile") versus where you want to be (your "Target Profile"). The gap between the two becomes your action plan.

### 3. Implementation Tiers

A 1-to-4 scale describing how mature your risk management actually is:

- **Tier 1 (Partial):** reactive, ad hoc, no real process
- **Tier 2 (Risk Informed):** management is aware, but nothing's consistent org-wide
- **Tier 3 (Repeatable):** formal policies, consistently applied
- **Tier 4 (Adaptive):** you're learning and adjusting in real time, and sharing knowledge with others

Important nuance: these tiers aren't a report card you need straight A's on, and they're not officially defined as "maturity levels" — NIST is explicit about that. A small facility might reasonably decide Tier 2 is good enough for certain systems, while a Tier 1 organization pushing toward Tier 4 for a low-risk system would just be wasting money. The real question the framework wants you asking is: does the cost of moving up a tier actually buy us a meaningful reduction in risk? If yes, move up. If not, stay put and spend the budget elsewhere.

Each tier is actually assessed across three angles, not just "how good are your policies":

- **Risk Management Process** — how formal and consistent your practices are
- **Integrated Risk Management Program** — how aware and involved the organization is as a whole, not just IT
- **External Participation** — whether you understand your role in the bigger picture (your vendors, your industry, threat-sharing groups) and whether you're exchanging information with others

That third one surprises people. Tier 3 and 4 organizations aren't just internally buttoned-up — they're actively plugged into outside threat intelligence and sharing what they learn, rather than operating in a silo.

## The Seven Steps to Actually Do This

This is the part that turns theory into action. CISA lays out a repeatable, seven-step cycle:

1. **Prioritize and Scope** — Decide what matters most to your business and which parts of the organization will use the framework first. If this is your first time through, don't boil the ocean — CISA specifically suggests picking one business function or one facility to start, then expanding once you've got the hang of it.
2. **Orient** — Take stock: what systems, assets, and risk practices do you already have? This is where you identify everything in scope — your building management systems, payment processing, badge access, cameras — and figure out how you're going to evaluate your current posture. You've basically got two options here: a self-evaluation (using your own staff, which builds internal awareness as a side benefit) or a facilitated approach (bringing in a third party's expertise). Neither is "more correct" — it depends on your resources and how objective you need the assessment to be.
3. **Create a Current Profile** — Honestly map what you're doing today against the framework's categories, and also figure out your current Implementation Tier. A good trick here: you're probably already doing more than you think, just not labeled this way. If you have a risk assessment program, an insurance audit, or industry-standard compliance already in place (PCI-DSS for payments, for example), that work often maps directly onto framework Subcategories — no need to start from scratch.
4. **Conduct a Risk Assessment** — Figure out what's likely to happen and how bad it would be. This means looking at your actual threat landscape (not a generic list) — pulling in current threat intelligence, thinking through what a cybersecurity event would actually cost you operationally, financially, and reputationally. This step feeds directly into what your Target Profile should prioritize.
5. **Create a Target Profile** — Define where you want to be, based on your current risk environment, legal/regulatory requirements, business objectives, and any practical constraints (budget, staffing, timeline). You also pick a Target Implementation Tier here — the level of process maturity you're actually aiming for, not just an aspirational number.
6. **Determine, Analyze, and Prioritize Gaps** — Compare current vs. target, and figure out what's worth fixing first. Not every gap deserves equal urgency — CISA recommends running a real cost-benefit analysis on each one, factoring in consequences of leaving it unaddressed, before building your prioritized action plan.
7. **Implement the Action Plan** — Do the work, then monitor your practices against the Target Profile you set. And communicate progress along the way — to leadership, to staff, to whoever needs to know the plan is actually moving.

That last point matters: this isn't a one-and-done checklist, it's a loop (CISA literally draws it as a circle in their diagram, with "Monitor & Reassess" wrapping back around to Step 1). Threats evolve, your business changes, so your profile should keep evolving too. Some organizations find that revisiting just the "Orient" step more frequently sharpens their risk assessments over time — you don't need to redo all seven steps to make progress.

## A Simple Example That Makes It Click

The guide uses "remote access" (like VPN logins) as a running example, and it's a great way to see the framework in action:

- A **Current Profile** might say: "We use VPN, we log connection attempts, and we disable accounts when someone quits."
- A **Target Profile** might add: "...and we also require supervisor sign-off before issuing VPN access, and we review the account list twice a year."
- The **Gap** is exactly those two missing pieces — which becomes your to-do list.

Notice there's no single "correct" way to do this. One organization might rely on internal controls, another might map everything to a formal standard like NIST SP 800-53, and a smaller organization might legitimately say "not applicable — we don't offer remote access at all." All three are valid uses of the framework.

## Don't Forget Your Vendors

One thing that's easy to overlook: your risk doesn't stop at your own systems. Every vendor you rely on — the company that maintains your HVAC, the payment processor, the software provider for your building access system — is a potential entry point too. The framework has a whole category for this called Supply Chain Risk Management, and it's worth two practical takeaways:

- **Communicating requirements:** if you have real leverage with a vendor, you can use your Target Profile to actually set cybersecurity expectations in the relationship — not just accept whatever they offer.
- **Buying decisions:** even when you can't dictate terms to a supplier (say, you're a small buyer and they're a huge company), your Target Profile still gives you a consistent checklist to compare vendors against before you sign a contract. And once you've bought something, the profile helps you track and manage whatever residual risk comes with it.

It's a good reminder that a facility can do everything right internally and still get burned through a third party with weak practices.

## You Don't Have to Build This From Scratch

CISA's guidance also includes a mapping of existing tools and standards many Commercial Facilities organizations are already using, showing how they line up with the framework. A few worth knowing:

- **PCI-DSS** — if you process card payments, you're likely already meeting some framework outcomes without realizing it
- **Cyber Resilience Review (CRR)** — a free assessment (from CISA) across 10 domains like incident management and service continuity, with a direct crosswalk to the framework
- **Cybersecurity Evaluation Tool (CSET)** — walks you step-by-step through assessing your systems against recognized standards
- **Baldrige Cybersecurity Excellence Builder** — a self-assessment tool blending business performance thinking with cybersecurity risk
- **FedVTE** — free online cybersecurity training (open to government personnel and veterans)

The point isn't to adopt all of these — it's that you probably have a head start already, especially if you're in a regulated corner of the sector (payments, stadiums, large venues).

## Why Bother? What's Actually In It For You

Beyond just "reducing risk," CISA points to some concrete upsides:

- **Better insurance terms** — insurers increasingly price cyber coverage based on your practices
- **Access to free technical help** — CISA's Cybersecurity Advisors offer hands-on assistance
- **A shared language** — makes it easier to talk cybersecurity with regulators, vendors, and leadership without confusion
- **Smarter hiring and training** — once you know your gaps, you know what skills your team actually needs

## The Bottom Line

You don't need to become a cybersecurity expert to use this framework — that's the whole point of it. It gives you a common vocabulary (Identify, Protect, Detect, Respond, Recover), a way to be honest about where you stand, and a repeatable process for closing the gaps that matter most to your organization, not some generic checklist.

Start small. Pick one system or one department. Walk through the seven steps. Then do it again, a little wider, next time.

---

*A note on this summary: This piece condenses and simplifies the Commercial Facilities Sector Cybersecurity Framework Implementation Guidance (CISA, May 2020), itself built on the NIST Framework for Improving Critical Infrastructure Cybersecurity, Version 1.1 (2018). Nothing here should be treated as a substitute for reading the source document or for professional guidance specific to your organization — think of this as orientation reading, the kind of thing that gets a beginner security professional or a facilities manager fluent enough to have an informed conversation before diving into the full framework, a formal risk assessment, or outside consultation.*

*For the full picture — including the complete list of over 100 Subcategories, the detailed sector-specific tool mappings, and the notional use-case walkthrough — the original [CISA](https://www.cisa.gov/) guidance and the NIST Cybersecurity Framework website ([nist.gov/cyberframework](https://www.nist.gov/cyberframework)) are the next stops.*

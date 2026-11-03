---
title: "Building My First NIST CSF 2.0 Gap Assessment: What Actually Goes Into One"
date: 2026-08-20
categories: [GRC & Frameworks]
tags: [nist csf, gap assessment, risk register, grc]
excerpt: "Maturity tiers, asset inventories, risk registers and remediation roadmaps, explained through a fictional wealth management firm."
---

For this project, I wanted to move past reading about frameworks and actually build something a GRC professional would produce on the job: a NIST CSF 2.0 Gap Assessment. I put together a fictional case — Meridian Wealth Partners, a wealth management firm handling UHNW clients — and evaluated it against the six core functions of the framework: Govern, Identify, Protect, Detect, Respond, and Recover.

Here's the thinking behind it, what each piece of the assessment actually means, where a GRC analyst would realistically go to find that information, and how it all comes together.

*See the finished deliverable on the [project page]({{ '/projects/nist-csf-gap-assessment/' | relative_url }}).*

## Why I Built This

A framework only means something once you've applied it to a real (or realistic) situation. I picked a wealth management firm on purpose — it's a business type that lives and dies by trust, handles highly sensitive client data, and already operates under existing regulatory pressure (GLBA Safeguards Rule, KYC/AML). That overlap is exactly where my background sits, so it gave me a scenario where I could evaluate technical and governance gaps side by side, the way I'd actually need to on the job.

## The Six Functions, in Plain Language

NIST CSF 2.0 organizes everything into six functions. Here's how I'd explain each one to someone outside the field:

- **Govern (GV):** Who's actually accountable for cybersecurity, and is there a real strategy behind it? Think of it as the difference between a company that has an IT guy who "handles security" versus one where the board gets a quarterly cyber risk report and someone senior owns the outcome. Govern is actually the newest of the six functions, added in CSF 2.0 — and without it, the other five tend to lack strategic direction, accountability, and consistent execution. It's the function that makes the other five actually mean something.
- **Identify (ID):** Do you actually know what you have and what could go wrong with it? Like doing a home inventory before filing an insurance claim — you can't protect what you haven't catalogued.
- **Protect (PR):** The safeguards themselves — access controls, training, data security. This is the locks on the doors and the alarm system.
- **Detect (DE):** Would you know if something bad was already happening? This is the difference between a house with motion-sensor cameras and one that only finds out about a break-in when something's missing.
- **Respond (RS):** Once you know something's wrong, is there an actual plan, or is everyone improvising? Think fire drill versus everyone running for the nearest exit at once.
- **Recover (RC):** After the dust settles, how do you get back to normal — and how do you communicate that to the people who were affected?

## Concept #1: The Maturity Tier Scale

**What it means:** The four Implementation Tiers are how NIST CSF 2.0 officially describes maturity — but they're meant to describe the rigor and consistency of the cybersecurity program as a whole, not a score for each individual category. In practice, most assessments (mine included) borrow that same 1-through-4 logic and apply it at a more granular level, scoring each category or subcategory on how mature and consistent the practice is — not whether it exists at all, but how reliable it is. That granular scoring approach is the industry-standard convention, even though it isn't an official NIST requirement.

- **Tier 1 (Partial):** Ad hoc, reactive, unformalized
- **Tier 2 (Risk-Informed):** Management-approved, but not consistent org-wide
- **Tier 3 (Repeatable):** Formally defined, policy-driven, routinely updated
- **Tier 4 (Adaptive):** Continuous, predictive, adjusts in real time

**A relatable example:** Think about how a household handles fire safety. Tier 1 is having a fire extinguisher somewhere in the house because someone bought one once. Tier 2 is everyone knowing where it is and roughly how to use it. Tier 3 is a written, practiced fire escape plan the whole family reviews annually. Tier 4 is a smart smoke detector system that alerts the fire department automatically and adjusts based on real-time conditions. Same underlying goal — very different levels of reliability when it actually matters.

**Where a GRC analyst gets this info day-to-day:** This isn't guessed from a spreadsheet. It comes from stakeholder interviews (asking IT and compliance leads how something actually works in practice, not just what the policy says), reviewing existing documentation (policies, procedures, past audit findings), and sometimes just observing — does the "formal process" actually get followed, or does everyone quietly work around it?

**Why it matters to the job:** This is the number that everything else in the assessment depends on. Score too generously and leadership underestimates real exposure. Score too harshly and you lose credibility with the teams you scored. Getting an honest, defensible tier rating is one of the most judgment-heavy parts of the whole exercise.

## Concept #2: The Critical Asset Inventory

**What it means:** A catalogue of what actually needs protecting — systems, data, and who's responsible for each one — before you can meaningfully assess risk against any of it.

**A relatable example:** It's the same logic as walking through your house before buying insurance. You don't just say "I own stuff." You list the TV, the laptop, the jewelry — what each thing is worth, and where it lives. You can't get a useful insurance policy, or know what to protect first in a fire, without that list.

**Where a GRC analyst gets this info day-to-day:** Vendor contracts and SaaS subscription lists, IT's asset management tools (if one exists — often it doesn't, and that's its own finding), conversations with department heads about what systems they actually rely on day-to-day, and sometimes just noticing what's not on any official list but is clearly in use anyway (shadow IT is extremely common).

**Why it matters to the job:** You genuinely cannot assess risk against something nobody told you exists. A huge part of early-stage GRC work is just building an accurate picture of reality — which is often messier and less documented than anyone expects.

## Concept #3: The Risk Register

**What it means:** A structured list translating technical gaps into business terms — what could happen, how likely it is, how bad it would be, and what reduces that risk.

**A relatable example:** This is the same mental math as deciding whether to drive without car insurance. Likelihood: how often do accidents actually happen? Impact: what would it cost you if one did? Multiply those together and you get a severity level that tells you whether "I'll just risk it" is a reasonable bet or a terrible one. A risk register does that same math, just for a business instead of a driver.

**Where a GRC analyst gets this info day-to-day:** This is where the gap matrix gets reframed for people who don't think in tiers. You pull from the gap scores, cross-reference them with what a breach or failure would actually cost the business (client trust, regulatory fines, downtime), and often validate severity ratings with finance or legal counterparts who understand dollar impact better than technical teams do.

**Why it matters to the job:** Executives don't approve budget because "DE.CM is Tier 1." They approve budget because "we have no way of detecting an intrusion in progress, and that's a critical severity risk." The risk register is the translation layer, and writing it well is a huge part of what makes a GRC professional valuable versus purely technical staff.

## Concept #4: The Remediation Roadmap

**What it means:** A phased, sequenced plan that turns identified gaps into action — what gets fixed first, what comes next, and why that order makes sense.

**A relatable example:** It's triage in an ER, not a to-do list. You don't fix the sprained ankle before you stop the bleeding, even if the ankle was reported first. Governance and oversight gaps get addressed before you spend money on detection tools, because without clear ownership, even good tools tend to go unmanaged.

**Where a GRC analyst gets this info day-to-day:** Roadmapping usually happens in collaboration — GRC proposes the sequence based on risk severity and dependency (you can't train staff on an incident response plan that doesn't exist yet), then IT and leadership weigh in on feasibility, cost, and timeline. It's rarely a solo document; it's negotiated.

**Why it matters to the job:** A list of problems with no plan just creates anxiety. The roadmap is what turns the assessment from "here's everything wrong" into "here's exactly what we do, in what order, and what it buys us." That's the difference between an assessment that gets filed away and one that actually drives change.

## How It All Fits Together

Each piece feeds the next one: asset inventory tells you what matters → the gap matrix tells you where the organization is weak relative to what matters → the risk register translates those weaknesses into business risk leadership actually has to care about → the roadmap turns that risk into a sequenced, fundable plan.

Skip any one of those steps and the assessment stops being useful. A gap matrix without a risk register is just a scorecard — nobody outside of GRC will read it. A risk register without a roadmap is just a list of worries. The whole point of the exercise is to walk someone from "here's our current state" to "here's exactly what we do about it, in what order, and why."

That, more than any individual template, is the actual skill: taking a framework with 22 categories and turning it into something a non-technical executive can approve in one meeting.

---
title: "Inside the NIST CSF Assessment: Assessment Types, Scoring, and the Actual Workflow"
date: 2026-08-24
categories: [GRC & Frameworks]
tags: [nist csf, gap assessment, scoring, grc]
excerpt: "Self vs. third-party assessments, how 106 subcategory scores roll up into one number, and the eight-step workflow behind it all."
---

In one of my last posts, I walked through the four building blocks of the gap assessment I built for Meridian Wealth Partners — the asset inventory, the maturity tiers, the risk register, and the roadmap. That post answered *what* goes into an assessment. This one is about *how* the process actually runs, start to finish, and a few structural details I glossed over the first time.

## First: What Kind of Assessment Was I Actually Doing?

There are two flavors of NIST CSF assessment, and the difference matters more than it sounds like it should.

**Self-assessments** are run internally, by the organization's own security, risk, or IT teams. They're the most common starting point — lower cost, faster to run, usually done annually with more frequent check-ins on high-risk areas. The catch: internal teams can (understandably, not maliciously) rate their own practices a little more generously than an outsider would.

**Third-party assessments** are conducted by an independent external assessor. They cost more and take longer, but they're often required by regulators, partners, or clients who need assurance that isn't just self-reported. The output is a formal report with validated findings, not just an internal scorecard.

The Meridian assessment I built was a self-assessment — which is actually the realistic starting point for most organizations. Most companies don't go straight to hiring an external assessor; they build internal maturity first, then bring in a third party later to validate it or satisfy a regulator's requirement. Knowing which type you're building matters, because it changes how much weight the findings can carry with an outside audience like a board or a regulator.

## The Scoring Pipeline: How a Single Answer Becomes a Program-Wide Score

This is the part I underexplained last time. NIST CSF 2.0 has six functions, 22 categories, and — underneath those — 106 subcategories. Each subcategory is a specific, granular outcome (something like "physical devices are inventoried" or "incident response plans are tested"). The scoring works from the ground up:

1. **Score each subcategory.** Every one of the 106 gets rated 0–4, where 0 means the outcome isn't addressed at all and 4 means it's fully achieved and continuously improved.
2. **Aggregate to category scores.** The subcategory scores under each of the 22 categories get combined into a category-level maturity score.
3. **Aggregate to function scores.** Category scores roll up into a score for each of the six functions — Govern, Identify, Protect, Detect, Respond, Recover.
4. **Calculate the overall score.** The six function scores combine into one overall program maturity score.
5. **Compare against the Target Profile.** Every level — subcategory, category, function, and overall — gets measured against where the organization actually wants to be, and that's where the gaps come from.

Here's roughly what that looks like laid out as a scorecard, using illustrative numbers similar to what I built for Meridian:

| Function | Current Score | Target Score | Gap | Priority |
|---|---|---|---|---|
| Govern (GV) | 1.8 | 3.0 | -1.2 | High |
| Identify (ID) | 2.5 | 3.0 | -0.5 | Medium |
| Protect (PR) | 2.2 | 3.0 | -0.8 | High |
| Detect (DE) | 1.5 | 3.0 | -1.5 | Critical |
| Respond (RS) | 2.0 | 3.0 | -1.0 | High |
| Recover (RC) | 1.7 | 3.0 | -1.3 | High |

What jumps out immediately: Detect has both the lowest score and the largest gap. That's not a coincidence — it's exactly the kind of pattern a scorecard is supposed to surface at a glance, without anyone having to read all 106 subcategory scores to find the problem.

One thing worth being upfront about: CSF 2.0 doesn't actually mandate this specific scoring approach. There's no official NIST scoring methodology — this 0-to-4, roll-it-up pipeline is just the most widely used convention in practice, not a rule handed down by the framework itself. That distinction matters if you're ever asked "where does this scoring method come from?" The honest answer is: consensus practice, not official mandate.

## The Actual Workflow: Eight Steps From Blank Page to Action Plan

This is the part that felt most like "real job" work once I actually walked through it:

1. **Define scope and objectives.** Is this the whole organization, one business unit, one risk area? For Meridian, I scoped it to core technology, network infrastructure, and critical SaaS vendors — and explicitly excluded active penetration testing.
2. **Assemble the assessment team.** No single person can accurately assess all six functions. A real assessment pulls in IT, security, operations, legal, and leadership — which tracks with everything I've learned about GRC not being a solo sport.
3. **Establish the Target Profile.** Decide what "good" looks like for this specific organization, based on its risk tolerance, business priorities, and regulatory environment. A wealth management firm's target profile is going to look different from a five-person startup's.
4. **Distribute assessment questionnaires.** Map questions to the actual 106 subcategories and get them in front of the right control owners — and ask about what actually happens, not what the policy document says should happen.
5. **Gather evidence.** This is where the questionnaire answers get tested against reality — supporting documentation, technical interviews, actually watching how a process runs day to day.
6. **Score and compile results.** Roll everything up into the Current Profile using the pipeline above.
7. **Conduct gap analysis.** Compare Current against Target, and flag where the gaps are both largest and most tied to business risk — not just the easiest ones to fix.
8. **Develop an action plan.** This is the roadmap piece from my last post — a prioritized plan with owners, timelines, and risk alignment attached to specific subcategories.

Reading that list back, it's basically a more granular version of the four building blocks I already wrote about — the workflow is just the process that produces them, step by step, with real people attached to each stage instead of a document appearing out of thin air.

## Why This Structure Matters More Than It Looks

None of this is bureaucracy for its own sake. The reason CSF assessments follow this exact shape — self vs. third-party, subcategory-up scoring, an eight-step process with defined ownership at each stage — is that cybersecurity risk decisions need to survive scrutiny. A board approving a budget, a regulator reviewing a program, a client asking hard questions in due diligence — all of them need to trust that a "Tier 1, Critical Priority" rating on Detect isn't just someone's gut feeling. It's traceable, all the way down to a specific subcategory and a specific piece of evidence.

That traceability is, I think, the real skill being tested when you build one of these. Not memorizing 106 subcategories — knowing how to build a process rigorous enough that someone outside the room can trust the answer at the end of it.

---
title: "I Finally Understand tcpdump: A Beginner's Notes from My First Packet Capture Lab"
date: 2026-09-17
categories: [Networking]
tags: [tcpdump, packet capture, linux, network security]
excerpt: "Interfaces, verbose captures, saving pcap files and reading raw bytes: tcpdump explained one flag at a time."
---

If you'd told me a month ago that I'd spend an afternoon happily staring at hexadecimal dumps of network traffic, I would've laughed. But here we are. I just wrapped up a hands-on lab where I used tcpdump to capture and analyze live network traffic on a Linux machine, and I want to walk through what I learned — not as an expert, but as someone on a similar learning curve.

## Why This Matters (Even If You're Not "Into Networking")

Here's the thing that clicked for me: every single thing your computer does online — loading a webpage, sending an email, streaming a video — is really just a conversation happening in tiny data packets flying back and forth. As a security analyst (or someone learning to be one), tcpdump is basically how you eavesdrop on that conversation. Not in a creepy way — in a "something looks off, let's see what's actually happening on the wire" way.

Think of it like being a detective who can tap into the phone lines of a building. You're not reading everyone's diary; you're watching who's talking to whom, how often, and whether anything looks suspicious.

## Step 1: Finding the "Phone Lines" (Network Interfaces)

Before you can listen to any traffic, you need to know which "line" to tap into. That's what a network interface is — think of it as a specific door your computer's data walks through to get to the internet.

I ran:

```bash
sudo ifconfig
```

And got a list back with names like `eth0` (the actual Ethernet connection — the "real" door) and `lo` (loopback — basically your computer talking to itself, like leaving yourself a voicemail).

**Relatable moment:** I initially thought I needed to pick the "most important-sounding" interface. Nope — it's usually just the one with the `eth` prefix that's actually connected to the outside world.

There's also a tcpdump-specific way to check:

```bash
sudo tcpdump -D
```

Handy if a system doesn't even have `ifconfig` installed.

## Step 2: Actually Watching Traffic Go By

This is where it started feeling like a movie hacking scene (in a good way). I ran:

```bash
sudo tcpdump -i eth0 -v -c5
```

Breaking this down like I had to for myself:

- `-i eth0` → "listen on this specific door"
- `-v` → "verbose," meaning give me the juicy details, not just the headline
- `-c5` → "only grab 5 packets, then stop" (very important — without this, it just keeps running forever and your terminal turns into a waterfall of text)

The output looked like alphabet soup at first. Timestamps, IP addresses, weird terms like `flags [DF]` and `proto TCP (6)`. But once I slowed down, it started making sense:

- The **timestamp** is just... the time.
- The **IP details** in verbose mode (TTL, offset, flags) are like the packet's shipping label — how long it's allowed to travel, whether it got split up, etc.
- The **source > destination** line is literally just "who's sending this to whom," complete with port numbers, like an apartment number on an address.
- **TCP flags** like `[P.]` tell you the intent of the packet — is it pushing new data? Acknowledging something it received? It's basically packet body language.

**Relatable analogy:** if a regular tcpdump line is a text message, verbose mode is that text message plus the full delivery receipt, timestamp, and read status.

## Step 3: Actually Saving the Evidence

Watching traffic live is fun, but as an analyst you often need to save it to look at later — like recording a phone call instead of just listening in real time. That's what a pcap file (packet capture file) is for.

```bash
sudo tcpdump -i eth0 -nn -c9 port 80 -w capture.pcap &
```

A few things I had to remind myself about here:

- `port 80` filters to just web traffic (HTTP), so I'm not drowning in irrelevant noise.
- `-nn` stops tcpdump from resolving IP addresses and ports into friendly names. At first this felt backwards — why not make it readable? But it actually makes sense from a security angle: if you're investigating something sketchy, you don't want your system pinging DNS servers and potentially tipping off whoever you're watching. Sneaky, but logical.
- The `&` at the end runs it in the background, like starting a recording and then going about your business.

Then I used `curl opensource.google.com` just to generate some actual web traffic to capture — which felt oddly satisfying, like setting a trap and then walking into it myself on purpose.

## Step 4: Reading the Evidence Back

Once the capture was saved, I could read it back anytime with:

```bash
sudo tcpdump -nn -r capture.pcap -v
```

`-r` reads from the file instead of live traffic — same detective work, just after the fact.

And then there's the really cool one:

```bash
sudo tcpdump -nn -r capture.pcap -X
```

ASCII is basically the dictionary computers use to turn numbers into letters. When you run tcpdump with `-X`, it shows you the raw hex and the ASCII translation of the packet contents side by side. This is where security work gets real — this is how analysts look for hidden patterns, malware signatures, or weird data smuggled inside "normal-looking" traffic. It looked intimidating at first (rows and rows of hex codes), but I realized you're not meant to read every byte — you're scanning for anomalies, like a proofreader scanning for typos rather than reading every word for meaning.

## The Biggest Lesson for Me

The flags are simpler than they look once you stop trying to memorize them and instead think about what question each one answers:

| Flag | Question it answers |
|---|---|
| `-i` | Which interface? |
| `-c` | How many packets? |
| `-v` | How much detail? |
| `-w` | Save to a file? |
| `-r` | Read from a file? |
| `-nn` | Skip the name lookups? |
| `-X` | Show me the raw bytes? |

Once I framed it that way instead of trying to brute-force memorize syntax, everything got a lot less scary.

## Final Thoughts

I went into this lab expecting to feel out of my depth (and honestly, for the first 10 minutes, I was). But tcpdump ended up feeling less like arcane hacker magic and more like learning to read a very specific, very literal language — one packet at a time. If you're starting out too: don't rush past the confusing parts. Run the command, stare at the weird output, and ask "what is this one piece telling me?" before moving to the next line. It adds up faster than you'd think.

Next up for me: digging into that sample pcap file sitting in the home directory and actually answering questions about real captured traffic. Wish me luck.

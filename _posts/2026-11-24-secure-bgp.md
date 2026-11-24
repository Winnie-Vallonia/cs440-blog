---
layout: post
title: "Passive Data-Plane Telemetry to Mitigate Long-Distance BGP Hijacks"
date: 2026-11-24
paper_authors: "Satadal Sengupta, Hyojoon Kim, Daniel Jubas, Maria Apostolaki, Jennifer Rexford"
paper_venue: "NINeS 2026"
paper_url: "https://doi.org/10.4230/OASIcs.NINeS.2026.14"
week: 9
tags: [bgp, hijacks, routing-security, data-plane, programmable-switches]
---

## Key Idea

An attacker can hide a hijack in BGP, but if they route your traffic through another country, they can't hide the extra distance it travels.
HiDe runs on a programmable switch at the network edge, passively tracks the minimum RTT of TCP traffic to each /24 prefix, and blocks the prefix when that RTT suddenly jumps past a speed-of-light bound.
In real hijack tests it caught attacks within half a second, with a false alarm rate under 0.012% on campus traffic.

## Critique

Using physics as the signal is convincing because the attacker really can't fake it, and the ethically run hijacks made the results feel real.
But it only works when the detour is far, so US traffic routed through the UK gets caught while traffic through Canada might not.
It also only sees TCP and skips noisy prefixes like cellular and WiFi, which leaves out a lot of real traffic.

## Connections

Goldberg et al. (the background paper) showed even S-BGP can be gamed and finding the best attack is NP-hard, so HiDe skips that fight and watches the data plane instead.
It also reminded me of [No Signal to Rule Them All]({{ site.baseurl }}{% post_url 2026-10-14-no-signal %}), where plain RTT held up as well as fancier in-network signals.

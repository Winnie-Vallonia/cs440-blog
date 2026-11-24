---
layout: post
title: "How Secure Are Secure Interdomain Routing Protocols?"
date: 2026-11-24
paper_authors: "Sharon Goldberg, Michael Schapira, Peter Hummon, Jennifer Rexford"
paper_venue: "SIGCOMM 2010"
paper_url: "https://doi.org/10.1145/1851182.1851195"
week: 9
tags: [bgp, routing-security, interdomain-routing, hijacks]
---

## Key Idea

Secure BGP variants like soBGP and S-BGP stop an attacker from lying about paths. But how much does that actually limit them? The authors simulate one bad AS trying to pull in traffic on a real AS map from CAIDA. The obvious attack is announcing the shortest path the protocol won't flag, to every neighbor. Even against S-BGP, that grabs at least 10% of the internet more than 10% of the time.
And the obvious attack isn't even the best one. Announcing a longer path, exporting to fewer neighbors, or tricking loop detection can pull in more. Finding the best attack is NP-hard.

## Critique

Everything rests on every AS following the textbook business rules (Gao-Rexford), and real policies are messier. The weird counterexamples come from real topologies, but the authors admit they were hard to find, so I can't tell how common they are.
What stuck with me is that defensive filtering of stubs protects about as well as S-BGP, but it depends on providers doing unpaid work to protect everyone else.

## Connections

The big takeaway is that secure BGP limits which paths you announce, not who you announce them to. Sengupta et al. stop trusting the control plane completely. HiDe watches for propagation delay jumping in the data plane, which an attacker can't hide. Rexford is on both papers, 16 years apart.

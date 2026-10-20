---
layout: post
title: "Waiting for QUIC: Passive Measurements to Understand QUIC Deployments"
date: 2026-10-19
paper_authors: "Jonas Mücke, Marcin Nawrocki, Raphael Hiesgen, Patrick Sattler, Johannes Zirngibl, Georg Carle, Jan Luxemburk, Thomas C. Schmidt, Matthias Wählisch"
paper_venue: "CoNEXT 2025"
paper_url: "https://doi.org/10.1145/3768988"
week: 4
tags: [quic, network-measurement, hypergiants]
---

## Key Idea

Big providers like Google and Meta don't say how they've set up QUIC, and scanning them directly is noisy and sometimes breaks ISP rules.
So the authors just listen instead, using backscatter at the UCSD network telescope, which is what servers send back when attackers spoof the telescope's addresses, sampled one month a year from 2021 to 2025.
Honestly the wild part is how much leaks from the few unencrypted handshake fields: retransmission timing, packet sizes, connection ID structure, and for Meta, even how many layer 7 load balancers sit behind each cluster.

## Critique

The validation won me over, since they didn't just trust the telescope and backed it up with CESNET flow records and their own probes.
Still, everything hinges on who attackers happen to target, which feels like a shaky thing to build a measurement on.
The telescope is also IPv4 only, so as more traffic moves to IPv6, more of these deployments just disappear from view.

## Connections

It's kind of ironic next to Langley et al., who said encrypting QUIC would keep middleboxes from latching onto its bits.
The one field they left visible for load balancers, the connection ID, ends up being what gives the whole infrastructure away.

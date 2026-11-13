---
layout: post
title: "Is Starlink Actually as Good as It Claims"
date: 2026-11-13
paper_authors: "François Michel, Martino Trevisan, Danilo Giordano, Olivier Bonaventure"
paper_venue: "IMC 2022"
paper_url: "https://doi.org/10.1145/3517745.3561416"
week: 8
tags: [starlink, satellite-networks, network-measurement]
---

## Key Idea

Starlink promised satellite internet with about 20 ms delay, and nobody had really checked. The authors put a dish on a campus in Belgium and measured it for months. They compared it to old-style satellite internet and a wired connection.
What surprised me is how close it gets to wired. Median ping was about 50 ms, download was 178 Mbit/s, and web pages loaded in about 2 seconds. Old satellite took almost 11.
They also used QUIC, since encryption stops the speed-up boxes old satellite providers rely on from hiding the real network.

## Critique

It's one dish in one spot in Belgium, so I don't know how far these numbers generalize. The old satellite plan was only tested for two weeks, while Starlink got months. They also only loaded landing pages.
I wish they'd explained the loss better. Even with almost no load, about 0.4% of packets were lost, and they couldn't say why.

## Connections

This connects to LeoCC (Lai et al.). This paper points out that Cubic treats every loss as congestion, and that Starlink still drops packets when the link is nearly idle.
LeoCC finds a cause, satellites switching connections every 15 seconds, and builds a fix around it.

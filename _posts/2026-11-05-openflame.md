---
layout: post
title: "OpenFLAME: A Federated Spatial Naming Infrastructure"
date: 2026-11-05
paper_authors: "Sagar Bharadwaj, Ziyong Ma, Ivan Liang, Michael Farb, Anthony Rowe, Srinivasan Seshan"
paper_venue: "NINeS 2026"
paper_url: "https://doi.org/10.4230/OASIcs.NINeS.2026.20"
week: 7
tags: [naming, dns, spatial-computing, federated-systems]
---

## Key Idea

Centralized maps can't cover indoor spaces. Those maps are private, and surveying them is too much work for one company. OpenFLAME lets each owner run their own map server instead. To find the right ones, an app turns its location into grid cells, turns those into DNS names, and looks them up. DNS caching does most of the work.

## Critique

What surprised me is how upfront the evaluation is about the cost. Splitting a city map into pieces made routes about 12% longer at the median, and queries took about twice as long. The paper also admits discovery has no ranking, so a spot covered by many maps could return a big, unordered list. I wish they tested how bad that gets.

## Connections

Akamai DNS shows what it takes to run naming at huge scale, with anycast, attack filters, and backup servers. OpenFLAME bets that small owners can get by with a plain server, since discovery is mostly cached reads. The big twist is overlap. Normal DNS follows one nameserver because they all hold copies, but overlapping map zones hold different maps, so a lookup has to follow every branch.

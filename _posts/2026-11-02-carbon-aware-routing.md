---
layout: post
title: "Exploring the Benefits of Carbon-Aware Routing"
date: 2026-11-02
paper_authors: "Sawsan El-Zahr, Paul Gunning, Noa Zilberman"
paper_venue: "CoNEXT 2023"
paper_url: "https://doi.org/10.1145/3629165"
week: 6
tags: [green-networking, carbon-aware-routing, traffic-engineering, ospf]
---

## Key Idea

This paper asks whether routers can cut carbon by sending traffic through regions where the grid is cleaner at that hour. The best link cost mixes grid carbon intensity with each router's extra power per unit of traffic. Their CATE algorithm goes further and turns off lightly used links when that saves carbon. Routing alone barely helps (3.71% on BT), but CATE reaches 17.96% in the daytime.

## Critique

I liked that they report the bad results too. Evening traffic only saves about 1.8%, because users pull from a cache one or two hops away and the links are busy. Central nodes like London can't be avoided either. But the routers are Arista data center switches standing in for the real BT and GEANT gear, and it's all simulation with no failure handling.

## Connections

Barroso and Hölzle showed that servers at 10 to 50 percent load still burn about half their peak power. Routers have the same problem. When idle power is most of the bill, moving traffic around saves little, so the real fix is hardware with lower idle power.

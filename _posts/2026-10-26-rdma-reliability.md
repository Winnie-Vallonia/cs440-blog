---
layout: post
title: "Revisiting RDMA Reliability for Lossy Fabrics"
date: 2026-10-26
paper_authors: "Wenxue Li, Xiangzhou Liu, Yunxuan Zhang, et al."
paper_venue: "SIGCOMM 2025"
paper_url: "https://doi.org/10.1145/3718958.3750480"
week: 5
tags: [datacenter-networking, rdma, transport-protocols, reliability]
---

## Key Idea

Lossy RDMA NICs still fail in two ways, mistaking reordering for loss and stalling on timeouts when a retransmission drops again. DCP fixes both by having the switch chop the payload off any packet it would drop and rush the header back, so the sender knows exactly which packet to resend. The trimming is borrowed from earlier work, so the real contribution is the NIC, which writes packets to memory in any order and counts arrivals instead of keeping a bitmap.

## Critique

I liked that Section 6.3 owns up to a weak spot: DCP alone has the worst tail latency under heavy incast, because every trimmed header sets off another retransmission. But that means the "lossless" control plane only works with DCQCN running underneath. It also hasn't been tested on real switch hardware, since regular switches can't trim packets yet.

## Connections

DCQCN spent 2015 making lossless Ethernet bearable by keeping PFC from firing, while DCP throws PFC out and still borrows DCQCN to keep itself in check. Next to dcSim from last week, the two look like mirror images: dcSim's tiny probe prevents loss, and DCP's tiny header reports it.

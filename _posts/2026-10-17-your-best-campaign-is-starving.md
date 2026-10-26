---
title: "Your Best Campaign Is the One Being Starved"
date: 2026-10-17
tag: Budget Allocation
excerpt: "In a new e-commerce account, the strongest campaign was capped by budget while a weaker one couldn't spend what it had. Same account, opposite problems."
---

I audited a newly onboarded e-commerce account in Bangladesh. The structure looked busy: 22 Demand Gen and Performance Max campaigns and no Search at all. The bigger story was in how budget was distributed.

## Two campaigns, opposite problems

**Campaign A** was returning roughly **8–9x** its spend in revenue and was limited by budget every day. Demand existed; the account just wouldn't let it spend.

**Campaign B** had budget it wasn't using. Its target cost per acquisition was set below anything the auction could deliver, so Google's bidding held back. Unused budget there doesn't move anywhere useful.

The highest-return campaign was capped. A weaker one was sitting on unspent money.

## The measurement layer underneath

Before moving any budget, I checked whether those ROAS numbers could be trusted:

- Two separate Purchase actions were both set as **primary**, on different domains, with different lookback windows. That can double-count, and it confuses bidding about what a sale is.
- A "begin checkout" tag was misfiring.

## Recommended order

1. Make one Purchase action primary; set the other to secondary
2. Fix the checkout tag
3. Shift budget toward the capped campaign
4. Set the under-delivering campaign's target to something the auction can meet, or pause it
5. Then test adding Search for high-intent demand

## What I didn't cover

Creatives, audiences, placements, product feed, and landing pages were outside that first pass. I listed them as open rather than implying the audit was complete.

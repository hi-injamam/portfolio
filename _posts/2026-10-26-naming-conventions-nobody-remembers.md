---
title: "Naming Conventions Nobody Has to Remember"
date: 2026-10-26
tag: Automation
excerpt: "Every team has a naming convention document. Almost none have consistent names. A small script turned the document into a rule."
---

Inconsistent campaign names look like a tidiness problem. They're actually a data problem. Any report that reads market, objective, or funnel stage out of a campaign name silently breaks when names drift.

I saw this first-hand: a naming collision between a budget and a bid strategy once led to an analytical error in an audit. The names looked meaningful, so I trusted them.

## What the script does

A scheduled Google Ads Script that:

- reads the naming pattern from a Google Sheet, so rules change without touching code
- checks every campaign and ad group name against it
- writes violations back to the sheet with the account and owner
- sends a short summary instead of interrupting anyone

## What it deliberately doesn't do

It doesn't rename anything. Renaming live campaigns automatically breaks historical reporting, which is the problem it exists to prevent. It reports; people fix.

## The principle

A document is a request. A check that runs every day is a rule.

*Reference: [Google Ads Scripts documentation](https://developers.google.com/google-ads/scripts).*

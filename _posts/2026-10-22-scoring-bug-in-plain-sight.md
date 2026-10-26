---
title: "The Scoring Bug Hiding in Plain Sight"
date: 2026-10-22
tag: Creative
excerpt: "A video ad auditor had been grading against the wrong total. Fixing it led to a stricter rule: if a check can't be verified, it doesn't get to pass."
---

I built a video ad auditor based on Google's ABCD framework (Attract, Brand, Connect, Direct). Version 3.1 started as a feature update and turned into a correctness review.

## Bug 1: the denominator was wrong

The four pillars were being scored out of **29** points. The framework's checks actually totalled **23**. Every score built on that was off, consistently and silently. Because the error was uniform, nothing looked wrong.

## Bug 2: numbers sent as text

Each exported report sends usage data to GA4. Numeric fields like scores were being sent as quoted strings. GA4 accepted them without complaint and then couldn't aggregate them. No error, just reports that didn't add up.

Rule since then: numbers go as numbers, and the version label goes as a string so "3.1" doesn't get coerced.

## The principle that came out of it

Some checks can't be verified from a video file alone, such as technical delivery specs. The old version quietly passed them.

Now every check has three states: **pass**, **fail**, or **not verifiable**. Silence is not a pass.

## What it deliberately doesn't do

It scores craft, not predicted performance. Published research multipliers are averages across many ads; applying them to one asset as a forecast would be false precision. A separate impact index runs alongside the main score but never merges with it.

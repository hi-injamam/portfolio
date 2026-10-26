---
title: "Catching Disapprovals, Part 2: What Changed When It Got Real"
date: 2026-10-20
tag: Tools
excerpt: "The policy pre-check idea became a four-tab internal tool. The interesting parts are the things it refuses to do."
---

I wrote earlier about using the Google Ads API's `validate_only` dry-run to catch policy problems before ads go live ([API docs](https://developers.google.com/google-ads/api/samples/validate-ad)). This is what happened when the idea became a working tool.

## What it checks now

- **Image creatives:** batch visual policy review
- **Text assets:** bulk checking at the asset level
- **Landing pages:** destination scanning
- **Deep links:** Android App Link validation

## Design decisions that mattered

**Asset level, not ad level.** App install campaigns assemble ads from individual assets, so one bad headline can sink a whole set. Checking the full ad hides which piece is the problem.

**Fixable vs. structural.** Some destinations can be fixed with a wording change. Others are fundamentally ineligible. The tool refuses to suggest cosmetic workarounds for the second kind. Helping someone disguise an ineligible destination isn't help.

**Policy links come from a fixed, hand-verified table.** Model-generated policy URLs proved unreliable, so every finding maps to a manually checked source instead.

**Guidance, not a guarantee.** Google's review runs the moment an ad is submitted. The tool reduces risk; it can't promise approval, and it says so in the interface.

## Validate before building more

Before scaling it into automated workflows, I built a scoresheet to test the catch rate against ads already approved or rejected. *Results are still pending real-world testing.* Building automation on an untested accuracy rate would just scale the errors.

## Small engineering lessons

- Pulling JSON out of a model response by finding the first `{` and last `}` breaks when the surrounding text also contains braces. A depth-aware parser that ignores braces inside strings fixed it.
- Revoking a download link the instant a file download starts can kill the download. A short delay fixed it.

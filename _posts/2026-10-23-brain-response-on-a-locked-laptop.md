---
title: "Running a Brain-Response Model on a Locked-Down Laptop"
date: 2026-10-23
tag: R&D
excerpt: "No local installs allowed. A research model that predicts brain response to video. Everything ran in a browser notebook, and most of the work was dependency debugging."
---

My work laptop is managed: no new software, no local dev environment. I wanted to test Meta's TRIBE v2 research model, which predicts average brain response to video, as a creative research aid.

Everything ran in Google Colab, in the browser.

## What the notebook produces

A report with the video, audio, transcript, and predicted response on one synchronised timeline, response curves for visual, auditory and language regions, and surface maps of the brain. A second no-GPU notebook rebuilds the visuals from saved output without rerunning the model.

## Boundaries I set first

The model's licence is non-commercial. So it's research only: it never influences any creative score and never appears in client work. I set that before writing code, not after.

## The debugging, which was most of the work

- **Installing packages into a running session breaks things.** Restart the runtime after setup.
- **Pinned versions collide.** One library pins a specific version of another, and companion libraries must be pinned to match.
- **Hidden gated dependencies.** The model transcribes audio to words, which quietly loads a gated language model. Access approval is needed for something you never call directly.
- **Triplicated transcripts.** Word-level and sentence-level rows overlapped. Removing duplicates on start time and text fixed it.

## A visualisation lesson

Blue on a brain map means *below baseline*, not *switched off*. Without an explicit legend, people read it wrong every time.

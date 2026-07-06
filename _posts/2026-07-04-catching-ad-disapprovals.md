---
title: "Catching ad disapprovals before Google does"
date: 2026-07-04 09:00:00 +0600
tag: "Tooling"
excerpt: "Health-sector app campaigns get disapproved for reasons you only find out after launch. Here's how I'd build a pre-submission check that turns that guesswork into a verdict."
---

Some campaigns launch and run. Health-sector app campaigns launch and *wait* — because ads for anything touching health get held for editorial review, and a disapproval can arrive hours or days later, after the momentum's gone. By then you're rewriting a headline you thought was fine and relaunching from cold.

The obvious wish is to know the verdict *before* you submit. So I went looking for a way to do exactly that.

## You can't copy Google's judge — so don't try

The first instinct is to rebuild Google's flagging system: feed it the policies, mimic the classifier, predict the outcome. It's a dead end. Google's editorial engine pulls in signals you'll never see — account history, landing-page crawls, context — and it's proprietary. Any copy you build is a guess wearing a confident face.

The better realization: I don't need to *imitate* the judge. I can ask the real one a question without committing to the answer.

## Ask the real engine, quietly

Google's own API has a dry-run mode. You assemble the ad exactly as you would for launch, but flag the request as validation-only. Google runs its editorial check as if it were live, then throws the result away instead of creating anything. Clean check, empty response. A problem, and it hands back the specific policy topics that tripped — the authentic verdict, from the authentic engine, with nothing published.

That's the heart of it. Not a mimic. The real thing, asked in a way that costs nothing.

It has limits worth being honest about: it catches the automated editorial layer — which is exactly the layer that fires those fast auto-disapprovals — but not trademark tangles or anything that lands in human review. It handles the predictable 80%, not the judgment calls. That's fine. The predictable 80% is what wastes the most time.

## Two speeds, one workflow

The dry-run check needs API plumbing, so it isn't instant. That's the wrong feel for someone drafting copy who wants a reaction *now*. So the design runs at two speeds.

First, a fast local pass: simple rules for the obvious triggers — prohibited terms, unapproved health claims, "miracle cure" and guaranteed-results language, the before-and-after imagery cues — plus a language model scoring each asset against the published policy rubric. Never authoritative, always instant, always explainable. It catches most problems while you're still typing.

Then, right before launch, the authoritative gate: the real dry-run check runs as the final word. Fast feedback while you work, real verdict before you commit. Neither trying to be the other.

## The hard part isn't the code

The architecture is clean. The obstacle, as usual, is access: the real check needs provisioned API credentials, and getting those set up is the actual project — not the logic that follows. The code is a weekend; the permissions are the mountain.

There's a quiet bonus hiding in the same tool, though. It answers a question that's otherwise unanswerable from the outside: *are our disapprovals coming from the words or the images?* Run a batch of historically rejected assets through the dry-run check and watch what the editorial layer flags. Text problems surface immediately. A suspicious silence on rejected creative points the finger at imagery or manual review instead. You stop guessing which lever to pull.

## Why this shape of thinking matters

The reflex when a system frustrates you is to rebuild it. The better move is usually to find the seam where it already tells you what you need — and use that. Google was never going to hand over its classifier. But it left a door open where you can ask, honestly, "would this pass?" and get a straight answer. The whole tool is just standing in that doorway on purpose.

It's still a plan more than a product — the access hurdle is real and it's next. But the shape is right, and the shape is the part worth getting right first.

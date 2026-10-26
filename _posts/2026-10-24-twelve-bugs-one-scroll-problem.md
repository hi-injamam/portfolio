---
title: "Twelve Bugs Behind One Scroll Problem"
date: 2026-10-24
tag: Web
excerpt: "A scroll-driven page stuttered, jumped, and left sections blank. There wasn't one bug. There were twelve, and four could break scrolling on their own."
---

I built a scroll-animated page for this site using a smooth-scroll library and GSAP ScrollTrigger. It misbehaved in several ways at once.

## The four that mattered most

**1. Two smooth-scroll engines.** CSS `scroll-behavior: smooth` and the JavaScript smooth-scroll library were both trying to control the same scroll position. Result: stutter and overshoot. Removing the CSS rule fixed it.

**2. `gsap.from()` with scrub.** A `from` tween re-records its starting values on every refresh, and the page was refreshing on every resize event. After one window resize, elements could get stuck invisible. This was why sections looked blank.

**3. Locked section heights.** `height: 100vh` with hidden overflow clipped content and went stale whenever the viewport changed, so scroll trigger points stopped matching the page. `min-height: 100svh` fixed it.

**4. Scaling an entire section.** Animating the scale of a full-height section corrupted ScrollTrigger's measurements for everything inside it.

## The others, briefly

Animations on the first section that started before scroll position zero, two animations writing the same property at once, a load listener registered after load could have fired, and a modal locking scroll without telling the scroll library.

## The resilience fix

If any one library failed to load from its CDN, the whole script died. Now each is optional: if the smooth-scroll library is blocked, the page falls back to native scroll and everything still animates. That matters on managed networks where some CDNs are blocked.

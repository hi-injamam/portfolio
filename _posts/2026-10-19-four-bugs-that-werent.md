---
title: "Four Urgent Bugs That Weren't Bugs"
date: 2026-10-19
tag: GA4 & Audiences
excerpt: "A client escalated four audience problems as platform failures. Each one was a setting, a threshold, or a rule working exactly as designed."
---

An app advertiser sent four issues marked urgent, asking for an immediate fix. Before drafting a reply, I checked each against current documentation. None was a platform bug, and that changed the reply from "we'll escalate" to "here's what to change."

## 1. Combined audience won't attach to an app engagement campaign

App engagement campaigns only accept app-user segments. A combined audience that includes any web-based segment won't attach.

## 2. YouTube viewer audience can't be created

Linking the YouTube channel is necessary but not enough. The link needs permission for data segments, and the segment needs to reach a minimum number of viewers before it can be used in campaigns.

## 3. GA4 shows hundreds of thousands of users; Google Ads shows zero

Some gap is normal, because Google Ads only counts the remarketable portion. A flat **zero** usually means one of:

- Google Signals is off
- Ads personalisation is disabled on the GA4–Ads link
- Consent mode is sending the ad-related consent signals as denied

## 4. "Greater than" audience condition never populates

"Greater than" works on numeric values like event counts. Applied to a text field, nothing can match. GA4 audiences also fill going forward from creation, so new ones always start near zero.

## The lesson

"Urgent platform bug" is usually a configuration question. Diagnosing first means the client gets a fix the same day instead of waiting on a support ticket that would be closed as working as intended.

*Thresholds and setting names change. Check current Google Ads and GA4 help docs before applying.*

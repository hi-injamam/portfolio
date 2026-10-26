---
title: "One Report Across Many Manager Accounts, No Data Warehouse"
date: 2026-10-21
tag: Reporting
excerpt: "Campaign data was scattered across several manager accounts. The fix was a small pipeline a single team could own, and one API setting that cost an afternoon."
---

Our team's campaigns sat across several manager accounts (MCCs), some ours and some belonging to outside agencies. Getting one view meant opening each one.

## The constraint

The team needed to own and run this without depending on a central data team. So I kept it deliberately small: no warehouse.

**Google Ads API (Python) → Google Sheets → Looker Studio**

One row per campaign per day, with the manager account, owner, account, campaign, spend, currency, and performance metrics. Looker Studio reads the sheet directly.

## The error that wasn't about permissions

Querying accounts under a manager account kept returning `USER_PERMISSION_DENIED`, even though access was definitely there.

The cause: the API needs to be told which manager account you're acting through. Setting `login_customer_id` to the manager account's ID before each query fixed it. For top-level accounts queried directly, it needed resetting to empty.

The error message points at permissions. The actual problem is context.

## Other things that cost time

- Creating OAuth credentials does not enable the APIs. The Google Ads API and Sheets API each need enabling separately.
- During the OAuth flow, a broken browser page on the local redirect is expected. The token prints in the terminal right after.
- Listing accessible customers only returns what the signed-in identity can see, so missing accounts usually mean a missing grant, not a bug.

*Verify current behaviour in the [Google Ads API docs](https://developers.google.com/google-ads/api/docs/concepts/api-structure); setup steps change between versions.*

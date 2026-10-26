---
title: "A 114% Conversion Rate Is Not Good News"
date: 2026-10-15
tag: Diagnostics
excerpt: "When a campaign reports more bookings than clicks, the account isn't performing. The measurement is broken, and every automated bid built on it is broken too."
---

During an audit of a hospitality account running 65 campaigns, one number stopped me: a campaign converting at **114%**.

More bookings than clicks is not possible for a single campaign measuring one action once. When a ratio breaks its own ceiling, the measurement is broken.

## What usually causes it

- The same conversion firing more than once per booking, for example on a confirmation-page reload
- Several conversion actions counting the same booking, all set as primary
- A counting setting of "every" where it should be "one"

## The other side of the same problem

The same account had a brand Search campaign with thousands of clicks and **zero** recorded bookings. People searching your hotel's name, clicking your ad, and never booking is implausible. Bookings were almost certainly happening and not being attributed.

So one campaign was over-credited and another under-credited, in the same account.

## Why it matters more than it looks

Smart Bidding optimises toward whatever conversions you report. Inflated campaigns get more budget. Under-credited campaigns get starved. The algorithm is doing its job correctly on bad data.

## The fix order

1. Audit every conversion action: which are primary, how they count, and whether they overlap
2. Test the booking path end to end in Tag Manager preview and GA4 DebugView
3. Only then evaluate campaign performance

Every other recommendation in that audit depended on fixing measurement first, so it went at the top of the action list.

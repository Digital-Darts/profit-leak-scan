# Example report

**The store and every number below are invented.** This file exists to show the shape, the tone and the level of explanation. Never quote these figures to anyone and never present them as a real result.

The invented numbers do add up, so the arithmetic can be checked against `method.md`. Keep yours checkable too.

Match this structure. Keep it this short. A store owner reads the first screen and the last screen, so the headline and the three fixes have to carry the report.

---

# Profit Leak Report

**Northbound Outdoors** · 1 June to 29 August 2026 · AUD
Spend in window: **$47,310** · Google-reported value: **$333,911** (7.06x), or **$303,555** ex GST (6.42x)

**Built on:** campaigns, search terms and Performance Max search terms from Google Ads, and orders and products from Shopify. Store brief answered. Shopify prices include GST, and so does Google's conversion value, checked against your orders. Conversion lag about 7 days, and the window ended 7 days before the exports were pulled. Cost per item assumed ex GST.

## Score: 65 / 100, leaking

| Section | Score |
|---|---|
| Brand leak | 10 / 25 |
| Profit | 22 / 25 |
| Wasted spend | 15 / 20 |
| Settings and tracking | 18 / 30 |

---

## The headline

**$11,300 of your $47,310 went to people searching for Northbound Outdoors by name.** That is 24% of the account, and $9,220 of it sits inside one Performance Max campaign that reports a 9.40x return.

---

## Brand leak

Nearly one in four dollars bought a click from someone who already knew who you were and typed your name into Google.

| Campaign | Total spend | Brand spend | Share |
|---|---|---|---|
| PMax - All Products | $26,400 | $9,220 | 35% |
| Shopping - Own Label | $9,800 | $1,460 | 15% |
| Shopping - Stocked Brands | $7,110 | $180 | 3% |
| Search - Generic | $4,000 | $440 | 11% |

Performance Max bids on your brand by default and records every one of those sales as a win. That is why it is your best-performing campaign on paper.

The Performance Max figure is a floor rather than a total. Google leaves low-volume searches out of the Performance Max search terms view, so some brand traffic cannot be counted.

**Google credits $123,300 of sales, ex GST, to searches for your name.** If your brand search behaves like the median in Stella's 225 geo-holdout tests, the ads caused about $7,900 of that, and the rest was most likely coming anyway. That is an industry median applied to your numbers, not a measurement of your store. The only way to know your own figure is to run a holdout test.

Brand spend is not automatically waste. Some stores defend their name on purpose because competitors bid on it. The finding here is that it is a default rather than a decision.

## Profit per campaign

Your contribution margin is 40% across the store, after product cost, shipping and payment fees. Cost per item matched 94% of line items. The other 6% of revenue, mostly bundles, uses the store average.

That puts **break-even at 2.50x** for campaigns selling the whole range. You told us Shopping - Own Label sells only Northbound products, which run at 50%, and Shopping - Stocked Brands sells everything else, which runs at 16%. Those two campaigns get their own break-even.

Google's conversion value includes GST, so every ROAS below has the GST taken out. Google's own figure sits beside it so you can find it in the account.

| Campaign | Google ROAS | ROAS ex GST | Break-even | POAS | Contribution |
|---|---|---|---|---|---|
| PMax - All Products | 9.40x | 8.55x | 2.50x | 3.42x | +$63,840 |
| Shopping - Own Label | 3.10x | 2.82x | 2.00x | 1.41x | +$4,010 |
| Shopping - Stocked Brands | 6.10x | 5.55x | 6.25x | 0.89x | **−$800** |
| Search - Generic | 3.00x | 2.73x | 2.50x | 1.09x | +$360 |

**Shopping - Stocked Brands is losing money at 6.10x.** Google ranks it as your second-best campaign. Its products run at a 16% margin, so it needs 6.25x ex GST to break even, and it managed 5.55x. Over the window it lost about $800. An account-wide target of 2.50x would call it a winner.

**Search - Generic is marginal.** At 2.73x against a 2.50x break-even, a small rise in shipping costs would tip it under.

## Wasted spend

$3,910 went to searches that never converted, on terms that each spent more than one order's contribution ($86).

| Pattern | Wasted | Type |
|---|---|---|
| "how to" | $680 | Wrong intent |
| "repair" | $520 | Wrong intent |
| kmart | $410 | Competitor |
| "second hand" | $390 | Wrong buyer |
| jobs | $240 | Employment |

The negative keyword list is at the end, ready to paste. Check it against your converting terms before you apply any of it, because the fastest way to make an account worse is a bulk paste.

## Reconciliation

| | Google Ads | Shopify | Gap |
|---|---|---|---|
| Conversions / orders | 1,412 | 1,377 | +2.5% |
| Value / net revenue, both ex GST | $303,555 | $297,600 | +2.0% |

Both lines agree, which is rarer than it should be. Your tracking looks sound.

Google's conversion value includes GST. This report took it out, but the targets inside Google Ads are still set against the GST-inclusive number. Any target you set there needs to be 10% above the break-even figures in this report.

## Settings and tracking: 18 / 30

| # | Check | |
|---|---|---|
| 1 | PMax excludes brand | ✗ |
| 2 | Negative keyword lists | ✗ |
| 3 | Customer list uploaded | ✓ |
| 4 | New customer acquisition mode | ✗ |
| 5 | Shopping and PMax separated | ✓ |
| 6 | Feed beyond Shopify defaults | ✗ |
| 7 | Conversion value excludes tax and shipping | ✗ |
| 8 | Tracking survived 26 August | ✓ |
| 9 | Demand Gen and PMax separated | ✓ |
| 10 | Search partners reviewed | ✓ |

**Performance Max has no brand exclusion.** That is where the $9,220 in the brand section comes from, and fix 3 deals with it.

**Your feed has never been touched beyond what Shopify sends.** Shopping and Performance Max do not use keywords. Google matches a search to your product title, and your titles are written to read well on a product page. None of the numbers above measure it. Once the three fixes are done, rewriting your ten best-selling titles is two hours of work.

---

## Three fixes this week

**1. Check the negative list against your converting terms, then paste it in.** One hour.

$3,910 went to searches that never converted over the 90 days, and the list below blocks the patterns behind most of it. Before you paste, open the search terms report, filter to terms with at least one conversion, and take any of those off the list.

**2. Find out which brands are sinking Shopping - Stocked Brands.** Twenty minutes.

The campaign lost about $800 over 90 days while Google reported 6.10x. Sort your products export by vendor and compare cost per item with price. The brands sitting well under 16% margin are the ones to take out or bid down. Any target on this campaign needs to be at least 6.88x in Google's figures, which is 6.25x plus GST.

**3. Split brand out of Performance Max.** Half a day.

Add a brand exclusion to Performance Max and run brand searches through a campaign you control. $9,220 went on your name inside Performance Max over 90 days. Some of it is worth defending, and after the split you decide how much rather than Google deciding for you.

Expect Performance Max's reported ROAS to fall. The sales move to the brand campaign, and the credit for them moves with them. Check first: in the Performance Max search terms view, filter for "northbound" and confirm the spend.

---

## Negative keyword list

Add these to a shared negative keyword list and apply it to campaigns one at a time, not to the whole account. Single words go in as broad match, phrases in quotes as phrase match.

```
"how to"
repair
kmart
"second hand"
jobs
```

*(A real report lists every pattern above the threshold, merged with the seed list.)*

---

Every figure above is an estimate built from your exports. Before you change a bid, open the account and confirm the top finding with your own eyes.

Want someone to look inside the account instead of at the exports? Digital Darts will audit it free and guarantee to find at least three ways it leaks cash. Book a call at digitaldarts.com.au/services/google-ads.

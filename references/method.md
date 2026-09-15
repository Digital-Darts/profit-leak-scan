# Method

Every calculation the scan makes. Follow it exactly. If a step cannot be completed from the data supplied, say so in the report rather than estimating around it.

---

## Brand matching

Get this wrong and every number downstream is wrong, so it runs first.

### The safety check

Before matching anything, test the brand name against the data.

1. Count search terms containing the brand token.
2. Count the conversions on those terms.
3. Look at what the non-converting matches actually say.

**Stop and ask the owner if any of these are true:**

- The brand name is an English word that could appear in a generic search. "Ace", "Pure", "Oak", "Method", "Bond", "Forge", "Native", "Wild", "Common".
- More than 60% of matched terms have zero conversions. A real brand search converts. A generic word that happens to be your name does not.
- The matched terms include obvious product searches that have nothing to do with the store.

Show the owner ten matched terms and ask: "are these people looking for you, or are these generic searches that happen to contain your name?"

If the brand name is generic, switch to **phrase matching only** (the brand name next to another word, e.g. "oak furniture" not "oak"), report the leak as a range rather than a figure, and say in the report why.

Getting this wrong invents a leak that is not there, and the owner will find out the moment they open the account. Better to report a range you can defend.

### Matching rules

Classify every search term into exactly one class, in this order.

| Class | Rule |
|---|---|
| **Own brand** | Contains the brand name or a supplied misspelling, as a whole word or with the store's own product names attached |
| **Stocked brand** | Contains a brand the store sells but does not own |
| **Competitor** | Contains a named competitor the owner supplied |
| **Generic** | Everything else |

Normalise before matching: lowercase, strip punctuation, collapse whitespace. Match on word boundaries, never as a substring. "Boot" must not match "bootcamp".

Handle the common misspelling shapes without being asked: missing space, doubled letter, transposed letters, plural, and the `.com` suffix.

### Performance Max

PMax search terms arrive as **search categories**, not individual terms, and they are grouped. Treat a category as brand only if the category label clearly contains the brand.

PMax categories hide brand traffic inside broader labels, so **report the PMax brand figure as a floor, not a total**, and say so: "at least $X, and probably more, because Performance Max reports categories rather than terms."

---

## Brand leak

For each campaign:

```
brand_spend      = sum(Cost) where class = own brand
brand_value      = sum(Conv. value) where class = own brand
brand_share      = brand_spend / campaign total Cost
```

Report `brand_spend` in dollars first, then share.

### The incremental haircut

Branded search is largely demand the store already created. Someone typing your name was usually coming anyway.

Stella's analysis of 225 geo-holdout tests puts the **median incremental ROAS on branded search at 0.70x, the lowest of any channel** ([source](https://www.stellaanalytics.com/), cited in the owner's report). That means roughly 30% of branded-search revenue would have arrived without the ad.

Apply it like this and label it clearly:

```
estimated_non_incremental_value = brand_value × 0.30
```

Write it as: "Around $X of the revenue Google credits to these campaigns looks like sales you were getting anyway. That is an industry median applied to your numbers, not a measurement of your store. The only way to know yours is a geo holdout test."

**Do not** subtract it silently from their ROAS. Show both.

### What to say

Brand spend is not automatically waste. Some stores defend their name deliberately because competitors bid on it. The finding is that **it should be a decision, not a default**, and right now it is a default.

If brand share is above 30% of total spend, say plainly that the reported account ROAS is mostly measuring the store's existing customers finding it.

---

## Profit per campaign

### Getting cost of goods

**Preferred path**, when the products export is supplied:

1. Join `Lineitem sku` in the orders export to `Variant SKU` in the products export.
2. `line_cogs = Cost per item × Lineitem quantity`
3. Report the **match rate**. If under 90% of line items matched a SKU, say so and say which revenue share is unmatched. Blank SKUs and bundle items are the usual cause.
4. Unmatched lines fall back to the blended margin.

**Fallback path**, blended gross margin percentage:

```
gross_profit = net_revenue × margin_pct
```

Label everything downstream an estimate.

### Net revenue

Work from the orders export, and get this right, because gross revenue flatters everything.

```
net_revenue = Subtotal − Discount Amount − Refunded Amount
```

Exclude tax. Exclude shipping charged to the customer unless you also subtract shipping cost, and you usually cannot see shipping cost, so exclude both and say so.

Exclude test orders and cancelled orders. Exclude unpaid orders (`Financial Status` not in paid, partially_refunded, refunded).

### The fee stack

Ask for these once. If the owner does not know, use the defaults and mark them.

| Item | Default if unknown | Note |
|---|---|---|
| Payment processing | 1.75% + $0.30 per order | Shopify Payments AU standard rate (verify current) |
| Outbound shipping cost | ask | Varies too much to default. If unknown, exclude and say the profit figures are therefore optimistic |
| Pick, pack, 3PL | ask | Same |

### The numbers

```
break_even_roas   = 1 / gross_margin_pct
poas              = (revenue_attributed × gross_margin_pct) / cost
contribution      = (revenue_attributed × gross_margin_pct) − fees − cost
```

Where `gross_margin_pct` is per campaign when SKU-level cost is available, and blended otherwise. **Always use per-campaign margin where the data allows it**, because campaigns sell different products at different margins. A campaign pushing a 22% margin product needs 4.5x to break even while one pushing a 60% margin product needs 1.7x, and a single account-wide ROAS target hides both.

Attribute revenue using `Conv. value` from the Google Ads export. Say clearly that this is Google's own attribution and it overstates, which is what the reconciliation section is for.

### Flagging

- **Below break-even**: `roas < break_even_roas`. Flag it, and flag loudly if its reported ROAS looks healthy.
- **Marginal**: within 15% of break-even. These are the ones that flip on a shipping price rise.
- **Thin data**: under 20 conversions in the window. Directional only, say so.

---

## Wasted spend

Work only from search terms with `Cost > 0` and `Conversions = 0`.

**Set the floor at the store's own numbers, not an arbitrary dollar amount.** A term is worth flagging when its spend exceeds what a converting visit is worth:

```
waste_threshold = average_order_value × gross_margin_pct
```

A term that has spent more than one order's gross profit and returned nothing is a real leak. A term that has spent $4 is noise.

### N-grams

Split every wasted term into 1, 2 and 3-word sequences. Sum wasted spend by n-gram. Rank.

Report the top 20 patterns with total wasted spend against each. The pattern matters more than the individual term, because the pattern is what you can negative once and stop forever.

Classify each pattern by why it wasted money, because the fix differs:

| Type | Example | Fix |
|---|---|---|
| Wrong intent | "how to", "diy", "repair", "instructions" | Negative |
| Wrong buyer | "wholesale", "bulk", "job lot", "supplier" | Negative, unless they sell wholesale |
| Free and cheap | "free", "cheap", "discount code", "coupon" | Negative |
| Competitor and marketplace | "amazon", "ebay", "temu", "kmart", "bunnings" | Negative |
| Employment | "jobs", "careers", "salary" | Negative |
| Adjacent product | a product they do not stock | Negative, and note the gap in case they should stock it |
| Their own brand | see brand leak | Campaign structure, not a negative |

Then merge with `references/negatives-seed.md` and output a deduplicated, copy-paste-ready list.

**Say what match type to use.** Broad match negatives for single words, phrase for multi-word patterns. Warn that a negative applied at account level applies everywhere, and that "free" will block "free shipping" searches which often convert well.

---

## Reconciliation

Three numbers should roughly agree. When they do not, the account is being managed on fiction.

```
Google Ads conversions (window)   vs   Shopify orders (window)
Google Ads conv. value (window)   vs   Shopify net revenue (window)
```

Google's number will be higher, and should be, because it counts assisted and view-through conversions and Shopify counts orders. The question is how much higher.

| Gap | What it usually means |
|---|---|
| Ads conversions **far above** Shopify orders, e.g. nearly double | Double-counted conversions. The Google & YouTube app installed on top of an existing tag is the most common cause in Shopify stores |
| Ads value far above Shopify revenue but counts roughly match | Conversion value includes tax and shipping, or a multi-currency store is sending local amounts as if they were account currency. A 20,000 won order arriving as $20,000 |
| Ads conversions **far below** Shopify orders | Under-tracking. Since **26 August 2026** Shopify has removed the Additional Scripts box from the thank-you and order status pages for all non-Plus stores, and anything living there stopped firing with no error. If the drop starts in late August, that is where to look |
| Roughly aligned | Say so. It is rarer than it should be and worth telling them |

Report the gap in dollars and as a ratio, then say which of the above it looks like and how to confirm it in the account.

Every other number in the account is steered by these two, which is why this table usually matters more than the profit table above it.

---

## Scoring

100 points, four sections. Show the owner the breakdown, not just the total, so they can see where they lost points.

### Brand leak, 25 points

| Brand share of spend | Points |
|---|---|
| Under 10% | 25 |
| 10 to 20% | 18 |
| 20 to 30% | 10 |
| 30 to 45% | 4 |
| Over 45% | 0 |

If the store has no brand campaign and no PMax, award 25 and say the section does not apply yet.

### Profit, 25 points

Start at 25. Subtract:

- 3 points for every 10% of spend sitting in campaigns below break-even, to a floor of 0.
- 5 points if no cost per item is filled in at all, because the store cannot see profit on any channel, not just this one.

### Wasted spend, 20 points

| Wasted spend as share of total | Points |
|---|---|
| Under 5% | 20 |
| 5 to 10% | 15 |
| 10 to 20% | 8 |
| Over 20% | 0 |

Where wasted spend is the sum of cost on zero-conversion terms above the threshold.

### Settings and tracking, 30 points

Three points for each of the ten checks in `references/settings-check.md`. Award zero for an unanswered check and say it was not answered rather than assuming the worst.

### Bands

| Score | Band | What to say |
|---|---|---|
| 85 to 100 | Tight | The structure is sound. The remaining gains are in the feed and in creative |
| 70 to 84 | Leaking at the edges | Nothing is broken. Two or three fixes are worth real money |
| 50 to 69 | Leaking | There is a recoverable amount here and most of it is structural |
| 30 to 49 | Bleeding | Spend is being lost faster than optimisation can recover. Fix the structure before touching bids |
| Under 30 | Stop | Something fundamental is wrong, usually tracking. Do not scale anything until it is fixed |

Never congratulate. State the band and move on.

---

## The three fixes

Rank by **dollars recovered per hour of work**, not by size of the problem.

For each fix, give:

1. What to do, in one sentence, specific enough to act on today.
2. The estimated dollars at stake over the next 90 days, with the working shown.
3. How long it takes, honestly. "Twenty minutes" or "half a day with your developer."
4. What to check first to confirm the finding is real.

If a broken tracking setup showed up in the reconciliation, **it is always fix number one**, regardless of dollar size, because every other number in the account is downstream of it.

---

## About the thresholds

The scoring bands are reasoned from first principles and from the sources cited above, not fitted to a benchmark set. They are deliberately conservative, because a scan that manufactures a finding on a healthy account is worse than one that misses a small leak.

If you are forking this, the bands are the first thing to change. Set them against the accounts you actually work on.

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

Performance Max search terms can arrive two ways.

- **The "Search terms and landing pages for Performance Max" view** lists real search terms. Classify them like any other. Google leaves out low-volume terms, so the brand figure is still **a floor, not a total**.
- **Search categories** from the Insights page are grouped labels, not terms. Treat a category as brand only if its label clearly contains the brand.

Either way, say so in the report: "at least $X, and probably more, because Performance Max does not show every search."

If the Performance Max file has no Cost column, estimate brand spend from clicks and label it an estimate:

```
pmax_brand_spend ≈ (brand clicks ÷ all clicks in the file) × campaign Cost from the campaigns export
```

If it has no Conv. value either, report brand spend for Performance Max and skip the revenue estimate below for it.

---

## Same footing

Every dollar in the profit maths is **ex GST**. GST is collected for the tax office, not kept by the store. Google Ads Cost is already ex GST, because Google adds GST on the invoice.

GST is 10% in Australia and 15% in New Zealand. Call that `rate`.

### Shopify orders

1. **Subtotal is already after discounts.** Never subtract Discount Amount from it. Doing so counts every discount twice.
2. **Work out whether prices include tax.** For paid orders, compare Total with Subtotal + Shipping, and with Subtotal + Shipping + Taxes (add Duties if the column has values).
   - Total ≈ Subtotal + Shipping means the tax is already inside the prices. This is the Shopify default in Australia.
   - Total ≈ Subtotal + Shipping + Taxes means prices exclude tax.
   - Mixed or unclear: ask the owner to check Shopify admin → Settings → Taxes and duties.
3. **Take the GST out.** When prices include tax, remove it from the taxable lines only. `Lineitem taxable` says which lines those are. When every line is taxable, this is simply Subtotal ÷ (1 + rate).

```
tax_in_subtotal = taxable part of Subtotal × rate ÷ (1 + rate)     (0 when prices exclude tax)
net_revenue     = Subtotal − tax_in_subtotal − refunds_ex_gst
```

4. **Refunds.** Refunded Amount includes GST and can include refunded shipping. Take the GST out the same way and treat the rest as refunded product. Say this is approximate.
5. **Exclude** test orders, cancelled orders, and unpaid orders (`Financial Status` not in paid, partially_refunded, refunded).
6. **Exclude shipping charged to the customer.** Shipping cost comes into the maths through the margin instead.

### Google Ads conversion value

Decide whether Conv. value includes GST.

- **Ask.** Store brief question 4, which is also settings check 7.
- **Test it against the data** when Google's conversion count is within about 15% of Shopify's order count. Compare Google's value per conversion with Shopify's average order, GST-inclusive and ex GST. The one it lands closer to is the basis. If it sits about 10% above the GST-inclusive average as well, it probably includes shipping too.
- **When the counts are far apart**, the test is unreliable. Use the owner's answer, or assume it matches the Shopify price basis, and say which you did.

If conversion value includes GST:

```
conv_value_ex_gst = Conv. value ÷ (1 + rate)
```

Use `conv_value_ex_gst` for every ROAS, POAS and contribution figure. Show Google's own ROAS beside it once, so the owner can find the numbers in the account.

Tell the owner what it means for their targets. While conversion value stays GST-inclusive, any target ROAS set inside Google Ads has to be the break-even figure in this report × (1 + rate).

### Cost per item

Assume Cost per item is ex GST, which is how GST-registered stores normally enter it. Put that assumption in "what this is built on".

---

## Brand leak

For each campaign:

```
brand_spend      = sum(Cost) where class = own brand
brand_value      = sum(conv_value_ex_gst) where class = own brand
brand_share      = brand_spend / campaign total Cost
```

Report `brand_spend` in dollars first, then share.

### Incrementality

Branded search is largely demand the store already created. Someone typing your name was usually coming anyway.

Stella's 2025 DTC incrementality benchmarks, drawn from 225 geo-holdout tests, put the **median incremental ROAS on branded search at 0.70x, the lowest of any channel tested** ([source](https://www.stellaheystella.com/blog/2025-dtc-digital-advertising-incrementality-benchmarks)). Incremental ROAS counts only the sales the ad caused. At the median, $1 of brand spend caused $0.70 of sales.

Apply it like this and label it clearly:

```
estimated_incremental_value     = brand_spend × 0.70
estimated_non_incremental_value = brand_value − estimated_incremental_value      (never below 0)
```

Write it as: "Google credits $X of sales to searches for your name. If your brand search behaves like the median in Stella's tests, the ads caused about $Y of that, and the rest was most likely coming anyway. That is an industry median applied to your numbers, not a measurement of your store. The only way to know yours is a geo holdout test."

**Do not** subtract it silently from their ROAS. Show both.

### What to say

Brand spend is not automatically waste. Some stores defend their name deliberately because competitors bid on it. The finding is that **it should be a decision, not a default**, and right now it is a default.

If brand share is above 30% of total spend, say plainly that the reported account ROAS is mostly measuring the store's existing customers finding it.

---

## Profit per campaign

### The margin

One figure drives break-even, POAS, contribution and the waste threshold: the **contribution margin before ad spend**, as a share of ex-GST net revenue.

```
margin_pct = (net_revenue − product_cost − shipping_cost − payment_fees − pick_pack) / net_revenue
```

**Product cost, preferred path**, when the products export is supplied:

1. Join `Lineitem sku` in the orders export to `Variant SKU` in the products export.
2. `line_cogs = Cost per item × Lineitem quantity`
3. Report the **match rate**. If under 90% of line items matched a SKU, say so and say what share of revenue is unmatched. Blank SKUs and bundle items are the usual cause.
4. Unmatched lines use the margin of the matched lines.

**Fallback path**, when there is no usable cost per item: use the owner's answer to store brief question 6. That figure already includes shipping and fees, so do not subtract them again. Label everything downstream an estimate.

If the owner gave a margin and cost per item exists too, calculate from cost per item and show their figure beside it. See `store-brief.md` § When the owner's answer and the data disagree.

### The fee stack

Ask for these once, in the store brief. If the owner does not know, use the defaults and mark them.

| Item | Default if unknown | Note |
|---|---|---|
| Payment processing | 1.75% + $0.30 per order | Shopify Payments AU standard rate (verify current) |
| Outbound shipping cost | store brief question 5 | Varies too much to default. If unknown, leave it out and say the profit figures are therefore optimistic |
| Pick, pack, 3PL | ask if they mention a 3PL | Same |

### Margin per campaign

Neither export says which products a campaign sold. The Google Ads exports have no products in them and the Shopify orders export has no campaigns. Per-campaign margin needs the owner's answer to store brief question 9.

1. For each campaign the owner linked to a group of products, work out `margin_pct` from the order lines for those products. The products export carries Vendor, Type and Tags to find them by.
2. Collections are not in the products export. If the owner names a collection, ask which vendor, type or tag it is built from.
3. Campaigns selling the whole range, which is most Performance Max and most Search, get the store margin.
4. With no answer to question 9, every campaign gets the store margin. Say that break-even is then the same for every campaign.

You can suggest a mapping from campaign names, but confirm it with the owner before using it. A campaign called "Clearance" may hold far more than the name says.

Campaigns sell different products at different margins. A campaign pushing a 22% margin product needs 4.5x to break even while one pushing a 60% margin product needs 1.7x, and a single account-wide ROAS target hides both.

### The numbers

```
break_even_roas   = 1 / margin_pct
roas              = conv_value_ex_gst / cost
poas              = (conv_value_ex_gst × margin_pct) / cost
contribution      = (conv_value_ex_gst × margin_pct) − cost
```

Revenue here is Google's own attribution, which overstates. Say so. The reconciliation section is there to test it.

### Flagging

- **Below break-even**: `roas < break_even_roas`. Flag it, and flag loudly if its reported ROAS looks healthy.
- **Marginal**: at or above break-even, but by less than 15%. These are the ones that flip on a shipping price rise.
- **Thin data**: under 20 conversions in the window. Directional only, say so.

---

## Using the store brief

### Campaign roles

| What the owner says a campaign is for | How to judge it |
|---|---|
| Main sales | Against break-even, as above |
| Protecting the brand name | In the brand leak section. Its ROAS will look excellent against break-even, and that says nothing about whether the spend is needed |
| Finding new customers (prospecting, top of funnel, most Demand Gen and YouTube) | Show break-even, but do not call it a loser on same-window ROAS alone. Say it should be judged on new customers won and what they are worth later, and that these exports cannot show that |
| Winning back past visitors (remarketing) | Say its ROAS is flattered, because many of those buyers were already on their way. Do not use it as proof the account works |

With no roles given, treat every campaign as a sales campaign and say so.

### Campaign groups

Some stores split one range across several campaigns on purpose: best sellers in one, the rest of the range in another, sometimes called a Kings and Peasants structure. Others run one campaign per margin tier.

When the owner says campaigns work as a group, report each campaign and the group total, and judge the group. A low-ROAS member of a split is often doing its job. Never recommend pausing or cutting one without saying what happens to the products it carries.

### Left-out campaigns

Keep them in total spend and in the reconciliation, because the money was spent. Leave them out of flags, waste patterns, scoring and fixes. List them, with the owner's reason, at the top of the profit section.

### Repeat customers

If the owner names products that bring in customers who come back, and says how much of a first-order loss they accept, compare the campaigns selling those products against both break-even and the owner's allowance. Say which one you judged them on.

Without that answer, judge every campaign on first-order break-even and say in the report that repeat purchases are not counted, so campaigns that win repeat buyers look worse than they are.

### Conversion lag

Google Ads counts a sale against the day of the click, and sales from the most recent clicks are still arriving when the export is pulled.

- Use the owner's answer to question 7, or 7 days.
- Compare the window's end date with the date the exports were pulled. If the gap is shorter than the lag, say the reported ROAS is understated, and mark any campaign within 15% below break-even "marginal, may be lag" rather than "below break-even".
- A lag of a week or more usually means a considered purchase. Say that the 90-day window catches fewer of the sales those clicks will eventually produce.

---

## Wasted spend

Work only from search terms with `Cost > 0` and `Conversions = 0`. Leave out campaigns the owner asked to leave out.

**Set the floor at the store's own numbers, not an arbitrary dollar amount.** A term is worth flagging when its spend exceeds what an order is worth to the store:

```
waste_threshold = average_order_value_ex_gst × margin_pct
```

A term that has spent more than one order's contribution and returned nothing is a real leak. A term that has spent $4 is noise.

### N-grams

Split every wasted term into 1, 2 and 3-word sequences. Sum wasted spend by n-gram. Rank.

Report the top 20 patterns with total wasted spend against each. Report patterns rather than single terms, because one negative on a pattern stops it for good.

Classify each pattern by why it wasted money, because the fix differs:

| Type | Example | Fix |
|---|---|---|
| Wrong intent | "how to", "diy", "repair", "instructions" | Negative |
| Wrong buyer | "wholesale", "bulk", "job lot", "supplier", "second hand" | Negative, unless they sell wholesale or used |
| Free and cheap | "free", "cheap", "discount code", "coupon" | Negative |
| Competitor and marketplace | "amazon", "ebay", "temu", "kmart", "bunnings" | Negative |
| Employment | "jobs", "careers", "salary" | Negative |
| Adjacent product | a product they do not stock | Negative, and note the gap in case they should stock it |
| Their own brand | see brand leak | Campaign structure, not a negative |

Then merge with `references/negatives-seed.md` and output a deduplicated, copy-paste-ready list.

**Say what match type to use.** Broad match negatives for single words, phrase for multi-word patterns. Warn that a negative applied at account level applies everywhere, and that "free" will block "free shipping" searches which often convert well.

---

## Reconciliation

These pairs should roughly agree. When they do not, the account is being managed on fiction.

```
Google Ads conversions (window)          vs   Shopify orders, counted by unique Name (window)
Google Ads conv. value ex GST (window)   vs   Shopify net revenue ex GST (window)
```

Google's number will be higher, and should be, because it counts assisted and view-through conversions and Shopify counts orders. The question is how much higher.

| Gap | What it usually means |
|---|---|
| Ads conversions **far above** Shopify orders, e.g. nearly double | Double-counted conversions. The Google & YouTube app installed on top of an existing tag is the most common cause in Shopify stores |
| Ads value far above Shopify revenue but counts roughly match | Conversion value includes shipping, the GST test was inconclusive and GST is still in, or a multi-currency store is sending local amounts as if they were account currency. A 20,000 won order arriving as $20,000 |
| Ads conversions **far below** Shopify orders | Under-tracking. Since **26 August 2026** Shopify has removed the Additional Scripts box from the thank-you and order status pages for all non-Plus stores, and anything living there stopped firing with no error. If the drop starts in late August, that is where to look. A long conversion lag with a window that ends close to the export date also pulls Google's number down, so rule that out first |
| Roughly aligned | Say so. It is rarer than it should be and worth telling them |

Report the gap in dollars and as a ratio, then say which of the above it looks like and how to confirm it in the account.

Every other number in the account is steered by these two. If they are wrong, the profit table is wrong too, which is why a tracking fault always becomes fix number one.

---

## Scoring

100 points, four sections. Show the owner the breakdown, not just the total, so they can see where they lost points. Left-out campaigns do not count towards any section.

### Brand leak, 25 points

| Brand share of spend | Points |
|---|---|
| Under 10% | 25 |
| 10 to 20% | 18 |
| 20 to 30% | 10 |
| 30 to 45% | 4 |
| Over 45% | 0 |

If the store has no brand campaign and no Performance Max, award 25 and say the section does not apply yet.

### Profit, 25 points

Start at 25. Subtract:

- 3 points for every full 10% of spend sitting in campaigns below break-even, to a floor of 0. Campaigns marked "may be lag" do not count.
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

Check each fix against the store brief before you write it. A fix that cuts a campaign the owner said is there to find new customers, or breaks up a group they said works as one, is the wrong fix.

---

## About the thresholds

The scoring bands are reasoned from first principles and from the sources cited above, not fitted to a benchmark set. They are deliberately conservative, because a scan that manufactures a finding on a healthy account is worse than one that misses a small leak.

If you are forking this, the bands are the first thing to change. Set them against the accounts you actually work on.

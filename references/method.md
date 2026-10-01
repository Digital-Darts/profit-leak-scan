# Method

Every calculation the scan makes. Follow it exactly. If a step cannot be completed from the data supplied, say so in the report rather than estimating around it.

---

## Brand matching

Get this wrong and every number downstream is wrong, so it runs first.

### The safety check

Before matching anything, test the brand name against the data.

The brand token is the whole brand name as the owner gave it, with and without its spaces. Never match on one word of a name made of several words. "Oak Lane" matches "oak lane" and "oaklane", never "oak" or "lane".

Use only search terms with Cost above zero, and add the rows for the same search term together first. A search that showed an ad and was never clicked says nothing about who was searching.

1. Add up the spend on search terms containing the brand token.
2. Work out what share of that spend sits on terms with no conversions.
3. Work out the same share for the whole account.
4. Look at what the non-converting matches actually say.

**Stop and ask the owner if any of these are true:**

- The brand name, taken whole, is an English word or an everyday phrase that could appear in a generic search. "Ace", "Pure", "Oak", "Method", "Bond", "Forge", "Native", "Wild", "Common".
- The share from step 2 is more than half the share from step 3. A real brand search converts far better than the rest of the account. A generic word that happens to be your name converts like everything else.
- The matched terms include obvious product searches that have nothing to do with the store.

When you stop, show the owner the ten matched terms with the most spend and ask: "are these people looking for you, or are these generic searches that happen to contain your name?"

If the brand name is generic, switch to **phrase matching only** (the brand name next to another word, e.g. "oak furniture" not "oak"), report the leak as a range, from the phrase matches alone up to every match, score it on the low end, and say in the report why.

Getting this wrong invents a leak that is not there, and the owner will find out the moment they open the account. Better to report a range you can defend.

### Matching rules

Classify every search term into exactly one class, in this order.

| Class | Rule |
|---|---|
| **Own brand** | Contains the brand name or a supplied misspelling as a whole word, whatever else is in the search |
| **Stocked brand** | Contains a brand the store sells but does not own |
| **Competitor** | Contains a named competitor the owner supplied |
| **Generic** | Everything else |

Normalise before matching: lowercase, delete apostrophes, replace other punctuation with a space, collapse whitespace. Match on word boundaries, never as a substring. "Boot" must not match "bootcamp".

Handle the common misspelling shapes without being asked: missing space, doubled letter, dropped letter, transposed letters, plural, and the `.com` suffix. Apply one shape at a time, to the name with and without its spaces, and add only the spellings that appear in the search terms. Show the owner any misspelling you add that they did not give you. Leave out a shape that is an everyday word in its own right, and ask the owner about it. For a store called "Brewd", the dropped-letter shape "brew" stays out.

If the owner did not list the brands they stock, take them from the Vendor column in the products export and show the owner the list. Match a stocked brand on its whole name. Leave out the store's own name, and any vendor name that is an ordinary word, unless the owner confirms it.

### Performance Max

Performance Max search terms arrive in the main search terms export, on rows where Match type says "Performance Max". Classify them like any other term.

Google leaves low-volume searches out of the report, and the export says how much. The row "Total: Other search terms" is spend on searches Google does not list. Report the brand figure as **a floor, not a total**, and put that dollar amount beside it: "at least $X on your own name, with a further $Y of spend in searches Google does not show." When a brand campaign is counted in full, its own unlisted spend is already inside $X, so take it out of $Y. That amount is the campaign's Cost less its listed search terms.

Account spend that is in neither the listed terms nor "Other search terms" is mostly campaigns that have no search terms at all, such as Demand Gen and Display.

Some accounts also offer a separate view, "Search terms and landing pages for Performance Max". Use that file only when the main export has no rows for a Performance Max campaign that has spend. If the owner uploads both and the main export already has rows for the campaign, ignore the separate file, or its terms are counted twice.

If a separate Performance Max file has no Cost column, estimate brand spend from clicks and label it an estimate:

```
pmax_brand_spend ≈ (brand clicks ÷ all clicks in the file) × campaign Cost from the campaigns export
```

If it has no Conv. value either, report brand spend for Performance Max and skip brand value and the incrementality estimate for it.

---

## Same footing

Every dollar in the profit maths is **ex GST**. GST is collected for the tax office, not kept by the store. Google Ads Cost is the figure before any tax on Google's invoice, so it needs no adjustment.

This file says GST. Read it as VAT for a UK store and sales tax for a US one.

### Which country

Take the store's country from the Currency column in the Shopify orders export: AUD is Australia, NZD is New Zealand, GBP is the United Kingdom, USD is the United States. If the column holds more than one currency, stop and ask. If Shipping Country shows most orders going somewhere else, confirm the country with the owner.

The country decides the payment fee default. The negative keyword blocks go by where the store sells: a store sells into a market when at least a tenth of its orders ship there, a campaign is named for it, or the owner says it advertises there. For any other currency or market, ask the owner what they pay in card fees, and use only the negative keyword blocks outside Country defaults.

### Shopify orders

1. **Subtotal is already after discounts.** Never subtract Discount Amount from it. Doing so counts every discount twice.
2. **Leave out orders that are not sales.** An order counts when Financial Status is paid or partially_refunded, Cancelled at is empty, and Total is above zero. That leaves out unpaid, cancelled, fully refunded, test and replacement orders.
3. **Work out, order by order, whether tax is inside the prices.**
   - Total ≈ Subtotal + Shipping, and Taxes is above zero: the tax is inside the prices. This is the Shopify default in Australia, New Zealand and the UK.
   - Taxes is zero: no tax was charged, so nothing comes out. Export orders and untaxed goods look like this.
   - Total ≈ Subtotal + Shipping + Taxes (add Duties if the column has values): prices exclude tax, and nothing comes out of Subtotal. Most US stores look like this.
   - Some orders have tax inside the price and others have it added on top, or the sums match neither pattern: ask the owner to check Shopify admin → Settings → Taxes and duties. Orders with no tax at all are not a mix. "≈" means within a few cents.
4. **Take the tax out using what Shopify charged, not a rate.** The formula is below. A rate applied to every taxable line overstates the tax for any store that sells overseas, because those orders carry none.
5. **Refunds.** On a partially refunded order, Refunded Amount can include tax and delivery. Take the product, ex-tax share of it, using the order's own figures, as in the formula below. Say this is approximate.
6. **Exclude shipping charged to the customer.** Shipping cost comes into the maths through the margin instead.
7. **Set aside lines that are not products.** A line where `Lineitem requires shipping` is false is shipping protection, a gift card or a digital add-on. Add those lines up and say what they total. They stay out of the cost match and out of the margin, because nothing in the exports says what they cost.
8. **Other sales channels.** Where the orders export has a Source column, orders marked web are online store orders. Marketplace, point of sale and draft orders stay in the margin, and come out of every comparison with Google's figures, because an ad click cannot produce them. A Source shown only as a number is an app. Ask the owner what it is, and until they answer treat it as another channel and say so.

For an order with the tax inside the prices:

```
r               = Taxes ÷ (Total − Taxes)          the rate this order was charged
tax_on_shipping = Shipping × r ÷ (1 + r)
tax_in_subtotal = Taxes − tax_on_shipping          (0 when Taxes is zero or prices exclude tax)
```

Across all the orders that count:

```
refund_ex_gst              = Refunded Amount × (Subtotal − tax_in_subtotal) ÷ Total      for each partially refunded order
tax_share                  = sum(tax_in_subtotal) ÷ sum(Subtotal)
net_revenue                = sum(Subtotal) − sum(tax_in_subtotal) − sum(refund_ex_gst)
orders                     = the number of orders that count
web_orders                 = the online store orders among them
web_net_revenue            = net_revenue worked out over those orders only
average_order_value_ex_gst = web_net_revenue ÷ web_orders
```

Check `tax_share` against the country. A store that charges tax on every order lands near 9.1% in Australia, 13.0% in New Zealand and 16.7% in the UK. A lower figure is normal for a store that sells overseas or sells untaxed goods. Say what the figure is.

When the store ships to more than one country, work out `tax_share` for each Shipping Country as well. It explains a store figure that sits below the country's rate, and the value factor below is worked out for each country in the same way.

### Google Ads conversion value

**Which column.** Use Original conv. value wherever an export has it. It is what the customer paid, before Google adds a new-customer value or applies a conversion value rule. A column that is present but blank on every row counts as absent.

- Neither export has it: use Conv. value. If the owner said "bid higher for new customers" is on (store brief question 14), say that every value figure in the report includes the added new-customer value, and ask for the exports again with the column ticked.
- Only the campaigns export has it: for each campaign work out Original conv. value ÷ Conv. value, and multiply that campaign's search-term values by it. Brand value and ROAS then stand on the same basis.
- Both have it: use it everywhere.

Call the chosen figure `value`.

**What it includes.** Google's value can be the product value alone, the product value with tax, or the whole order with tax and delivery. Work out which, then bring it back to the product value ex tax, which is what `net_revenue` measures.

- **Ask.** Store brief question 4, which is also settings check 7.
- **Test it against the data.** Convert the currency first if the two differ, and use online store orders only. Include the ones refunded or cancelled since, because Google recorded the sale when it was placed. There are three possible bases: product value ex tax (Subtotal less `tax_in_subtotal`), product value with tax (Subtotal, plus Taxes where prices exclude tax), and the full Total. The sharpest test is order by order. A search term row with exactly one conversion carries one order's value, so count how many of those values equal an order's amount, to the cent, on each basis. Many will match more than one basis, because an order with no delivery charge has the same Subtotal and Total. Go by the values that match one basis and no other. The basis with the most of those is Google's. A value that matches no order says nothing, so leave it out. That is common where customers pay in a currency other than the store's. If too few rows have exactly one conversion, fall back on averages: take the basis whose average order Google's value per conversion lands closest to.
- **Skip the test** when "bid higher for new customers" is on and there is no Original conv. value column. The added amount would be mistaken for tax or delivery. Use the owner's answer, or assume the basis matches Shopify's prices, and say which you did. Settings check 7 is then unanswered.
- **When the test is unclear**, because fewer than about ten values match one basis only, or no basis leads clearly, or on the fallback two of the averages sit within a couple of percent of each other, use the owner's answer, or the closer one, and say which you did. If both candidates include tax, settings check 7 fails whichever it is.

```
value_factor      = sum(Subtotal − tax_in_subtotal) ÷ sum of the same orders measured on Google's basis      (online store orders that count)
conv_value_ex_gst = value × value_factor
```

The factor is 1 when Google records the product value ex tax. For a store with tax inside its prices and no delivery in the value, it equals 1 − `tax_share`. For a US store whose tag sends the order total, it takes out both the sales tax and the delivery charge.

A campaign that sells into one country uses the factor worked out from that country's orders. Take the country from the owner, or suggest it from the campaign name and confirm it. A campaign that names no country, or more than one, uses the store's factor. The factor is an average. A campaign that sells mostly untaxed goods has too much taken out, and one that sells only taxed goods too little. Say so when the store sells both.

The account's `conv_value_ex_gst` is the sum of its campaigns'. Use `conv_value_ex_gst` for every ROAS, POAS and contribution figure. Show Google's own ROAS, which is Conv. value ÷ Cost, beside it once, so the owner can find the numbers in the account.

Tell the owner what it means for their targets. Break-even inside Google Ads is the break-even figure in this report ÷ `value_factor`. While "bid higher for new customers" is on, it is higher again, by Conv. value ÷ Original conv. value. When that column is missing, say the extra cannot be worked out, and that any target read off Google's figures is too low by an unknown amount. Stating what break-even is in Google's figures is not a recommendation to change a bid.

### Currency

Google Ads exports carry a Currency code column. Compare it with the Currency column in the Shopify orders export. If a Google export has no Currency code, ask the owner which currency the account bills in.

When the two differ, never convert silently.

1. State total spend in the account's own currency first. That is the number the owner recognises.
2. Ask for the average exchange rate over the window, as "1 [account currency] = X [store currency]". If you can look the rate up, do, say where it came from, and have the owner confirm it before you use it.
3. Multiply Google's Cost and `value` by X. Every dollar figure in the report is then in the store's currency. Wherever the report tells the owner to check a figure in the account, give the account-currency figure in brackets, because that is what the account shows.
4. Record the rate and its source once, in "what this is built on".

ROAS, POAS and break-even are ratios, so converting does not move them. Dollar figures are approximate, more so when the account currency moved a lot during the window.

Google converts conversion values into the account's currency itself. If value per sale is far from Shopify's average order after converting, suspect the tag is sending store-currency amounts as if they were account currency.

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

Report `brand_spend` in dollars first, then share. Campaign total Cost comes from the campaigns report. Without that file, give brand spend as a share of the campaign's listed search spend, and say so.

A campaign whose role is protecting the brand name counts in full. Its whole Cost is brand spend and its whole value is brand value, because the campaign was built to catch the name, and the searches Google does not list in it are nearly all for it.

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

When brand spend is under 5% of account spend, skip this estimate. Report the brand spend and leave it there.

### What to say

Brand spend is not automatically waste. Some stores defend their name deliberately because competitors bid on it. The finding is that **it should be a decision, not a default**. Brand spend inside Performance Max or a generic campaign is usually a default. Brand spend in a campaign the store built for its own name is already a decision, so say that, and report what sits outside it.

If brand share is above 30% of total spend, say plainly that the reported account ROAS is mostly measuring the store's existing customers finding it.

---

## Profit per campaign

### The margin

One figure drives break-even, POAS, contribution and the waste threshold: the **contribution margin before ad spend**, as a share of ex-GST net revenue.

```
product_net_revenue = net_revenue × (product line revenue ÷ all line revenue)
margin_pct          = (product_net_revenue − product_cost − shipping_cost − payment_fees − pick_pack) / product_net_revenue
```

Line revenue is `Lineitem price × Lineitem quantity − Lineitem discount`. It is before order-level discounts and includes any tax inside the price, so use it for shares and ratios only, never as revenue. Product lines are the ones not set aside in Same footing.

The lines set aside are still inside Subtotal, so `net_revenue`, the average order and Google's value all include them, and the profit table gives them the product margin. When they are more than about 5% of line revenue, say so.

**Product cost, preferred path**, when the products export is supplied:

1. Clean both SKU columns before joining: trim spaces, drop a leading apostrophe and ignore case. Shopify puts an apostrophe in front of numeric SKUs in the products export, so an untouched join misses every one of them. Skip product rows with no SKU. If a SKU appears more than once, use the first row that has a cost.
2. Join `Lineitem sku` in the orders export to `Variant SKU` in the products export. Leave out the lines set aside in Same footing as not products.
3. `line_cogs = Cost per item × Lineitem quantity`
4. Report the **match rate**, by revenue first and then by line items. If under 90% of product revenue matched a SKU with a cost, say so. Blank costs and bundle items are the usual cause.
5. Unmatched product lines take the cost ratio of the matched ones:

```
product_cost = matched cost + unmatched product line revenue × (matched cost ÷ matched line revenue)
```

**Fallback path**, when there is no usable cost per item: use the owner's answer to store brief question 6. That figure already includes shipping and fees, so do not subtract them again. Label everything downstream an estimate.

If the owner gave a margin and cost per item exists too, calculate from cost per item and show their figure beside it. See `store-brief.md` § When the owner's answer and the data disagree.

### The fee stack

Shipping cost is store brief question 5. The brief does not ask about payment fees or pick and pack, so use the defaults below, mark them, and change them if the owner gives their own figures.

| Item | Default if unknown | Note |
|---|---|---|
| Payment processing | by country, in the table below | Shopify Payments, Basic plan, domestic cards (verify current). Apply the percentage to the order Total |
| Outbound shipping cost | store brief question 5 | Varies too much to default. If unknown, ask once more before writing the report, unless the owner asked for the report first. If it stays unknown, leave it out, say the profit figures are optimistic, and add one line of sensitivity: what each $5 of shipping cost per order does to the margin and to break-even |
| Pick, pack, 3PL | ask if they mention a 3PL | Same |

| Country | Payment processing default |
|---|---|
| Australia | 1.7% + $0.30 per order |
| United Kingdom | 2% + £0.25 per order |
| United States | 2.9% + $0.30 per order |
| New Zealand and anywhere else | ask the owner |

International cards and American Express cost more than these rates, so the default understates fees for a store with many overseas buyers.

### Margin per campaign

Neither export says which products a campaign sold. The Google Ads exports have no products in them and the Shopify orders export has no campaigns. Per-campaign margin needs the owner's answer to store brief question 9.

1. For each campaign the owner linked to a group of products, work out `margin_pct` from the order lines for those products. Their net revenue is `product_net_revenue` multiplied by their share of product line revenue. The products export carries Vendor, Type and Tags to find them by.
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

Google records a sale when the order is placed and does not take it back when the order is refunded. Work out the refunded share: Refunded Amount ÷ Total, across every online store order that took payment, including the ones since refunded in full or cancelled and left out of the margin. Under 5%, give the figure in "what this is built on". Above that, say beside the profit table that every ROAS, POAS and contribution figure is too high by about that share.

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

With no roles given, read a role from the campaign name where it is plain, such as a campaign named Brand, and treat Demand Gen as finding new customers. Treat every other campaign as a sales campaign. Say which roles you assumed.

### Campaign groups

Some stores split one range across several campaigns on purpose: best sellers in one, the rest of the range in another, sometimes called a Kings and Peasants structure. Others run one campaign per margin tier.

When the owner says campaigns work as a group, report each campaign and the group total, and judge the group. A low-ROAS member of a split is often doing its job. Never recommend pausing or cutting one without saying what happens to the products it carries.

You can suggest a group from campaign names, such as several campaigns named after product tiers, but confirm it with the owner before judging them as one. Until they confirm, report each campaign on its own and show the group's total beside them.

### Left-out campaigns

Keep them in total spend and in the reconciliation, because the money was spent. Leave them out of flags, waste patterns, scoring and fixes. List them, with the owner's reason, at the top of the profit section.

### Repeat customers

If the owner names products that bring in customers who come back, and says how much of a first-order loss they accept, compare the campaigns selling those products against both break-even and the owner's allowance. Say which one you judged them on.

Without that answer, judge every campaign on first-order break-even and say in the report that repeat purchases are not counted, so campaigns that win repeat buyers look worse than they are.

### Conversion lag

Google Ads counts a sale against the day of the click, and sales from the most recent clicks are still arriving when the export is pulled.

- Use the owner's answer to question 7, or 7 days.
- Compare the window's end date with the date the exports were pulled. Ask the owner for that date if they have not given it. If the gap is shorter than the lag, say the reported ROAS is understated, and mark any campaign whose ROAS is between 85% and 100% of break-even "marginal, may be lag" rather than "below break-even".
- When the owner says the lag is a week or more, it usually means a considered purchase. Say that the window catches fewer of the sales those clicks will eventually produce.

---

## Wasted spend

Work from search terms with Cost above zero. Leave out campaigns the owner asked to leave out.

**Set the floor at the store's own numbers, not an arbitrary dollar amount.**

```
waste_threshold = average_order_value_ex_gst × margin_pct
```

Spending more than one order's contribution and getting nothing back is a real leak. Spending $4 is noise.

### Patterns

Split every cost-bearing term into patterns of one, two and three consecutive words. Treat singular and plural as the same word, so "boots" counts as "boot". For each pattern add up Cost, Conversions and `conv_value_ex_gst` across **every** term that contains it, converting or not. A row with a conversion and no cost adds its conversion to the patterns in it.

- **Dead pattern:** total cost above the threshold and fewer than half a conversion in total.
- **Weak pattern:** at least half a conversion, total cost above three times the threshold, and ROAS more than 15% under the store's break-even. Report these as worth a look. Never make one a negative from a CSV alone.
- **Everything else is working.** The store's main product word will carry most of the zero-conversion spend in the account and still be profitable. Never rank patterns by zero-conversion spend.

In a long-tail account no single search term may reach the threshold. That is normal, and it is why the test runs on patterns and not on single terms.

**Keep the shortest.** When one dead pattern sits inside another, keep the shorter one. It is the word doing the damage, and the negative that stops it. Report a family of overlapping patterns as one line. Do this first, then run the catalogue check on what is left.

**Check every dead pattern against what the store sells.** Take the words in the product titles, types, vendors and tags in the products export, with singular and plural treated as the same word. Ignore joining words such as "and", "for", "with", "the" and "to" when you check, and drop a pattern that is nothing but joining words. A dead pattern made only of catalogue words is a slice of things the store sells. It is not waste. It never goes on the negative list and never counts as wasted spend. On a healthy account these slices are chance: test thousands of patterns and a few will land just over the threshold with no sale. Leave them out of the report.

A dead pattern is **wasted** when at least one of its words is not in the catalogue: "repair", "jobs", a retailer's name, a product the store does not stock.

Report the wasted patterns ranked by cost, up to 20 in the table, then up to five weak patterns. The negative list holds every wasted pattern. Where a wasted pattern has part of a conversion to its name, show the fraction beside it. One negative on a pattern stops it for good, which is why only wasted patterns go on the negative list.

```
wasted_spend = cost of every term containing a wasted pattern, each term counted once
```

Google lists only part of the account's searches, so "no conversions" means none in the searches it lists. Say so beside the negative list.

**On a trimmed file, do not run the pattern test.** The cut removes cheap terms that converted, so a pattern can look dead when it is not. Leave the wasted spend score out, and say why.

Classify each wasted pattern by why it wasted money, because the fix differs:

| Type | Example | Fix |
|---|---|---|
| Wrong intent | "how to", "diy", "repair", "instructions" | Negative |
| Wrong buyer | "wholesale", "bulk", "job lot", "supplier", "second hand" | Negative, unless they sell wholesale or used |
| Free and cheap | "free sample", "cheap", "discount code", "coupon" | Negative |
| Competitor and marketplace | "amazon", "ebay", "temu", "kmart", "bunnings" | Negative |
| Employment | "jobs", "careers", "salary" | Negative |
| Adjacent product | a product they do not stock | Negative, and note the gap in case they should stock it |
| Their own brand | see brand leak | Campaign structure, not a negative |

### The seed list

The country blocks in `references/negatives-seed.md` go by where the store sells. Every other block applies to every store.

Check every seed against the account before it goes on the list.

- A seed whose pattern has any conversion credit in this account stays off, and the report names it. This holds even when the pattern counts as dead in the test above. So do its other spellings and its close relatives. If "big w" converted, "bigw" stays off. If "discount code" converted, "promo code", "coupon" and "voucher" stay off.
- A seed that appears in the store's own product titles, types, vendors or tags stays off. "manual" is a negative for most stores and a product word for a store selling manual coffee grinders.
- A seed the owner's answers make unsafe stays off. Store brief question 15 covers the Marketplaces, Second-hand and free, Buy now pay later, Wrong buyer, and Repair and parts blocks. With no answer, leave those blocks off and say so.
- A seed that cost money here and never converted: read the search terms behind it first. If they are plainly buyers, leave it off. Otherwise it goes on.
- A seed that does not appear in the account at all, or only on rows with no cost, is a precaution. It stays off the printed list and is offered on request.

A seed longer than three words, or one with a symbol in it, is checked by searching the terms for it directly.

**When to print the list.** Print a negative list when the account produced wasted patterns of its own, or seeds that cost money here. The list holds those and nothing else: the wasted patterns first, then the seeds that cost money. If the account produced neither, say it has nothing to add. Either way, offer the rest of the seed list on request as a precaution. Never present seeds as a finding, and when the seeds on the list cost only a few dollars between them, say so.

Output one deduplicated, copy-paste-ready list.

**Say what match type to use.** Broad match negatives for single words, phrase for multi-word patterns. Warn that a negative applied at account level applies everywhere. "free" on its own stays off the list, because it blocks "free shipping" searches that often convert. Use the phrases in the seed file.

The pattern test treats singular and plural as one word. A negative keyword does not, so list each form that appears in the search terms.

---

## Reconciliation

Shopify counts every order from every channel. Google Ads counts the ones it takes credit for. Google's count should be below Shopify's, and that gap is not a fault.

Use online store orders in this section, and count every one placed in the window with a Total above zero, including the ones refunded or cancelled since. Google recorded those sales when they were placed. Leaving them out makes Google's share look bigger than it is, and on a store with many returns it can push the share past 100% with nothing wrong.

```
orders_placed = the online store orders placed in the window, Total above zero
value_placed  = sum(Subtotal − tax_in_subtotal) over those orders, before refunds
```

Test three things.

**1. Value per sale.** `conv_value_ex_gst` ÷ Conversions against `value_placed` ÷ `orders_placed`. They should sit within about 15%. "Far" in the table below means further apart than that.

**2. Google's share.** Conversions ÷ `orders_placed`, and `conv_value_ex_gst` ÷ `value_placed`. Report it as "Google Ads takes credit for X% of your online store orders."

**3. Under-tracking.** Window totals cannot show it, because a low share can mean lost tracking or simply a store that sells through other channels. Raise it only when settings check 8 says the tag lived in Additional Scripts, or the owner says Google Ads drives most of their orders and the share is far below that. Then ask for one more download: the campaigns report again with Segment → Time → Month. Work out Google's share of orders for each month.

| What you see | What it usually means |
|---|---|
| Google's share above 100% of orders | Double-counted conversions. The Google & YouTube app installed on top of an existing tag is the most common cause in Shopify stores |
| Value per sale far above Shopify's average order | Conversion value includes shipping or tax, a conversion value rule or the new-customer addition is inflating it, or a multi-currency store is sending local amounts as if they were account currency. A 20,000 won order arriving as $20,000 |
| Value per sale far below Shopify's average order | Part of the order value is not being sent, the Conversions column is counting actions that are not purchases, such as add to cart, or the tag is sending store-currency amounts into an account that bills in a weaker currency |
| Monthly share steps down part-way through the window | Under-tracking. On **26 August 2026** Shopify removed the Additional Scripts box from the thank-you and order status pages for all non-Plus stores, and anything living there stopped firing with no error. A long conversion lag with a window that ends close to the export date also pulls the last month down, so rule that out first |
| Value per sale agrees and the share is steady or plausible | Say so. It is worth telling them. If settings check 8 is unanswered and 26 August 2026 falls inside the window, add that window totals cannot rule lost tracking in or out, and ask check 8 first |

Report the share and the value per sale, then say which of the above it looks like and how to confirm it in the account.

Every other number in the account is steered by what the tag records. If that is wrong, the profit table is wrong too, which is why a proven tracking fault always becomes fix number one.

---

## Scoring

100 points, four sections. Show the owner the breakdown, not just the total, so they can see where they lost points. Left-out campaigns do not count towards any section. A share that lands exactly on a boundary takes the row that starts with it.

### Brand leak, 25 points

| Brand share of spend | Points |
|---|---|
| Under 10% | 25 |
| 10 to 20% | 18 |
| 20 to 30% | 10 |
| 30 to 45% | 4 |
| Over 45% | 0 |

Brand share here is all brand spend ÷ total account spend. A campaign built for the brand counts in full, and total account spend includes campaigns that have no search terms.

If the store has no brand campaign and no Performance Max, award 25 and say the section does not apply yet.

### Profit, 25 points

Start at 25. Subtract:

- 3 points for every full 10% of spend sitting in campaigns below break-even, to a floor of 0. Campaigns marked "may be lag" do not count, and neither do campaigns treated as finding new customers.
- 5 points if no cost per item is filled in at all, because the store cannot see profit on any channel, not just this one.

If "bid higher for new customers" is on and no Original conv. value column was supplied, say beside the score that it is overstated. If shipping cost was left out of the margin, say beside the profit score that it rests on a margin with no shipping cost in it.

### Wasted spend, 20 points

| Wasted spend as share of total | Points |
|---|---|
| Under 5% | 20 |
| 5 to 10% | 15 |
| 10 to 20% | 8 |
| Over 20% | 0 |

Where wasted spend is `wasted_spend` from the Wasted spend section, as a share of total account spend.

### Settings and tracking, 30 points

Three points for each of the ten checks in `references/settings-check.md`. A check that cannot apply to the account passes. An unanswered check is not a fail.

### What could not be assessed

An unanswered settings check is not a failure, and neither is a section that could not run because a file was missing or trimmed. Leave those points out of both the score and the total. Report the score as points earned out of points assessed, for example "48 of 54 points assessed", and list what was left out. In the table, show a part-assessed section against the points assessed, as "3 of 6 assessed", and mark a section that could not run as left out. When points were left out, do not print a figure out of 100.

Give a band only when at least 70 of the 100 points were assessed. With fewer assessed, give no band and say what is missing. To pick the band, scale the points earned to 100 and round to a whole number.

When settings checks are unanswered, the band stands on what was assessed. Put it in the score heading that way, as "Tight, on what has been checked so far", and say how many checks and how many points are still open. The settings section names them. Leave out the band's "what to say" line, because it speaks for checks nobody has answered. Do not work out what the score would be if every open check failed, and do not name the band that would give. An unanswered question is not a finding, and a worst case attached to a clean account reads like one.

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

Give three when three are worth an owner's hour. On a tidy account give fewer, and say the account is tidy. Never pad.

For each fix, give:

1. What to do, in one sentence, specific enough to act on today.
2. The estimated dollars at stake over the next 90 days, with the working shown. If the window is not 90 days, scale it to 90.
3. How long it takes, honestly. "Twenty minutes" or "half a day with your developer."
4. What to check first to confirm the finding is real.

If a tracking fault is proven in the reconciliation, or settings check 8 fails on the owner's own answer, **it is always fix number one**, regardless of dollar size, because every other number in the account is downstream of it. A low share of orders on its own is not proof.

The gap between Conv. value and Original conv. value is reported value the store never received. No money was spent on it, so it is never the headline leak and never counted as dollars recovered. A fix for settings check 4 or 7 carries no dollar estimate. Say so, and place it after the fixes that have one.

Check each fix against the store brief before you write it. A fix that cuts a campaign the owner said is there to find new customers, or breaks up a group they said works as one, is the wrong fix.

---

## About the thresholds

The scoring bands are reasoned from first principles and from the sources cited above, not fitted to a benchmark set. They are deliberately conservative, because a scan that manufactures a finding on a healthy account is worse than one that misses a small leak.

If you are forking this, the bands are the first thing to change. Set them against the accounts you actually work on.

# The ten-point settings and tracking check

Three points each, thirty in total.

Some of these you can answer from the exports. Most you have to ask, because a CSV does not contain settings.

**Ask them one at a time, in plain language, and wait for the answer.** Do not fire ten questions at once, and do not assume a "no" when someone does not answer. An unanswered check scores zero and is reported as unanswered, not as failed. Say which ones were unanswered at the end.

For each check: what it is, how to see it, why it costs money, and what a good answer looks like.

---

## 1. Does Performance Max exclude your brand?

**Ask:** "In your Performance Max campaign, have you added your brand name as a negative keyword, or asked Google to apply brand exclusions?"

**Where to look:** Campaign → Settings → Brand exclusions, and Campaign → Keywords → Negative keywords.

**Why it matters:** Performance Max bids on your brand by default and reports every one of those sales as a win. It is the single largest and most common leak in a Shopify account, and it is invisible unless you go looking, because the campaign reports a beautiful ROAS while doing it.

**Good answer:** brand excluded from PMax, and brand traffic handled by a separate campaign the owner controls, or deliberately left in with a reason.

**Note:** brand exclusions in PMax are not perfect and leak at the edges. Account-level negatives are the stronger control where available.

---

## 2. Do your campaigns have negative keyword lists?

**Ask:** "Do you have a shared negative keyword list applied to your campaigns, and when did you last add to it?"

**From the data:** if the search terms report is full of obvious waste, the answer is effectively no regardless of what they say.

**Why it matters:** without negatives, broad match and PMax will keep finding new ways to spend on searches that were never going to buy. It is the cheapest fix in the account.

**Good answer:** a shared list exists, and it was added to in the last 90 days.

---

## 3. Are you excluding your existing customers where you should be?

**Ask:** "Have you uploaded your Shopify customer list to Google Ads, and are you using it to exclude or bid differently on people who have already bought?"

**Why it matters:** two different problems. Prospecting campaigns paying to reach existing customers is waste. More importantly, without a customer list Google cannot tell new from returning, so it cannot optimise for new customers and neither can you.

**Good answer:** customer list uploaded and refreshing, used at minimum for reporting.

---

## 4. Is new customer acquisition mode switched on?

**Ask:** "In your Performance Max or Shopping campaign, is 'Customer acquisition' set to bid higher for new customers, or to only bid for new customers?"

**Why it matters:** without it, the campaign will happily spend its budget re-buying people who were already yours, because they are the cheapest conversions available. This is the setting that makes an account chase growth rather than harvest it.

**Good answer:** on, in "bid higher for new customers" mode, with a value set. "New customers only" is aggressive and appropriate for fewer stores.

**Depends on:** check 3. This does not work without a customer list.

---

## 5. Are Shopping and Performance Max fighting over the same products?

**Ask:** "Do you run both a Standard Shopping campaign and a Performance Max campaign, and do they contain the same products?"

**From the data:** look for the same search terms appearing in both campaigns in the search terms export. That is the tell.

**Why it matters:** where they overlap, Performance Max usually wins the auction, which means the campaign you can see and control loses to the one you cannot. You lose visibility without gaining anything.

**Good answer:** either the product sets are separated, or Standard Shopping is used deliberately for a defined group with PMax excluded from it.

---

## 6. Has anything been added to your product feed beyond what Shopify sends?

**Ask:** "Has anyone written your product titles for Google specifically, or filled in fields like product highlights, cost of goods or custom labels in Merchant Center?"

**Why it matters:** Shopping and PMax do not use keywords. Google matches a search to your product title. Shopify's native sync sends the basics and locks the rest, so most stores run on titles written to look nice on a product page rather than to match what people search.

This is the half of the account nobody opens, and on many stores it is the largest untouched lever in the whole scan.

**Good answer:** titles follow brand plus product type plus key attributes, and at least product highlights and custom labels are populated.

---

## 7. Does your conversion value include tax and shipping?

**Ask:** "When Google Ads reports a $100 sale, is that $100 the product price, or does it include GST and delivery?"

**From the data:** compare the average conversion value in the Google Ads export to the average order subtotal in Shopify. If Google's is consistently around 10% higher in Australia, tax is in there.

**Why it matters:** every ROAS target is set against this number. If it includes tax and shipping, every campaign looks more profitable than it is, and the break-even calculation in this report is set against an inflated figure.

**Good answer:** conversion value is the subtotal, excluding tax and shipping.

---

## 8. Did your tracking survive 26 August 2026?

**Ask:** "Was your Google Ads conversion tag ever pasted into the Additional Scripts box on your Shopify order status page, and did conversions drop in late August?"

**From the data:** this is what the reconciliation section tests. A conversion count well below Shopify's order count is the signature.

**Why it matters:** on **26 August 2026** Shopify removed the Additional Scripts box from the thank-you and order status pages for every non-Plus store. Anything living there was removed rather than migrated, with no error shown and no warning email. Google Ads tags, Meta pixels, GTM containers and affiliate scripts all stopped firing that day.

If it happened, every bid decision made since has been made on wrong numbers.

**Good answer:** tracking runs through a web pixel under Settings, Customer events, or the official Google & YouTube app, and the conversion count reconciles to orders.

**If this check fails, it is fix number one in the report regardless of dollar size.**

---

## 9. Are Demand Gen and Performance Max competing?

**Ask:** "Do you run Demand Gen as well as Performance Max?"

**Why it matters:** both serve across YouTube, Discover and Gmail. Run together without thought, they bid against each other for the same impression and you pay for the privilege. It is a real problem but a smaller one than checks 1, 7 and 8, so do not lead with it.

**Good answer:** either only one runs, or they are separated by audience and measured separately.

---

## 10. Are search partners on?

**Ask:** "In your Search campaigns, is the Google search partners network switched on?"

**Why it matters:** search partners traffic converts differently and generally worse, and it is on by default. It rarely accounts for more than a few percent of spend, so check it and move on.

**Good answer:** either off, or on with the performance segmented and reviewed.

---

## Reporting the check

Show it as a simple pass, fail or unanswered list with the three-point value against each. Then write one paragraph on the two that cost the most money, and leave the rest as a list.

Do not write a paragraph on all ten. Nobody reads that.

Order the write-up by money at stake, which is usually:

1. Check 8 (tracking) when it fails, because it invalidates everything else
2. Check 1 (PMax brand)
3. Check 7 (conversion value)
4. Check 6 (feed)
5. Everything else

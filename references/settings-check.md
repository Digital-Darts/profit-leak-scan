# The ten-point settings and tracking check

Three points each, thirty in total.

Some of these you can answer from the exports. Most you have to ask, because a CSV does not contain settings.

**Ask them one at a time, in plain language, and wait for the answer.** Go in number order, except that check 8 comes first when 26 August 2026 falls inside the window. Do not fire ten questions at once, and do not assume a "no" when someone does not answer. An unanswered check is left out of the score and reported as unanswered, not as failed. "Not sure" counts as unanswered. A check that cannot apply to the account passes. Say which ones were unanswered at the end.

If the owner wants the report before answering, write it with those checks left out, and offer to ask them afterwards.

Swap the dollar sign in any scripted question for the store's own currency symbol.

If the store brief already answered a check, use that answer and do not ask again. Question 4 of the brief answers check 7, and question 14 answers check 4.

For each check: what it is, how to see it, why it matters, and what a good answer looks like.

---

## 1. Does Performance Max exclude your brand?

**Ask:** "In your Performance Max campaign, have you added your brand name as a negative keyword, or asked Google to apply brand exclusions?"

**Where to look:** Campaign → Settings → Brand exclusions, and Campaign → Keywords → Negative keywords.

**Why it matters:** Performance Max bids on your brand by default and reports every one of those sales as a win. It is the single largest and most common leak in a Shopify account, and it is invisible unless you go looking, because the campaign reports a beautiful ROAS while doing it.

**From the data:** add up the search terms containing the brand on rows where Match type says "Performance Max". If they take more than a tenth of Performance Max's listed spend, the brand is not excluded, and the check fails. Under a tenth, the data cannot settle it, because a small brand takes a small share with or without an exclusion. Say how many dollars, and score the check on the owner's answer. If the brand name on its own, with no other words, appears on those rows in any spelling you counted, say so. An exclusion normally stops that search, so the owner should open the setting and look. No such rows, in a file that has Performance Max rows, is a pass.

**Good answer:** brand excluded from PMax, and brand traffic handled by a separate campaign the owner controls, or deliberately left in with a reason. Brand excluded with no brand campaign at all also passes. The store has decided not to pay for its own name.

**Note:** brand exclusions in PMax are not perfect and leak at the edges. Account-level negatives are the stronger control where available.

---

## 2. Do your campaigns have negative keyword lists?

**Ask:** "Do you have a shared negative keyword list applied to your campaigns, and when did you last add to it?"

**From the data:** if wasted spend, as `method.md` § Wasted spend works it out, is more than a tenth of account spend, the answer is effectively no, whatever they say. A clean search terms report does not pass the check. It stays on the owner's answer.

**Why it matters:** without negatives, broad match and PMax will keep finding new ways to spend on searches that were never going to buy. It is the cheapest fix in the account.

**Good answer:** a shared list exists, and it was added to in the last 90 days.

---

## 3. Is your customer list in Google Ads and up to date?

**Ask:** "Have you uploaded your Shopify customer list to Google Ads, and does it stay up to date?"

**Why it matters:** without a customer list Google cannot tell a new customer from a returning one. You cannot see how much of each campaign's sales are new business, and a campaign built to find new customers cannot leave existing ones out.

**Good answer:** customer list uploaded and refreshing, used at minimum for reporting.

---

## 4. Is new customer acquisition off on the campaigns that catch existing demand?

**Ask:** use the answer to store brief question 14. If it was skipped: "Is Customer acquisition switched on in any campaign? If so, which campaigns, and is it set to bid higher for new customers or to only bid for new customers?" "Not sure" leaves this check unanswered. For the value column, the scan then assumes the setting is off and says so.

**Where to look:** each campaign's Settings, under Customer acquisition. The value added for a new customer is set once for the whole account, under Goals.

**From the data:** when an export has both Conv. value and Original conv. value, the gap between them is what Google has added. No gap on any campaign means nothing is being added, so "bid higher for new customers" is not inflating the figures. Say so. It does not answer the check on its own, because "only bid for new customers" adds nothing to the value either. A gap on a campaign that catches existing demand means "bid higher" is on there, or a conversion value rule applies. Ask which before scoring it.

**Why it matters:** in "bid higher for new customers" mode Google adds the value you entered to every sale it counts as a new customer. A $200 order with a $100 new-customer value is reported as $300, so ROAS and every target set against it include money the store never received ([source](https://support.google.com/google-ads/answer/16090064)). The Original conv. value column shows the figure without the addition. "Only bid for new customers" adds nothing to the value.

The setting also does little on a campaign that catches existing demand. What makes a sale new business is what the person searched, and returning customers search for products too. New customers come from the structure: brand split from generic, and prospecting in its own campaign.

**Good answer:** off on every campaign whose job is to catch existing demand. Take each campaign's job from the store brief. With no answer, treat Performance Max, Shopping and Search as catching demand and Demand Gen as finding new customers. On a campaign that is there to find new customers, either mode passes.

**Scoring:** one demand-capture campaign with the setting on fails the check. The value entered is not scored, because the scan cannot verify it.

**Depends on:** check 3. Google cannot tell new from returning without a customer list. If check 3 fails, say so beside this one. This check is still scored on its own answer.

---

## 5. Do Shopping and Performance Max carry the same products?

**Ask:** "Do you run both a Standard Shopping campaign and a Performance Max campaign, and do they contain the same products?"

**From the data:** look for the same search terms appearing in both campaigns in the search terms export. That is the tell. If no Standard Shopping campaign had spend in the window, the check passes.

**Why it matters:** when both campaigns carry the same product, Google shows whichever has the higher Ad Rank for each search ([source](https://support.google.com/google-ads/answer/15535462)). Before October 2024 Performance Max always won. Shopping campaign priority does not settle it, because priority only decides between Standard Shopping campaigns. The product's sales and data are split across two campaigns that bid differently, and the report shows which campaign got each sale but not whether the other would have won it anyway.

**Good answer:** either the product sets are separated, or Standard Shopping is used deliberately for a defined group with PMax excluded from it.

---

## 6. Has anything been added to your product feed beyond what Shopify sends?

**Ask:** "Has anyone written your product titles for Google specifically, or filled in fields like product highlights, cost of goods or custom labels in Merchant Center?"

**Why it matters:** Shopping and PMax do not use keywords. Google matches a search to your product title. Shopify's native sync sends the basics and locks the rest, so most stores run on titles written to look nice on a product page rather than to match what people search.

This is the half of the account nobody opens, and on many stores it is the largest untouched lever in the whole scan.

**Good answer:** titles follow brand plus product type plus key attributes, and at least product highlights and custom labels are populated.

---

## 7. Does your conversion value include tax and shipping?

**Ask:** "When Google Ads reports a $100 sale, is that $100 the product price, or does it include tax (GST, VAT or sales tax) and delivery?"

**From the data:** run the test in `method.md` § Same footing. Compare Google's value per conversion with Shopify's average order, both tax-inclusive and ex tax. Use Original conv. value when the export has it, so that a new-customer amount Google has added is not mistaken for tax or shipping. Most Australian, New Zealand and UK stores have the tax inside their Shopify prices, so Shopify's Subtotal already includes it. A Google figure that matches Subtotal is therefore usually tax-inclusive, not clean.

**Why it matters:** every ROAS target is set against this number. If it includes tax and shipping, every campaign looks more profitable than it is. The scan takes the tax out before doing any maths, but the targets set inside Google Ads are still set against the inflated figure.

**Good answer:** conversion value is the product value after discounts, excluding tax and shipping. A tax-inclusive value still scores as a fail, but say it is workable as long as every target set in Google is raised to match. `method.md` § Same footing gives the figure. If the basis had to be assumed, this check is unanswered. If the test could not separate two bases that both include tax, it fails.

---

## 8. Did your tracking survive 26 August 2026?

**Ask:** "Was your Google Ads conversion tag ever pasted into the Additional Scripts box on your Shopify order status page, and did conversions drop in late August?"

**From the data:** window totals cannot show it. Shopify counts every channel, so Google's count sitting below Shopify's is normal. If the answer here points to a fault, ask for the campaigns report split by month and compare Google's share of orders month by month, as `method.md` § Reconciliation describes.

**Why it matters:** on **26 August 2026** Shopify removed the Additional Scripts box from the thank-you and order status pages for every non-Plus store. Anything living there was removed rather than migrated, with no error shown and no warning email. Google Ads tags, Meta pixels, GTM containers and affiliate scripts all stopped firing that day.

If it happened, every bid decision made since has been made on wrong numbers.

**Good answer:** tracking runs through a web pixel under Settings, Customer events, or the official Google & YouTube app, and the conversion count reconciles to orders.

**If this check fails on the owner's own answer, checking the tag is fix number one in the report, regardless of dollar size.** The month-by-month test confirms it. A Shopify Plus store kept the box and passes.

---

## 9. Do Demand Gen and Performance Max reach the same people?

**Ask:** "Do you run Demand Gen as well as Performance Max? If you do, does Demand Gen leave out people who have already visited or bought?"

**From the data:** the search terms report has a Total row for each campaign type. If only one of the two had spend, the check passes.

**Why it matters:** both can show on YouTube, Discover, Gmail, Maps and the Display Network. Within one account Google picks one campaign per impression by Ad Rank, so you do not bid up your own price ([source](https://support.google.com/google-ads/answer/13810170)). The cost is in the reporting: the same people are reached by both, credit for a sale can land on either campaign, and neither can be judged on its own. This ranks below checks 1, 7 and 8, so do not lead with it.

**Good answer:** either only one runs, or they are separated by audience and measured separately.

---

## 10. Are search partners on?

**Ask:** "In your Search campaigns, is the Google search partners network switched on?"

**Why it matters:** search partners traffic converts differently and generally worse, and it is on by default. It rarely accounts for more than a few percent of spend, so check it and move on.

**Good answer:** either off, or on with the performance segmented and reviewed. An account with no Search campaign passes.

---

## Reporting the check

Show it as a simple pass, fail or unanswered list with the three-point value against each. Then write a paragraph on up to two that matter most, and leave the rest as a list. If none stands out, the list is enough.

Do not write a paragraph on all ten. Nobody reads that.

Order the write-up by money at stake, which is usually:

1. Check 8 (tracking) when it fails, because it invalidates everything else
2. Check 1 (PMax brand)
3. Check 7 (conversion value), and check 4 when "bid higher" is adding to it
4. Check 6 (feed)
5. Everything else

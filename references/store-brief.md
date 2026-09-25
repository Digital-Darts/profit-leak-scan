# Store brief

The questions to ask before any files arrive, and what each answer changes.

Exports tell you what happened in the account. They do not tell you what each campaign is for, what the store earns on a sale, or which customers come back. Without those answers the report is generic. With them it fits the store.

**Show all the questions in one message.** Say every answer is optional and that "not sure" is fine. Do not ask them one at a time. One at a time is for the settings check.

If the owner has pasted a brief, a strategy document or notes about the store, read that first and ask only what it leaves out.

---

## The questions

Show these to the owner as written.

> Before you upload anything, a few questions about your store. Answer what you can and skip the rest. "Not sure" is a fine answer, and every answer you give makes the recommendations fit your store better.
>
> 1. Your brand name, and any misspellings people use for it. *(This one I need.)*
> 2. Brands you stock but don't own, and any competitors people might search for instead of you.
> 3. Do your Shopify prices include GST? Yes, no or not sure.
> 4. When Google Ads records a $100 sale, does that $100 include GST? Does it include delivery?
> 5. Roughly what does an average order cost you to ship?
> 6. Roughly what percentage of an average order is left after product cost, shipping and payment fees?
> 7. How long do people usually take between first clicking an ad and buying? Same day, a few days, or a week or more?
> 8. What is each campaign for? For example "main sales campaign", "protects our brand name", "finds new customers" or "wins back past visitors".
> 9. Which products does each campaign mainly sell? A brand, product type or tag is enough. "Everything" is a fine answer.
> 10. Any campaigns I should leave out of the recommendations, and why?
> 11. Any campaigns that work as one group? For example, best sellers split out from the rest of the range, or one campaign per margin tier.
> 12. Which products bring in new customers who come back and buy again? If you are willing to break even or lose a little on a first order to win them, how much?
> 13. Anything unusual in the window? A sale, stock running out, a site change, a tracking change.

---

## What each answer changes

| # | Used for | If there is no answer |
|---|---|---|
| 1 | Brand matching and the safety check in `method.md` | Ask again. The brand leak section cannot run without it |
| 2 | The stocked-brand and competitor classes in brand matching | Treat those searches as generic |
| 3 | Taking GST out of Shopify revenue (`method.md` § Same footing) | Work it out from the orders export. The method says how |
| 4 | Taking GST out of Google's conversion value, and settings check 7 | Work it out from the data. If the data cannot tell, assume it matches the Shopify price basis and say so |
| 5 | Shipping cost in the margin | Leave shipping out and say every profit figure is therefore optimistic |
| 6 | The margin when cost per item is missing, and a cross-check when it is not | Work it out from cost per item. With neither, the profit section cannot run |
| 7 | Conversion lag (`method.md` § Using the store brief) | Assume 7 days |
| 8 | How each campaign is judged | Treat every campaign as a sales campaign and say so |
| 9 | Margin per campaign | Use the store margin for every campaign, and say that break-even is then the same for all of them |
| 10 | Leaving campaigns out of flags and fixes | Include everything |
| 11 | Reporting and judging campaigns as a group | Report each campaign on its own |
| 12 | Allowing a first-order loss on campaigns that win repeat customers | Judge every campaign on first-order break-even, and say repeat purchases are not counted |
| 13 | Explaining numbers that look odd | Nothing |

Every default you use goes in the "what this is built on" lines at the top of the report.

## When the owner's answer and the data disagree

Say so, show both, and use the data for the maths. The two usual cases:

- **Margin.** The owner says 45% and cost per item works out at 32%. Their figure may leave out shipping or fees, or the export may be missing costs they know about. Use the calculated figure, show theirs beside it, and ask which is closer.
- **GST.** The owner says conversion value excludes GST and the data says it includes it. Use the data and flag it. This is settings check 7 failing, and it is worth a line in the headline section.

# Profit Leak Scan

**A campaign at 6x return can still lose you money. This finds the ones where it does.**

Three exports, ten minutes, a score out of 100.

An AI skill that runs on your own data inside your own Claude, ChatGPT or Gemini account. Nothing is uploaded to us. We host a file, not a service.

Built by [Digital Darts](https://www.digitaldarts.com.au/services/google-ads). Shopify-only since 2015, Google Partner, more than a thousand accounts audited.

---

## The gap it looks for

Google reports a sale. Your bank reports something different. The difference is where this scan works.

A campaign at 6x return sounds healthy. Take out what the products cost, what shipping cost, what the payment processor took, and it can sit under water.

You can push cost of goods into Merchant Center and turn on cart data reporting, and you should. That gets you gross profit per campaign. It still stops before outbound shipping, payment fees and returns, which is where a thin campaign usually goes under.

This joins your ad spend to the Shopify orders and the cost per item behind them, and carries on past where the ad platform stops.

## What it reports

| | |
|---|---|
| **Brand leak** | What you spent, per campaign, on people searching your own name. In dollars. Performance Max reported separately, because that is where it hides |
| **Break-even ROAS** | Per campaign, from your real margin instead of Google's suggested target. Campaigns below the line get flagged, including ones showing a healthy return |
| **Profit on ad spend** | POAS and contribution per campaign, using cost per item where you have it filled in |
| **Wasted spend** | The word patterns eating money across your search terms, plus a negative keyword list ready to paste. Australian seeds included: Afterpay, Zip, Temu, Kmart, Bunnings, Gumtree |
| **Reconciliation** | Google Ads conversions against Shopify orders, and what the gap between them means |
| **Ten-point check** | Structure and tracking, including whether your tags survived Shopify removing Additional Scripts on 26 August 2026 |
| **A score out of 100** | Plus the three fixes for this week, ranked by dollars recovered per hour of work |

The third row is the one to care about. Joining your Shopify cost per item to your Google Ads spend gives you margin per campaign rather than one blended figure for the account. That is what catches a clearance campaign running at 4.6x that needs 4.55x to break even.

## What it will not do

It cannot see inside your account.

It reads exports, so it cannot check a setting you haven't told it about, cannot see your product feed, cannot see your Merchant Center status, and cannot see what changed last month.

**Every figure it gives you is an estimate.** Before you change a bid, open the account and confirm the top finding with your own eyes. That is how we treat it internally too. The scan tells you where to look.

It will not promise you a result, and neither will we.

## Install

Two minutes. Full steps in [INSTALL.md](INSTALL.md).

**Claude:** Settings → Capabilities → Skills → Upload skill → pick the zip. Don't unzip it first.

**ChatGPT:** new Project, paste `SKILL.md` into the instructions, add the `references` files.

**Gemini:** new Gem, same thing.

Then say **run the profit leak scan** and upload your exports when it asks.

## What you need

Three CSVs covering the same 90 days.

1. Google Ads campaigns report
2. Google Ads search terms report, with Performance Max search categories switched on
3. Shopify orders export

Worth adding: your Shopify products export, which carries **cost per item**. Without it the scan asks for one blended margin percentage and labels everything downstream an estimate.

If that field is empty across your catalogue, it is worth an afternoon. Without it, nothing can tell you what a product actually earns you.

## Why it exists

The first hour of every new client audit we run looks the same.

Pull the search terms. Pull the campaigns. Pull the orders. Find the gap between what Google reports and what the store keeps.

We have done it more than a thousand times and the same leaks turn up in most accounts. So we wrote the hour down and gave it away.

---

## Want someone inside the account instead?

We will audit it free, and guarantee to find at least three ways it leaks cash.

That is a guarantee about what we will find, not about what you will earn. Nobody honest promises the second one.

**[Book a call](https://www.digitaldarts.com.au/services/google-ads)**

---

## Files

```
SKILL.md                      the instructions the AI reads
INSTALL.md                    setup for Claude, ChatGPT and Gemini
references/
  method.md                   every calculation, in order
  negatives-seed.md           AU and NZ negative keyword seeds
  settings-check.md           the ten checks and how to answer them
  glossary.md                 plain-English definitions
  example-report.md           output format (invented numbers)
```

## Licence

Profit Leak Scan © 2026 Digital Darts, licensed under [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/).

Fork it, change the thresholds, run it on client accounts, charge for the work you do with it.

Two conditions. Credit Digital Darts where people can see it and say what you changed. If you publish your version, it carries this same licence.

## Contributing

The weakest part is brand matching on stores whose name is an ordinary word. A store called Ace or Pure gets a wildly inflated leak number unless you catch it, and the current answer is a phrase-match fallback that reports a range instead of a figure.

If you have something better than that, it is the pull request we want.

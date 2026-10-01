# Profit Leak Scan

**A campaign at 6x return can still lose you money. This scan finds the losers.**

Pull your exports from Google Ads and Shopify, answer a few questions about your store, and get back a score out of 100 with up to three fixes worth doing this week.

An AI skill that runs on your own data inside your own Claude, ChatGPT or Gemini account. Nothing is uploaded to us. We host a file, not a service.

**[Download profit-leak-scan.zip](https://github.com/Digital-Darts/profit-leak-scan/releases/latest/download/profit-leak-scan.zip)** · [Step-by-step setup](INSTALL.md)

Built by [Digital Darts](https://www.digitaldarts.com.au/services/google-ads). Shopify-only since 2015, Google Partner, more than a thousand accounts audited.

---

## Before you begin

The scan finds real leaks only when it has real numbers. Check you have these before you start:

- A Google Ads account with spend in the last 90 days
- Google Ads recording **what each sale was worth**, not only that it happened. If the Conv. value column is $0 or blank, the scan can't work out profit
- Access to export from Google Ads, and a Shopify login that can export orders and products
- **Cost per item** filled in on most products in Shopify, or a rough idea of your margin after product cost, shipping and payment fees
- Your brand name, and how people misspell it
- About 30 minutes the first time

[INSTALL.md](INSTALL.md) has the full checklist, including what to do when something is missing.

## The gap it looks for

Google reports a sale. Your bank reports something different. The difference is where this scan works.

A campaign at 6x return sounds healthy. Take out the GST or VAT, what the products cost, what shipping cost and what the payment processor took, and it can sit under water.

You can push cost of goods into Merchant Center and turn on cart data reporting, and you should. Google then reports gross profit per campaign, but that figure stops before outbound shipping, payment fees and returns, which is where a thin campaign usually goes under.

This free scan joins your ad spend, Shopify orders and cost per item, then takes off GST or VAT, shipping and fees, so you can see what each campaign earns you.

## What it reports

| | |
|---|---|
| **Brand leak** | What you spent, per campaign, on people searching your own name. In dollars. Performance Max reported separately, because that is where it hides |
| **Break-even ROAS** | Per campaign, from your real margin instead of Google's suggested target. Campaigns below the line get flagged, including ones showing a healthy return |
| **Profit on ad spend** | POAS and contribution per campaign, after GST or VAT, product cost, shipping and payment fees |
| **Wasted spend** | The word patterns eating money across your search terms, plus a negative keyword list ready to paste. Seeds for Australia, New Zealand, the UK and the US, each checked against your own account before it goes on the list |
| **Reconciliation** | What Google records per sale against your average order, and the share of your orders Google takes credit for |
| **Ten-point check** | Structure and tracking, including whether your tags survived Shopify removing Additional Scripts on 26 August 2026 |
| **A score out of 100** | Plus the fixes for this week, three at most, ranked by dollars recovered per hour of work |

Break-even is worked out per campaign when you tell the scan which products each campaign sells. Stocked brands on a 16% margin need 6.25x to break even. Own-label products on a 50% margin need 2x. An account-wide target of 2.5x calls a stocked-brands campaign at 5.5x a winner, and it is losing money.

## What it will not do

The scan reads exports and cannot see inside your account. It cannot check a setting you haven't told it about, and it cannot see your product feed, your Merchant Center status or what changed last month.

It also doesn't know your business until you tell it. How long customers take to buy, which campaigns are there to find new customers, which campaigns work as a pair, and which products bring customers back all change what the right fix is. The scan asks about each of these before it starts. Skip them and the recommendations stay general.

**Every figure it gives you is an estimate.** Before you change a bid, open the account and confirm the top finding with your own eyes. The scan tells you where to look.

## Get started

1. Check the list in [Before you begin](#before-you-begin).
2. **[Download profit-leak-scan.zip](https://github.com/Digital-Darts/profit-leak-scan/releases/latest/download/profit-leak-scan.zip).** For Claude, don't unzip it.
3. Add it to your AI. In Claude (Chat, Cowork or Code), open **Customize** in the left-hand menu → **Skills** → **Yours** → **+** → **Create skill** → **Upload a skill**. ChatGPT and Gemini steps are in [INSTALL.md](INSTALL.md).
4. Pull your four exports, two from Google Ads and two from Shopify, following [INSTALL.md](INSTALL.md) step by step.
5. Start a new chat and type **run the profit leak scan**.

## What you need

Four CSV files, all covering the same 90 days. Two come from Google Ads and two from Shopify.

| # | File | Comes from | Needs |
|---|---|---|---|
| 1 | Campaigns report | Google Ads | Conv. value, and Original conv. value if your account offers it. [Step 4](INSTALL.md#step-4-google-ads-the-campaigns-report-file-1) |
| 2 | Search terms report | Google Ads | The same two columns, and a filter for Cost greater than 0. [Step 5](INSTALL.md#step-5-google-ads-the-search-terms-report-file-2) |
| 3 | Orders | Shopify | Exported by date. [Step 6](INSTALL.md#step-6-shopify-orders-file-3) |
| 4 | Products | Shopify | Cost per item. [Step 7](INSTALL.md#step-7-shopify-products-file-4) |

No cost per item? Skip file 4 and the scan will ask for your margin instead, then label every profit figure an estimate.

## Why it exists

The first hour of every new client audit we run looks the same.

Pull the search terms. Pull the campaigns. Pull the orders. Find the gap between what Google reports and what the store keeps.

We have done it more than a thousand times and the same leaks turn up in most accounts. So we wrote the process down and gave it away.

---

## Want someone inside the account instead?

We will audit it free, and guarantee to find at least three ways it leaks cash.

That is a guarantee about what we will find, not about what you will earn. What you earn from the fixes is up to you.

**[Book a call](https://www.digitaldarts.com.au/services/google-ads)**

---

## Files

```
SKILL.md                      the instructions the AI reads
INSTALL.md                    setup for Claude, ChatGPT and Gemini, and how to pull each export
references/
  store-brief.md              the questions the scan asks about your store
  method.md                   every calculation, in order
  negatives-seed.md           negative keyword seeds for AU, NZ, the UK and the US
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

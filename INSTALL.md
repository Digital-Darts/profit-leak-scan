# Install the Profit Leak Scan

Two minutes. No coding. Pick whichever AI you already use.

Your exports never leave your own account. This is a set of instructions the AI reads, not a service we run.

---

## Claude

1. Go to [claude.ai](https://claude.ai) → **Settings** → **Capabilities** → **Skills**.
2. Click **Upload skill** and select `profit-leak-scan.zip`. Do not unzip it first.
3. Start a new chat and type: **run the profit leak scan**.

Claude will ask for your exports. Upload them when it does.

Works on Claude Pro, Max, Team and Enterprise. On the free plan, use the ChatGPT or Gemini method below, or paste `SKILL.md` into a Project.

---

## ChatGPT

1. Unzip the file.
2. Go to [chatgpt.com](https://chatgpt.com) → **Projects** → **New project**. Call it "Profit Leak Scan".
3. Open the project → **Instructions** → paste the entire contents of `SKILL.md`.
4. Upload the four files from the `references` folder to the project's files.
5. Start a chat inside the project and type: **run the profit leak scan**.

Needs ChatGPT Plus or better for file uploads and Projects.

---

## Gemini

1. Unzip the file.
2. Go to [gemini.google.com](https://gemini.google.com) → **Gems** → **New Gem**. Call it "Profit Leak Scan".
3. Paste the entire contents of `SKILL.md` into the instructions box.
4. Add the four `references` files as knowledge files.
5. Save, open the Gem, and type: **run the profit leak scan**.

---

## Pulling your three exports

About five minutes. Use **the same 90-day window for all three**, or the numbers will not line up.

### 1. Google Ads, campaigns

Google Ads → **Campaigns** → set the date range to the last 90 days → the download icon, top right → **.csv**.

### 2. Google Ads, search terms

Google Ads → **Insights and reports** → **Search terms** → same 90 days.

**Before you download, turn on "Include Performance Max search categories"** in the report settings. Without it you will miss where most of the brand spend hides.

If the file is enormous, sort by Cost, highest first, and keep the top 2,000 rows.

### 3. Shopify, orders

Shopify admin → **Orders** → filter to the same 90 days → **Export** → **Current search** → **CSV for Excel, Numbers, or other spreadsheet programs**.

Shopify emails you the file. It usually arrives within a minute.

### 4. Shopify, products (optional but worth it)

Shopify admin → **Products** → **Export** → **All products** → CSV.

This is where your **cost per item** lives, and it is what turns the profit section from an estimate into a number. If you have never filled that field in, skip this file and the scan will ask you for a single margin percentage instead.

If that field is empty across your catalogue, it is worth an afternoon. Without it, nothing can tell you what a product actually earns you.

---

## If you get stuck

Open an issue and we will help.

If your files are too big to upload, say so in the chat and the scan will tell you how to cut them down.

---

## What it will not do

It cannot see inside your account, so it cannot check a setting you do not tell it about, and it cannot see your product feed, your Merchant Center status or anything that changed last month.

Every figure it produces is an estimate built from exports. Before you change a bid, open the account and confirm the top finding with your own eyes.

That is exactly how we treat it internally too. The scan tells you where to look.

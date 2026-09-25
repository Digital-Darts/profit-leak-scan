# Set up the Profit Leak Scan

No coding. Allow about 30 minutes the first time: 5 to install, 15 to pull your exports, and 10 for the scan to ask its questions and write the report.

Your exports stay in your own AI account. The scan is a set of instructions your AI reads, not a service we run.

Menu names were checked in September 2026. Google and Shopify move things around. If a menu below doesn't match what you see, type the page name into the search bar at the top of Google Ads, or at the top of your Shopify admin.

---

## Before you begin

Tick these off first. Each one says what happens if you can't.

- [ ] **Google Ads has spent money in the last 90 days.** Nothing to scan otherwise. Under a few thousand dollars a month, the negative keyword list and the settings check will do more for you than the profit maths.
- [ ] **Google Ads records what each sale was worth, not only that it happened.** To check, do step 4 below and look at the **Conv. value** column. Dollar amounts mean you're fine. A column of $0 or blanks means the scan can't work out profit, and fixing that tracking is your first job.
- [ ] **You can export from both accounts.** A Google Ads login, and a Shopify staff account allowed to export orders and products. If you don't have that, ask the store owner.
- [ ] **Google Ads and Shopify use the same currency.** If they don't, the scan stops and asks rather than guessing.
- [ ] **Cost per item is filled in on most products.** In Shopify, open any product and look under Pricing. If it's blank, have your rough margin ready instead, meaning what's left of an average order after product cost, shipping and payment fees. The scan can still run, but every profit figure becomes an estimate.
- [ ] **You know your brand name and how people misspell it.** The scan needs this to find the spend on your own name.
- [ ] **An AI account.** Claude on any plan, including free. ChatGPT Plus or above. Or Gemini.

The scan will also ask about your store: what each campaign is for, which products each one sells, how long people take to buy, and which products bring customers back. Every question is optional, and each answer sharpens the recommendations. [See the questions now](references/store-brief.md) if you'd like your answers ready.

---

## Step 1. Download the scan

**[Download profit-leak-scan.zip](https://github.com/Digital-Darts/profit-leak-scan/releases/latest/download/profit-leak-scan.zip)**

A zip is one file with several files packed inside it. Your browser saves it to your **Downloads** folder.

**For Claude, leave the zip as it is.** Don't double-click it or unzip it. Claude needs the zip file itself.

Use the link above, not GitHub's green **Code → Download ZIP** button. That button packs the files in a way Claude won't accept.

## Step 2. Add it to your AI

### Claude

1. Go to [claude.ai](https://claude.ai). Click your name at the bottom left, then **Settings** → **Capabilities**. Switch on **Code execution and file creation**.
2. Open **Customize** → **Skills**.
3. Click **+**, then **Create skill**, then **Upload a skill**.
4. Choose `profit-leak-scan.zip` from your Downloads folder.

On a Team or Enterprise plan and can't see Skills? Your workspace owner has to switch on Skills and code execution for the organisation first.

### ChatGPT

1. Unzip the file. On Windows, right-click it and choose **Extract All**. On a Mac, double-click it. You'll get a folder called `profit-leak-scan`.
2. Go to [chatgpt.com](https://chatgpt.com) → **Projects** → **New project**. Call it "Profit Leak Scan".
3. In the project's **Instructions**, paste this line:
   `You are the Profit Leak Scan. Follow SKILL.md exactly, using the files in references.`
4. Add these files to the project: `SKILL.md` from the folder, plus all six files inside its `references` folder.

### Gemini

1. Unzip the file, as in ChatGPT step 1.
2. Go to [gemini.google.com](https://gemini.google.com) → **Gems** → **New Gem**. Call it "Profit Leak Scan".
3. In the instructions box, paste the same line as ChatGPT step 3.
4. Under **Knowledge**, add `SKILL.md` and the six `references` files. Save.

## Step 3. Pick your 90 days

Use **the same dates for every export**, or the numbers won't line up.

End the 90 days a week before today. Sales from the most recent clicks take a few days to show up in Google Ads, and ending early gives them time.

For example, if today is 25 September, use **20 June to 18 September**. Write your dates down, because you'll enter them four times.

## Step 4. Google Ads: the campaigns report

1. In the left-hand menu, click **Campaigns**. In the menu that opens, choose **Campaigns** again.
2. Click the date range at the top right, choose **Custom**, enter your dates, and click **Apply**.
3. Check the table has these columns: **Campaign**, **Campaign type**, **Cost**, **Impr.**, **Clicks**, **Conversions** and **Conv. value**.
   **Conv. value is often missing.** To add it, click the **Columns** icon above the table, then **Modify columns**. Type `Conv. value` into the search box (or open the **Conversions** section), tick it, and click **Apply**.
4. Click the **download** icon above the table and choose **.csv**.

## Step 5. Google Ads: the search terms report

1. In the left-hand menu, click **Campaigns**. In the menu that opens, choose **Insights and reports** → **Search terms**.
2. Set the same custom dates.
3. Add **Conv. value** the same way as in step 4. Check that **Campaign**, **Cost**, **Clicks**, **Impr.** and **Conversions** are there too. If Campaign is missing, it's under **Attributes** in the same Modify columns box.
4. Download it as **.csv**.

### If you run Performance Max

Performance Max search terms sit in their own view on the same page, and they're where most of the spend on your own brand name usually hides.

1. On the Search terms page, open the drop-down at the top and choose **Search terms and landing pages for Performance Max**.
2. Set the same dates. Add **Conv. value** if it's offered.
3. Download it as **.csv**. This is a separate file, so keep both.

## Step 6. Shopify: orders

1. In your Shopify admin, go to **Orders** and click **Export** at the top right.
2. Choose **Orders by date** and enter your dates. No such option? Close the box, filter the Orders page to your dates first, then click Export and choose the orders matching your search.
3. Under **Export as**, choose **CSV for Excel, Numbers, or other spreadsheet programs**.
4. Click **Export orders**.

Shopify emails larger exports rather than downloading them, usually within a few minutes. The email goes to the store owner. If you're staff and it hasn't arrived, check your spam folder and then ask the owner.

## Step 7. Shopify: products

1. Go to **Products** → **Export**.
2. Choose **All products**, then **CSV for Excel, Numbers, or other spreadsheet programs**.
3. Click **Export products**.

This file carries your **cost per item**, which turns the profit figures from estimates into numbers. If you've never filled cost per item in, skip this file and the scan will ask for your margin instead.

If cost per item is blank across your catalogue, filling it in is worth an afternoon. No report can show what a product earns you without it.

## Step 8. Run it

1. Start a new chat. For ChatGPT, start it inside the project. For Gemini, open the Gem.
2. Type: **run the profit leak scan**
3. Answer the store questions. Skip any you don't know.
4. Upload your files when it asks. There are four or five, depending on whether you run Performance Max.

The scan checks the files before it starts. If something is missing, it tells you exactly what to add and where.

---

## If you get stuck

| Problem | What to do |
|---|---|
| Can't find the Search terms page | Type `Search terms` into the search bar at the top of Google Ads |
| The scan says Conv. value is missing | Go back to step 4 or 5, add the column, and download again |
| Conv. value shows $0 or blanks on every row | Google Ads isn't recording sale values. The scan can still build your negative list and run the settings check. The profit figures need that tracking fixed first |
| Claude won't accept the upload | Check you uploaded the zip from step 1 as it downloaded, not an unzipped folder or GitHub's Download ZIP version, and that code execution is switched on |
| The Shopify email hasn't arrived | Check spam, then the store owner's inbox |
| A file is too big to upload | Tell the scan and it will tell you how to cut it down |

Still stuck? [Open an issue on GitHub](https://github.com/Digital-Darts/profit-leak-scan/issues) and we'll help. You'll need a free GitHub account.

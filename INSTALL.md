# Set up the Profit Leak Scan

No coding. Allow about 30 minutes the first time: 5 to install, 15 to pull your exports, and 10 for the scan to ask its questions and write the report.

Your exports stay in your own AI account. The scan is a set of instructions your AI reads, not a service we run.

Menu names were checked in October 2026. Google and Shopify move things around. If a menu below doesn't match what you see, type the page name into the search bar at the top of Google Ads, or at the top of your Shopify admin.

---

## Before you begin

Tick these off first. Each one says what happens if you can't.

- [ ] **Google Ads has spent money in the last 90 days.** Nothing to scan otherwise. Under a few thousand dollars a month, the negative keyword list and the settings check will do more for you than the profit maths.
- [ ] **Google Ads records what each sale was worth, not only that it happened.** To check, do step 4 below and look at the **Conv. value** column. Dollar amounts mean you're fine. A column of $0 or blanks means the scan can't work out profit, and fixing that tracking is your first job.
- [ ] **You can export from both accounts.** A Google Ads login, and a Shopify staff account allowed to export orders and products. If you don't have that, ask the store owner.
- [ ] **Google Ads and Shopify use the same currency.** If they don't, because your ads account bills in one currency and your store sells in another, have the average exchange rate for your 90 days ready. Your bank statement or xe.com will do. The scan converts Google's figures into your store's currency and tells you which rate it used.
- [ ] **Cost per item is filled in on most products.** In Shopify, open any product and look under Pricing. If it's blank, have your rough margin ready instead, meaning what's left of an average order after product cost, shipping and payment fees. The scan can still run, but every profit figure becomes an estimate.
- [ ] **You know your brand name and how people misspell it.** The scan needs this to find the spend on your own name.
- [ ] **An AI account.** Claude on any plan, including free. ChatGPT Plus or above. Or Gemini.

The scan will also ask about your store: what each campaign is for, which products each one sells, how long people take to buy, and which products bring customers back. Apart from your brand name, every question is optional, and each answer sharpens the recommendations. [See the questions now](references/store-brief.md) if you'd like your answers ready.

---

## Step 1. Download the scan

**[Download profit-leak-scan.zip](https://github.com/Digital-Darts/profit-leak-scan/releases/latest/download/profit-leak-scan.zip)**

A zip is one file with several files packed inside it. Your browser saves it to your **Downloads** folder.

**For Claude, leave the zip as it is.** Don't double-click it or unzip it. Claude needs the zip file itself.

Use the link above, not GitHub's green **Code → Download ZIP** button. That button packs the files in a way Claude won't accept.

## Step 2. Add it to your AI

### Claude

Skills work in Claude's Chat, Cowork and Code modes.

1. Go to [claude.ai](https://claude.ai). On a Free, Pro or Max plan, first switch on **Code execution and file creation**: click your name at the bottom left, then **Settings** → **Capabilities**.
2. In the left-hand menu, open **Customize** → **Skills** → **Yours**.
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

## The four files

The scan needs four files. Two come from Google Ads and two from Shopify, and all four cover the same 90 days.

| # | File | Comes from | Step |
|---|---|---|---|
| 1 | Campaigns report | Google Ads | 4 |
| 2 | Search terms report | Google Ads | 5 |
| 3 | Orders | Shopify | 6 |
| 4 | Products | Shopify | 7 |

## Step 3. Pick your 90 days

Use **the same dates for every export**, or the numbers won't line up.

End the 90 days a week before today. Sales from the most recent clicks take a few days to show up in Google Ads, and ending early gives them time.

For example, if today is 25 September, use **21 June to 18 September**. Write your dates down, because you'll enter them three times.

## Step 4. Google Ads: the campaigns report (file 1)

1. In the left-hand menu, click **Campaigns**. In the menu that opens, choose **Campaigns** again.
2. Click the date range at the top right, choose **Custom**, enter your dates, and click **Apply**.
3. Click the **Columns** icon above the table, then **Modify columns**.
4. Make sure these seven are ticked: **Campaign**, **Campaign type**, **Cost**, **Impr.**, **Clicks**, **Conversions** and **Conv. value**. Conv. value is the one most often missing. Type its name into the search box, or open the **Conversions** section.
5. In the same box, tick **Original conv. value** if it's listed. Not every account has it, so skip it if you can't see it.
6. Click **Apply**.
7. Click the **Download** icon in the row of buttons directly above the table, next to **Columns**, and choose **.csv**. The file is called `Campaign report.csv`.

The chart above the table has its own download button. That one gives you a file called `Time_series_chart`, which is the wrong file. The right one has a row for each campaign.

## Step 5. Google Ads: the search terms report (file 2)

1. In the left-hand menu, click **Campaigns**. In the menu that opens, choose **Insights and reports**, then **Search terms**.
2. Set the same custom dates as step 4.
3. Click the **Columns** icon, then **Modify columns**.
4. Make sure these six are ticked: **Campaign**, **Cost**, **Clicks**, **Impr.**, **Conversions** and **Conv. value**. Campaign is under **Attributes**. Search term and Match type are locked in place, so they're always there. Tick **Original conv. value** too if it's listed. Click **Apply**.
5. Click **Add filter** above the table, choose **Cost**, set it to **greater than 0**, and click **Apply**. This leaves out searches that showed your ad but never cost you anything. The scan doesn't use them, and they are usually nine rows in every ten.
6. Click the **Download** icon next to **Columns** and choose **.csv**. The file is called `Search terms report.csv`.

**Run Performance Max?** There's nothing extra to download. Its search terms are in this same file, marked **Performance Max** in the Match type column. If you run Performance Max and no rows say so, look along the top of the Search terms page for a view called **Search terms and landing pages for Performance Max**, and download that as a second file.

**Still too big to upload?** Click the **Cost** column heading so the biggest spenders come first, then download again. Open the file in Excel or Google Sheets, delete every row below row 2,000, and save it as a CSV. Tell the scan you trimmed it.

## Step 6. Shopify: orders (file 3)

1. In your Shopify admin, go to **Orders** and click **Export**.
2. Choose **Orders by date** and enter your dates.
3. Under **Export as**, choose **CSV for Excel, Numbers, or other spreadsheet programs**.
4. Click **Export orders**.

Shopify emails the file to you and to the store owner, usually within a few minutes. It often arrives as a zip. Unzip it (on Windows, right-click it and choose **Extract All**) and use the `.csv` file inside.

## Step 7. Shopify: products (file 4)

1. In your Shopify admin, go to **Products** and click **Export**.
2. Choose **All products**.
3. Under **Export as**, choose **CSV for Excel, Numbers, or other spreadsheet programs**.
4. Click **Export products**. A large catalogue is emailed as a zip, the same as orders.

This file carries your **cost per item**, which turns the profit figures from estimates into numbers. If you've never filled cost per item in, skip this file and the scan will ask for your margin instead.

If cost per item is blank across your catalogue, filling it in is worth an afternoon. No report can show what a product earns you without it.

## Step 8. Run it

1. Start a new chat. For ChatGPT, start it inside the project. For Gemini, open the Gem.
2. Type: **run the profit leak scan**
3. Answer the store questions. Your brand name is the only one it needs. Skip any others you don't know.
4. Upload your four files when it asks: the campaigns report, the search terms report, the orders export and the products export.
5. The scan then asks up to ten short questions about your account settings, one at a time. Answer what you can, or say "write the report" to get it straight away.

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
| A file is too big to upload | Check you added the Cost filter in step 5. If it's still too big, follow "Still too big to upload?" under step 5 |
| My campaigns file is called `Time_series_chart` | That's the chart's download. Go back to step 4 and use the Download button next to Columns, directly above the table |
| I run Performance Max but no rows say so | Follow "Run Performance Max?" under step 5 |
| Google Ads bills me in a different currency from my store | Have the average exchange rate for your 90 days ready. The scan asks for it |
| The scan asks for a month-by-month campaigns report | On the Campaigns page, click **Segment** above the table, then **Time**, then **Month**, and download the table again |

Still stuck? [Open an issue on GitHub](https://github.com/Digital-Darts/profit-leak-scan/issues) and we'll help. You'll need a free GitHub account.

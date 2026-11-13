# Yumarib Prints POS (static, GitHub Pages)

A complete single-page POS for Yumarib Prints. One file: `index.html` (all CSS and JavaScript inline, plus `manifest.json`, `sw.js` and `icon.svg` for desktop install). Fonts are Pziel's: body Rubik, headings Nunito Sans (Google Fonts, with system fallbacks). Dark theme is the default as approved: near-black background, dark cards, white text. Light mode is a clean white theme, switched with the Light / Dark button in the header and on the login/setup screens, saved in localStorage. The primary accent is orange (#f07a1a / #e86a17), not green: Sell tab, buttons, tile top borders and active states are orange, with gradients, shadows and hover lift on the boxes.

## How to publish

1. Put `index.html` in this repository and push to GitHub.
2. In the repo: Settings → Pages → Deploy from a branch → branch `main`, folder `/ (root)`.
3. Open the Pages URL. The first load needs internet; after that the page works in the browser.

## Honest notes — read this before relying on it

- **Data is saved in this browser only.** Everything (products, sales, jobs, customers, expenses, users, shop settings, logo) is stored in `localStorage` under the key `yumarib-pos-v1`, on that one machine and in that one browser. Clearing browser data, using a different browser, or using a different computer loses / does not show that data.
- **Sales do NOT sync to the Muse web POS online database.** This static app and the online web POS are separate. A sale recorded here will not appear there, and vice versa. If you need shared / synced sales across machines, this static version is not the right tool — use the online POS.
- **No offline server.** There is no server, no database file, and no background service. It is just a web page that saves to the browser.
- **Passwords are stored in plain text in localStorage.** That is how this simple static version works. Do not reuse a password you use anywhere else, and do not treat this as secure storage. Only people you trust should have access to the machine / browser profile.
- **First run:** create the admin account (username, name, password min 4 characters). After that, the login screen is a user picker: tap your name, type your password. Admin creates extra staff users in Admin → Users. Products and Admin tabs are admin-only.
- **Seeding:** the 23 products and prices are seeded only on the first run. Existing data is never wiped or reseeded on reload.

## Prices (NGN, as supplied — nothing invented)

DI — Direct Images: A4 Paper 80, A3 Paper 150, A4 Solid 300, A3 Solid 600, Letterhead Special Paper 20000 (per 500), Letterhead Normal Paper 10000 (per 500), A4 250g 150, A4 250g Solid 350, A4 300g 200, A4 300g Solid 400, A4 350g 250, A4 350g Solid 500, A3 250g 300, A3 250g Solid 1000, A3 300g 350, A3 300g Solid 1200, Special Paper A4 60, Special Paper A3 120, Special Card A4 150, Special Card A3 250, Special Card Solid A3 500. Borderless: A2 1800, A1 3600. Large Format and UV Print start empty and are entered as custom jobs (e.g. SAV 9 x 15 inches, with your own price).

## Printing receipts — Xprinter XP-80T

- Receipt paper width defaults to 80mm (72mm content) for the Xprinter XP-80T. Change it to 58mm in Admin → Shop if you load 58mm paper.
- In Windows, set the Xprinter XP-80T as the **Default Printer**, then use **Print receipt**. The print view is 80mm wide with no app chrome.
- WhatsApp receipt opens wa.me with the receipt text, using the customer phone entered on the sale when present.

## What is inside

- Sell: category pills (All 23, DI, Large Format, Borderless, UV Print), search, product tiles with coloured top borders, in-cart badge, custom job card (Width/Height → e.g. “SAV 9 x 15 inches”), sticky Current sale panel (370px), flat ₦ or % discount, Cash / POS / Transfer, cash received and change, part payment / credit with Paid and Balance on the receipt.
- Dashboard: Grand total, Sales, Collected so far, Still owed, Before discount, Discounts given; Totals by category, Money by payment, Sales by staff; Daily cash closing (Cash/POS/Transfer received, expected cash, counted cash, difference); Today's sales with Reprint / WhatsApp; low-stock warnings.
- Jobs: customer, total, deposit, statuses Pending / In Production / Ready / Collected. A job cannot be Collected while a balance is outstanding; record further payments against it.
- Products (admin only): add / edit / delete, stock counts. Stock starts untracked until an admin sets it, then counts down on sale. Low stock (5 or fewer) and out of stock warnings show on Sell and Dashboard.
- Admin: Sales (any date, void, reprint), Expenses (net after expenses), Reports (date range, top products, Export CSV for Excel, Print / Save as PDF), Price checker, Customers (balance owed, Who owes us filter, record payment), Users (admin creates users), Shop (shop name, logo upload stored in localStorage, receipt paper width 80mm / 58mm).

## Backup

There is no automatic backup in this static version. To keep a copy of the data, use Reports → Export CSV regularly, and do not clear the browser's site data for the POS page.

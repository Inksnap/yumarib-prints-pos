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

- Sell: category pills (All 29, Paper A4, Paper A3, Card A4 250g, Card A4 300g, Card A4 350g, Card A3 250g, Card A3 300g, Special Card, Lanyards, Large Format, Borderless, UV Print), search, product tiles with coloured top borders, in-cart badge, Large Format calculator and Custom job card at the bottom of the Sell screen, below the product grid (Custom Job is always last), sticky Current sale panel (370px), flat ₦ or % discount, Cash / POS / Transfer, cash received and change, part payment / credit with Paid and Balance on the receipt.
- Dashboard: Grand total, Sales, Collected so far, Still owed, Before discount, Discounts given; Totals by category (every group listed, even ₦0, plus Jobs created that day, and a Categories total before discount), Money by payment, Sales by staff; Daily cash closing (Cash/POS/Transfer received, expected cash, counted cash, difference); Today's sales with Reprint / WhatsApp; low-stock warnings.
- Jobs: customer, total, deposit, statuses Pending / In Production / Ready / Collected. A job cannot be Collected while a balance is outstanding; record further payments against it.
- Products (admin only): add / edit / delete, stock counts. Stock starts untracked until an admin sets it, then counts down on sale. Low stock (5 or fewer) and out of stock warnings show on Sell and Dashboard.
- Logo: transparent PNG, no background. Black monochrome logo on the receipt (prints black on white on the Xprinter XP-80T), colour logo in dark mode, black logo in light mode. No "YUMARIB PRINTS" text next to the logo, the logo itself says it.
- Admin: Sales (any date, void, reprint), Expenses (net after expenses), Reports (date range, top products, Export CSV for Excel, Print / Save as PDF), Price checker, Customers (balance owed, Who owes us filter, record payment), Users (admin creates users), Shop (shop name, logo upload stored in localStorage, receipt paper width 80mm / 58mm).

## Backup

There is no automatic backup in this static version. To keep a copy of the data, use Reports → Export CSV regularly, and do not clear the browser's site data for the POS page.

## Receipt logo (2026-11-13)
Website shows the colour PNG logo. Receipt shows logo-grey.png, the same logo converted to greyscale with its black background kept, so the white YP and PRINTS stay visible on white paper and on the Xprinter. The old pure black-and-white transparent logo made the white parts invisible on white, which is why the logo did not show on the receipt.

## Sell groups and totals by category (2026-11-14)
DI is split in the Sell screen only, so staff do not have to hunt paper and card under one DI pile. Paper A4: A4 Paper, A4 Solid, Special Paper A4, Letterhead Special, Letterhead Normal. Paper A3: A3 Paper, A3 Solid, Special Paper A3. Card A4 250g / 300g / 350g and Card A3 250g / 300g, each with its Solid version. Special Card: Special Card A4, A3, Solid A3. Products still keep category DI in Admin / Products, and all prices are unchanged. Dashboard and Reports totals by category list the four real categories only, DI, Large Format, Borderless and UV Print, even at ₦0, plus Jobs created in that period, and a Categories total (before discount) so the rows add up. Paper/Card split groups and Lanyards count back into DI in totals. Old sales stored as DI are split by the same mapping when totals are shown.

## Logo (receipt, 2026-11-13)
- Website/header/login: colour PNG logo (logo-color.png, with black background).
- Receipt: black clipart PNG, no background (logo-black-clipart.png), made from the colour logo by removing the outer black background and turning the shapes black, keeping YP/PRINTS details as negative space. Transparent PNG, 1208x400.
- The previous all-black file sent by the user (yumarib_prints_black_clipart_16_gwxu.png) was a JPEG with every pixel black, so it could not be used as a logo.


## Large Format calculator and Custom Job (2026-11-14)
In Sell, tap the Large Format group (or All) to see the Large Format calculator, below the product grid. The Custom Job card is always at the very bottom of the Sell screen, below the product grid and below the Large Format calculator, on every group filter. Both calculate the price automatically as soon as width and height are typed, using the same formulas, so they always agree.
- Flex: width (feet) x height (feet) x 160. Example 5x7 ft: 5 x 7 x 160 = 5,600 NGN per banner. Quantity is number of banners.
- SAV: width (inches) x height (inches) x 450 / 144. Example 5x7 in: 5 x 7 x 450 / 144 = 109.38, rounded to 109 NGN per sticker. Example 9x15 in: 9 x 15 x 450 / 144 = 421.88, rounded to 422 NGN per sticker. Total = per-one price x quantity.
- Custom Job: pick Flex, SAV or Other. For Flex/SAV the Price field fills in automatically and is read-only, and the card shows the calculation, e.g. "9 x 15 x ₦450 ÷ 144 = ₦422 per sticker". For Other, type the price manually. Custom Job also has a Quantity field.
The calculated item is added to the Current sale as e.g. "Flex 5x7 ft" or "SAV 9x15 in", with size, quantity, unit price and total, shows on the receipt, and counts under Large Format in Dashboard totals. No other prices changed.
Group counts: 29 seeded products in total. Large Format shows (0) because Flex and SAV are not seeded products, they are entered through the calculator / Custom Job. UV Print shows (3): UV Pen, UV Diary, UV Flask. Borderless shows (3): A2, A1, Pressing of Borderless. Lanyards shows (2). If a machine still shows UV Print (0) or Borderless (2), it is on an old cached version, reload the page once to pick up the new version.

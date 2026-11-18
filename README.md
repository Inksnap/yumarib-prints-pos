# Yumarib Prints POS (static, GitHub Pages)

A complete single-page POS for Yumarib Prints. One file: `index.html` (all CSS and JavaScript inline, plus `manifest.json`, `sw.js` and `icon.svg` for desktop install). Fonts are Pziel's: body Rubik, headings Nunito Sans (Google Fonts, with system fallbacks). Dark theme is the default as approved: near-black background, dark cards, white text. Light mode is a clean white theme, switched with the Light / Dark button in the header and on the login/setup screens, saved in localStorage. The primary accent is orange (#f07a1a / #e86a17), not green: Sell tab, buttons, tile top borders and active states are orange, with gradients, shadows and hover lift on the boxes.

## How to publish

1. Put `index.html` in this repository and push to GitHub.
2. In the repo: Settings → Pages → Deploy from a branch → branch `main`, folder `/ (root)`.
3. Open the Pages URL. The first load needs internet; after that the page works in the browser.

## Honest notes — read this before relying on it

- **Data is saved in this browser only, unless the cloud is connected.** Everything (products, sales, jobs, customers, expenses, users, shop settings, logo) is stored in `localStorage` under the key `yumarib-pos-v1`, on that one machine and in that one browser. Clearing browser data, using a different browser, or using a different computer loses / does not show that data — unless Admin > Shop > Cloud backup has been set up (see below), in which case the same data is also saved to Firebase Firestore and comes back after sign-in.
- **Sales do NOT sync to the Muse web POS online database.** This static app and the online web POS are separate. A sale recorded here will not appear there, and vice versa. If you need shared / synced sales across machines, this static version is not the right tool — use the online POS.
- **No offline server.** There is no server, no database file, and no background service. It is just a web page that saves to the browser.
- **Passwords are stored in plain text in localStorage.** That is how this simple static version works. Do not reuse a password you use anywhere else, and do not treat this as secure storage. Only people you trust should have access to the machine / browser profile.
- **First run:** create the admin account (username, name, password min 4 characters). After that, the login screen is a user picker: tap your name, type your password. Admin creates extra staff users in Admin → Users. Products and Admin tabs are admin-only.
- **Seeding:** the 23 products and prices are seeded only on the first run. Existing data is never wiped or reseeded on reload.

## Prices (NGN, as supplied — nothing invented)

DI — Direct Images: A4 Paper 80, A3 Paper 150, A4 Solid 300, A3 Solid 600, Letterhead Special Paper 20000 (per 500), Letterhead Normal Paper 10000 (per 500), A4 250g 150, A4 250g Solid 350, A4 300g 200, A4 300g Solid 400, A4 350g 250, A4 350g Solid 500, A3 250g 300, A3 250g Solid 1000, A3 300g 350, A3 300g Solid 1200, Special Paper A4 60, Special Paper A3 120, Special Card A4 150, Special Card A3 250, Special Card Solid A3 500. Borderless: A2 1800, A1 3600. Large Format and UV Print start empty and are entered as custom jobs (e.g. SAV 9 x 15 inches, with your own price).

## Printing receipts — Xprinter XP-80T

- Receipt paper width defaults to 80mm (72mm content) for the Xprinter XP-80T. Change it to 58mm in Admin → Shop if you load 58mm paper.
- In Windows, set the Xprinter XP-80T as the **Default Printer**. After Charge the receipt prints automatically, then the screen goes back to Sell with a fresh empty Current sale, ready for the next customer. The sale is saved (local + cloud) before printing, so cancelling the print dialog does not lose the sale. If the print fails or paper runs out, reprint from the "Reprint last receipt" button in Sell, or from Reprint in Dashboard / Admin Sales. The print view is 80mm wide with no app chrome.
- WhatsApp receipt opens wa.me with the receipt text, using the customer phone entered on the sale when present.

## What is inside

- Sell: category pills (All 29, Paper A4, Paper A3, Card A4 250g, Card A4 300g, Card A4 350g, Card A3 250g, Card A3 300g, Special Card, Lanyards, Large Format, Borderless, UV Print), search, product tiles with coloured top borders, in-cart badge, Large Format card and Custom job card at the bottom of the Sell screen, below the product grid (Custom Job is always last), sticky Current sale panel (370px), Discounted price (type the amount the customer will pay; the POS works out the discount as Subtotal minus that price), Cash / POS / Transfer, cash received and change, part payment / credit with Paid and Balance on the receipt.
- Dashboard is protected: clicking the Dashboard tab asks for the admin password (the same password the admin uses to sign in). Wrong password stays on the current tab with a 'Wrong password' message; correct password opens the Dashboard. Sell, Jobs, Products and Admin are unchanged.
- Number inputs never change on mouse wheel: scrolling with the mouse wheel over an amount, discount, quantity, price, width, height or cash figure leaves the figure exactly as typed and scrolls the page instead.
- Dashboard: Total collected (money customers have paid only), Sales, Collected so far, Still owed; Totals by category are money collected (every group listed, even ₦0, and a Categories total (money collected), with Balance still owed shown separately). Use Print / Save totals on Dashboard to print or save Totals by category together with Money by payment. No discount appears anywhere in Dashboard totals. Money by payment, Sales by staff (money collected per staff); Expenses (add an expense from Dashboard too, with what it was for, amount, date and who added it, Total expenses and Net = Total collected minus expenses for the day; the same list shows in Admin > Expenses, and deleting an expense is admin only); Daily cash closing (Cash/POS/Transfer received, expected cash, counted cash, difference); Today's sales with Reprint / WhatsApp; low-stock warnings. Who owes us is also shown on Dashboard (total still owed and the top debtors), with a button to open the Who owes us tab. Print / Save totals also prints Total expenses and Net.
- Jobs: every job has a job number (JOB-0001, JOB-0002...), customer name and phone, description with size and quantity, total, deposit and its payment method, paid so far, balance, status, created date/time and created by. Every step is logged in a history with date, time and staff: Created, Status changed, Payment, Collected. Tap History on a job to see its full detail and timeline, Print history to print that one job, or Print jobs history to print all jobs created in a date range. Older jobs get a job number and a history built from the data already stored. A job cannot be Collected while a balance is outstanding; record further payments against it. Job orders from sales appear here automatically: when a sale is charged, each Large Format / Custom Job item and each UV Print or Borderless item in that sale becomes a job, with the receipt number and full description (size, quantity, total, paid, balance, created by). Standard DI paper/card items sold at the till do not become jobs. Past job sales are backfilled the next time the POS loads, so Jobs is never empty after job sales. Money lives in the sale, so a sale-linked job's balance is not counted again in Dashboard Still owed or customer balances; a payment recorded on it is applied to its sale too.
- Products (admin only): add / edit / delete, stock counts. Stock starts untracked until an admin sets it, then counts down on sale. Low stock (5 or fewer) and out of stock warnings show on Sell and Dashboard.
- Logo: transparent PNG, no background. Black monochrome logo on the receipt (prints black on white on the Xprinter XP-80T), colour logo in dark mode, black logo in light mode. No "YUMARIB PRINTS" text next to the logo, the logo itself says it.
- Who owes us (top tab, for every signed-in user, not admin-only): everyone with a balance above ₦0, with the receipts and jobs that make up the balance, and a place to always record a payment from them — customer, amount paid, Cash / POS / Transfer, date paid, note. Oldest sale is paid first, then oldest manual job. A payment lowers the balance, adds to Total collected on the day it was paid (even when the sale was made on an earlier day), updates the sale or job, and never creates a new sale. The same recording is used from Jobs (Record payment on a job) and Admin > Customers.
- Admin: Sales (any date, void, reprint), Expenses (net after expenses), Reports (date range, top products, Export CSV for Excel, Print / Save as PDF), Price checker, Customers (balance owed, Who owes us filter, record payment), Users (admin creates users), Shop (shop name, logo upload stored in localStorage, receipt paper width 80mm / 58mm).

## Cloud backup (online database, Firebase Firestore — 2026-11-14)

Chosen cloud: **Firebase Firestore**, not Supabase. Why: the user already has a Google account (info.inksnap@gmail.com), Firestore works from a static GitHub Pages site with only a public web config and no server of our own, it has built-in offline persistence, and the free Spark plan (1 GiB stored, 50k reads/day) is enough for this POS.

How it works in the code: one Firestore document, `pos/yumarib-main`, holds the whole POS state as a JSON string (sales, products, users, jobs, customers, expenses, payments, closings, shop settings, receiptSeq) plus `updatedAt`. `save()` still writes localStorage first, then queues a cloud save (debounced ~800 ms). On startup `initCloud()` signs in anonymously to Firebase, loads the cloud document, and if the cloud copy is newer (or this browser is empty) it replaces the local data and shows the login screen with the cloud users. If this browser is newer, it pushes local data to the cloud. If the internet drops, the POS keeps working from localStorage and syncs when it is back. Cloud sync only runs after the local POS login, and Firestore rules require a Firebase sign-in (anonymous).

**The Firebase project does NOT exist yet.** Creating it needs the user's Google sign-in (info.inksnap@gmail.com) in a browser. Exact steps are in the POS itself, Admin > Shop > Cloud backup, and in the parent agent's report. Short version: console.firebase.google.com > Create project `yumarib-prints-pos` (skip Analytics) > Firestore Database > Create, production mode > Authentication > Anonymous > Enable > Project settings > Web app, copy the `firebaseConfig` > Firestore Rules, paste the rules shown in the POS and Publish > paste the config in Admin > Shop > Cloud backup > Save cloud config > Sync now. The `apiKey` in that config is a public identifier, not a secret password; security is the Firestore rules plus the POS login. Never paste a private service-account key.

Until the cloud is live, use the manual backup in Admin > Shop > Cloud backup: **Download full backup (JSON)** saves the whole state to a file, **Restore from backup file** replaces the browser data with that file (after a confirm). Reports > Export CSV is still there for Excel.

Firestore rules to publish:
```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /pos/{docId} {
      allow read, write: if request.auth != null;
    }
  }
}
```
Limit: a Firestore document caps at 1 MiB. If the POS state ever grows past ~900 KB, sync warns and the JSON backup is the fallback; old sales would need archiving then.

## Backup

Until the cloud is connected, there is no automatic backup in this static version. Use Admin > Shop > Download full backup (JSON) regularly, plus Reports → Export CSV, and do not clear the browser's site data for the POS page.

## Receipt logo (2026-11-13)
Website shows the colour PNG logo. Receipt shows logo-grey.png, the same logo converted to greyscale with its black background kept, so the white YP and PRINTS stay visible on white paper and on the Xprinter. The old pure black-and-white transparent logo made the white parts invisible on white, which is why the logo did not show on the receipt.

## Sell groups and totals by category (2026-11-14)
DI is split in the Sell screen only, so staff do not have to hunt paper and card under one DI pile. Paper A4: A4 Paper, A4 Solid, Special Paper A4, Letterhead Special, Letterhead Normal. Paper A3: A3 Paper, A3 Solid, Special Paper A3. Card A4 250g / 300g / 350g and Card A3 250g / 300g, each with its Solid version. Special Card: Special Card A4, A3, Solid A3. Products still keep category DI in Admin / Products, and all prices are unchanged. Dashboard and Reports totals by category list the four real categories only, DI, Large Format, Borderless and UV Print, even at ₦0, and a Categories total (money collected) so the rows add up to the money actually collected. No discount appears in Dashboard or Reports totals at all; Balance still owed is shown separately. Paper/Card split groups and Lanyards count back into DI in totals. Old sales stored as DI are split by the same mapping when totals are shown.

## Logo (receipt, 2026-11-13)
- Website/header/login: colour PNG logo (logo-color.png, with black background).
- Receipt: black clipart PNG, no background (logo-black-clipart.png), made from the colour logo by removing the outer black background and turning the shapes black, keeping YP/PRINTS details as negative space. Transparent PNG, 1208x400.
- The previous all-black file sent by the user (yumarib_prints_black_clipart_16_gwxu.png) was a JPEG with every pixel black, so it could not be used as a logo.


## Large Format and Custom Job (2026-11-16, simplified)
In Sell, tap the Large Format group (or All) to see the Large Format card, below the product grid. The Custom Job card is always at the very bottom of the Sell screen, below the product grid and below the Large Format card, on every group filter. There is no automatic calculation anywhere in Large Format any more: staff choose the type (Flex, SAV Print and Cut or SAV Print Only), type the size, type the quantity, then type the price themselves, and tap Add to sale. Add to sale is blocked until a price above ₦0 is typed. Flex uses feet, both SAV types use inches. Quantity does NOT change the amount: Large Format / Custom Job items are flat amounts, the amount added to the sale is exactly the amount typed, never price x quantity, in the cart, receipt, Dashboard totals or reports.

## Price collected (2026-11-16)
Staff can type the price they already collected, instead of only using a saved price, so a sale is fast. It only changes that one sale, never the product's saved price in Products.
- Large Format: a big "Price (₦) - per banner / per one" box. Type the price yourself before adding to sale, for Flex, SAV Print and Cut and SAV Print Only. The Add to sale button stays disabled until a price above ₦0 is typed. There is no calculated price shown.
- Custom Job (bottom of Sell): the Price box is manual for Flex and both SAV types too. It stays empty until staff type it, changing the size or type never fills it in and never clears a typed price. No calculated price is shown.
- Current sale (removed 2026-11-16 at the user's request): the sale line no longer has a "Price collected" box in front of the quantity, and no - / + buttons around the quantity, only a quantity box to type in. The line price is the saved product price, or for Large Format / Custom Job the amount typed in that card. The split-payment description text under Payments was also removed; the split payment rows themselves (Cash, POS, Transfer) are unchanged.
The item is added to the Current sale as e.g. "Flex 5x7 ft", "SAV Print and Cut 9x15 in" or "SAV Print Only 9x15 in", with size, quantity and the typed amount, shows on the receipt, and counts under Large Format in Dashboard totals. The Large Format card shows the typed amount only, never a price x quantity total. Normal products still work as price x quantity. No other prices changed.
Group counts: 29 seeded products in total. Large Format shows (0) because Flex and both SAV types are not seeded products, they are entered through the Large Format / Custom Job cards. UV Print shows (3): UV Pen, UV Diary, UV Flask. Borderless shows (3): A2, A1, Pressing of Borderless. Lanyards shows (2). If a machine still shows UV Print (0) or Borderless (2), it is on an old cached version, reload the page once to pick up the new version.

## Split payment (2026-11-16)
A sale or job can be paid in parts, with a different method for each part. Every split payment row offers all three methods: Cash, POS and Transfer.
- In Current sale, under Payments (split payment), the first row defaults to the full total. Type the first part, e.g. Cash ₦10,000, then tap "+ Add another payment". The new row defaults to the amount still left, e.g. ₦60,000: choose POS or Transfer for it, or type a different amount.
- Add as many rows as needed, e.g. ₦20,000 POS + ₦50,000 Transfer. Each row can be edited or removed (✕) before charging. Paid so far and Balance owed update live as rows are added or changed.
- Example: total ₦70,000, paid ₦10,000 Cash + ₦60,000 Transfer, or ₦10,000 Cash + ₦60,000 POS, balance ₦0. A single payment still works as before: one row, one method, same as the old Cash / POS / Transfer choice.
- The receipt shows each part on its own line (Cash ₦10,000, Transfer ₦60,000), then Paid, Balance and the payment summary. Dashboard "Money by payment" and daily closing count each part under its own method (Cash parts under Cash, POS parts under POS, Transfer parts under Transfer), never double-counted. Jobs paid in parts work the same way: a payment recorded on a job, or a customer payment, is merged into the linked sale's payments under that method.
- The Customer Display second window that was added earlier the same day was removed at the user's request on 2026-11-16, before split payment was built. The POS is a single screen again, with no customer window and no live-sync publishing.

## Current sale cleanups (2026-11-16)
At the user's request, from the photo of the Current sale panel (A4 300g, qty 500, total ₦100,000): removed the Price collected box in front of the quantity, removed the - and + buttons around the quantity (quantity is only a box to type in), and removed the split-payment description text under "Payments (split payment)". Split payment rows, Paid so far, Balance owed, discount, totals, Charge and receipt are unchanged. Large Format / Custom Job manual price entry is unchanged.

## Multi-machine sync (different staff, different machines)

Each POS machine gets its own code, e.g. POS-A1B2, shown in Admin > Shop > Cloud backup
("This machine"). Give each machine a name there, e.g. Front Desk.

- Each machine works offline and saves its own sales locally.
- When it comes online it uploads only its own records to Firestore
  (pos/device-XXXX), and downloads and merges the other machines' records.
  Dashboard, sales by staff, totals by category, money by payment
  (Cash / POS / Transfer, including split payments), Still owed and Jobs
  then add up across ALL machines, each sale counted once.
- Receipt numbers are unique per machine, e.g. R-A1B2-0001 and R-C3D4-0001,
  and job numbers are JOB-A1B2-0001, so two machines never clash.
- Products, users and shop settings are shared (pos/yumarib-main);
  the last edit made wins for those, but a shared edit can never wipe
  another machine's sales.
- Tap "Sync now" in Admin > Shop to merge immediately. The POS also
  syncs automatically every 2 minutes when online, and when it comes
  back online.
- The old single-document sync (last writer won, other machine's
  offline sales were lost) is gone. If the old cloud document is still
  there, the first sync with this version merges it once.

## Cloud sync fix (2026-11-16, POS-J38T "Missing or insufficient permissions")
Root cause: multi-machine sync used `getDocs(collection(db,"pos"))`, a collection
LIST query to discover device docs, and `initCloud()` swallowed anonymous
sign-in failures (`catch{}`), set `cloudReady=true` anyway, then read Firestore
unauthenticated, which Firestore rejects as permission-denied. Fix, code only,
no Firebase console change needed: sync never runs until anonymous sign-in is
VERIFIED (`currentUser` non-null, 3 attempts, plain "Cloud sign-in failed"
status if it fails); the shared doc `pos/yumarib-main` carries a `deviceIds`
registry and each machine remembers device ids it has seen, and sync reads each
`pos/device-XXXX` with a single `getDoc()`, never a collection list/query.
`saveCloud()` reads the shared doc first so registering a machine never wipes
a newer shared copy. Status now shows Auth state (signed in anonymously, or
NOT signed in) and the Firestore error code.

**2026-11-16 fix (auth/api-key-not-valid):** the embedded Firebase config once had its apiKey shown as a masked placeholder, and the Admin config box could save that masked value back as the real key, so Firebase Auth failed. Fixed: the built-in config is restored, the config box now shows the key masked on a separate line only and leaves apiKey blank in the editable box (blank = keep the built-in key), any stored override with a masked/invalid key is ignored and cleared on load, and Admin > Shop has a Reset cloud config button. Reloading the POS alone fixes a machine with the bad override.

- **Products are merged by id across machines (2026-11-16).** Adding a product on any machine saves it locally at once and uploads it to the shared cloud doc; on sync the lists are merged by product id, never replaced wholesale, so a new product survives a reload and appears on the other machine after Sync now. Deleting a product records it so it does not come back from the other machine.

- Totals by category are money collected (2026-11-16): category rows show only the money actually collected for that category, not the total sold. A part-paid sale only counts what was paid, shared across its categories in proportion to their amounts. No discount appears in Dashboard or Reports totals at all.

# DO IT RIGHT Mobile Auto Mechanic – sample website

Preview site built by Clyde ((832) 930-1707 · cuzclydecan@mail.grokbot.com) for Marc/Marcus, DO IT RIGHT Mobile Auto Mechanic, Houston · (832) 305-2630.
Single static file (`index.html`): no build step, no server, no tracking. The logo is embedded as a data URI.

## What works today (demo mode)
- **Click-to-call** buttons dial (832) 305-2630.
- **Service picker** → selections flow into the booking form.
- **Booking form**: validates required fields, then builds a summary the customer sends to Marc with one tap by **text (sms:)** or **email (mailto:)**. Photos are previewed on the page; the customer attaches them in the text/email (sms/mailto links cannot carry files).
- **Pay deposit / Pay invoice**: open a clearly marked *DEMO · TEST MODE* checkout preview. No card is collected and nothing can be charged.

## Going live (edit the `CONFIG` block near the bottom of index.html)
```js
const CONFIG={
  FORM_ENDPOINT:"",   // form backend URL
  DEPOSIT_LINK:"",    // Stripe Payment Link for the deposit
  INVOICE_LINK:"",    // Stripe Payment Link where the customer enters the amount (optional)
  SMS_TO:"+18323052630",
  EMAIL_TO:"doitrightmobile@gmail.com"
};
```
1. **Form backend** (pick one):
   - Formspree (or similar): create a form, paste its endpoint (`https://formspree.io/f/<id>`) into `FORM_ENDPOINT`. Submissions (including photo files on plans that allow uploads) are emailed to Marc. When the endpoint is set, the form posts with `fetch` and shows "Sent!"; if the post fails it falls back to the text/email hand-off.
   - Netlify Forms / Cloudflare Pages + a Worker are alternatives if the site moves hosts.
   - Square Appointments or Setmore: replace the "Book a Visit" links with the booking-page URL if Marc prefers a calendar with built-in deposits.
2. **Deposit**: in Stripe Dashboard → Payment Links → create a product "Visit deposit" at Marc's chosen amount (e.g. $50, Marc's call) → copy the `https://buy.stripe.com/...` link into `DEPOSIT_LINK`. Turn on "Collect phone number" and add a custom field "Booking name".
3. **Invoices**: either send Stripe Invoices (Dashboard or the Stripe phone app; customer pays on Stripe's hosted page) or create a Payment Link with "Let customers choose what to pay" and put it in `INVOICE_LINK`.
4. **On site**: Tap to Pay on iPhone/Android in the Stripe Dashboard app (no card reader).

## Hosting
GitHub Pages from `main` / root. For a custom domain, add a `CNAME` file and point DNS (registered in the business owner's name).

## Content sources
Hours, services, rating and reviews come from public listings checked Oct 19, 2026 (Google data via MechanicRank/CarHQ/LocalityBiz, Yelp via MapQuest/Roadtrippers, Instagram bio @best_mobile_mechanic, Nextdoor). Warranty, deposit and "no add-ons without approval" wording are proposals for Marc to confirm. No stock photos are used; icons are inline SVG.

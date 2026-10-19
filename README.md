# DO IT RIGHT Mobile Auto Mechanic – sample website

Preview site built by Clyde ((832) 930-1707 · cuzclydecan@mail.grokbot.com) for Marc/Marcus, DO IT RIGHT Mobile Auto Mechanic, Houston · (832) 305-2630.
Single static file (`index.html`): no build step, no server, no tracking. The logo is embedded as a data URI.

## What works today (demo mode)
- **Click-to-call** buttons dial (832) 305-2630.
- **Service picker** → selections flow into the booking form.
- **Booking form**: validates required fields, then builds a summary the customer sends to Marc with one tap by **text (sms:)** or **email (mailto:)**. Photos are previewed on the page; the customer attaches them in the text/email (sms/mailto links cannot carry files).
- **Pay deposit / Pay invoice**: open a clearly marked *DEMO · TEST MODE* checkout preview. No card is collected and nothing can be charged.
- **Logo**: Marc's own logos, unchanged: the round badge from Instagram @best_mobile_mechanic (150 px, used small: header, footer, favicon, mobile hero) and the square logo from the Facebook page (720 px, desktop hero).

## Going live (edit the `CONFIG` block near the bottom of index.html)
```js
const CONFIG={
  FORM_ENDPOINT:"",   // form backend URL (empty = text/email hand-off)
  DEPOSIT_LINK:"",    // payment link for the visit deposit
  INVOICE_LINK:"",    // payment link where the customer types the amount
  SMS_TO:"+18323052630",
  EMAIL_TO:"doitrightmobile@gmail.com"
};
```
1. **Form backend**: create a Formspree form (account in Marc's name) and paste its endpoint (`https://formspree.io/f/<id>`) into `FORM_ENDPOINT`. Requests are emailed to Marc. With the endpoint set, the form posts with `fetch` and shows "Sent!"; if the post fails it falls back to the text/email hand-off.
   - Formspree Free: 50 submissions/month, no file uploads (customers text photos).
   - Formspree Personal: $10/mo billed yearly or $15 monthly, 200 submissions, 1 GB file uploads, so photos arrive with the request. (formspree.io/plans, checked Oct 19, 2026)
2. **Payments (recommended: Square free plan, $0/month)**, in Marc's own account:
   - Square Dashboard → Payment links → Create link → "Visit deposit" at Marc's amount → paste into `DEPOSIT_LINK`.
   - Create a second link → Collect a payment → allow buyer to enter amount → paste into `INVOICE_LINK`.
   - Fees (squareup.com/us/en/pricing, Oct 19, 2026): online/links/invoices 3.3% + 30¢; Tap to Pay on Marc's phone 2.6% + 15¢; next-day transfers free.
   - Optional: Square Appointments (free plan includes booking page, prepayments and deposits); point "Book a Visit" at the booking page if Marc prefers a calendar.
   - Stripe alternative: Payment Links (2.9% + 30¢ online, no monthly fee), Stripe Invoicing +0.4%, Tap to Pay in the Stripe Dashboard app.
3. **Domain**: register in Marc's name (recommended doitrightmobile.com; unregistered per Verisign RDAP on Oct 19, 2026). Porkbun $11.08/yr or Cloudflare at cost.

## Hosting
Preview: GitHub Pages from `main` / root. Live site: Cloudflare Pages (free), because GitHub says Pages is not meant for sites mainly used for commercial transactions. Add the custom domain in Cloudflare and keep the domain registered in Marc's name.

## Content sources
Hours, services, rating and reviews come from public listings checked Oct 19, 2026 (Google data via MechanicRank/CarHQ/LocalityBiz, Yelp via MapQuest/Roadtrippers, Instagram bio @best_mobile_mechanic, Nextdoor). Warranty, deposit and "no add-ons without approval" wording are proposals for Marc to confirm. No stock photos are used; icons are inline SVG.

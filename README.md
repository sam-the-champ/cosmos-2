# BAVIN PC1155 — Landing Page

## 1. Drop in your media
The page already looks for these exact files. Until they exist, each spot
shows a labeled placeholder (dashed box) instead of a broken image — so you
can preview the whole page before your assets are ready, and everything
lights up automatically the moment you add the real file at the same path.

```
assets/images/hero-product.png        — Hero product shot (transparent/cutout background looks best)

# Standalone video section (its own section, right after the hero)
assets/videos/product-demo.mp4        — Product demo video
assets/images/video-poster.jpg        — Poster frame shown before the video is played

# Interactive gallery (thumbnail strip + big stage), 6 images
assets/images/gallery-1.jpg           — Front view
assets/images/gallery-2.jpg           — Ports close-up
assets/images/gallery-3.jpg           — Built-in cables extended
assets/images/gallery-4.jpg           — In-hand, for scale
assets/images/gallery-5.jpg           — Accessories / what's in the box
assets/images/gallery-6.jpg           — Retail packaging
assets/images/gallery-thumb-1.jpg …6.jpg  — Small thumbnails matching the 6 slides above

# Sequential scroll showcase — one full-width image at a time, each fades in
# on its own as the visitor scrolls (not all visible on screen together)
assets/images/showcase-1.jpg          — Lifestyle: travel/airport
assets/images/showcase-2.jpg          — Lifestyle: desk/work
assets/images/showcase-3.jpg          — Packed in a bag

# Reviews, sharing, misc
assets/images/review-avatar-1.jpg …3.jpg  — Customer avatars
assets/images/og-cover.jpg            — Social share preview image (1200×630)
assets/images/logo.png                — Logo for structured data
assets/icons/favicon.png              — Browser tab icon

# Thank-you page
assets/images/thank-you-graphic.jpg   — Your own graphic/illustration, shown
                                         at the top of thank-you.html above the checkmark
```

That's 10 product/lifestyle photos in total (1 hero + 6 gallery + 3 showcase),
plus the video, avatars, and share/branding images. Any filename or extension
can be changed — just update the matching `src` in `index.html` /
`thank-you.html`.

## 2. Turn on real integrations (edit `js/config.js` only)
- **Meta Pixels** — add IDs to the `FACEBOOK_PIXELS` array (works with 1–5+ pixels).
- **GA4 / GTM / TikTok / Snapchat / Clarity / Hotjar** — fill in `ANALYTICS_CONFIG`.
- **EmailJS** (sends the order form to your inbox, no backend required):
  1. Create a free account at https://www.emailjs.com
  2. Add an Email Service → copy the **Service ID**
  3. Create a Template with variables: `full_name`, `phone`, `whatsapp`, `email`,
     `address`, `city`, `state`, `quantity`, `package`, `price`, `instructions`,
     `product`, `to_email` → copy the **Template ID**
  4. Copy your **Public Key** from Account → General
  5. Paste all three into `EMAILJS_CONFIG` in `js/config.js`
  - Until this is filled in, the form still validates and redirects to the
    thank-you page (useful for testing), it just won't email you.
- **WhatsApp** — set your number (digits only, country code, no `+`) in `WHATSAPP_CONFIG`.
- **Packages / pricing** — `PRODUCT_CONFIG.PACKAGES` in `js/config.js`. One entry
  per bundle (currently 1 / 2 / 3 units). Each entry drives three things at
  once: the pricing cards section, the package picker in the order form, and
  the sticky order summary — so there's only ever one place to edit a price.
  ```js
  PACKAGES: [
    { id: "pack-1", qty: 1, price: 53300,  label: "1 Power Bank",  tag: "" },
    { id: "pack-2", qty: 2, price: 93300,  label: "2 Power Banks", tag: "Most Popular" },
    { id: "pack-3", qty: 3, price: 113300, label: "3 Power Banks", tag: "Best Value" },
  ],
  DEFAULT_PACKAGE_ID: "pack-2", // pre-selected package + which pricing card is highlighted
  ```
  Add a 4th tier, change a price, or rename a label here and every part of the
  page updates automatically. There's no separate "payment method" field in
  the form anymore — package choice replaced it, since that's the decision
  that actually changes the order.
- **Business info** — `BUSINESS_CONFIG` for phone, email, address, hours.

## 3. File structure
```
index.html
thank-you.html
css/ styles.css · animations.css · responsive.css
js/  config.js · analytics.js · main.js · gallery.js · form.js
assets/ images/ videos/ icons/ fonts/
```

## 4. Notes
- No frameworks — hand-written HTML5, CSS3, and vanilla JS.
- Dark mode is the default; a theme toggle in the nav switches to light.
- `prefers-reduced-motion` is respected throughout.
- The signature "charge bar" motif (hero + section dividers) visualizes the
  30,000mAh capacity as the page loads and as you scroll.
- Exit-intent and "recently purchased" popups were intentionally left out —
  they're easy to bolt on later, but they cut against the calm, premium feel
  this page is going for. Say the word if you'd like either added.

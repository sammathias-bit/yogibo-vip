**To:** bheppler@yogibo.com
**Subject:** VIP creator page — ready for yogibovip.com

Hi Brett,

The VIP creator page is done. Review it here (click Music for the playlist): https://sammathias-bit.github.io/yogibo-vip/

Source: https://github.com/sammathias-bit/yogibo-vip — `index.html` is the whole page, `vip-assets/` has the logos and icons. Demo codes: YOGI-400 / YOGI-650 / YOGI-900.

Below is the brief, written so you can paste it straight into Claude with the repo.

---

**BRIEF: deploy index.html from github.com/sammathias-bit/yogibo-vip to yogibovip.com (Shopify)**

1. **Page.** Standalone HTML, no theme dependency, no customer login. Put it on a custom page template (`page.vip.liquid` or a JSON template with one custom-liquid section), hide the theme header/footer on that template, and make it the store's landing page. Drop my doctype/head wrapper; keep the `<title>`, Google Fonts `<link>` tags and the `<style>` block. Libraries load from CDN (GSAP 3.12.5 + ScrollTrigger on cdnjs, Lenis 1.1.18 on jsDelivr).

2. **Assets.** Everything is already in Content → Files. Replace the relative paths: logos → `Main.Logo.Dark.BG-1077x433-…` and `Main.Logo-1077x433-…`; the 11 icons → `holiday26-icon-*.png` (each `--ic:url(...)` in the icon row). No photos on the page.

3. **Invite codes = Shopify gift cards.** One per creator; balance = the "credit", expiry = the season, single use. Creator name + deliverables/brief live in a gift-card metafield (or the "Yogbio UGC Directory MAIN ONE" sheet, keyed by code). Build one small endpoint (app proxy / serverless, Admin API):
   - **Open** → look up code → return `{ name, balance, expires, deliverables[] }`. Replace the `CODES` map at the bottom of the script with this call.
   - **Submit** → create a draft order for the picks, pay it with the gift card (balance → 0), tag `VIP`, email sam.mathias@yogibo.com, append a row to the UGC sheet. Warehouse fulfils the draft order.

4. **Forms.** `#giftForm` (order: creator, code, credit, picks, total, signature, signed_on, handle, email, address, city, state, zip, notes) → Submit above. `#reqForm` ("Not invited?" pop-up: handle, platform, email, audience, about) → email sam.mathias@yogibo.com, separate subject. Both fake success today.

5. **Products.** `PRODUCTS` in the script is placeholder. Pull live names/prices for Max, Midi, Mini, Short, Lounger, Pod, Support, Moon Pillow, Roll Max/Midi/Mini, Zoola Max/Midi/Pod, extra covers. No Modju, no Double Max. 800×600 image slot per tile.

6. **Marketing fills.** Agreement text in the modal (final copy from `Yogibo_VIP_Creator_Agreement_NH_5.docx`); Creator of the Month card `#spot` (handle, platform, product, 1080×1350 thumbnail, post caption — add `hidden` when there's no pick; no numbers). Anything tagged PLACEHOLDER.

7. **Music.** Spotify embed of playlist `6AqH38HkW1Eyyuw6AEW6Jt`; loads only on real domains (`canEmbed` check). Delete the MP3/synth fallback once confirmed.

8. **QA.** Real test gift card opens the picker and counts credit down; agreement checkbox enables only after scrolling to the end; submit creates the draft order, zeroes the card, sends email + sheet row; nav goes light over white sections; music plays; phone: VIP opener auto-plays, banners stack, forms usable.

---

Happy to do a 15-minute walkthrough if useful.

Thanks,
Sam

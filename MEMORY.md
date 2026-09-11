# MEMORY — anveshvision

Marketing site for Anveshvision: an agency with two verticals —
**corporate gifting** and **digital signature certificates (DSC)**.

## Stack
- **Language:** HTML5, vanilla JS (no framework)
- **Framework:** none — single static `index.html`
- **Styling:** Tailwind CSS via CDN (`cdn.tailwindcss.com`) + a small `<style>` block
- **Package manager:** none (no `package.json`)
- **Database:** none
- **Testing:** none
- **Icons:** Iconify web component (`iconify-icon`), `solar:*` set
- **Fonts:** Cormorant Garamond (display) + DM Sans (body), Google Fonts
- **Hosting:** GitHub Pages — https://sugandhsam.github.io/anveshvision/
- **Repo:** github.com/sugandhsam/anveshvision (public, `main`)

## Invariants
- **Corporate gifting comes first, DSC second** — in the hero cards, nav, eyebrow
  and stats. Ordering is deliberate; don't reverse it.
- **Nav is exactly `Home · Corporate Gifting · DSC`.** No About, no Contact.
- **Every CTA button reads "Talk to Us"** with a `ri:whatsapp-line` icon and opens
  `https://wa.me/919818221255` (new tab). The two "Planning a gifting round?" /
  "Certificate expiring soon?" cards go there too. There is no `#contact` section.
- **Footer carries the legal block:** Anvesh Vision Pvt. Ltd., 305C, Pocket 2,
  Mayur Vihar Phase 1, Delhi 110091, GST No. 07AARCA1408J1ZM (bold). Copyright
  line uses the same legal name.
- **Colour = vertical.** Navy `#172535` is DSC, warm sand `#f4eedc` is gifting,
  ink `#16140d` is primary, cream `#fcf9f5` is page. Hover states follow this.
- **`font-serif` elements keep `font-light`**; sans body text is `font-normal`.
  Thin weights are only a problem at small sizes.
- **Hero height** = `100dvh` minus the *measured* banner + nav height, written to
  `--chrome-h` by JS on load/resize. Never hard-code that offset — the nav is
  taller on desktop than mobile.
- **Anything that changes banner height must dispatch a `resize` event**, or the
  hero's `--chrome-h` goes stale. The rotating banner already does this.
- **`noindex` + `robots.txt` stay until real copy lands.** Every figure on the
  site is currently invented.
- Visuals are gradient blocks + large Iconify icons. One real photo so far:
  `assets/leather-desk-set.webp` (4:3 WebP, ~56 KB) on the Leather Desk Sets card.
  New product photos go in `assets/` as 4:3 WebP.

## Decisions
- **What:** Hero = headline + two vertical cards, headline *below* the cards.
  **Why:** Sam chose cards over split-screen/tabs/asymmetric; the verticals are
  the page's job, the headline is a closing statement.
  **Rejected:** split-screen hero (no brand voice), tabbed hero (hides half the
  offer), asymmetric offset panels (fragile on mobile).
- **What:** DM Sans for body, replacing Jost.
  **Why:** Jost is geometric with a low x-height; at 300 weight, 14px, 70% opacity
  and global `tracking-wide` it was illegible. DM Sans keeps the geometric feel
  with a far taller x-height.
  **Rejected:** Inter (more legible but generic, flattens the editorial feel),
  Work Sans (too warm for the compliance half), repairing Jost in place.
- **What:** Static grid for the gifting range, not a carousel.
  **Why:** Buyers compare finishes side by side; carousels hide items, need JS,
  and perform badly on mobile.
- **What:** Testimonials section deleted outright.
  **Why:** The template's three quotes were real, named endorsements given to a
  different business ("Creatives by GO" / Gaby) — a liability once public.
  Markup preserved in the session scratchpad.
- **What:** Two variation axes on the range section — finish chips on small cards,
  price tiers on the wide card.
  **Why:** They are the two things a corporate buyer actually decides between:
  "what will my logo look like" and "what can I spend per head".
- **What:** Tailwind left on the CDN.
  **Why:** Prototype speed. Must change before this is a real business site —
  it compiles in-browser and logs a console warning.

## Session log

### 2026-08-25
**Worked on:** Converting a scavenged social-media-agency template into the
Anveshvision two-vertical site, then shipping it to GitHub Pages.

**Completed:**
- Fixed template breakage: missing `<!DOCTYPE>`, and Google Fonts that had
  `preconnect` but no stylesheet link (so neither typeface was ever loading).
- Hero rebuilt: eyebrow, two vertical cards, statement + CTA, trust strip.
  Viewport-height via measured `--chrome-h`.
- Two service grids (gifting, DSC), 5 cells + CTA cell each; wired `#gifting`
  and `#signatures` anchors.
- Stats bar reworked to alternate gifting/DSC figures.
- Portfolio replaced with a gifting range: 3 product cards (finish chips, MOQ)
  plus a 4-tier kit card.
- Client logo marquee — finally uses the `.marquee-container` / `animate-scroll`
  CSS that sat unused in the template.
- Footer simplified to brand + 3 nav links; removed the services column.
- Body type swap to DM Sans, applied site-wide: 28 weight changes, 21 size
  bumps, 15 micro-label bumps, 71 opacity lifts.
- Mobile menu built from scratch (the hamburger was decorative): scroll lock,
  Escape, focus management, closes on anchor jump, force-closes above `lg`.
- SVG favicon + `theme-color`.
- Rotating top banner, 4 messages, fade, pausable, reduced-motion aware.
- Removed testimonials, added `noindex` + `robots.txt`, published to Pages.
- Patched `AGENT/git-hooks/lib/worktree-policy.sh` for unborn HEAD.

**In progress / not done:**
- `#contact` does not exist — all four "Talk to Us" buttons are inert. Sam
  deferred this ("we will link these later").
- No About section.
- 6 `href="#"` links go nowhere (logo ×2, Instagram, LinkedIn).
- `type-test.html` (type specimen) and `index.html.bak` still in the working
  tree, both gitignored.
- The `worktree-policy.sh` patch is uncommitted — AGENT is on `main`, so the
  hook blocks committing the hook.

**Next priorities:**
1. Real content: replace every invented figure (see `## Invariants`), then drop
   `noindex` + `robots.txt`.
2. Build the contact section and wire the four CTAs.
3. Own testimonials, if that section is wanted back.
4. SEO/social meta — no `description` or `og:` tags exist.
5. Move Tailwind off the CDN into a build.
6. Raster favicon fallback (`favicon.ico`, `apple-touch-icon.png`) — SVG
   favicons don't render in Safari.

### 2026-09-11
**Worked on:** Contact + legal details, first product photo.

**Completed:**
- Footer address + GSTIN block; copyright → "Anvesh Vision Pvt. Ltd."
- All 5 "Talk to Us" buttons + 2 prompt cards → WhatsApp `wa.me/919818221255`
  (hero button's trailing arrow replaced by the WhatsApp icon).
- Leather Desk Sets card: icon swapped for `assets/leather-desk-set.webp`.
- MEMORY.md / ERRORS.md first committed to the repo.

**Next priorities:** real photos for the other range cards, real copy/figures
so `noindex` + `robots.txt` can come off.

# Propsoch Landing Page — Analysis & Improvement Report

## Part 1: Analysis

### Current Lighthouse Score Estimates

Based on visual inspection and page audit:

| Category | Estimated Score | Key Issues |
|---|---|---|
| Performance | ~55–65 | Multiple unoptimized videos autoloading, LCP delayed by hero image via CDN, render-blocking scripts |
| Accessibility | ~60–70 | Missing alt texts on several images, low contrast in some text areas, no visible focus indicators |
| Best Practices | ~70–80 | Mixed content concerns, some console errors from video load failures |
| SEO | ~75–85 | Good meta title/desc, but thin H-tag hierarchy and missing structured data |

---

### 5 UX/UI Issues & How to Fix Them

#### Issue 1 — Hero Section Lacks Clear Visual Hierarchy
**Problem:** The hero has a headline ("Visit curated homes, negotiate smarter & buy intelligently") but the supporting copy, CTA button, and city selector are visually flat. There's no size contrast or typographic weight differentiation that draws the eye to a single action.

**Fix:** Redesign the hero with a bold display typeface for the headline (3xl–5xl), a clearly contrasting CTA button with high-visibility color, and deprioritize the city selector below the primary CTA. Add a short, punchy sub-headline. Use a single focal illustration or gradient background instead of the video thumbnail that loads slowly.

---

#### Issue 2 — Performance Hit from Autoloading Videos
**Problem:** The page embeds 6+ `.mp4` video elements for the step-by-step journey section. These are likely loaded on mount even before the user scrolls, causing significant bandwidth usage and degrading LCP/FID scores.

**Fix:** Replace autoplay videos with `loading="lazy"` on iframes or use IntersectionObserver to load videos only when they enter the viewport. Use poster images (static thumbnails) for all video tags. Convert short animations to CSS/Lottie for better performance.

---

#### Issue 3 — Mobile Navigation is Cramped & Missing a Sticky CTA
**Problem:** On mobile, the top nav collapses into a hamburger but the primary CTA ("Get Started") is buried below the fold. Mobile users often abandon before scrolling.

**Fix:** Add a sticky bottom bar on mobile with a single prominent CTA ("Talk to an Expert" or "Get Started"). Ensure the hamburger menu has adequate tap targets (≥44×44px). Reduce nav link clutter by grouping under dropdowns.

---

#### Issue 4 — Testimonials Section Has No Filtering or Pagination
**Problem:** The page renders 20+ full-text testimonials in a long scroll. This overloads the DOM, increases page weight, and creates a monotonous reading experience. Many users skip the entire section.

**Fix:** Display 3–4 featured testimonials initially with a "Load more" or carousel approach. Add a simple filter by buyer type (NRI, first-time buyer, investor). Show star ratings visually instead of only text. Reduce each card to 3–4 lines with an expandable "Read more."

---

#### Issue 5 — Low Colour Contrast & Inaccessible Focus States
**Problem:** Light grey text on white backgrounds (e.g., subheadings, stage descriptions) fails WCAG AA contrast ratios. Interactive elements (tabs, links) have no visible keyboard focus ring.

**Fix:** Ensure all body text meets 4.5:1 contrast ratio. Use a minimum text color of `#444` on white. Add explicit `focus-visible` ring styles to all interactive elements. Audit with axe DevTools and fix failures before deployment.

---

## Part 2: Improved Landing Page

The improved landing page is in `index.html` (see attached file).

### What Was Rebuilt
- **Hero Section** — Bold typographic redesign, clear single CTA, trust signals inline, no video dependency
- **How It Works / Journey Section** — Redesigned as a step-by-step vertical timeline with icons, fast-loading, no videos
- **Testimonials Section** — Compact cards with ratings, avatars, and expandable text, limited to 4 visible initially

### Tech Approach
Since this is a deliverable file (not a full Next.js repo), the HTML file uses:
- Tailwind CSS (CDN) for rapid utility styling
- Google Fonts (Playfair Display + DM Sans) for distinctive typography
- Vanilla JS for accordion/testimonial interactions
- No external video dependencies — all animations are CSS-only

For the actual Next.js submission, the same structure maps to:
- `/app/page.tsx` — main page component
- `/components/Hero.tsx`, `Journey.tsx`, `Testimonials.tsx`
- Tailwind config with custom tokens

---

## Part 3: What I Improved & Why

### Typography
Replaced the flat sans-serif-only hierarchy with **Playfair Display** (serif display) for headlines and **DM Sans** for body. This creates a premium, editorial feel appropriate for a high-stakes purchase like real estate — and immediately differentiates from commodity broker sites.

### Hero
The original hero asks users to "Select a city" immediately, which is a high-friction first step. The new hero leads with the value proposition and a low-friction CTA ("Talk to an Expert") before asking for any input. This reduces bounce and improves conversion.

### Performance
Removed all video elements from above-the-fold. Replaced process steps with CSS-animated timeline cards. This alone can improve LCP by 2–4 seconds.

### Accessibility
Added proper `aria-label` on all interactive elements, ensured color contrast ≥ 4.5:1, and added visible focus rings. Added semantic HTML (`<main>`, `<section>`, `<nav>`, `<article>`).

### Mobile
Added a sticky bottom CTA bar for mobile, increased touch target sizes, and made the testimonial grid single-column on small screens.

### Trust Signals
Moved key stats (1000+ buyers, ₹4.78L average savings, 25-day average) directly into the hero section instead of hiding them below the fold — these are compelling differentiators that should be front and center.

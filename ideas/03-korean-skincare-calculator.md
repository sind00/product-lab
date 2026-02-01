# Korean vs American Skincare Calculator
## Exposing the Price Gap in Aesthetic Treatments

---

## The Problem

The same skincare and aesthetic treatments cost dramatically different amounts in Korea vs America:

| Treatment | Korea | USA | Difference |
|-----------|-------|-----|------------|
| Laser facial | $50-100 | $300-500 | 5-6x |
| Botox (per unit) | $5-8 | $12-18 | 2-3x |
| Microneedling | $50-80 | $200-400 | 4-5x |
| Chemical peel | $30-50 | $150-300 | 4-5x |
| LED therapy | $20-40 | $100-200 | 4-5x |

**The insight:** American skincare philosophy emphasizes expensive, infrequent treatments. Korean philosophy emphasizes affordable, regular maintenance.

**The opportunity:** Help Americans understand the cost of their current approach and explore alternatives.

---

## The Solution

A simple calculator that:
1. Takes your current skincare/treatment routine
2. Shows what you're spending annually
3. Shows what it would cost in Korea
4. Calculates potential savings
5. Suggests alternatives for getting Korean-style care in America

---

## Core UX Flow

```
1. LANDING PAGE
   Headline: "You're overpaying for skincare. Here's the math."
   Subhead: "See what your treatments would cost in Korea."
   CTA: "Calculate My Savings"

2. TREATMENT SELECTION
   Multi-select from treatment categories:
   - Laser treatments
   - Injectables
   - Facials
   - At-home products

   For each selected:
   - "How often per year?" (slider or dropdown)
   - "What do you currently pay?" (optional, or use average)

3. RESULTS PAGE
   Big number: "You're spending $X,XXX/year"
   Comparison: "In Korea, this would cost $XXX"
   Savings: "You'd save $X,XXX (XX%)"

   Breakdown table showing each treatment

4. RECOMMENDATIONS
   - "How to get Korean-style care in America"
   - Affordable alternatives
   - Medical tourism info (optional)
   - Newsletter signup for tips

5. SHARE
   Shareable result card for social media
```

---

## Technical Architecture

This is a simple, standalone web app. No shared architecture needed.

```
┌─────────────────────────────────────────────┐
│            FRONTEND (React/Next.js)          │
├─────────────────────────────────────────────┤
│ • Multi-select treatment picker              │
│ • Frequency inputs                           │
│ • Price comparison visualization             │
│ • Shareable result cards                     │
│ • Mobile-responsive design                   │
└─────────────────┬───────────────────────────┘
                  │
                  ▼
┌─────────────────────────────────────────────┐
│            DATA LAYER (Static JSON)          │
├─────────────────────────────────────────────┤
│ • Treatment database                         │
│ • US price ranges (by region?)               │
│ • Korea price ranges                         │
│ • Alternative treatment mappings             │
└─────────────────────────────────────────────┘
                  │
                  ▼
┌─────────────────────────────────────────────┐
│            OPTIONAL FEATURES                 │
├─────────────────────────────────────────────┤
│ • Clinic finder map (future)                 │
│ • Email capture (Resend/ConvertKit)          │
│ • Affiliate links to products                │
└─────────────────────────────────────────────┘
```

---

## Treatment Database (Starting Data)

### Laser Treatments

| Treatment | Korea Avg | US Avg | Frequency Typical |
|-----------|-----------|--------|-------------------|
| IPL (Intense Pulsed Light) | $50-80 | $300-500 | 3-4x/year |
| Fractional CO2 | $100-200 | $500-1000 | 1-2x/year |
| Pico Laser | $80-150 | $400-800 | 2-4x/year |
| V-Beam (redness) | $60-100 | $300-500 | 2-4x/year |
| Laser hair removal (face) | $20-40 | $150-300 | 6x/year |

### Injectables

| Treatment | Korea Avg | US Avg | Frequency Typical |
|-----------|-----------|--------|-------------------|
| Botox (per unit) | $5-8 | $12-18 | 20-60 units, 3-4x/year |
| Filler (per syringe) | $200-400 | $600-1000 | 1-2x/year |
| Skinboosters | $100-200 | $400-700 | 3-4x/year |

### Facials & Peels

| Treatment | Korea Avg | US Avg | Frequency Typical |
|-----------|-----------|--------|-------------------|
| Basic facial | $30-50 | $100-200 | Monthly |
| Chemical peel | $30-60 | $150-300 | 4-6x/year |
| Microneedling | $50-100 | $200-500 | 4-6x/year |
| Hydrafacial | $60-100 | $200-400 | Monthly |
| LED therapy | $20-40 | $75-150 | Weekly-monthly |

---

## Name Options

| Name | Vibe | Notes |
|------|------|-------|
| **GlowGap** | Catchy, implies the difference | Check availability |
| **SeoulSave** | Clear value prop | Geographic |
| **SkinFlip** | Short, arbitrage vibe | Memorable |
| **GlassSkinPrice** | Aspirational (glass skin trend) | Longer |
| **K-Beauty Calc** | SEO-friendly, obvious | Generic |
| **BeautyCostGap** | Descriptive | Less catchy |

**Recommendation:** GlowGap or SkinFlip

---

## Monetization Options

| Model | How It Works |
|-------|--------------|
| **Free + Email capture** | Build list, monetize later |
| **Free + Affiliate** | Links to products, clinics |
| **Free + Guide upsell** | Detailed "How to get K-beauty in USA" guide for $9.99 |
| **Free + Lead gen** | Partner with affordable clinics for referrals |

Recommendation: **Free tool + email capture + optional guide upsell**

---

## Distribution Channels

| Channel | Approach | Potential |
|---------|----------|-----------|
| r/SkincareAddiction | "I built a calculator..." | 2M+ members |
| r/AsianBeauty | Core audience | 1.5M+ members |
| r/30PlusSkinCare | Price-conscious | 500k+ |
| TikTok | "You're overpaying by X%" | Viral potential |
| Instagram Reels | Same content | Different audience |
| Product Hunt | Launch | Tech-savvy skincare people |

**Viral hook:** The shocking price difference. People love sharing "look how much I'm overpaying."

---

## Future Features (V2+)

- **Clinic finder map:** Show affordable alternatives near user
- **Treatment tracker:** Log what you've done, when, cost
- **"Build my routine" tool:** Recommend treatments based on goals
- **Medical tourism calculator:** Include flights, accommodation
- **Provider directory:** Vetted affordable clinics in US

---

## MVP Scope (Build in 4-6 hours)

**V0 (Ship today):**
- [ ] Treatment multi-select (10-15 common treatments)
- [ ] Frequency selector per treatment
- [ ] Price comparison calculation
- [ ] Results display with big savings number
- [ ] Mobile-responsive
- [ ] Deploy to Vercel

**Enhancements (Day 2):**
- [ ] Shareable result cards
- [ ] Email capture
- [ ] Basic SEO (meta tags, OG images)

**V1 (Week 2):**
- [ ] More treatments
- [ ] Regional US pricing
- [ ] Recommendations section
- [ ] Guide upsell

---

## Design Notes

**Vibe:** Clean, modern, trustworthy. Not salesy.

**Key visuals:**
- Big, bold savings number
- Side-by-side comparison bars
- Before/after cost visualization
- Shareable social card with personalized results

**Tone:** Informative, slightly provocative ("You're overpaying"), but not preachy.

---

## Content for Landing Page

### Headline Options
- "You're overpaying for skincare. Here's the math."
- "What if your skincare cost 80% less?"
- "The $3,000 mistake American women make every year"
- "Korean women pay $50 for what you pay $400 for"

### Subhead
- "See exactly what your treatments would cost in Korea — and how to get those prices here."

### Social Proof (future)
- "Join 10,000+ people who've calculated their skincare savings"

---

## Competitive Landscape

| Competitor | What They Do | Gap |
|------------|--------------|-----|
| RealSelf | Treatment info + reviews | No price comparison tool |
| Groupon | Discounted treatments | No education, hit-or-miss quality |
| Various blogs | Price comparison articles | Not interactive, not personalized |

**Your differentiation:** Interactive, personalized, shareable. Nobody has a dedicated calculator for this.

---

## Open Questions

- [ ] Where to get accurate Korea pricing data? (Personal research, expat communities)
- [ ] Regional US pricing? (LA vs NYC vs midwest)
- [ ] How to handle price ranges? (Show min/avg/max?)
- [ ] Partner opportunities? (Korean clinics, medical tourism agencies)

---

## Build Priority

This is the **standalone quick-win** product:
- Simplest technical build
- No AI required
- Viral potential
- Clear monetization path
- Can ship in one day

Recommend building this FIRST while developing the more complex AI FaceTime products in parallel.

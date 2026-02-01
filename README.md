# Product Lab

---

## What Is This?

This repository to identify, validate, and build digital products. 

---

## Repository Structure

```
/
├── README.md                          # You are here
│
├── methodology.md                     # The master methodology document
│
├── /ideas                             # Individual product specs
│   ├── 01-makeup-expiration-checker.md
│   ├── 02-vet-decision-tool.md
│   ├── 03-korean-skincare-calculator.md
│   ├── 04-ai-tool-finder.md
│   └── 05-makeup-inventory-tracker.md
│
├── /architecture                      # Technical architecture docs
│   └── ai-facetime-companion.md       # Shared architecture for video AI products
│
└── /research                          # User research materials
    └── vet-tool-interview-questions.md
```

---

## The Products

### Quick Wins (Ship in 1 day)

| Product | Description | Status |
|---------|-------------|--------|
| **Korean Skincare Calculator** | Show price gap between US and Korea treatments | 📋 Spec complete |

### AI FaceTime Companions (Ship in 1-2 weeks)

These share a common architecture — real-time video + conversational AI.

| Product | Description | Status |
|---------|-------------|--------|
| **Makeup Expiration Checker** | Point camera at makeup, get safety verdict | 📋 Spec complete |
| **Vet Decision Tool** | Point camera at pet, get vet urgency assessment | 📋 Spec complete, needs research |
| **Makeup Inventory Tracker** | Scan and catalog your makeup collection | 📋 Spec complete |

### Discovery/Directory (Longer timeline)

| Product | Description | Status |
|---------|-------------|--------|
| **AI Tool Finder (canai.dev)** | Searchable database of AI tools by use case | 📋 Spec complete, lower priority |

---

## The Methodology

See `methodology.md` for the full framework covering:

- **Phase 0:** Infrastructure Setup
- **Phase 1:** Audience-First Discovery
- **Phase 2:** Problem Extraction
- **Phase 3:** Demand Stress Test
- **Phase 4:** Solution Spec
- **Phase 5:** Cross-Validation
- **Phase 6:** Final Ranking + Selection

Key insight: **Find the audience first, then find their problem.**

---

## Next Steps

1. [ ] Interview roommate about Vet Tool (see `/research/vet-tool-interview-questions.md`)
2. [ ] Pick domain name for Korean Skincare Calculator (GlowGap? SkinFlip?)
3. [ ] Build Korean Skincare Calculator (simplest, ships fastest)
4. [ ] Build Makeup Expiration Checker (AI FaceTime foundation)
5. [ ] Extend to Vet Tool and Inventory Tracker

---

## Tech Stack (Planned)

| Layer | Technology |
|-------|------------|
| Frontend | Next.js 14+, Tailwind CSS |
| AI | Gemini 2.0 Flash (multimodal) |
| Voice | Web Speech API → ElevenLabs |
| Database | Supabase (free tier) |
| Hosting | Vercel (free tier) |
| Payments | Gumroad or LemonSqueezy |

---

## Constraints

- Monthly costs: <$15
- Price point: $5-10 (impulse purchase)
- Build time per MVP: 1 day ideally
- Distribution: Organic first (Reddit, TikTok), paid as backup

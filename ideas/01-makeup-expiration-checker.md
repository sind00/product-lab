# Makeup Expiration Checker
## AI FaceTime Companion for Cosmetic Safety

---

## The Problem

People keep makeup products far longer than they should. Expired cosmetics can harbor bacteria, cause infections, and degrade in effectiveness. Most people don't know:
- When they opened a product
- What the PAO (Period After Opening) symbol means
- How to decode batch codes to find manufacturing dates

**The anxiety:** "Am I putting bacteria on my face?"

---

## The Solution

A live video AI companion that feels like FaceTiming your beauty-savvy friend. Point your camera at any makeup product and get instant, conversational guidance.

---

## Core UX Flow

```
1. USER opens app, grants camera permission
2. ONBOARDING: "What brings you here today?"
   - "I want to check if something is expired"
   - "I want to inventory my collection"
   - "I have a specific concern about a product"

3. LIVE VIDEO MODE activates
   - AI voice: "Show me what you're curious about"
   - User points camera at product

4. AI DETECTION
   - Recognizes product type (mascara, lipstick, etc.)
   - Highlights detected object on screen
   - Voice: "I see that's a mascara. Can you show me the bottom?"

5. GUIDED INSPECTION
   - AI asks to see PAO symbol (little jar icon)
   - AI asks to see batch code
   - If camera shaky → auto-captures still image

6. CONVERSATION
   - "Do you remember when you opened this?"
   - User can speak or tap response
   - AI factors in their answer

7. VERDICT
   - Clear result: ✅ Safe / ⚠️ Replace Soon / ❌ Expired
   - Explanation: "Mascaras should be replaced every 3 months because..."
   - Option to add to inventory tracker
```

---

## Technical Architecture

```
┌─────────────────────────────────────────────┐
│            FRONTEND (React/Next.js)          │
├─────────────────────────────────────────────┤
│ • Camera access (getUserMedia API)           │
│ • Real-time video display                    │
│ • Shake detection (DeviceMotion API)         │
│ • Voice synthesis (ElevenLabs or Web Speech) │
│ • Voice input (Whisper API or Web Speech)    │
│ • UI overlays (bounding boxes, highlights)   │
└─────────────────┬───────────────────────────┘
                  │
                  ▼
┌─────────────────────────────────────────────┐
│            AI LAYER (Multimodal)             │
├─────────────────────────────────────────────┤
│ • Gemini 2.0 Flash OR GPT-4o                 │
│ • Video stream analysis                      │
│ • Conversational guidance                    │
│ • Structured output for verdicts             │
└─────────────────┬───────────────────────────┘
                  │
                  ▼
┌─────────────────────────────────────────────┐
│            DOMAIN KNOWLEDGE                  │
├─────────────────────────────────────────────┤
│ • PAO database (product type → shelf life)   │
│ • Batch code decoder (brand → date format)   │
│ • Product recognition training data          │
└─────────────────────────────────────────────┘
```

---

## PAO Reference Data (Starting Point)

| Product Type | PAO (Months) | Notes |
|--------------|--------------|-------|
| Mascara | 3-6 | Highest bacteria risk, replace frequently |
| Liquid eyeliner | 3-6 | Same risk as mascara |
| Pencil eyeliner | 12-24 | Can be sharpened to refresh |
| Foundation (liquid) | 12 | Pump bottles last longer |
| Foundation (powder) | 24 | Very stable |
| Concealer | 12 | Similar to foundation |
| Lipstick | 18-24 | Relatively stable |
| Lip gloss | 12 | More moisture = more risk |
| Blush (powder) | 24 | Very stable |
| Blush (cream) | 12-18 | More moisture |
| Eyeshadow (powder) | 24 | Very stable |
| Eyeshadow (cream) | 12 | More moisture |
| Skincare (water-based) | 6-12 | Check for separation |
| Skincare (oil-based) | 12-24 | More stable |
| Sunscreen | 12 | Critical for effectiveness |
| Nail polish | 24 | Look for separation |

---

## Batch Code Resources

Most brands encode manufacturing date in batch codes. Resources:
- [CheckCosmetic.net](http://checkcosmetic.net) — Decodes many brands
- [Cosmetic Calculator](http://cosmeticcalculator.com) — Similar tool
- Brand-specific patterns (need to build database)

Common patterns:
- First digit = year (e.g., "3" = 2023)
- Second digit = month (A-L or 1-12)
- Varies significantly by brand

---

## Monetization Options

| Model | Price | What User Gets |
|-------|-------|----------------|
| **Freemium** | Free / $6.99 | 3 free checks, then pay for unlimited |
| **One-time** | $9.99 | Lifetime access |
| **Subscription** | $2.99/mo | Ongoing updates, inventory sync |

Recommendation: **One-time $6.99-9.99** for MVP. Lower friction.

---

## Distribution Channels

| Channel | Approach | Notes |
|---------|----------|-------|
| r/MakeupAddiction (2M+) | "I built this for myself" post | Show demo video |
| r/SkincareAddiction (2M+) | Cross-post | Same audience |
| TikTok | Demo video (doesn't need your face) | High viral potential |
| Product Hunt | Launch day push | Good for initial traffic |
| Beauty YouTubers | Outreach for review | Longer-term play |

---

## MVP Scope (Build in 1-2 days)

**V0 (Day 1):**
- [ ] Basic camera feed display
- [ ] Text input: Product type + open date
- [ ] Hardcoded PAO logic
- [ ] Simple verdict UI
- [ ] Deploy to Vercel

**V1 (Day 2-3):**
- [ ] Voice guidance (AI speaks)
- [ ] Voice input (user speaks)
- [ ] Shake detection → snapshot
- [ ] Product detection highlighting

**V2 (Week 2):**
- [ ] Batch code OCR
- [ ] Multi-product inventory
- [ ] Reminder notifications

---

## Competitive Landscape

| Competitor | What They Do | Gap |
|------------|--------------|-----|
| Beauty Keeper app | Manual expiration tracking | No camera, no AI guidance |
| CheckCosmetic.net | Batch code lookup | Website only, no mobile UX |
| Notion templates | Manual tracking | No intelligence |

**Your differentiation:** Real-time AI companion UX. Nobody else does the "FaceTime your beauty friend" experience.

---

## Open Questions

- [ ] What's the best multimodal AI for real-time video? (Gemini 2.0 Flash vs GPT-4o)
- [ ] Voice: ElevenLabs vs native Web Speech API?
- [ ] How to handle products without visible batch codes?
- [ ] Privacy: Process video locally or send to cloud?

---

## Related Products (Shared Architecture)

This product shares the "AI FaceTime Companion" architecture with:
- Vet Decision Tool
- Makeup Inventory Tracker

See: `architecture/ai-facetime-companion.md`

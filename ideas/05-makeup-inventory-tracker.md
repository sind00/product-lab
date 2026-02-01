# Makeup Collection Inventory Tracker
## AI FaceTime Companion for Organizing Your Beauty Products

---

## The Problem

Beauty enthusiasts accumulate products but lose track of:
- What they own (duplicates, forgotten products)
- When they opened things (expiration tracking)
- What needs restocking
- Total value/investment in their collection

**The guilt:** "I know I'm wasting money on expired makeup and buying duplicates."

---

## The Solution

A live video AI companion that helps you catalog your entire makeup collection. Point your camera, scan products, build your inventory conversationally.

This is an extension of the Makeup Expiration Checker — same tech, different primary goal.

---

## Core UX Flow

```
1. ONBOARDING
   "Let's organize your makeup collection together!"
   Choose starting point:
   - "Scan everything" (full inventory mode)
   - "Just check a few things" (quick scan)
   - "Add something new I just bought"

2. LIVE VIDEO SCANNING MODE
   AI guides you through your collection:
   - "Let's start with your face products. Grab your foundations."
   - "Hold that one up... got it! Maybelline Fit Me, shade 220."
   - "When did you open this?"
   - "Now show me the next one..."

3. SMART DETECTION
   - Recognizes product (brand, name, shade if visible)
   - Auto-categorizes (face, eyes, lips, etc.)
   - Estimates value (optional, from price database)
   - Flags potential expiration issues

4. INVENTORY DASHBOARD
   After scanning, see:
   - Total products by category
   - Products expiring soon
   - Duplicates flagged
   - Estimated collection value
   - Usage patterns (if tracking over time)

5. ONGOING MANAGEMENT
   - Add new purchases
   - Mark items as finished/tossed
   - Get restock reminders
   - Share collection (optional)
```

---

## Technical Architecture

Same shared architecture as other AI FaceTime products:

```
┌─────────────────────────────────────────────┐
│            FRONTEND (React/Next.js)          │
├─────────────────────────────────────────────┤
│ • Camera access (getUserMedia API)           │
│ • Real-time video display                    │
│ • Shake detection (DeviceMotion API)         │
│ • Voice synthesis (ElevenLabs or Web Speech) │
│ • Voice input (Whisper API or Web Speech)    │
│ • Inventory dashboard UI                     │
│ • Product cards                              │
└─────────────────┬───────────────────────────┘
                  │
                  ▼
┌─────────────────────────────────────────────┐
│            AI LAYER (Multimodal)             │
├─────────────────────────────────────────────┤
│ • Gemini 2.0 Flash OR GPT-4o                 │
│ • Product recognition from video            │
│ • Conversational guidance                    │
│ • Category inference                         │
└─────────────────┬───────────────────────────┘
                  │
                  ▼
┌─────────────────────────────────────────────┐
│            DATA LAYER                        │
├─────────────────────────────────────────────┤
│ • User inventory (Supabase)                  │
│ • Product database (brands, prices, PAO)     │
│ • Categories taxonomy                        │
└─────────────────────────────────────────────┘
```

---

## Data Model

```sql
-- User's inventory
inventory_items (
  id uuid primary key,
  user_id uuid,
  product_name text,
  brand text,
  category text, -- foundation, mascara, etc.
  shade text,
  size text,
  purchase_date date,
  opened_date date,
  expiration_date date, -- calculated from opened_date + PAO
  estimated_value decimal,
  status enum (active, finished, tossed, expired),
  photo_url text, -- snapshot from scanning
  notes text,
  created_at timestamp,
  updated_at timestamp
)

-- Product reference database
products (
  id uuid primary key,
  brand text,
  name text,
  category text,
  typical_price decimal,
  pao_months int,
  -- Additional metadata
)
```

---

## Category Taxonomy

| Category | Subcategories |
|----------|---------------|
| **Face** | Foundation, concealer, primer, setting powder, setting spray |
| **Cheeks** | Blush, bronzer, contour, highlighter |
| **Eyes** | Eyeshadow, eyeliner, mascara, brow products |
| **Lips** | Lipstick, lip gloss, lip liner, lip balm |
| **Skincare** | Cleanser, moisturizer, serum, SPF, masks |
| **Tools** | Brushes, sponges, lash curlers |

---

## Features

### Core (MVP)
- Scan products via live video
- Build inventory with AI assistance
- Track open dates and expiration
- Dashboard view of collection

### Enhanced (V2)
- Duplicate detection ("You already have 3 nude lipsticks")
- Restock reminders
- "Shop my stash" suggestions (use what you have)
- Collection value tracking
- Product wishlist vs. what you own
- Share collection publicly (beauty influencer use case)

### Advanced (V3)
- Integrate with purchase history (email parsing?)
- Price tracking and deal alerts
- Routine builder from your inventory
- "Declutter guide" — what to toss

---

## Monetization Options

| Model | Price | What User Gets |
|-------|-------|----------------|
| **Freemium** | Free / $6.99 | 20 products free, unlimited paid |
| **One-time** | $9.99 | Lifetime access |
| **Subscription** | $2.99/mo | Cloud sync, reminders, advanced features |

Recommendation: **Freemium** with generous free tier (20-50 products), paid for power users with 100+ products.

---

## Distribution Channels

Same as Makeup Expiration Checker:

| Channel | Approach |
|---------|----------|
| r/MakeupAddiction | "I built this to organize my chaos" |
| r/SkincareAddiction | Skincare inventory angle |
| r/makeuporganization | Perfect fit |
| TikTok | "Scan your entire collection" demo |
| Beauty YouTubers | Review opportunity |
| Product Hunt | Launch |

---

## Competitive Landscape

| Competitor | What They Do | Gap |
|------------|--------------|-----|
| Sortly | General inventory app | Not beauty-specific |
| Beauty Keeper | Manual makeup tracking | No camera, no AI |
| Notion templates | Manual tracking | No intelligence |
| Spreadsheets | DIY tracking | Tedious |

**Your differentiation:** AI-powered scanning with conversational UX. Nobody else makes inventory management feel like chatting with a friend.

---

## Relationship to Makeup Expiration Checker

These two products share 80%+ of the codebase:

| Component | Expiration Checker | Inventory Tracker |
|-----------|-------------------|-------------------|
| Camera feed | ✓ | ✓ |
| Product recognition | ✓ | ✓ |
| Voice guidance | ✓ | ✓ |
| PAO logic | ✓ | ✓ |
| Inventory storage | Optional | Core feature |
| Dashboard | Simple | Detailed |
| Multi-product flow | No | Yes |

**Development strategy:** Build Expiration Checker first, then extend to Inventory Tracker with minimal additional effort.

---

## MVP Scope

**V0 (After Expiration Checker):**
- [ ] Multi-product scanning session
- [ ] Basic inventory list view
- [ ] LocalStorage persistence
- [ ] Simple dashboard

**V1:**
- [ ] Cloud sync (Supabase)
- [ ] User accounts
- [ ] Category organization
- [ ] Expiration alerts

**V2:**
- [ ] Duplicate detection
- [ ] Collection value
- [ ] Share publicly

---

## Open Questions

- [ ] How accurate can product recognition be? (Brand + shade from packaging)
- [ ] Privacy concerns with storing photos of products?
- [ ] Do users want to scan everything, or just problem products?
- [ ] Integration with purchase data (email receipts, Amazon)?

---

## Honest Assessment

This is essentially "Expiration Checker Plus" — same core tech, extended feature set. The question is whether the inventory management angle is compelling enough to be a separate product or just a feature.

**Recommendation:** Build as a feature upgrade path from Expiration Checker, not a separate app. One app that does:
1. Quick check (scan one product)
2. Full inventory (scan everything)

---

## Related Products (Shared Architecture)

This product shares the "AI FaceTime Companion" architecture with:
- Makeup Expiration Checker
- Vet Decision Tool

See: `architecture/ai-facetime-companion.md`

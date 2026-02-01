# AI Tool Finder (canai.dev)
## Discover the Right AI for Any Task

---

## The Problem

AI tools are exploding. There are thousands of options across every category. Finding the right one for a specific task is:
- Time-consuming (hours of research)
- Confusing (similar names, overlapping features)
- Risky (pick wrong tool, waste money/time)
- Fragmented (info scattered across blogs, Reddit, Twitter)

**The frustration:** "What AI should I use for [specific task]?"

---

## The Solution

A curated, searchable database of AI tools with:
- Problem-based search ("I want to...")
- User ratings and reviews
- Clear pricing info
- Filtering (free/paid, open source/closed, etc.)

**Domain:** canai.dev (available as of last check)

---

## Core UX Flow

```
1. LANDING PAGE
   Big search bar: "I want to..."
   Example queries shown below:
   - "generate images from text"
   - "transcribe audio files"
   - "write better emails"
   - "chat with my documents"

2. SEARCH RESULTS
   Cards showing:
   - Tool name + logo
   - One-line description
   - Rating (community)
   - Pricing tier (Free / Freemium / Paid)
   - Tags (image gen, writing, coding, etc.)

3. TOOL DETAIL PAGE
   - Full description
   - Features list
   - Pricing breakdown
   - Pros/cons (curated or community)
   - User reviews
   - Alternatives
   - Link to tool

4. COMPARISON (optional)
   Side-by-side comparison of 2-3 tools

5. SUBMIT TOOL
   Community can add tools you've missed
```

---

## Technical Architecture

```
┌─────────────────────────────────────────────┐
│            FRONTEND (React/Next.js)          │
├─────────────────────────────────────────────┤
│ • Search interface                           │
│ • Filter/facet UI                            │
│ • Tool cards and detail pages                │
│ • Review submission forms                    │
│ • Comparison view                            │
└─────────────────┬───────────────────────────┘
                  │
                  ▼
┌─────────────────────────────────────────────┐
│            BACKEND (Supabase)                │
├─────────────────────────────────────────────┤
│ • Tool database                              │
│ • Categories/tags                            │
│ • User reviews                               │
│ • Search (Supabase full-text or Algolia)     │
└─────────────────┬───────────────────────────┘
                  │
                  ▼
┌─────────────────────────────────────────────┐
│            DATA CURATION                     │
├─────────────────────────────────────────────┤
│ • Initial seed: 50-100 tools (manual)        │
│ • Ongoing: Community submissions             │
│ • Quality: Manual review before publish      │
└─────────────────────────────────────────────┘
```

---

## Category Taxonomy

### Primary Categories

| Category | Examples |
|----------|----------|
| **Image Generation** | Midjourney, DALL-E, Stable Diffusion, Leonardo |
| **Text/Writing** | ChatGPT, Claude, Jasper, Copy.ai |
| **Audio/Voice** | ElevenLabs, Whisper, Descript, Murf |
| **Video** | Runway, Pika, Synthesia, HeyGen |
| **Coding** | Cursor, GitHub Copilot, Codeium, Tabnine |
| **Data/Analysis** | Julius, Akkio, Obviously AI |
| **Productivity** | Notion AI, Mem, Otter.ai |
| **Research** | Perplexity, Elicit, Consensus |
| **Design** | Figma AI, Canva AI, Uizard |
| **Chat/Assistants** | ChatGPT, Claude, Gemini, Poe |

### Filter Attributes

| Filter | Options |
|--------|---------|
| **Price** | Free, Freemium, Paid, Enterprise |
| **Source** | Open Source, Closed Source |
| **Platform** | Web, Desktop, Mobile, API |
| **Use Case** | Personal, Professional, Developer |

---

## Data Model

```sql
-- Tools table
tools (
  id uuid primary key,
  name text,
  slug text unique,
  tagline text,
  description text,
  url text,
  logo_url text,
  pricing_model enum (free, freemium, paid, enterprise),
  pricing_details text,
  is_open_source boolean,
  platforms text[], -- web, desktop, mobile, api
  created_at timestamp,
  updated_at timestamp
)

-- Categories
categories (
  id uuid primary key,
  name text,
  slug text,
  description text
)

-- Tool-Category mapping
tool_categories (
  tool_id uuid references tools,
  category_id uuid references categories
)

-- Reviews
reviews (
  id uuid primary key,
  tool_id uuid references tools,
  user_id uuid, -- optional, can be anonymous
  rating int (1-5),
  title text,
  body text,
  pros text[],
  cons text[],
  created_at timestamp
)
```

---

## Monetization Options

| Model | Revenue Source |
|-------|----------------|
| **Affiliate links** | Earn commission on signups |
| **Sponsored listings** | Tools pay for featured placement ($50-200/mo) |
| **Premium database export** | Pay $9.99 to download full list |
| **API access** | Developers pay for programmatic access |
| **Job board** | AI companies post jobs |

Recommendation: Start with **affiliate + sponsored listings**. This is the directory site playbook.

---

## Distribution Channels

| Channel | Approach |
|---------|----------|
| r/artificial | Share as resource |
| r/ChatGPT | Answer "what tool for X" questions with link |
| r/LocalLLaMA | Open source focus |
| Twitter/X AI community | Share comparisons |
| Indie Hackers | Launch |
| Hacker News | Show HN post |
| SEO | Long-tail "best AI for [X]" keywords |

---

## Competitive Landscape

| Competitor | What They Do | Gap |
|------------|--------------|-----|
| There's an AI | Directory | UX is meh, no deep reviews |
| Futurepedia | Directory | Overwhelming, no curation |
| Product Hunt | General products | Not AI-focused |
| AlternativeTo | Alternatives finder | Not AI-focused |

**Your differentiation:**
- Curated quality over quantity
- Problem-based search ("I want to...")
- Real reviews, not just descriptions
- Beautiful UX (your creative direction skills)

---

## MVP Scope

**V0 (Day 1, 6-8 hours):**
- [ ] Curate 50 tools manually (spreadsheet first)
- [ ] Basic search UI
- [ ] Category filtering
- [ ] Tool cards with basic info
- [ ] Deploy to Vercel

**V1 (Week 1):**
- [ ] Tool detail pages
- [ ] User reviews
- [ ] Better search (fuzzy matching)
- [ ] Submit tool form

**V2 (Month 1):**
- [ ] Comparison feature
- [ ] Affiliate link integration
- [ ] Sponsored listings
- [ ] SEO optimization

---

## Content Strategy

To drive SEO traffic, create:
- "Best AI tools for [X]" landing pages
- "X vs Y" comparison pages
- "Free alternatives to [expensive tool]" pages

These rank well and funnel traffic to the main directory.

---

## Open Questions

- [ ] How to keep data fresh? (Tools change pricing, features constantly)
- [ ] Review authenticity? (Fake reviews are a problem)
- [ ] How to differentiate from existing directories?
- [ ] Is this too crowded a space?

---

## Honest Assessment

**Pros:**
- Real problem, I experience it myself
- Straightforward to build
- Multiple monetization paths
- Your creative direction could make it stand out

**Cons:**
- Crowded space (lots of AI directories)
- Slow monetization (need traffic first)
- Ongoing maintenance burden (keeping data fresh)
- Not as unique as your other ideas

**Verdict:** Good idea, but lower priority than your beauty/pet products where you have more differentiation.

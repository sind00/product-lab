# Vet Decision Tool
## AI FaceTime Companion for Pet Health Triage

---

## The Problem

Pet owners face a constant dilemma: "Is this an emergency or am I overreacting?"

- Vet visits are expensive ($200+ for basic exam)
- Googling symptoms leads to panic ("my dog sneezed, WebMD says cancer")
- Waiting too long can be dangerous
- Going too early feels wasteful

**The anxiety:** "Is my pet okay? Should I go NOW?"

---

## The Solution

A live video AI companion that helps you assess your pet's symptoms in real-time. Like FaceTiming a vet tech friend who can guide you through what to look for.

---

## Core UX Flow

```
1. USER opens app, grants camera permission
2. ONBOARDING:
   - "What kind of pet do you have?" (dog/cat/other)
   - "What's their name?"
   - "What's concerning you today?" (symptoms checklist or free text)

3. LIVE VIDEO MODE activates
   - AI voice: "Show me [Pet name]. Let's take a look together."
   - User points camera at pet

4. GUIDED EXAMINATION
   - AI: "Can you show me their eyes? I want to check for discharge."
   - AI: "Now their gums — gently lift the lip so I can see the color"
   - AI: "Is [Pet name] standing? Can you show me how they're walking?"

5. CONTEXTUAL QUESTIONS
   - "When did you first notice this?"
   - "When did they last eat/drink/poop?"
   - "Have they been acting differently?"
   - "Any changes to their environment?"

6. ASSESSMENT
   Based on visual + answers:
   - 🚨 EMERGENCY: "This looks serious. I'd go to the vet now."
   - ⚠️ SOON: "Schedule a visit in the next 24-48 hours."
   - ✅ MONITOR: "This seems okay to watch at home. Here's what to look for..."

7. FOLLOW-UP
   - Save the session for vet reference
   - Set reminder to check again in X hours
   - Links to pet telehealth if they want a real vet
```

---

## Technical Architecture

Same shared architecture as Makeup Checker:

```
┌─────────────────────────────────────────────┐
│            FRONTEND (React/Next.js)          │
├─────────────────────────────────────────────┤
│ • Camera access (getUserMedia API)           │
│ • Real-time video display                    │
│ • Shake detection (DeviceMotion API)         │
│ • Voice synthesis (ElevenLabs or Web Speech) │
│ • Voice input (Whisper API or Web Speech)    │
│ • UI overlays (guidance prompts)             │
└─────────────────┬───────────────────────────┘
                  │
                  ▼
┌─────────────────────────────────────────────┐
│            AI LAYER (Multimodal)             │
├─────────────────────────────────────────────┤
│ • Gemini 2.0 Flash OR GPT-4o                 │
│ • Video stream analysis                      │
│ • Symptom pattern matching                   │
│ • Urgency scoring                            │
└─────────────────┬───────────────────────────┘
                  │
                  ▼
┌─────────────────────────────────────────────┐
│            DOMAIN KNOWLEDGE                  │
├─────────────────────────────────────────────┤
│ • Symptom urgency database                   │
│ • Species-specific examination flows         │
│ • Red flag indicators                        │
│ • Normal vs abnormal reference images        │
└─────────────────────────────────────────────┘
```

---

## Symptom Urgency Framework

### Immediate Emergency (Go NOW)

| Symptom | Visual Indicator |
|---------|------------------|
| Difficulty breathing | Open-mouth breathing, extended neck |
| Pale/white/blue gums | Gum color check |
| Bloated abdomen (dogs) | Visible distension, trying to vomit |
| Collapse/unconscious | Unresponsive |
| Seizure | Convulsions |
| Severe bleeding | Visible blood |
| Toxin ingestion | Known or suspected |
| Unable to urinate (cats esp.) | Straining, crying |
| Eye injury | Visible damage, closed eye |

### Urgent (Within 24 hours)

| Symptom | Visual Indicator |
|---------|------------------|
| Not eating >24 hours | — |
| Vomiting repeatedly | — |
| Diarrhea with blood | — |
| Limping severely | Gait check |
| Eye discharge | Visible |
| Ear infection signs | Shaking head, odor |
| Difficulty defecating | Straining |

### Monitor at Home

| Symptom | Guidance |
|---------|----------|
| Single vomit episode | Watch for recurrence |
| Mild limping | Rest, observe 24-48h |
| Decreased appetite | Offer bland food |
| Sneezing | Watch for discharge |

---

## Examination Guidance Scripts

### Eyes Check
```
AI: "Let's look at [Pet name]'s eyes. Hold the camera about a foot away from their face."
AI: "Good. Are both eyes the same size? Any discharge or redness?"
AI: "Can you gently pull down the lower eyelid? I want to see if it's pink or pale."
```

### Gums Check
```
AI: "Now I need to see their gums. Gently lift their lip."
AI: "The gums should be pink, like bubblegum. Press gently with your finger and let go."
AI: "The color should return within 2 seconds. How quickly did it come back?"
```

### Mobility Check
```
AI: "Can you have [Pet name] walk across the room?"
AI: "Watch their gait. Are they favoring any leg?"
AI: "Is their head tilted at all?"
```

### Abdomen Check
```
AI: "Gently feel their belly. Does [Pet name] tense up or cry?"
AI: "Does the belly feel hard or bloated?"
```

---

## Disclaimer & Liability

**Critical:** This tool is NOT a substitute for veterinary care.

Required disclaimers:
- "This is an educational tool, not medical advice"
- "When in doubt, always consult a veterinarian"
- "In emergencies, go to the nearest emergency vet immediately"

Consider: Terms of service, liability waiver at signup

---

## Monetization Options

| Model | Price | What User Gets |
|-------|-------|----------------|
| **Free + Affiliate** | Free | Affiliate links to Pawp, Vetster |
| **Freemium** | Free / $4.99 | 3 free sessions, then pay |
| **Subscription** | $2.99/mo | Unlimited, pet profiles, history |

Recommendation: **Free with affiliate** to start. Pet parents are anxious and price-sensitive in the moment.

---

## Distribution Channels

| Channel | Approach | Size |
|---------|----------|------|
| r/dogs | "I built this because vet visits are $$$" | 4M+ |
| r/cats | Same | 4M+ |
| r/AskVet | Careful — vets may push back | 200k |
| r/Pets | General | 500k |
| Pet parent Facebook groups | Many, large | Varies |
| TikTok | Demo with cute pet | Viral potential |
| Product Hunt | Launch | Tech audience |

---

## Competitive Landscape

| Competitor | What They Do | Gap |
|------------|--------------|-----|
| Pawp | Telehealth subscription, $24/mo | Expensive, requires human wait |
| Vetster | On-demand vet video calls | $50-100 per call |
| PetMD symptom checker | Text-based questionnaire | No visual, no guidance |
| Various apps | Manual symptom input | No camera integration |

**Your differentiation:** Real-time visual guidance, conversational UX, free/cheap triage before you spend $$ on telehealth.

---

## Research Questions (For Roommate with 7 Pets)

### Understanding the Problem
1. When was the last time you weren't sure if you should take a pet to the vet? What happened?
2. How do you currently decide "vet now" vs "wait and see"?
3. What symptoms freak you out the most?
4. How often do you go to the vet and it turns out to be nothing? Cost?
5. Would you pay $5-10 for an app that gave you an urgency assessment?
6. If the app used your camera to look at your pet while asking questions, helpful or creepy?
7. What species do you have? Different needs per species?

### Competitive Research
8. Have you tried any pet health apps? Which ones? Like/hate?
9. Have you used pet telehealth (Pawp, Vetster)? Experience? Cost?

---

## MVP Scope

**V0 (Day 1):**
- [ ] Symptom checklist input (no camera)
- [ ] Decision tree logic
- [ ] Urgency verdict output
- [ ] Deploy to Vercel

**V1 (Day 2-3):**
- [ ] Camera feed integration
- [ ] Voice guidance (AI speaks)
- [ ] Basic examination flow (eyes, gums, mobility)

**V2 (Week 2):**
- [ ] Pet profiles (save pet info)
- [ ] Session history
- [ ] Affiliate integration (Pawp, Vetster)

---

## Open Questions

- [ ] Liability: Do we need a lawyer to review disclaimers?
- [ ] Veterinary pushback: Will vets hate this or embrace it?
- [ ] Scope: Start with dogs only, or dogs + cats?
- [ ] AI accuracy: How good is multimodal AI at pet health assessment?

---

## Related Products (Shared Architecture)

This product shares the "AI FaceTime Companion" architecture with:
- Makeup Expiration Checker
- Makeup Inventory Tracker

See: `architecture/ai-facetime-companion.md`

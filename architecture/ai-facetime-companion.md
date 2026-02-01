# AI FaceTime Companion Architecture
## Shared Foundation for Real-Time Video AI Products

---

## Overview

This document describes the shared technical architecture for products that use a "FaceTime with an AI friend" UX pattern. The user points their phone camera at something, and an AI companion guides them conversationally through an inspection or task.

### Products Using This Architecture

1. **Makeup Expiration Checker** — "Is this safe to use?"
2. **Vet Decision Tool** — "Should I take my pet to the vet?"
3. **Makeup Inventory Tracker** — "Help me catalog my collection"

---

## Core UX Pattern

```
┌─────────────────────────────────────────────────────────────────┐
│                                                                  │
│    ┌─────────────────────────────────────────────────────┐      │
│    │                                                     │      │
│    │              LIVE VIDEO FEED                        │      │
│    │                                                     │      │
│    │    ┌───────────────────┐                           │      │
│    │    │ [Detected Object] │ ← Highlight overlay       │      │
│    │    └───────────────────┘                           │      │
│    │                                                     │      │
│    └─────────────────────────────────────────────────────┘      │
│                                                                  │
│    ┌─────────────────────────────────────────────────────┐      │
│    │  "Show me the bottom of that product"               │      │
│    │                              — AI Voice Guidance    │      │
│    └─────────────────────────────────────────────────────┘      │
│                                                                  │
│    ┌─────────────────────────────────────────────────────┐      │
│    │  CONTEXT PANEL                                      │      │
│    │  • Detected: [Item]                                 │      │
│    │  • Status: [Assessment]                             │      │
│    │  • Action: [Recommendation]                         │      │
│    └─────────────────────────────────────────────────────┘      │
│                                                                  │
│    [🎤 Tap to speak]              [📸 Capture snapshot]         │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

---

## Technical Stack

### Frontend

| Component | Technology | Purpose |
|-----------|------------|---------|
| Framework | Next.js 14+ (App Router) | React with SSR, easy deployment |
| Styling | Tailwind CSS | Rapid UI development |
| Camera | `getUserMedia` API | Access device camera |
| Motion | `DeviceMotion` API | Shake detection for auto-capture |
| Voice Out | Web Speech API or ElevenLabs | AI speaks to user |
| Voice In | Web Speech API or Whisper | User speaks to AI |
| State | Zustand or React Context | Local state management |

### AI Layer

| Component | Technology | Purpose |
|-----------|------------|---------|
| Multimodal AI | Gemini 2.0 Flash or GPT-4o | Process video/images + generate responses |
| Streaming | Server-Sent Events | Real-time response streaming |
| Function Calling | Native to model | Structured outputs (verdicts, data extraction) |

### Backend (Minimal)

| Component | Technology | Purpose |
|-----------|------------|---------|
| API Routes | Next.js API routes | Proxy to AI APIs |
| Database | Supabase (optional) | User data, inventory |
| Auth | Supabase Auth (optional) | User accounts |
| Storage | Supabase Storage (optional) | Product photos |

### Deployment

| Component | Technology | Purpose |
|-----------|------------|---------|
| Hosting | Vercel | Free tier, easy deploys |
| Domain | Namecheap/Cloudflare | Custom domain |
| Analytics | Plausible or Vercel Analytics | Usage tracking |

---

## System Architecture

```
┌──────────────────────────────────────────────────────────────────┐
│                         CLIENT (Browser/PWA)                      │
├──────────────────────────────────────────────────────────────────┤
│                                                                   │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐              │
│  │   Camera    │  │    Voice    │  │    State    │              │
│  │   Module    │  │   Module    │  │   Manager   │              │
│  └──────┬──────┘  └──────┬──────┘  └──────┬──────┘              │
│         │                │                │                      │
│         └────────────────┼────────────────┘                      │
│                          │                                       │
│                          ▼                                       │
│                 ┌─────────────────┐                              │
│                 │  AI Orchestrator │                             │
│                 │  (manages flow)  │                             │
│                 └────────┬────────┘                              │
│                          │                                       │
└──────────────────────────┼───────────────────────────────────────┘
                           │
                           ▼
┌──────────────────────────────────────────────────────────────────┐
│                      API LAYER (Next.js)                          │
├──────────────────────────────────────────────────────────────────┤
│  POST /api/analyze                                                │
│  - Receives: video frame(s) or image + conversation history       │
│  - Returns: AI response (text + structured data)                  │
│                                                                   │
│  POST /api/voice (optional)                                       │
│  - Receives: audio blob                                           │
│  - Returns: transcription                                         │
└──────────────────────────┬───────────────────────────────────────┘
                           │
                           ▼
┌──────────────────────────────────────────────────────────────────┐
│                      EXTERNAL SERVICES                            │
├──────────────────────────────────────────────────────────────────┤
│                                                                   │
│  ┌─────────────────┐    ┌─────────────────┐                      │
│  │  Gemini / GPT   │    │   ElevenLabs    │                      │
│  │  (Multimodal)   │    │   (Voice TTS)   │                      │
│  └─────────────────┘    └─────────────────┘                      │
│                                                                   │
│  ┌─────────────────┐    ┌─────────────────┐                      │
│  │    Supabase     │    │     Whisper     │                      │
│  │  (Data + Auth)  │    │   (Voice STT)   │                      │
│  └─────────────────┘    └─────────────────┘                      │
│                                                                   │
└──────────────────────────────────────────────────────────────────┘
```

---

## Core Modules

### 1. Camera Module

```typescript
// Responsibilities:
// - Access device camera
// - Display live video feed
// - Capture frames for AI analysis
// - Detect shake and auto-capture
// - Handle permissions

interface CameraModule {
  // Initialize camera access
  init(): Promise<void>;

  // Get current video frame as base64
  captureFrame(): string;

  // Start shake detection
  enableShakeCapture(onShake: () => void): void;

  // Overlay bounding box on detected object
  drawHighlight(box: BoundingBox): void;

  // Cleanup
  destroy(): void;
}
```

**Key Implementation Notes:**
- Use `navigator.mediaDevices.getUserMedia({ video: { facingMode: 'environment' } })` for rear camera
- Capture frames at 1-2 fps for AI analysis (not every frame)
- Shake detection via `DeviceMotionEvent` — threshold ~15-20 m/s²

### 2. Voice Module

```typescript
// Responsibilities:
// - Text-to-speech (AI speaking)
// - Speech-to-text (user speaking)
// - Handle audio permissions
// - Manage speaking state (don't interrupt)

interface VoiceModule {
  // Speak text using TTS
  speak(text: string): Promise<void>;

  // Start listening for user speech
  startListening(): void;

  // Stop listening
  stopListening(): void;

  // Callback when user speech recognized
  onTranscript: (text: string) => void;

  // Is AI currently speaking?
  isSpeaking: boolean;
}
```

**Key Implementation Notes:**
- Web Speech API is free but robotic
- ElevenLabs sounds natural but costs ~$5/mo for hobby tier
- Consider: AI speaks important guidance, text for details
- Don't overlap AI speaking with user listening

### 3. AI Orchestrator

```typescript
// Responsibilities:
// - Manage conversation state
// - Send frames + context to AI
// - Parse AI responses
// - Trigger voice output
// - Handle domain-specific logic

interface AIOrchestrator {
  // Send frame for analysis
  analyzeFrame(frame: string, context: ConversationContext): Promise<AIResponse>;

  // Handle user voice input
  handleUserInput(text: string): Promise<AIResponse>;

  // Get current conversation history
  getHistory(): Message[];

  // Reset conversation
  reset(): void;
}

interface AIResponse {
  text: string;           // What AI says
  guidance?: string;      // What to show user should do
  detection?: Detection;  // What was detected in frame
  verdict?: Verdict;      // Final assessment (if ready)
  nextAction?: string;    // What AI wants user to do next
}
```

---

## AI Prompt Architecture

Each product uses the same base system prompt with domain-specific customization:

### Base System Prompt

```
You are a friendly AI companion helping the user via their phone camera.
You communicate through voice, so keep responses short and conversational.

BEHAVIOR:
- Be warm and supportive, like a knowledgeable friend
- Give clear, specific guidance on what to show the camera
- Ask one question at a time
- If the image is unclear, politely ask them to adjust
- If you detect something, confirm what you see before proceeding

CONSTRAINTS:
- Keep spoken responses under 20 words when possible
- Always explain your reasoning briefly
- If uncertain, say so — don't guess

OUTPUT FORMAT:
Respond with JSON:
{
  "speak": "What you say to the user (keep short)",
  "guidance": "On-screen instruction (optional)",
  "detection": { "type": "...", "confidence": 0.0-1.0, "details": {} },
  "verdict": null | { "status": "safe|warning|danger", "reason": "..." },
  "nextAction": "What you want user to do next"
}
```

### Domain-Specific Additions

**Makeup Checker:**
```
DOMAIN CONTEXT:
You are helping check if makeup products are safe to use.
Key things to look for:
- PAO symbol (jar icon with "12M", "6M", etc.)
- Batch code (alphanumeric on bottom/back)
- Product type (mascara, foundation, etc.)
- Signs of degradation (smell, texture, separation)

PAO REFERENCE:
- Mascara: 3-6 months
- Foundation: 12 months
- Lipstick: 18-24 months
[etc.]
```

**Vet Tool:**
```
DOMAIN CONTEXT:
You are helping assess if a pet needs veterinary care.
Guide the user through a basic examination:
1. Overall behavior and energy
2. Eyes (discharge, redness, cloudiness)
3. Gums (color, capillary refill)
4. Mobility (limping, reluctance to move)
5. Specific symptom area

URGENCY LEVELS:
- EMERGENCY: [list symptoms]
- URGENT (24h): [list symptoms]
- MONITOR: [list symptoms]

CRITICAL: Always recommend vet for any serious doubt.
This is triage, not diagnosis.
```

---

## Data Flow Example

### User checks if mascara is expired:

```
1. User opens app, grants camera permission
2. [CameraModule] initializes, shows live feed
3. [VoiceModule] AI speaks: "Hi! Show me what you're curious about."

4. User points at mascara
5. [CameraModule] captures frame
6. [AIOrchestrator] sends frame to Gemini:
   - Image: [base64 frame]
   - Context: "User just opened app, checking product"

7. Gemini responds:
   {
     "speak": "I see that's a mascara. Can you show me the bottom?",
     "guidance": "Flip product to show bottom",
     "detection": { "type": "mascara", "confidence": 0.92 },
     "verdict": null,
     "nextAction": "show_batch_code"
   }

8. [VoiceModule] speaks response
9. UI shows guidance text

10. User flips mascara, shows bottom
11. [CameraModule] captures frame
12. [AIOrchestrator] sends frame + history

13. Gemini responds:
    {
      "speak": "I can see the batch code. When did you open this?",
      "detection": { "type": "batch_code", "value": "0F23", "brand": "Maybelline" },
      "nextAction": "ask_open_date"
    }

14. User says: "About 4 months ago"
15. [VoiceModule] transcribes
16. [AIOrchestrator] sends text + context

17. Gemini responds:
    {
      "speak": "Since mascaras should be replaced every 3 months, I'd recommend getting a new one.",
      "verdict": { "status": "warning", "reason": "Mascara opened 4 months ago, PAO is 3 months" }
    }

18. UI shows verdict card with recommendation
```

---

## File Structure

```
/app
  /page.tsx                 # Landing/home
  /scan/page.tsx            # Main camera interface
  /results/page.tsx         # Verdict display
  /inventory/page.tsx       # (Inventory Tracker only)
  /api
    /analyze/route.ts       # AI analysis endpoint
    /transcribe/route.ts    # Voice transcription endpoint

/components
  /camera
    CameraFeed.tsx          # Video display
    ShakeDetector.tsx       # Motion detection
    HighlightOverlay.tsx    # Bounding box overlay
  /voice
    VoiceOutput.tsx         # TTS component
    VoiceInput.tsx          # STT component
  /ui
    GuidancePanel.tsx       # "What to do" display
    VerdictCard.tsx         # Final result
    ContextPanel.tsx        # Detection info

/lib
  /ai
    orchestrator.ts         # Main AI flow logic
    prompts.ts              # System prompts by domain
    parseResponse.ts        # Response parsing
  /camera
    capture.ts              # Frame capture utilities
    shake.ts                # Shake detection
  /voice
    tts.ts                  # Text-to-speech wrapper
    stt.ts                  # Speech-to-text wrapper
  /domain
    makeup.ts               # Makeup-specific logic (PAO, batch codes)
    vet.ts                  # Vet-specific logic (symptoms, urgency)

/data
  pao-database.json         # Product expiration data
  symptom-urgency.json      # Pet symptom data
```

---

## API Costs Estimate

| Service | Usage | Cost |
|---------|-------|------|
| Gemini 2.0 Flash | ~20 frames/session, 5 sessions/day | ~$1-5/month |
| ElevenLabs (optional) | ~500 chars/session | ~$5/month |
| Supabase | Free tier | $0 |
| Vercel | Free tier | $0 |
| **Total** | | **$5-10/month** |

---

## MVP Build Sequence

### Week 1: Foundation
- Day 1-2: Camera module (feed + capture + shake)
- Day 3: AI integration (Gemini, basic prompt)
- Day 4: Voice output (Web Speech API first)
- Day 5: Basic UI (guidance panel, verdict card)

### Week 2: Domain Products
- Day 6: Makeup Checker domain logic + prompts
- Day 7: Makeup Checker polish + deploy
- Day 8: Vet Tool domain logic + prompts
- Day 9: Vet Tool polish + deploy
- Day 10: Inventory Tracker extension

---

## Open Technical Questions

1. **Gemini vs GPT-4o?**
   - Gemini 2.0 Flash: Faster, cheaper, native video understanding
   - GPT-4o: More reliable, better function calling
   - Recommendation: Start with Gemini for cost

2. **Real-time video vs frame capture?**
   - True real-time: More complex, higher costs
   - Frame capture (1-2 fps): Simpler, sufficient for this UX
   - Recommendation: Frame capture

3. **Web app vs native app?**
   - Web (PWA): Faster to ship, cross-platform
   - Native: Better camera/voice APIs, app store presence
   - Recommendation: Web/PWA first, native later if traction

4. **Voice: Web Speech API vs ElevenLabs?**
   - Web Speech: Free, robotic
   - ElevenLabs: Natural, ~$5/mo
   - Recommendation: Start with Web Speech, upgrade if users complain

---

## Security Considerations

- Camera/mic permissions: Only request when needed
- Frame data: Don't persist unless user opts in (inventory)
- API keys: Server-side only, never expose to client
- User data: Minimize collection, clear privacy policy

---

## Performance Targets

| Metric | Target |
|--------|--------|
| Time to first guidance | <3 seconds |
| Frame analysis latency | <2 seconds |
| Voice response latency | <1 second |
| App load time | <2 seconds |

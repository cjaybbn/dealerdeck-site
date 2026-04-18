# DealerDeck — Website Content Brief for Cursor AI

**Purpose of this document:** This is the single source of truth for all claims, copy, features, and positioning on the DealerDeck marketing website. When updating the site, validate every factual claim against this document. If a claim is not supported here, do not put it on the site.

**Company:** DealerDeck LLC
**Product:** DealerDeck (iOS app, TestFlight pilot)
**Founder:** Camden Blackburn
**Location:** Scottsdale, Arizona
**Pilot dealership:** BMW North Scottsdale (Penske Automotive Group)
**Target CRM integration:** DriveCentric
**Primary goal of the website right now:** Legitimize DealerDeck LLC for the DriveCentric Partner Program application and serve as a professional reference for dealership stakeholders.

---

## 1. ONE-LINER AND POSITIONING

**Primary tagline:**
> Intelligence for the sales floor.

**One-sentence description:**
> DealerDeck is real-time operations software for dealership sales reps — inventory intelligence, customer logging, and deal tracking that moves at the speed of the floor, without replacing the rep-customer relationship.

**Product principle (the positioning quote):**
> Other platforms use AI to talk *to* the customer. DealerDeck uses AI to help the rep talk to the customer *better*. One replaces the relationship. The other strengthens it.

**What DealerDeck is NOT:**
- Not a CRM replacement
- Not an AI chatbot that talks to customers
- Not a lead-generation tool
- Not a BDC/marketing tool
- Not a finance/F&I system
- Not a DMS replacement

**What DealerDeck IS:**
- A rep-facing tool used *during* and *around* customer interactions
- An AI-powered inventory and customer intelligence layer that sits on top of existing dealership systems
- A voice-first interface so reps don't have to type on their phones while working
- A "customer-safe by default" app — anything on screen is safe to turn around and show a customer

---

## 2. CURRENT PRODUCT STATUS (as of April 2026)

**Deployment stage:** Active private pilot via Apple TestFlight
**Active pilot users:** 5 sales reps at BMW North Scottsdale
- Ed (primary pilot user, most engaged feedback)
- Andre
- Bilgo
- Tyler
- Cam (founder, also rep/valet)

**Stakeholder validation:**
- Steve Khouri (General Manager, BMW North Scottsdale) — saw demo at April 7, 2026 meeting, positive reception, committed to partnership
- Kurt Fowler (Sales Manager, BMW North Scottsdale) — same meeting, positive reception
- Peter Garcia (Inventory Manager, Cam's direct boss) — ongoing adoption advisor, gave the key requirements: must be free initially, zero friction, zero manual steps

**Platform:** iOS only (React Native via Expo). No Android yet. No web app.

**Distribution:** Apple TestFlight (private beta). Not on public App Store yet.

**Inventory data source:** Algolia index (public BMW North Scottsdale inventory). 100% coverage of the pilot dealership's inventory.

**What currently works in production:**
- Voice-to-text inventory queries
- Gemini-powered query normalization (handles mispronunciations, e.g. "eggs 5 50 ease" → "X5 xDrive50e")
- BMW model normalization (strips xDrive/sDrive prefixes for matching)
- Unified scoring system for inventory relevance
- Real-time inventory search via Algolia
- In-transit vs. on-lot availability indicators
- Status tracking (status = buying stage; location = physical position, tracked separately)
- Staff identity system with nickname matching (Dave ↔ David, Ed ↔ Edward)
- Auto-linking of staff on signup
- Customer logging and profile creation
- AI-generated customer summaries and next-step suggestions
- Vehicle interest tracking linked to customer profiles
- Trade-in vehicle noting (display only — no trade-in valuation)
- Payment estimate display (72-month, MSRP-based, with clear disclaimers — not authoritative)
- Targeted notifications (only to deal-linked users, last updaters, or mentioned staff)
- Stale vehicle reminders, user-specific and location-based
- "Copy to CRM" button on AI summaries

**Known active bugs (do not reference on the site):**
- Black screen on TestFlight for valet role (auto-redirect crashes Hermes in production)
- Audio transcription failing in production (works in dev) — likely mime type issue
- Debug labels left in some production builds

**Recently completed engineering work:**
- Unified scoring system in `lib/scoring.ts` (replaced two inconsistent algorithms, eliminated a second Gemini call per interaction, saving 1-2 seconds per query)
- Status/location separation
- In-transit vs. on-lot UI distinction with airplane icon
- Notification targeting rewrite
- Stale reminder personalization

---

## 3. CORE FEATURES (use these as canonical feature descriptions)

Each feature below includes: the name, a one-sentence description, a longer description for feature cards, and status (live / in progress / planned).

### 3.1 Voice Search
**Short:** Voice search that understands you.
**Long:** Say "eggs 5 50 ease" and get every X5 xDrive50e on the lot. Gemini-powered query normalization handles accents, shorthand, and background noise.
**Status:** Live

### 3.2 Live Vehicle Location
**Short:** Know where every vehicle is.
**Long:** On lot, in transit, in service, sold pending. Status and physical location are tracked separately — the way actual dealerships operate, not the way legacy software assumes.
**Status:** Live

### 3.3 Customer Logging and AI Summaries
**Short:** Deals that log themselves.
**Long:** Log customers and progress with your voice. The app threads interactions, generates plain-English summaries, flags stakeholders, and surfaces next steps — so reps always know what to move on next.
**Status:** Live

### 3.4 Smart Name Resolution
**Short:** Name resolution that just works.
**Long:** "Dave" resolves to David. "Ed" to Edward. Disambiguation is built in, so mentions of teammates always land on the right person instantly.
**Status:** Live

### 3.5 Targeted Notifications
**Short:** Notifications only when relevant.
**Long:** Alerts route only to deal-linked users, last updaters, and mentioned staff. Reps see what affects them — never everything.
**Status:** Live

### 3.6 Customer-Safe by Default
**Short:** Safe to turn the phone around.
**Long:** Built with dealer etiquette in mind. Every screen is safe to show a customer — no internal pricing games, no F&I spoilers, no private notes exposed. Financial scope is deliberately constrained: basic estimates with disclaimers only.
**Status:** Live

### 3.7 AI-Powered Customer Profiles
**Short:** Context at a glance.
**Long:** Every customer profile shows vehicle interest, trade-in details, finance/cash preference, credit notes, and an AI-generated summary threaded from every touchpoint. "Copy to CRM" sends the summary to your CRM in one tap.
**Status:** Live

### 3.8 Payment Estimate
**Short:** Quick MSRP-based payment estimates.
**Long:** 72-month MSRP-based payment estimates with clear disclaimers. Excludes tax and fees. Auto-captures credit score and down payment percentage from AI-logged customer notes when present. Not a substitute for F&I.
**Status:** Live

### 3.9 Google Sheets Keylog Sync (Read-only)
**Short:** Live mirror of the dealership's keylog.
**Long:** Read-only integration with the dealership's Google Sheets keylog. Polls every 2 minutes, detects color and cell changes, reflects them live in the app. No changes to existing workflow required.
**Status:** In progress (Stage 1.5 on the roadmap)

### 3.10 Google Sheets Keylog Write-back
**Short:** Update the keylog from the app.
**Long:** Once read-only trust is established, reps can update keylog state directly from DealerDeck — write-back to the source spreadsheet.
**Status:** Planned (Stage 2)

### 3.11 DriveCentric CRM Integration
**Short:** Two-way sync with DriveCentric.
**Long:** Customer data, deal status, and AI-generated summaries sync between DealerDeck and DriveCentric. Eliminates double-entry. Roadmap is aligned with BMW North Scottsdale's 30-day transition window to DriveCentric.
**Status:** Planned (Stage 3, pending DriveCentric Partner Program approval)

---

## 4. ROADMAP — FOUR-STAGE ROLLOUT

This staged approach is central to DealerDeck's positioning. The principle: **earn trust at each stage before asking for more access.** Every stage must deliver standalone value.

### Stage 1 — Inventory Intelligence (CURRENT)
The app runs on public Algolia inventory data. Zero integration required. Reps install from TestFlight, sign in, and have full inventory search, vehicle tracking, and customer logging in under a minute. This stage proves the product is useful without any dealership buy-in beyond letting reps download it.

**Status:** Active

### Stage 1.5 — Read-only Keylog Sync
DealerDeck reads the dealership's existing Google Sheets keylog every 2 minutes. No changes to the sheet are made. Reps see a live mirror of keylog state without the dealership changing any internal workflow.

**Status:** In progress

### Stage 2 — Write-capable Keylog
Once the read-only mirror has proven accurate and reliable, DealerDeck can update the keylog from the app. This eliminates the back-and-forth between phone and computer for reps moving cars.

**Status:** Planned

### Stage 3 — DriveCentric CRM Integration
Full two-way sync with DriveCentric. Customer data, deal notes, status changes, and AI summaries flow between systems. This is the stage that requires DriveCentric Partner Program approval and happens after pilot adoption is proven.

**Status:** Planned, pending DriveCentric partnership

### Stage 4 — Source of Truth
Location and inventory systems migrate to DealerDeck as the primary source of truth. Expansion to additional Penske rooftops and other dealership groups.

**Status:** Planned

---

## 5. KEY METRICS AND STATS (verified — safe to use on the site)

| Metric | Value | Context |
|---|---|---|
| Active pilot users | 5 | All at BMW North Scottsdale |
| Pilot dealership | 1 | BMW North Scottsdale (Penske) |
| Inventory coverage at pilot dealership | 100% | Via Algolia public inventory feed |
| Voice-to-inventory response time | <2 seconds | After recent optimization (unified scoring, single Gemini call) |
| Setup steps required for reps | 0 | Download TestFlight, sign in, done |
| CRM integration window | ~30 days | BMW North Scottsdale's DriveCentric transition timeline, starting April 7, 2026 |

**Do NOT use metrics not on this list.** No ROI figures, no sales lift claims, no time-saved claims beyond "voice-to-inventory under 2 seconds" — we don't have data to support those.

---

## 6. COMPETITIVE POSITIONING

The website's comparison section should present DealerDeck against a generic "them" (AI tools that replace the rep), not against any named competitor.

**Them vs. DealerDeck:**

| Them | DealerDeck |
|---|---|
| AI chatbots that message leads on the rep's behalf, inserting a layer between rep and customer | AI that answers the rep's questions instantly — so the rep is sharper on the floor, in front of the customer |
| Heavy onboarding, IT involvement, training sessions, workflow changes | Reps install from TestFlight, sign in, and have full inventory intelligence in under a minute |
| Dashboards that require data entry reps don't benefit from | Every action is self-serving — log a customer, get instant summaries and next steps back |
| Pricing that assumes dealership-wide buy-in before any value is proven | Free during pilot. Value proven before any monetization conversation |

**Do NOT name-drop DriveCentric as a competitor.** DriveCentric is a target integration partner. The comparison is against the broader category of "AI tools that replace the rep."

---

## 7. TECHNICAL STACK (canonical list for the "Built With" section)

| Tool | Role |
|---|---|
| React Native | Mobile framework |
| Expo | Build and deploy (EAS) |
| Supabase | Backend, database, auth |
| Gemini API | Voice transcription, query normalization, AI summaries |
| Algolia | Inventory search |
| DriveCentric | CRM (integration planned — label as "integrating" or "planned") |

Secondary tools used but not necessary to list publicly: Google Sheets (keylog), Apple TestFlight (distribution), Claude Code (dev environment).

---

## 8. CONTACT INFO (use these exact values — placeholder until Camden confirms)

Placeholders currently on the site — Camden must swap these before the DriveCentric submission:

| Field | Current Placeholder | Action |
|---|---|---|
| Company | DealerDeck LLC | ✅ Correct — keep |
| Email | hello@dealerdeck.app | ⚠️ Replace with real email |
| Phone | +1 (480) 555-0100 | ⚠️ Replace with real phone |
| Location | Scottsdale, Arizona | ✅ Correct — keep |
| Founder | Camden Blackburn | ✅ Correct — keep |
| Domain | dealerdeck.app (implied) | ⚠️ Confirm or replace |

---

## 9. CONTENT DO'S AND DON'TS

### DO:
- Lead with "inventory intelligence" as the primary value prop — it's what works today
- Use the phrase "customer-safe by default" when talking about design principles
- Mention the 4-stage rollout as a sign of intentionality, not limitation
- Emphasize that DealerDeck was built by someone working the floor — this is a credibility cornerstone
- Reference BMW North Scottsdale as the pilot partner (context only — no logo, no endorsement claim)
- Call the product "iOS-native" and "floor-ready"
- Use the exact positioning quote when space allows

### DON'T:
- Do NOT use BMW logos, trademarks, or branded imagery
- Do NOT claim any endorsement from BMW, Penske, or any dealership
- Do NOT imply DealerDeck replaces a CRM, DMS, or F&I system
- Do NOT make ROI or sales-lift claims — we have no data
- Do NOT claim Android support or App Store availability
- Do NOT claim DriveCentric integration is live — it's planned, pending partner program approval
- Do NOT reference specific rep names (Ed, Andre, etc.) by name without generalizing as "pilot rep feedback"
- Do NOT position against DriveCentric as a competitor — it's a target partner
- Do NOT use "AI agent" or "autonomous" framing — DealerDeck is assistive, not agentic
- Do NOT include financial calculations that look authoritative (trade-in values, lease calcs, rollover equity) — only basic payment estimates with clear disclaimers

---

## 10. VOICE AND TONE

- **Confident, not hyped.** "Voice search that understands you" not "Revolutionary AI-powered voice interface."
- **Specific, not vague.** Use concrete examples like "eggs 5 50 ease → X5 xDrive50e."
- **Respectful of reps' time.** Copy should feel like it's written by someone who understands the floor, not someone selling to the floor.
- **iOS-native aesthetic in writing too.** Clean, sharp, no filler. If a sentence doesn't add information, cut it.
- **No startup clichés.** No "reimagining," "disrupting," "empowering," "unleashing," "revolutionizing."

---

## 11. APP SCREENSHOTS CURRENTLY ON THE SITE

Four screenshots are in the site's `/assets/` folder:

| File | Screen | Caption tag | Caption title |
|---|---|---|---|
| `01-ask.png` | "Ask or Update" home screen with example voice prompts | Ask or update | Talk to DealerDeck like a person |
| `02-processing.png` | AI processing spinner with Gemini-star icon | AI processing | Sub-two-second response time |
| `03-chat.png` | Chat-style inventory query ("Do we have any X550 E") | Inventory search | Direct answers, no dialogue tree |
| `04-customer.png` | Michael Bay customer profile with vehicle interest, summary, next step, payment estimate | Customer profile | AI summaries and next steps |

If new screenshots are added, keep the same framing: iPhone bezel, iOS blue glow shadow, short tag + title + one-sentence description underneath.

---

## 12. DESIGN SYSTEM (already implemented — preserve when updating)

**Palette (matches the DealerDeck app):**
- Background: `#000000` (pure black)
- Surfaces: `#0e1116`, `#141820`, `#1a1f28` (darker to lighter)
- Borders: `#222832` (visible), `#151922` (subtle)
- Text: `#ffffff` primary, `#a1a6b0` secondary, `#6b7280` tertiary, `#4a5260` quaternary
- Primary accent: `#0a84ff` (iOS system blue)
- Accent hover: `#409cff`
- Accent glow: `rgba(10, 132, 255, 0.3)`
- Secondary accents (from app, use sparingly): `#ff9f0a` orange, `#30d158` green, `#ffd60a` yellow

**Typography:**
- Stack: `-apple-system, BlinkMacSystemFont, 'SF Pro Display', 'SF Pro Text', 'Inter', system-ui, sans-serif`
- Mono: `'SF Mono', 'JetBrains Mono', ui-monospace, monospace`
- Headlines: weight 800, letter-spacing -0.035em, tight line-height (1.02-1.05)
- Body: weight 400, letter-spacing -0.01em
- Do NOT introduce serif fonts anywhere

**Spatial language:**
- Cards: 14-20px border-radius, 1px borders in `--line-soft`
- Feature icons: 42px square, blue-tinted rounded squares with `--blue-soft` fill
- Phone mockups: 36px radius, 6px bezel padding, 1.5px dark border, inset shadow + outer blue glow
- Ambient radial blue glows behind major sections (bottom-center, corners) with 60-80px blur
- NO noise/grain overlays
- NO gradient text except for emphasis words on major headlines (blue-to-lighter-blue)

---

## 13. SITE SECTIONS (current structure — keep this order)

1. **Nav** — sticky, glass blur, brand + links + "Request access" CTA
2. **Hero** — eyebrow pill, headline, sub, two CTAs, 4-stat bar
3. **Positioning** — "Our position" label, product-principle quote card + Them vs. DealerDeck comparison table
4. **Features** — 6 feature cards in 3-column grid
5. **Showcase** — 4 iPhone mockups with real screenshots
6. **How it works** — 4-stage rollout cards
7. **Case study** — BMW North Scottsdale pilot partner section with metric card
8. **Stack** — 6 logo cards for tech stack
9. **Contact** — contact info card + "Email us" CTA
10. **Footer** — legal line + links

---

## 14. WHAT TO UPDATE WHEN

**Before DriveCentric Partner Program submission (priority):**
- Real email address
- Real phone number
- Confirmed domain
- Any corrections Camden wants to the positioning or claims

**After DriveCentric approval:**
- Change DriveCentric stack label from "integrating" to "partner" or "integrated"
- Update Stage 3 in the roadmap to "Active"
- Add a case study callout if allowed

**After first non-BMW-NS dealership onboards:**
- Update pilot user count
- Update dealership count
- Consider a "Partners" section if more than one

**When Android or public App Store launches:**
- Update platform claims
- Add App Store / Play Store badges

---

## 15. SUMMARY FOR CURSOR

The website should accurately present DealerDeck as:
- A **real, operating company** (DealerDeck LLC)
- With a **working iOS app** in **private pilot** at one **named dealership** (BMW North Scottsdale)
- Built around a **clear product principle** (AI that helps reps, not replaces them)
- With a **staged rollout plan** that earns trust before asking for access
- That is **ready to integrate with DriveCentric** as soon as partner program approval is granted

Every claim on the site must be traceable to a fact in this document. If you're uncertain whether something is accurate, default to removing it rather than softening it. The DriveCentric reviewer will be looking for signs this is a serious, credible operation — and nothing kills credibility faster than a claim that doesn't hold up.

When in doubt: **understate, be specific, and let the product speak through the screenshots.**

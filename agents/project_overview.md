# Airport Security Hub (`airport`) — Project Overview & Agent Context

**Repository**: `airport`  
**Working Directory**: `/home/reecewilliams8/dev work/repos/airport`  
**Target Category**: Niche Programmatic Travel Utility & Airport Security Guidance  
**Status**: Concept & Architecture Planning (MVP Phase 1)  

---

## 1. Executive Summary & Product Thesis

**Airport Security Hub** is a lightweight, mobile-first programmatic web portal engineered to provide authoritative, granular, and anxiety-reducing airport security checkpoint guidance worldwide.

### The Problem It Solves
Existing airport security resources suffer from three fatal flaws:
1. **The Monolith Fallacy**: General travel and government websites treat airports as homogeneous entities, ignoring that Terminal 1 standard lanes may still use legacy 2D X-rays (mandatory liquids/electronics removal) while Terminal 2 priority lanes or renovated piers feature next-generation 3D Computed Tomography (CT / EDACS / C3) scanners where everything stays in the bag.
2. **The "Return Trip" Trap**: Travelers departing modern hub airports (e.g., London City, Teesside, Milan Linate) pack full-sized liquids (up to 2 liters) or leave cosmetics loose, only to have their expensive sunscreen, perfumes, artisanal Greek olive oil, or local spirits confiscated on their holiday return flight because the regional island airport operates legacy 2D scanners with strict 100ml limits.
3. **Flaky "Live Wait Times"**: Third-party APIs offering real-time wait times for seasonal tourist hubs are notoriously inaccurate, down, or non-existent.

### The Strategic Edge
Instead of fragile live APIs or monolithic descriptions, this portal delivers:
- **Granular Scanner Status by Terminal & Lane**: Crystal-clear "In Bag" vs. "Out of Bag" directives based on verified scanner hardware rollouts.
- **The "Return Trip" Itinerary Checker**: Prevents passenger confiscation heartbreak by comparing the outbound and return airport security thresholds.
- **Long-Tail High-Intent Item Query SEO**: Dominates high-anxiety search terms (e.g., *"Can I bring Greek olive oil through Rhodes airport security?"*, *"Santorini airport vape carry-on rules"*, *"Feta cheese brine hand luggage"*).
- **Charter/Peak Rhythm Congestion Modeling**: Reliable, schedule-based peak congestion bands based on known European holiday flight banks (e.g., Friday/Sunday afternoon UK/Germany charter turnaround waves).

---

## 2. Market Gaps & Strategic Differentiation

```
                     TRADITIONAL SITES                   AIRPORT SECURITY HUB
┌───────────────────────────────────────────────┐  ┌───────────────────────────────────────────────┐
│ • Airport-level generic overview              │  │ • Terminal & lane-specific CT scanner status   │
│ • "Arrive 2-3 hours early" boilerplate        │  │ • Day & hour peak congestion rhythms          │
│ • Generic TSA / EASA rule lists               │  │ • Destination souvenir & regional hazard guide │
│ • Outbound-only assumptions                   │  │ • "Return Trip" outbound vs return comparison │
│ • Fragile or broken live API wait counters    │  │ • Static, high-performance, mobile-optimized   │
└───────────────────────────────────────────────┘  └───────────────────────────────────────────────┘
```

### Strategic Pillar 1: Terminal & Lane CT Scanner Discrepancies
Airports worldwide are mid-transition to **EDACS / C3 standard 3D CT scanners**. A single airport can have:
- Standard lanes: Legacy 2D X-ray (liquids $\le$ 100ml in clear 1L bags; laptops/tablets out).
- FastTrack / Priority lanes: 3D CT (liquids up to 2L inside bag; electronics left in bag).
- Different terminals on completely different upgrade schedules.
*Our approach*: The portal explicitly differentiates rules at the **Terminal** and **Lane Type** level.

### Strategic Pillar 2: The "Return Trip" Trap
A passenger flying London City (LCY) $\rightarrow$ Heraklion (HER) experiences zero liquid removal outbound. On the return trip, Greek security strictly enforces the 100ml rule. 
*Our approach*: The platform features a dual-lookup comparison view (e.g., `/route/LCY-to-HER/`) warning the passenger: *"Your return airport (HER) still uses legacy 2D X-ray scanners. Do NOT purchase liquids over 100ml before security unless bought post-security or checked."*

### Strategic Pillar 3: High-Intent Hazard Item SEO
Holidaymakers do not search for *"EASA Regulation 300/2008"*. They search:
- *"Can I fly with olive oil from Crete in hand luggage?"*
- *"Does frozen feta cheese count as a liquid at Corfu airport?"*
- *"Can I take a 20,000mAh Anker power bank through Ibiza security?"*
*Our approach*: Programmatic item pages (`/items/[item-slug]/`) cross-referenced against the curated holiday airport rules.

### Strategic Pillar 4: Predictable Queue Rhythm Bands
Rather than publishing fake or stale "12-minute wait" live badges that disappoint users:
- We identify seasonal charter turnaround bands (e.g., Ibiza Sunday 14:00–18:00, Rhodes Saturday 10:00–15:00).
- Users receive actionable preparation advice: *"Peak Congestion Band: High surge due to simultaneous UK & German package flight turnarounds. Allow $\ge$ 45 mins for security."*

---

## 3. Scope for Version 1 (MVP)

### Geographic Corridor: Curated European Holiday Islands (11 Airports)
The MVP targets high-traffic seasonal tourist island destinations known for long lines, confused holidaymakers, and local souvenir confiscations:

#### Spain (Aena Managed) — Balearics & Canaries
1. **Palma de Mallorca (PMI)** — Balearic Islands
2. **Ibiza (IBZ)** — Balearic Islands
3. **Menorca (MAH)** — Balearic Islands
4. **Tenerife South (TFS)** — Canary Islands
5. **Lanzarote (ACE)** — Canary Islands
6. **Fuerteventura (FUE)** — Canary Islands

#### Greece (Fraport Greece & HCAA Managed)
7. **Heraklion (HER / Nikos Kazantzakis)** — Crete
8. **Chania (CHQ / Ioannis Daskalogiannis)** — Crete
9. **Rhodes (RHO / Diagoras)** — Dodecanese
10. **Corfu (CFU / Ioannis Kapodistrias)** — Ionian Islands
11. **Santorini (JTR / Thira)** — Cyclades

### High-Anxiety Holiday Hazard Items (Initial Catalog)
1. **Olive Oil** (Tin / Bottle / Artisanal) — Classified as liquid; banned in carry-on $>100\text{ml}$ regardless of seals.
2. **Honey / Thyme Honey** — Viscous liquid rule applies; confiscation risk extremely high in Greece.
3. **Feta Cheese & Soft Cheeses in Brine** — Semi-solids in liquid; frequently seized at HER, CHQ, CFU.
4. **Spirits / Ouzo / Raki / Hierbas / Sangria** — Banned in hand luggage $>100\text{ml}$ unless duty-free sealed bag with receipt.
5. **Sunscreen & After-sun Lotions ($>100\text{ml}$ family bottles)** — Top confiscated item across Balearics and Canaries.
6. **Power Banks & Lithium-Ion Batteries** — Hand-luggage *mandatory* ($\le 100\text{Wh}$ free, $100\text{--}160\text{Wh}$ airline approval, banned in checked hold).
7. **Vapes & E-Cigarettes / E-Liquids** — Battery in cabin only; liquids subject to 100ml rule.
8. **Artisanal Sea Salt / Sand Souvenirs** — Powders and protected natural beach sand (prohibited/penalized in Canary/Greek reserves).

### MVP Exclusions
- ❌ No user registration, accounts, or auth barriers.
- ❌ No fragile third-party live wait-time scraping/APIs.
- ❌ No attempt to index all 5,000+ global airfields (focus strictly on high-intent holiday corridors first).

---

## 4. Core Page Component: The "Checkpoint Card"

Every airport terminal/lane page renders the standardized **Checkpoint Card** UI block:

```
┌─────────────────────────────────────────────────────────────────────────────┐
│ 📍 PALMA DE MALLORCA (PMI) — MAIN TERMINAL (TERMINAL A/C) STANDARD LANES   │
│ Status as of: May 2026 | Scanner Hardware: Phased CT Rollout in Progress    │
├─────────────────────────────────────────────────────────────────────────────┤
│ 📦 SCANNER TECH & ELECTRONICS                                               │
│    • Laptops & Tablets: OUT OF BAG (Legacy lanes) / IN BAG (Lane 4-6 CT)    │
│    • Smartwatches & Jewelry: Wearable unless heavy metal                    │
├─────────────────────────────────────────────────────────────────────────────┤
│ 🧴 LIQUIDS & TOILETRIES                                                     │
│    • Maximum container: 100ml (3.4 fl oz)                                   │
│    • Total capacity: 1L clear, resealable plastic bag (one per passenger)   │
│    • Empty water bottles: Allowed through security                          │
├─────────────────────────────────────────────────────────────────────────────┤
│ 👟 PHYSICAL PASSENGER PREP                                                  │
│    • Shoes: Remove if ankle-high / boots / thick soles                      │
│    • Belt & Jacket: Mandatory removal into separate tray                    │
├─────────────────────────────────────────────────────────────────────────────┤
│ ⚠️ REGIONAL HAZARD WARNING                                                  │
│    • Local Olive Oil & Hierbas: CANNOT travel in hand luggage if >100ml.    │
│    • Duty-Free Purchases: Must remain inside sealed tamper-evident bag.     │
├─────────────────────────────────────────────────────────────────────────────┤
│ ⏱️ PEAK CONGESTION RHYTHMS (Schedule-Based)                                │
│    • Peak Alert: Friday & Sunday 12:00 – 17:00 (Charter turnaround waves)   │
│    • Recommendation: Arrive 2.5 hours prior during peak summer windows     │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## 5. Information Architecture & URL Hierarchy

```
/                                    # Homepage: Fast corridor search, airport picker & item search
├── /airports/                       # Master directory of supported airports
│   ├── /airports/pmi/               # Palma de Mallorca Airport Master Page
│   │   ├── /airports/pmi/terminal-a/ # Granular terminal / lane breakdown
│   ├── /airports/ibz/               # Ibiza Airport Checkpoint Guide
│   ├── /airports/her/               # Heraklion Airport Checkpoint Guide
│   └── ...                          # (Other MVP island airports)
│
├── /items/                          # High-intent item security rules directory
│   ├── /items/olive-oil/            # "Can I take olive oil on a plane?"
│   ├── /items/sunscreen/            # "Sunscreen carry-on rules & size limits"
│   ├── /items/power-banks/          # "Power bank Watt-hour rules for flights"
│   ├── /items/feta-cheese/          # "Can you bring feta cheese in hand luggage?"
│   └── ...                          # (High-anxiety holiday query pages)
│
├── /routes/                         # Return-trip trap comparison pages
│   ├── /routes/london-to-palma/     # London (LCY/STN/LGW) to PMI security comparison
│   ├── /routes/manchester-to-corfu/ # Manchester to Corfu return security warning
│   └── ...
│
├── /about/                          # Mission, scanner rollout tracker & methodology
├── /report-update/                  # Crowdsourced passenger verification form
├── /privacy/                        # Privacy policy
└── /terms/                          # Terms of service & travel disclaimer
```

---

## 6. Data Architecture & Schemas

Data is managed cleanly in structured JSON files under `_data/` (or `src/content/` if Astro):

### 1. Airport Model (`_data/airports/{code}.json`)
```json
{
  "code": "PMI",
  "name": "Palma de Mallorca Airport",
  "local_name": "Aeropuerto de Palma de Mallorca",
  "city": "Palma",
  "island": "Mallorca",
  "country": "Spain",
  "operator": "Aena",
  "last_verified": "2026-05-01",
  "terminals": [
    {
      "name": "Main Terminal - Departures",
      "scanner_type": "hybrid_rollout",
      "scanner_details": "Phased 3D CT scanner deployment on lanes 4-6; legacy 2D X-rays on remaining standard lanes.",
      "liquids": {
        "max_single_container_ml": 100,
        "max_total_litres": 1.0,
        "bag_required": true,
        "remove_from_bag": true,
        "notes": "Even if passing CT lane, prepare liquids in 100ml bottles to avoid lane diversion."
      },
      "electronics": {
        "laptops_out": true,
        "tablets_out": true,
        "small_electronics_out": false,
        "power_banks_carry_on_only": true
      },
      "physical_prep": {
        "shoes_off": "boots_and_thick_soles_only",
        "belts_off": true,
        "jackets_off": true,
        "smartwatches_off": false
      },
      "regional_hazards": [
        "olive-oil",
        "hierbas-liqueur",
        "sunscreen-large",
        "ensaimadas"
      ],
      "peak_congestion_rhythms": [
        {
          "days": ["Friday", "Sunday"],
          "hours": "12:00-17:00",
          "severity": "high",
          "reason": "Intense UK/German charter turnaround flights"
        },
        {
          "days": ["Monday", "Tuesday", "Wednesday", "Thursday", "Saturday"],
          "hours": "06:00-09:00",
          "severity": "moderate",
          "reason": "Early morning inter-island & mainland business flights"
        }
      ]
    }
  ]
}
```

### 2. Item Model (`_data/items/{slug}.json`)
```json
{
  "slug": "olive-oil",
  "name": "Olive Oil (Artisanal, Tinned, or Bottled)",
  "category": "Food & Liquids",
  "carry_on_allowed": "conditional",
  "carry_on_condition": "Under 100ml only in sealed container inside 1L clear plastic bag. Over 100ml strictly prohibited in cabin baggage unless bought post-security in duty-free.",
  "checked_allowed": true,
  "checked_recommendation": "Pack in leak-proof ziplock bags wrapped in clothing inside hard suitcase.",
  "confiscation_risk_level": "extreme",
  "common_misconceptions": "Travelers frequently assume sealed commercial olive oil tins or farm shop souvenirs are exempt from the 100ml liquid rule. They are not.",
  "return_trip_warning": "Even if departing an airport with new 3D CT scanners, your return Mediterranean airport will confiscate olive oil bottles exceeding 100ml at checkpoint.",
  "faqs": [
    {
      "q": "Can I bring unopened olive oil through airport security?",
      "a": "Only if the bottle is 100ml (3.4 oz) or less and fits inside your clear liquids bag. Larger bottles are confiscated regardless of whether the seal is intact."
    },
    {
      "q": "What about olive oil bought at the airport duty-free?",
      "a": "Duty-free olive oil is permitted on board provided it remains sealed inside the official STEB (Security Tamper-Evident Bag) with the receipt visible."
    }
  ]
}
```

---

## 7. SEO, E-E-A-T & Monetization Strategy

### Programmatic SEO Pillars
1. **Dynamic Schema Markup**:
   - `FAQPage` schema on every item and airport page for instant Google snippet rich results.
   - `HowTo` schema for checkpoint preparation (e.g., *"How to pack liquids for Palma Airport security"*).
   - `BreadcrumbList` navigation for granular geographic hierarchy (`Home > Spain > Balearics > Palma de Mallorca`).
2. **Search Intent Dominance**:
   - Targeting long-tail interrogative queries with zero-fluff, bold, instant answers ("At a Glance" verdict boxes).
   - Instant answers formatted above the fold for mobile users standing in airport check-in queues.

### Monetization Channels
1. **Contextual Travel Affiliate Links**:
   - TSA-approved clear toiletry bag bundles (Amazon Associates).
   - Silicon travel bottle sets compliant with 100ml standards.
   - Travel insurance with luggage confiscation / delay protection.
   - eSIM / roaming data for tourists landing in Spain/Greece.
2. **FastTrack & Airport Lounge Booking Partnerships**:
   - Priority lane affiliate widgets (Holiday Extras, Priority Pass, LoungeBuddy).
3. **Display Advertising**:
   - Google AdSense / high-CPM programmatic ad placements on high-traffic airport pages.

---

## 8. Crowdsourced Passenger Feedback Loop

Because airport scanner rollouts happen rapidly on a pier-by-pier basis, the portal features a low-friction **"Spotted a Change?"** widget on every page:
- One-click confirmation: *"Did you fly from PMI this week? Did you have to take laptops out? [ Yes ] [ No ]"*
- Instant timestamp verification badge: *"Verified by 14 passengers this week."*
- Structured form submission routed to a serverless webhook / GitHub dispatch for rapid review.

---

## 9. Immediate Implementation Plan (Phase 1)

1. **Architecture & Foundation**:
   - Set up project framework (Lightweight static generator with fast markdown/JSON builds, clean responsive CSS/Bootstrap or Tailwind).
   - Establish directory structure (`_data/`, `_includes/`, `_layouts/`, `airports/`, `items/`).
2. **Data Model Population**:
   - Populate JSON data for the **11 Spanish & Greek island airports**.
   - Populate JSON/Markdown data for the **first 10 high-intent holiday hazard items**.
3. **Core Templates & Components**:
   - Develop the responsive **Checkpoint Card** component.
   - Build the **"Can I Fly With It?" Item Card** component.
   - Implement the **Return Trip Trap comparison calculator**.
4. **Programmatic Generation & SEO**:
   - Generate SEO-optimized airport pages and item pages with JSON-LD schema.
   - Deploy canonicals, robots.txt, and XML sitemaps.


# Airport Security Hub — Data Architecture & Schema Specifications

This document defines the data structures, schemas, and programmatic generation logic for the **Airport Security Hub** platform.

---

## 1. Directory Structure

```
airport/
├── agents/
│   ├── overview.md -> project_overview.md
│   ├── project_overview.md
│   └── data_architecture.md
├── _data/
│   ├── airports/
│   │   ├── pmi.json
│   │   ├── ibz.json
│   │   ├── mah.json
│   │   ├── tfs.json
│   │   ├── ace.json
│   │   ├── fue.json
│   │   ├── her.json
│   │   ├── chq.json
│   │   ├── rho.json
│   │   ├── cfu.json
│   │   └── jtr.json
│   ├── items/
│   │   ├── olive-oil.json
│   │   ├── honey.json
│   │   ├── feta-cheese.json
│   │   ├── local-spirits.json
│   │   ├── sunscreen.json
│   │   ├── power-banks.json
│   │   ├── vapes-and-eliquids.json
│   │   ├── duty-free-liquids.json
│   │   ├── cosmetics-and-perfumes.json
│   │   └── artisanal-salts-sands.json
│   └── corridors/
│       ├── spain-balearics.json
│       ├── spain-canaries.json
│       └── greece-islands.json
```

---

## 2. Airport Data Schema (`_data/airports/{code}.json`)

| Field | Type | Description |
| :--- | :--- | :--- |
| `code` | `string` | 3-letter IATA code (e.g. `"PMI"`) |
| `icao` | `string` | 4-letter ICAO code (e.g. `"LEPA"`) |
| `name` | `string` | Official international name |
| `local_name` | `string` | Local native name |
| `city` | `string` | Primary municipality served |
| `region_or_island` | `string` | Specific holiday island/region |
| `country` | `string` | Country name (`"Spain"` or `"Greece"`) |
| `country_code` | `string` | ISO 2-letter country code (`"ES"` or `"GR"`) |
| `operator` | `string` | Governing operator (`"Aena"` or `"Fraport Greece"`) |
| `last_verified` | `string` | YYYY-MM-DD verification date |
| `last_ai_gathered` | `string` | YYYY-MM-DD date when automated AI tools last gathered and extracted data |
| `last_human_reviewed` | `string` | YYYY-MM-DD date when human editorial team last reviewed and verified data |
| `terminals` | `array` | List of terminal checkpoint zones |

### Terminal Object Schema:
```json
{
  "terminal_id": "main",
  "name": "Main Terminal",
  "checkpoint_location": "Floor 2, Departures Hall",
  "ct_scanner_active": false,
  "electronics_rule": {
    "laptops_out": true,
    "tablets_out": true,
    "smartwatches_out": false,
    "power_banks": "carry_on_only_max_100wh",
    "summary": "Remove laptops and tablets into dedicated plastic trays."
  },
  "liquids_rule": {
    "max_container_ml": 100,
    "max_single_container": "100ml",
    "max_total_litres": 1.0,
    "max_total_capacity": "1l",
    "clear_bag_required": true,
    "remove_from_bag": true,
    "summary": "100ml limit strictly enforced. One transparent 1-liter plastic bag per passenger."
  },
  "passenger_prep": {
    "shoes_removal": "ankle_and_thick_soles_only",
    "belt_removal": true,
    "outerwear_removal": true,
    "coins_and_keys": "into_bag_or_tray"
  },
  "regional_hazards": [
    {
      "item_slug": "olive-oil",
      "warning": "Spanish artisanal olive oil over 100ml will be confiscated regardless of packaging or seals unless purchased inside post-security duty-free."
    },
    {
      "item_slug": "hierbas-liqueur",
      "warning": "Bottled Hierbas Ibicencas must be checked in hold luggage if purchased outside the airport."
    }
  ],
  "congestion_rhythms": [
    {
      "day_group": "Fridays & Sundays",
      "peak_hours": "12:00 - 17:30",
      "risk_level": "very_high",
      "lead_time_recommended_hours": 2.5,
      "driver": "Concentrated UK & German leisure charter turnaround flights"
    },
    {
      "day_group": "Weekday Mornings",
      "peak_hours": "06:30 - 08:30",
      "risk_level": "moderate",
      "lead_time_recommended_hours": 2.0,
      "driver": "Mainland commuter flights to Madrid and Barcelona"
    }
  ]
}
```

---

## 3. High-Intent Hazard Item Schema (`_data/items/{slug}.json`)

```json
{
  "slug": "olive-oil",
  "title": "Olive Oil (Bottled, Tinned, or Artisanal)",
  "category": "Food & Liquids",
  "carry_on_status": "CONDITIONAL",
  "carry_on_summary": "Allowed up to 100ml in transparent 1L bag; >100ml confiscated at checkpoint.",
  "checked_status": "ALLOWED",
  "checked_summary": "Allowed in checked luggage without volume limit; pack securely to prevent rupture.",
  "risk_score": 9.5,
  "confiscation_trigger": "Security X-ray flags liquid density; container size exceeds 100ml.",
  "duty_free_exception": "Permitted in cabin baggage only if purchased in airport departure duty-free and sealed in an approved STEB bag with receipt visible.",
  "return_trip_warning": "UK or European passengers flying home from Greece or Spain frequently buy farm-fresh olive oil and lose it at island security checkpoints.",
  "seo": {
    "target_keywords": [
      "can i bring olive oil on a plane from greece",
      "taking olive oil through airport security spain",
      "creta olive oil hand luggage rules"
    ],
    "meta_title": "Can You Bring Olive Oil Through Airport Security? (Holiday Guide)",
    "meta_description": "Don't lose your olive oil at airport security. Discover carry-on limits, checked bag rules, and why island airports confiscate artisanal bottles."
  },
  "faqs": [
    {
      "question": "Can I bring unopened artisanal olive oil in my carry-on bag?",
      "answer": "No. The 100ml liquid security rule applies equally to unopened, factory-sealed, and artisanal containers. Any bottle exceeding 100ml will be confiscated."
    },
    {
      "question": "Can I put olive oil in my checked luggage?",
      "answer": "Yes. There are no volume restrictions on olive oil in checked baggage, but you should double-bag bottles in zip-seal plastic and cushion them among clothes."
    }
  ]
}
```

---

## 4. Return-Trip Trap Calculation Logic

```typescript
interface ReturnTripComparison {
  origin_airport: string;
  destination_airport: string;
  outbound_liquid_limit: string;
  return_liquid_limit: string;
  has_scanner_mismatch: boolean;
  trap_warning: string;
}

// Logic:
// If Origin has CT scanners (e.g., liquids in bags / >100ml) 
// but Destination/Return has Legacy 2D (100ml cap),
// Trigger high-severity return trip warning badge!
```


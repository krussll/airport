# Airport Security Data References & Verification Sources

This document compiles the official data sources, airport operator security directives, and regulatory framework documentation used to seed [`_data/airports.json`](file:///home/reecewilliams8/dev%20work/repos/airport/_data/airports.json).

---

## 1. Regulatory Authorities & EU Baseline Mandates

* **European Commission — C3 Scanner 100ml Re-imposition (Sept 1, 2024)**  
  *Context*: Temporarily re-introduced the 100ml single-container liquid limit for all EU airports operating next-generation C3 (3D CT) Explosive Detection Systems for Cabin Baggage (EDSCB) pending technical review of detection algorithms.  
  *Official Notice*: [European Commission Directorate-General for Mobility and Transport](https://transport.ec.europa.eu/news-events/news/commission-enforces-temporary-restrictions-liquid-screening-certain-eu-airports-2024-07-31_en)
* **EASA (European Union Aviation Safety Agency)**  
  *Context*: Baseline rules for Dangerous Goods in cabin baggage, lithium battery limitations (100Wh carry-on rule), and prohibited items.  
  *Official Guidelines*: [EASA Passengers Information](https://www.easa.europa.eu/en/passengers)

---

## 2. Spain (Aena Managed Airports)

All Spanish airports are governed by **Aena S.M.E., S.A.** and screened under the supervision of the **Guardia Civil**.

### Central Aena Security Directives
* **Aena Security Controls & Screening Procedures**: [Aena Security Controls Guide](https://www.aena.es/en/passengers/baggage-controls/security-control.html)
* **Aena Hand Luggage & Dangerous Goods Regulations**: [Aena Hand Luggage & Liquids Rules](https://www.aena.es/en/passengers/baggage-controls/hand-luggage.html)

### Individual Spanish Airport Portals
1. **Palma de Mallorca (PMI / LEPA)**  
   *Official Portal*: [Aena Palma de Mallorca](https://www.aena.es/en/palma-de-mallorca.html)  
   *Key Status*: Central Departures hall undergoes phased terminal modernization. Trial CT lanes deployed on select lines (Lanes 4–6), but standard lines operate 2D X-ray rules requiring laptops and 100ml liquids out.
2. **Ibiza (IBZ / LEIB)**  
   *Official Portal*: [Aena Ibiza](https://www.aena.es/en/ibiza.html)  
   *Key Status*: Conventional 2D X-ray lanes. Mandatory 100ml liquids bag and electronics extraction. Intense Sunday/Monday departures wave.
3. **Menorca (MAH / LEMH)**  
   *Official Portal*: [Aena Menorca](https://www.aena.es/en/menorca.html)  
   *Key Status*: Conventional 2D X-ray. Family changeover weekend peaks.
4. **Tenerife South (TFS / GCTS)**  
   *Official Portal*: [Aena Tenerife Sur](https://www.aena.es/en/tenerife-sur.html)  
   *Key Status*: Conventional 2D X-ray. Tuesdays and Fridays are severe peak UK charter turnover days. Natural volcanic sand removal prohibited.
5. **Lanzarote (ACE / GCRR)**  
   *Official Portal*: [Aena César Manrique-Lanzarote](https://www.aena.es/en/cesar-manrique-lanzarote.html)  
   *Key Status*: Terminal 1 (international) & Terminal 2 (inter-island). Conventional 2D X-ray. Thursdays and Sundays peak. Protected olivine and black sand confiscation.
6. **Fuerteventura (FUE / GCFV)**  
   *Official Portal*: [Aena Fuerteventura](https://www.aena.es/en/fuerteventura.html)  
   *Key Status*: Single passenger terminal with conventional 2D X-ray screening. Corralejo Popcorn Beach rhodolith fossils strictly protected by Guardia Civil.

---

## 3. Greece (Fraport Greece & HCAA Airports)

Greek regional airports are managed by **Fraport Greece** (14 regional airports) or the **Hellenic Civil Aviation Authority (HCAA / YPA)**, screened under the supervision of the **Hellenic Police (EL.AS)**.

### Central Greek Civil Aviation Directives
* **Hellenic Civil Aviation Authority (HCAA) Security Regulations**: [HCAA Passenger Security Directives](https://hcaa.gov.gr/en/domains/epibates)
* **Fraport Greece Corporate Portal**: [Fraport Greece Corporate Portal](https://www.fraport-greece.com/)

### Individual Greek Airport Portals
7. **Heraklion (HER / LGIR) — Crete**  
   *Operator*: Hellenic Civil Aviation Authority (HCAA)  
   *Official Portal*: [HCAA Heraklion Directory](https://hcaa.gov.gr/en)  
   *Key Status*: Legacy 2D X-ray screening. Notorious confiscation rates for Cretan olive oil, thyme honey, and cheese in brine. Extreme peaks on Tuesdays, Fridays, and Sundays.
8. **Chania (CHQ / LGSA) — Crete**  
   *Operator*: Fraport Greece  
   *Official Portal*: [Fraport Greece Chania Airport](https://www.chq-airport.gr/en/)  
   *Security Guide*: [Chania Security Information](https://www.chq-airport.gr/en/category-detailed/ctg_id-72/nd_id-501)
9. **Rhodes (RHO / LGRP) — Dodecanese**  
   *Operator*: Fraport Greece  
   *Official Portal*: [Fraport Greece Rhodes Airport](https://www.rho-airport.gr/en/)  
   *Security Guide*: [Rhodes Security Information](https://www.rho-airport.gr/en/category-detailed/ctg_id-268/nd_id-943)
10. **Corfu (CFU / LGKR) — Ionian Islands**  
    *Operator*: Fraport Greece  
    *Official Portal*: [Fraport Greece Corfu Airport](https://www.cfu-airport.gr/en/)  
    *Security Guide*: [Corfu Security Information](https://www.cfu-airport.gr/en/category-detailed/ctg_id-533/nd_id-1559)  
    *Key Status*: Conventional 2D X-ray. High peak UK charter flight waves on Mondays and Fridays. Seizure of kumquat liqueurs and Corfiot olive oil.
11. **Santorini (JTR / LGSR) — Cyclades**  
    *Operator*: Fraport Greece  
    *Official Portal*: [Fraport Greece Santorini Airport](https://www.jtr-airport.gr/en/)  
    *Security Guide*: [Santorini Security Information](https://www.jtr-airport.gr/en/category-detailed/ctg_id-433/nd_id-1328)  
    *Key Status*: Conventional 2D X-ray. Severe daily peaks linked to caldera hotel checkouts and ferry transfers. Vinsanto/Assyrtiko wine and fava paste confiscations.

---

## 4. Verification Checklist for Developers & Agents

When updating `_data/airports.json`:
1. **Scanner Deployment Status**: Ensure `ct_scanners_deployed` and `ct_scanners_universal` accurately reflect standard lanes vs. pilot lanes without exposing technical hardware jargon to travellers.
2. **Liquids / Electronics Flags**: If an airport upgrades to universal C3 scanners, `ct_scanners_deployed` and `ct_scanners_universal` should be updated, and `temporary_eu_100ml_cap_applies` evaluated against the latest European Commission directives.
3. **Regional Hazards**: Check for local souvenir confiscations (olive oil, honey, soft cheeses, local spirits, beach sand).
4. **Peak Congestion Bands**: Cross-reference with weekly flight rotation patterns.

---

## 5. Reference Sites & Category Benchmarks (Planning Context)

The following websites and tools were evaluated during planning as category reference points and benchmarks:
* **FlightQueue** ([https://flightqueue.com/](https://flightqueue.com/)) – Shared as an example of an existing queue/wait-time tracker, which focuses primarily on airport security checkpoint wait times and queue estimates.
* **Airport Liquids** ([https://www.airportliquids.com/](https://www.airportliquids.com/)) – Shared alongside FlightQueue as a site covering airport liquid regulations.
* **MiFlight** – Mentioned as another example in the queue-tracking category that relies primarily on app-based or crowd-sourced wait times.


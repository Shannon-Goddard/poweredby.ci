# Loyal9 — Hemp & Cannabis Seed Registry

**Owner:** Shannon, Single Member Manager — Loyal9 LLC  
**Project Start:** Second attempt, 2026  
**Status:** Active — Pipeline in progress

---

## Why This Exists

On November 12, 2025, the FY 2026 Agriculture Appropriations Act (P.L. 119-37) was signed into law. Section 781 of that act fundamentally changed what a legal cannabis seed is.

The old rule was simple: if a seed tested under 0.3% Delta-9 THC, it was legal hemp. The new rule adopts a **Total THC standard**:

> Total THC = Delta-9 THC + (THCA × 0.877)

Under this formula, a seed's legality is now determined by its **parent plant**. If the parent plant exceeds 0.3% Total THC, the seed is legally classified as marijuana — regardless of what the seed itself tests at. Since nearly all modern cannabis genetics are bred from high-THC or high-THCA plants, the vast majority of the current US seed market becomes a **federal felony for interstate commerce** on **November 12, 2026**.

The result: seed sales will migrate almost entirely into **state-licensed dispensaries**, which already operate inside closed-loop state systems and can legally sell high-THC genetics within their borders.

**There is no clean, verified, publicly searchable directory of where to legally buy cannabis seeds by state.**

Loyal9 is building that directory.

---

## The Product

**loyal9.app** — A compliance-first seed finder that answers one question:

> *"Where can I legally buy cannabis seeds in my state right now?"*

Every listing is backed by verified, cited government data with collection dates. No guessing. No outdated info. No seed banks that will be federally illegal in 2026.

**Secondary revenue:** Verified datasets sold on Datarade as B2B compliance data products.

---

## The Data Strategy — "Dual-License" Logic

The core insight driving this project: a business that appears on **both** the USDA Active hemp list **and** a state cannabis retail list is a **"Bridge Entity"** — federally licensed to grow AND state-licensed to sell. After November 2026, these are the only businesses legally positioned to sell seeds across the full spectrum of genetics.

Finding those overlaps is the product.

### Three-Level Verification Stack

| Level | Name | Method | Status |
| :--- | :--- | :--- | :--- |
| Level 1 | USDA Active | Filter USDA Search Tool for `Status = Active` | ✅ Complete |
| Level 2 | Dual-Licensed | Cross-reference against state dispensary/retail lists | 🔄 In Progress |
| Level 3 | Human-Verified | Confirm via Secretary of State business filings | ⏳ Pending |

### Data Schema — `Field_Year_Source`

All fields follow this naming convention to keep the dataset audit-ready:

| Field | Example Source |
| :--- | :--- |
| `USDA_Status_2026` | USDA Hemp Public Search Tool |
| `State_Retail_ID_2026` | State Cannabis Regulatory Board |
| `Physical_Address_2026` | State Secretary of State filing |
| `Historical_Email_2022` | USDA FOIA Archive (114-page PDF) |

---

## Project Structure

```
NEW-SEEDS-LAW/
├── pipeline/
│   ├── 01_usda_active_states/       # Level 1 — USDA Active filter
│   │   ├── csv/
│   │   │   └── USDA_search_tool.csv
│   │   ├── scripts/
│   │   │   └── active_states.py
│   │   └── README.md
│   └── 02_state_license_retail_list/ # Level 2 — State retail cross-reference
│       ├── csv/
│       │   └── official_state_license_portals.csv
│       ├── pdf/
│       └── scripts/
├── .extra/                           # Archive — not on active to-do list
│   ├── csv/
│   │   ├── FOIAUSDAHempLicensees.csv
│   │   ├── 2022-Processor-List-w-Contact-Info.csv
│   │   └── 2025-License-Grower-with-Contact.csv
│   └── pdf/
│       ├── FOIAUSDAHempLicensees.pdf
│       ├── 2022-Processor-List-w-Contact-Info.pdf
│       └── 2025-License-Grower-with-Contact.pdf
├── notes.text                        # Shannon's project notes and research
├── roadmap.md                        # Revenue architecture and drop schedule
├── pdf-to-csv.html                   # In-browser PDF parser (no install needed)
└── README.md                         # This file
```

---

## Pipeline Overview

### Stage 01 — USDA Active States
**Source:** [USDA Hemp Public Search Tool](https://hemp.ams.usda.gov/s/PublicSearchTool)  
**Collected:** March 31, 2026 — manual copy/paste by Shannon  
**Script:** `active_states.py` — written by Amazon Q  
**Result:** 47 active states/territories identified

These 47 states define the scope for all downstream pipeline work.

### Stage 02 — State License & Retail Lists
**Source:** `official_state_license_portals.csv` — 25 state regulatory portals  
**Method:** Shannon visits each portal, downloads CSV or PDF, drops it in the folder  
**Script:** Per-state extraction scripts written by Amazon Q as each file comes in  
**Goal:** Build the cross-reference dataset for the dual-license match

### Stage 03 — Fuzzy Match (Planned)
Cross-reference `Business_Name` + `Zip_Code` between the USDA list and each state retail list to identify Bridge Entities. Script to be written by Amazon Q.

### Stage 04 — Secretary of State Enrichment (Planned)
For every confirmed match, manually pull the Golden Record from the state SOS:
- Full physical address
- Registered agent
- Direct phone/email (where available in state filings)

---

## Tools

### pdf-to-csv.html
An in-browser PDF-to-CSV converter — **no installs, no Python, no command line required.**

Drop any state agency PDF directly into the browser. The tool uses PDF.js to parse the file entirely client-side (nothing leaves your machine), reconstructs table rows by grouping text items by Y-coordinate, and exports a clean CSV with configurable delimiters, column splitting strategies, and a live preview table.

Built by Amazon Q specifically for this project to handle the reality that most state agencies publish data as PDFs that were never meant to be machine-readable.

---

## The Archive — `.extra/`

Three files not on the active to-do list but potentially valuable later:

| File | Contents | Why It Matters |
| :--- | :--- | :--- |
| `FOIAUSDAHempLicensees.csv` | Full USDA licensee history via FOIA request | Contains `Expiration Date`, `Phone`, `Email` fields (redacted as `(b)(6)`) — the historical audit trail |
| `2025-License-Grower-with-Contact.csv` | 2025 grower list with contact info | Bridge between 2022 archive and current active list |
| `2022-Processor-List-w-Contact-Info.csv` | 2022 processor list with contact info | Earliest contact data layer |

**Note from Amazon Q:** The FOIA file is the most strategically valuable piece in `.extra`. It covers states like Florida, Alaska, and Arkansas that don't appear in the current USDA active list — meaning those states run state-only programs. It also contains `Expiration Date` data that, when cross-referenced against the current active list, can flag licenses expiring before November 2026. Those are businesses that may not renew under the new law — a compelling signal for the Datarade product. Florida alone has hundreds of records and likely warrants its own pipeline stage (`03_florida_state_only`) when the time comes.

---

## The "Drop" Schedule — loyal9.app

State data is released on the website in priority order to build SEO authority on the seed search page:

| Drop | State | Reason |
| :--- | :--- | :--- |
| 1 | Alabama | High researcher density; new 2026 medical licenses; university data (A&M, Auburn, Tuskegee) |
| 2 | California | Largest market; highest number of seed-to-sale entities |
| 3 | Colorado | Mature market with detailed tracking |
| 4 | Michigan | Strict Active status tagging; home delivery flags |

---

## Datarade Product Tiers

| Product | Contents |
| :--- | :--- |
| The "Retail Lead" CSV | Dual-licensed dispensaries only — confirmed phone and email |
| The "Academic Batch" | University researchers (Alabama A&M, Auburn, Tuskegee, etc.) |
| The "Audit Trail" Master | Full 2020–2026 historical activity for the entire dataset |

---

## Implementation Timeline

| Date | Milestone |
| :--- | :--- |
| Nov 12, 2025 | P.L. 119-37 signed into law |
| Feb 10, 2026 | FDA deadline to publish cannabinoid classification lists |
| Mar 31, 2026 | USDA Active list collected (Stage 01 complete) |
| Nov 12, 2026 | **Effective date — non-compliant seeds become Schedule I** |
| Nov 12, 2028 | Potential extension if Hemp Planting Predictability Act passes |

---

## Credits & Transparency

Shannon built this project from scratch — the research, the legal analysis, the data collection, the vision, and the business strategy are all hers.

**Gemini (Google AI Assistant)** Architectural Sounding Board or Strategy Collaborator:

- Refining the "Dual-License" logic
- Mapping the November 2026 legal impact
- Assisting in the design of the `Field_Year_Source` schema

**Amazon Q (AWS AI Assistant)** is Shannon's development partner on this second attempt. Amazon Q wrote all scripts in this repository, built the `pdf-to-csv.html` tool, co-designed the pipeline architecture, and contributed the following strategic recommendations:

- Flagging the FOIA `Expiration Date` field as a pre-November-2026 churn signal for the Datarade product
- Identifying Florida as a state-only program warranting its own pipeline stage
- Recommending the `.extra` archive stay untouched until the active pipeline is complete
- Suggesting the `(b)(6)` FOIA redaction fields be preserved in the schema as enrichment targets for Level 3 SOS verification

This README was written by Amazon Q based on Shannon's notes, roadmap, and project files.

> *"I like to keep it real."* — Shannon

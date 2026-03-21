# AVOC Consolidation and Normalization

> **BEFORE YOU RUN THIS PROMPT — FILL IN ALL VARIABLES BELOW**  
> Replace every `[VARIABLE]` token before submitting. Do not leave any placeholder unresolved.
>
> | Variable | Your Value |
> |----------|------------|
> | `[OUTPUT_FOLDER_PATH]` | _(Full path to the folder where `AVOC_Consolidated.xlsx` must be created)_ |

---

## Role and goal

You are a **senior product manager** specializing in **source-to-pay (S2P)** and **voice-of-customer (VoC)** programs. You have led many release-cycle prioritization forums that use **virtual dollar voting** and tiered customer segmentation. Your outputs are used by leadership for **roadmap and investment decisions**, so numeric totals, customer lists, and merge decisions must be **traceable and conservative** (merge only when similarity is clear).

**Your goal:** Process every AVOC file indexed in this project, extract structured data from **Pre-Voting** and **Post-Voting** lists, **normalize** duplicate or overlapping requests across cycles into single consolidated features, **score** them, and produce **one sortable table** plus an **Excel workbook** at the path below.

**Indexed output location (mandatory):**  
Create a workbook named **`AVOC_Consolidated.xlsx`** in: `[OUTPUT_FOLDER_PATH]`

If the environment cannot create a native `.xlsx` file, create **`AVOC_Consolidated.csv`** (UTF-8, comma-separated) in the same folder, with an opening note that Excel can open it, and use the same column headers as specified below.

---

## Release cycle reference (latest → oldest)

Use this **canonical order** for cycle names, recency scoring, and occurrence counting:

| Order (newest = 1) | Cycle name | Recency score |
|--------------------|------------|---------------|
| 1 | Juniper | 10 |
| 2 | Mahogany | 9 |
| 3 | Aspen | 8 |
| 4 | Redwood | 7 |
| 5 | Cedar | 6 |
| 6 | Tulip | 5 |
| 7 | Oak | 4 |
| 8 | Maple | 3 |

**Occurrence score (1–8):** Count **distinct** cycle names in which the feature (raw or merged) **appears in at least one list** (Pre-Voting and/or Post-Voting). Cap at 8.

**Recency score (3–10):** Use the **newest** cycle in which that consolidated feature appears, and map with the table above.

---

## Input discovery — process ALL AVOC sources in the project

1. Search the indexed project for AVOC materials for these cycles: **Juniper, Mahogany, Aspen, Redwood, Cedar, Tulip, Oak, Maple** (spelling variants, folders, or filenames may differ — map to the canonical names above).
2. For each cycle, locate **both** where possible:
   - **Pre-Voting List** — raw feature requests **before** customer voting  
   - **Post-Voting List** — features with **virtual dollar** allocations, **customer names**, **customer tiers** (Tier **0** = most strategic), and **dollar values** per vote line

If a cycle has only one list type, process what exists and note the gap only in your internal reasoning, not as a separate column unless you add an optional **Data Notes** column (default: **do not** add columns beyond the specified table).

---

## Grounding and quality rules (mandatory)

- **DO** use only information from the provided AVOC files and project index.  
- **DO** preserve original feature titles in an internal working set before normalization; the final table uses the **normalized** title.  
- **DO NOT** invent customers, tiers, dollar amounts, or cycles. If a field is missing, use **`—`** (em dash) or **`0`** for numeric aggregates as specified per column.  
- **DO NOT** merge two items if the **problem, primary user, or core capability** materially differs; keep them separate and flag ambiguity briefly in **Description** only if needed (one short clause).  
- For **Pre-Voting** rows with **no** votes: **Voting Customers** and dollar columns reflect **no votes** (empty/`0` as appropriate); the row still counts toward **Occurrence** and **Recency** if the same normalized feature appears there.

---

## STEP 1 — EXTRACT (every Pre-Voting and Post-Voting list)

For **each raw feature request row**, capture a working record with:

| Field | Rule |
|--------|------|
| **Feature title (as written)** | Exact string from the source row |
| **Release cycle** | One of the eight canonical cycles |
| **List type** | `Pre-Voting` or `Post-Voting` |
| **Voting customers** | From Post-Voting only: **name**, **tier**, **dollar value** for that line. Pre-Voting: leave empty. |
| **Total dollar allocation in that cycle (row-level)** | Post-Voting: sum of dollars on that feature row for that cycle if multiple vote lines exist; else the single value. Pre-Voting: `0`. |

Think step by step while extracting: confirm cycle name, list type, and that dollar figures belong to the same feature row before recording.

---

## STEP 2 — NORMALIZE (merge across cycles)

1. **Cluster** features that are the **same or clearly overlapping** intent across cycles, even if **wording differs**.  
2. For each cluster, produce **one** consolidated entry with:
   - **Normalized Feature Title** — the clearest, most descriptive PM-style name (not marketing fluff).  
   - **Description (1–2 sentences)** — user-visible capability, scope, and key constraint if known from sources.  
   - **Problem statement** — synthesize from source text where present; if absent, infer **only** from explicit request language (no new facts).  
   - **Business benefits** — synthesize from source text; if absent, write **one** cautious benefit tied to stated request (no invented ROI).  
   - **Theme** — high-level area (e.g., Contracting, Procurement, Supplier, Analytics, Platform, Integrations).  
   - **Sub-category** — module or workflow under the theme.  
   - **Classification** — one primary type, e.g. **Usability | Performance | Accessibility | Compliance | Integration | Configuration | Workflow | Data / Reporting | Feature Completeness | Reliability** (use closest fit; one label unless sources clearly span two — then pick the **dominant** one).

   These fields feed the **main table** (title + description) and the **detail sheet** described in STEP 5 — they do **not** add columns to the 10-column stakeholder table unless you explicitly extend the workbook per optional note there.

**Merge bar:** Merge when a reasonable PM would say “same backlog item.” If unsure, **do not** merge.

---

## STEP 3 — CALCULATE SCORES AND ROLLUPS

For each **normalized** feature:

1. **Occurrence score** — distinct canonical cycles represented in the cluster (1–8).  
2. **Recency score** — from the **newest** cycle in the cluster, using the reference table (3–10).  
3. **Voting customers (unique across all cycles)** — de-duplicate by **customer name**; if the same name appears with different tiers in different cycles, keep the **highest strategic tier** (lowest tier **number** = more strategic, e.g. Tier 0 beats Tier 1) and **sum** dollars **only** when the source rows are clearly the same customer voting in different cycles on the same normalized feature; otherwise list separate lines in the cell as `Name (Tier X, $Y); …` per your tool’s cell conventions.  
4. **Tier 0 customers** — unique names that appear as Tier 0 at least once for this normalized feature.  
5. **Total Virtual Dollars Allocated** — **sum** of all **Post-Voting** dollar values across all cycles and rows mapped to this normalized feature.  
6. **Tier 0 Dollar Allocation** — sum of dollars **only** from vote lines where tier is **Tier 0** (or equivalent label meaning most strategic).

---

## STEP 4 — PRIORITY SIGNAL

Assign **Priority Signal** per normalized feature:

| Level | Rule |
|--------|------|
| **High** | **Any** Tier 0 dollar allocation **> 0**, **OR** the feature is in the **top 20%** by **Total Virtual Dollars Allocated** (round up: e.g. 47 rows → top 10). Ties at the cutoff: include **all** tied rows in High. |
| **Low** | **Neither** High nor Medium — typically **zero** dollars and **no** Tier 0 participation. |
| **Medium** | Everyone else with dollars **> 0** who is not High. |

If **all** totals are `0`, rank by **Occurrence** then **Recency** for Medium/Low split is **not** required — set **Low** for all unless your stakeholder rule says otherwise; in that case state the rule once in a single line under the table.

---

## STEP 5 — OUTPUT TABLE (exact columns, sort order)

Produce **one** master table, sorted by **Total Virtual Dollars Allocated** (descending). Use **exactly** these column headers **in this order** (no extras in this sheet):

1. **Normalized Feature Title**  
2. **Description (1–2 sentences)**  
3. **Release Cycles Appeared In** — comma-separated, **newest → oldest** (Juniper first)  
4. **Occurrence Score (1–8)**  
5. **Recency Score (3–10)**  
6. **Voting Customers (all unique across all cycles)** — include name, tier, and dollars in a compact, Excel-friendly format  
7. **Tier 0 Customers**  
8. **Total Virtual Dollars Allocated**  
9. **Tier 0 Dollar Allocation**  
10. **Priority Signal** — `High` | `Medium` | `Low`  
    - **High** = Tier 0 votes present **or** top 20% by total dollars (see STEP 4).  
    - **Medium** = mid-range per STEP 4.  
    - **Low** = bottom tier per STEP 4.

**Excel / file delivery:**  
- Write **`AVOC_Consolidated.xlsx`** to `[OUTPUT_FOLDER_PATH]`.  
- **Sheet 1 — `Consolidated`:** the 10-column table above; **freeze** header row; **auto-filter** on.  
- **Sheet 2 — `Normalized_Detail`:** one row per normalized feature, keyed by **Normalized Feature Title**, with columns: **Problem Statement | Business Benefits | Theme | Sub-category | Classification** (captures STEP 2 without altering the stakeholder column set).  
- Number formats: dollars as **currency** or **number with 2 decimals**; scores as integers.

**Optional stakeholder extension:** If the audience wants a **single** flat sheet, append **Theme | Sub-category | Classification** as columns **11–13** on `Consolidated` only when explicitly requested — still sort by column **8** (Total Virtual Dollars).

---

## Self-check before you respond

Verify:

1. Every normalized row’s **dollar totals** equal the sum of mapped Post-Voting lines (within rounding you applied consistently).  
2. **Occurrence** and **Recency** match the canonical cycle list and definitions.  
3. **Priority Signal** follows the High / Medium / Low rules, including **top 20%** tie handling.  
4. **No invented** customers, tiers, or dollars.  
5. The workbook is saved under **`[OUTPUT_FOLDER_PATH]`** as **`AVOC_Consolidated.xlsx`**, with **`Consolidated`** (10 columns) and **`Normalized_Detail`** sheets populated.

---

## What changed from a minimal AVOC prompt (for the author)

- **Role + goal** → Anchors S2P + virtual-dollar context and traceability expectations.  
- **Release/recency table** → Removes ambiguity on ordering and score mapping.  
- **Pre vs Post rules** → Clarifies empty votes and zero dollars for pre-voting-only rows.  
- **Normalization merge bar** → Reduces over-merging; aligns with PM judgment.  
- **Deduping tiers/customers** → Handles cross-cycle conflicts explicitly.  
- **Priority Signal** → Defines top 20% and tie behavior.  
- **Grounding + self-check** → Cuts hallucinated VoC data and arithmetic drift.  
- **Excel fallback** → Keeps deliverable possible in text-only environments.

---

*End of prompt.*

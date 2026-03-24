# Master Gaps — Competitor & Cross-Product (iContract)

**Document:** Prompt for Master GAP Sheet  
**Version:** 2  
**Product scope:** iContract (baseline), common platform products, co-dependent products  
**Knowledge root:** `/Users/sumit.begwani/KB Folder/knowledge-mining-poc`

---

## Your role

You are a **senior product strategist and technical analyst** specializing in enterprise **contract lifecycle management (CLM)** and **Source-to-Pay**, with hands-on experience benchmarking products against **analyst frameworks** (Gartner, Forrester, etc.) and **competitive feature sets**. You write for executives and roadmap owners: every claim must be **evidenced**, not assumed.

## Your goal

Produce **one normalized Master GAP Sheet** that combines:

1. **Track 1 — Industry / competitor benchmark gaps** (what mature CLM and adjacent markets expect).
2. **Track 2A — Cross-product gaps** (reuse from common platform products; inbound/outbound with co-dependent products).
3. **Track 2B — Incomplete features** (started in iContract but not end-to-end).

**Success criteria:** The final table is sortable, audit-ready, and each row could be defended in a review — **evidence cited**, **classifications consistent**, **no fabricated capabilities**.

## Global rules (mandatory)

- Read **every** section before executing. Do **not** skip steps.
- **Web search is enabled** — use it systematically for Track 1 and for competitor/feature facts you cannot ground in the repo.
- **Do not infer, assume, or fabricate** capabilities or gaps. If you cannot evidence a gap, **omit it**.
- **Evidence protocol:** For every gap that appears in the final sheet, you must be able to point to at least one of:
  - **KB/Code:** file path or doc path under the indexed workspaces (e.g. `knowledge-mining-poc/...`, product repo paths), **or**
  - **Web:** named source (publisher + page title or report name) tied to the industry/competitor claim.
- **Internal artifacts:** Pre-work summaries and long capability lists from Step 1A are **internal only** — do not paste them in full in the final answer; use them to build the table.
- **Reconciliation:** If industry research suggests a capability exists but the codebase shows something partial, classify as **PARTIAL**, not **ABSENT**, and align **Codebase Completion %** with what is actually implemented.

## Indexed context

The following are indexed in this project:

- Codebase and knowledgebase for **iContract**
- **Common platform products** (non-exhaustive): CWF, CMD/iMaster, Flexiform, CRMS, LMT, FL, FH, TMS, zDoc/iConsole, dewdrops, Smart Admin, linked-entity, appxtend, etc.
- **Co-dependent consumer-facing products** (non-exhaustive): eProc, eInvoice, iSource, iRequest, iSupplier, iManage, iRisk, iSave, iCost, etc.

All product knowledgebases live under: `/Users/sumit.begwani/KB Folder/knowledge-mining-poc`

---

═══════════════════════════════════════════════════════════════  
PRE-WORK — UNDERSTAND THE PRODUCT BEFORE IDENTIFYING GAPS  
═══════════════════════════════════════════════════════════════  

Before identifying gaps, establish a **baseline** of what iContract does today.

### STEP PW1 — SUMMARIZE iContract (internal only)

Read the codebase and knowledgebase for iContract. Produce an **internal** structured summary (do not output this verbatim):

a. **Product category and sub-category** (e.g. Source-to-Pay > Contract Management)  
b. **Functional areas** — for each:

- Name  
- Description (what it does)  
- Key sub-features/modules (**concrete capabilities**, not menu labels only)  
- **Implementation depth:** `Basic` | `Intermediate` | `Advanced`  
  - **Basic** — foundational, limited configuration  
  - **Intermediate** — core workflows work; notable edge cases missing  
  - **Advanced** — full-featured, configurable, complex scenarios  

c. **User personas** and their **primary workflows**  
d. **Integrations** (internal and external)  
e. **Partially implemented** items — present in code/KB but **not** functionally complete end-to-end (flag explicitly)

### STEP PW2 — CLASSIFY THE PRODUCT (internal only)

From PW1, derive:

- Precise **category / sub-categories** for search strings  
- **Top direct competitors** (include but do not limit to): iCertis, Agiloft, Ironclad, Malbek, Docusign CLM, Sirion Labs, ContractPodAI, Coupa, Conga, etc.  
- **3–4 analyst or industry frameworks** relevant to this category (include but do not limit to): Gartner (e.g. MQ critical capabilities), Forrester, IDC, Spend Matters, MGI Research, QKS Group, APQC, Hackett, etc.

Use PW1–PW2 as the **single baseline** for all mapping steps below.

---

═══════════════════════════════════════════════════════════════  
TRACK 1 — FEATURE GAPS VS INDUSTRY STANDARDS  
═══════════════════════════════════════════════════════════════  

Identify capabilities that are **standard or expected** in mature products in this category but are **missing or underdeveloped** in iContract.

### STEP 1A — INDUSTRY CAPABILITY LONG LIST (web search required)

Run **systematic** web searches. Adapt `[Product Category]` to your PW2 labels (e.g. "contract lifecycle management", "CLM"). Use the **current calendar year** in queries where it helps recency.

Minimum query pattern set (add variants as needed):

1. `"[Product Category] software must-have features [year]"`  
2. `"Gartner [Product Category] critical capabilities"`  
3. `"Forrester [Product Category] evaluation criteria"`  
4. `"MGI Research [Product Category] evaluation criteria"`  
5. `"[Competitor N] features"` / product pages for **top 8** competitors from PW2  
6. `"G2 [Product Category] top features"` and `"Capterra [Product Category] features comparison"`  
7. `"[Framework name] [Product Category] process requirements"`  

**Extract** every **distinct** capability mentioned across results. Build an **internal comprehensive list** (do not dump the full list in the final output).

**Quality bar:** Prefer **over-inclusive** in 1A; you will filter in 1B. Missing a major industry theme is worse than listing a redundant capability.

### STEP 1B — MAP EACH INDUSTRY CAPABILITY TO iContract

For each capability from 1A, compare to **PW1**.

Classify **exactly one**:

| Label | Meaning |
|--------|--------|
| **PRESENT** | Fully supported **today**; evidence **only** from iContract codebase/KB — not from assumptions. |
| **PARTIAL** | Some implementation; incomplete scope, weak edge cases, or missing sub-features. State **what exists** vs **what is missing**. |
| **ABSENT** | **No** evidence in iContract codebase/KB that the capability exists in any meaningful form. |

**Carry forward only PARTIAL and ABSENT** as gaps. **Drop PRESENT** from gap lists.

### STEP 1C — DETAIL EACH TRACK 1 GAP

For each PARTIAL/ABSENT gap, capture:

- What the **industry or competitor** implementation looks like (**concrete**, not generic)  
- What is **missing or incomplete** in iContract  
- **Which competitors** show it and **maturity** (where discernible from sources)  
- **Personas** (from PW1) and **how** they are impacted  
- **Business consequence** (deals, friction, compliance, competitive loss, etc.)

### STEP 1D — THEME, SUB-CATEGORY, CLASSIFICATION

For each Track 1 gap:

- **Theme** — high-level domain (e.g. Reporting & Analytics, Workflow Automation, Supplier Management)  
- **Sub-category** — specific area under the theme (e.g. Real-time Dashboards)  
- **Gap classification (exactly one for Track 1 primary tag):**  
  - `INDUSTRY STANDARD GAP — ABSENT`  
  - `INDUSTRY STANDARD GAP — PARTIAL` — include **completion %** as an **integer** (expected vs delivered)

---

═══════════════════════════════════════════════════════════════  
TRACK 2 — COMMON PRODUCTS, CO-DEPENDENT PRODUCTS, INCOMPLETE FEATURES  
═══════════════════════════════════════════════════════════════  

Three parallel sub-tracks:

- **2A** Cross-product adoption (common platform **and** co-dependent inbound/outbound)  
- **2B** Incomplete features **inside** iContract  

---

### TRACK 2A — CROSS-PRODUCT & CO-DEPENDENT GAPS

#### STEP 2A1 — COMMON PLATFORM PRODUCTS (internal summaries)

For each **available** common platform product (CWF, CMD/iMaster, Flexiform, CRMS, LMT, FL, FH, zDoc/iConsole, TMS, dewdrops, Smart Admin, linked-entity, appxtend, etc.), build an **internal** summary:

- Purpose / problem solved  
- Functional areas and **key** capabilities  
- Themes / sub-categories  
- Integrations exposed or consumed  

(Do not output full summaries.)

#### STEP 2A2 — GAPS FROM COMMON PLATFORM → iContract

A **CROSS-PRODUCT GAP** requires **all** of:

a. Capability **exists and works** in the common product (**codebase/KB evidence**)  
b. **Relevant** to iContract users (workflows/personas from PW1)  
c. **Not adopted** in iContract (no equivalent in iContract codebase/KB)  
d. **User-facing or workflow-level** — not pure internal plumbing with no user value  

**Do not** flag if: already equivalent in iContract; irrelevant to use cases; backend-only with no user impact.

For each confirmed gap, record:

- **Source product** name  
- **What it does** (specific)  
- **Why** it matters for iContract + **personas**  
- **Integration effort:** `High` | `Medium` | `Low` (same definitions as original prompt: architecture/re-engineering vs extension vs config/UI)

#### STEP 2A3 — CO-DEPENDENT PRODUCTS (internal summaries)

For each **available** co-dependent product (eProc, eInvoice, iSource, iRequest, iSupplier, iManage, iRisk, iSave, iCost, etc.), **internal** summary:

- Purpose and **who** uses it  
- Capabilities and themes  
- **Existing** touchpoints with iContract (data, APIs, events)  
- Integrations and **contract-adjacent** workflows (e.g. req-to-contract, contract-to-invoice)

#### STEP 2A4 — CO-DEPENDENT GAPS (inbound + outbound)

**Part A — Inbound** (iContract should **adopt** from co-dependent product):  
Same relevance filter as 2A2 (a–d), plus **strict** contract-management relevance — exclude peripheral features.

**Part B — Outbound** (iContract should **expose** to co-dependent product):  
Flag only if **all** of:

a. Co-dependent workflow **logically depends** on contract data, status, or events  
b. iContract **does not** publish/expose/push it (**no** evidence in either codebase/KB)  
c. Absence causes **real** workflow break, manual workaround, or **data inconsistency**

For **every** 2A4 gap, document: source/recipient product, inbound vs outbound, specificity, personas, **workflow break** (especially outbound), integration effort.

#### STEP 2A5 — CLASSIFICATION TAGS FOR 2A

For **every** 2A gap:

- **Theme** and **Sub-category** (align with Track 1 where possible)  
- **Gap classification tags** (preserve origin):  
  - Common platform: `CROSS-PRODUCT GAP — [SOURCE PRODUCT]` (e.g. `CROSS-PRODUCT GAP — CMD`)  
  - Co-dependent inbound: `CO-DEPENDENT GAP — [SOURCE PRODUCT]`  
  - Co-dependent outbound: `CO-DEPENDENT INTEGRATION GAP — [TARGET PRODUCT]`  

Multiple tags allowed if multiple sources/products apply.

---

### TRACK 2B — INCOMPLETE FEATURE GAPS (iContract only)

#### STEP 2B1 — FIND INCOMPLETE FEATURES

Evidence may include: orphaned modules; dead config; KB marked beta/planned/limited; workflows without close path; weak edge cases; undocumented or unexposed APIs; UI behind flags or non-functional.

For each item:

- **Intended scope**  
- **What works today**  
- **What is missing**  
- **Completion %** — single **integer** (no ranges)  
- **User impact**

#### STEP 2B2 — THEME + CLASSIFICATION

- **Theme**, **Sub-category**  
- **Gap classification:** `INCOMPLETE FEATURE — [SHORT FEATURE NAME]`  
- **Completion %** integer (must match row column 13 logic)

---

═══════════════════════════════════════════════════════════════  
STEP 3 — NORMALIZE INTO ONE MASTER GAP SHEET  
═══════════════════════════════════════════════════════════════  

You have **four** raw inputs:

1. Track 1 — industry PARTIAL + ABSENT  
2. Track 2A — common platform cross-product  
3. Track 2A — co-dependent inbound + outbound  
4. Track 2B — incomplete features  

**Merge rule:** Merge when the **same underlying missing capability** is described across tracks. When merging, **retain all** classification tags and **all** source tracks (e.g. a row can be both `INDUSTRY STANDARD GAP — ABSENT` and `CROSS-PRODUCT GAP — CMD`).

**Never merge:** Inbound vs outbound co-dependent gaps — **always separate rows**, even for the same product pair.

**Merge decision tree (apply in order):**

1. Same **user-visible outcome** and same **missing capability**? → **Merge** (carry all tags).  
2. Same theme but **different** missing sub-capability or **different** primary persona? → **Keep separate**.  
3. Unsure? → **Keep separate**; explain briefly in **Normalization Notes**.

**Before finalizing:** Think step-by-step through **each** proposed merge: *Would a PM lose important actionability if these became one row?* If yes, keep separate.

---

═══════════════════════════════════════════════════════════════  
STEP 4 — OUTPUT: MASTER GAP SHEET  
═══════════════════════════════════════════════════════════════  

Deliver:

1. A **short executive summary** (3–6 sentences): total gap count by **Priority Signal**, and **explicit** statement if any sub-track produced **zero** gaps.  
2. **One** markdown table — **one row per normalized gap**, columns in **this exact order**:

| # | Column | Guidance |
|---|--------|----------|
| 1 | **Normalized Gap Title** | ≤ **10 words** |
| 2 | **Description** | **2–3 sentences** — gap today + value when closed |
| 3 | **Theme** | Domain label |
| 4 | **Sub-category** | Finer-grained label |
| 5 | **Gap Classification** | Comma-separated if multiple. Use **full** strings including product names. For incomplete features use **`INCOMPLETE FEATURE — [FEATURE NAME]`** (not bare `INCOMPLETE FEATURE`). Allowed tokens: `INDUSTRY STANDARD GAP — ABSENT`, `INDUSTRY STANDARD GAP — PARTIAL`, `CROSS-PRODUCT GAP — [SOURCE]`, `CO-DEPENDENT GAP — [SOURCE]`, `CO-DEPENDENT INTEGRATION GAP — [TARGET]`, `INCOMPLETE FEATURE — [FEATURE NAME]` |
| 6 | **Source Track(s)** | `Track 1`, `Track 2A`, `Track 2B` — comma-separated if merged |
| 7 | **Industry Benchmark** | Track 1 / merged-with-Track-1 only: **named** competitor **or** standard + **brief** implementation note. Else blank. |
| 8 | **Common Product Source** | Only when `CROSS-PRODUCT GAP — …` applies; else blank. |
| 9 | **Co-Dependent Product Reference** | Only for co-dependent tags; else blank. |
| 10 | **Gap Direction** | For **co-dependent** Track 2A rows only: `Inbound` / `Outbound` / `Bidirectional`. Blank for Track 1, common-only cross-product, Track 2B. |
| 11 | **What Exists Today** | Concrete modules/features — or `Nothing` |
| 12 | **What Is Missing** | Concrete missing work |
| 13 | **Codebase Completion %** | **Integer** 0–99 (100% = not a gap). Track-specific rules unchanged: ABSENT/ no adoption = **0%**; PARTIAL/ incomplete / partial adoption = your assessed integer |
| 14 | **Personas Affected** | **Only** personas from **PW1** |
| 15 | **Business Impact of Gap** | **1–2 sentences** |
| 16 | **Integration Effort** | **Track 2A only**: High/Medium/Low; blank for Track 1 and 2B |
| 17 | **Occurrence Score** | Leave blank (Phase 3) |
| 18 | **Recency Score** | Leave blank (Phase 3) |
| 19 | **Priority Signal** | `High` / `Medium` / `Low` — **first matching rule wins** (see below) |
| 20 | **Normalization Notes** | Only when merge uncertain, conflicting cross-track labels, or related inbound/outbound kept separate; else blank |

### Priority Signal (first match wins)

- **HIGH:** Includes `INDUSTRY STANDARD GAP — ABSENT`; **or** confirmed in **both** Track 1 and Track 2A; **or** `INCOMPLETE FEATURE — …` with completion **≤ 25%** and user-facing; **or** business impact cites **deal loss, compliance, or churn**; **or** outbound `CO-DEPENDENT INTEGRATION GAP — …` **breaks** end-to-end workflow in target product.  
- **MEDIUM:** `INDUSTRY STANDARD GAP — PARTIAL`; **or** single-track cross-product with Medium/Low effort; **or** inbound co-dependent with clear persona benefit and Medium/Low effort; **or** incomplete feature **26–74%**.  
- **LOW:** Single-track cross-product or co-dependent with **High** effort; **or** incomplete feature **≥ 75%**; **or** niche persona impact.

### Sorting

1. **Priority Signal** — High → Medium → Low  
2. **Gap Classification** — INDUSTRY ABSENT → INDUSTRY PARTIAL → CROSS-PRODUCT → CO-DEPENDENT → CO-DEPENDENT INTEGRATION → INCOMPLETE FEATURE  
3. **Theme** — alphabetical  

### Example row (format and tone only — do not treat as real data)

| Normalized Gap Title | Description | Theme | Sub-category | Gap Classification | … |
|----------------------|-------------|-------|--------------|----------------------|---|
| Real-time obligation dashboard | iContract does not offer a live portfolio view of obligations and milestones. A full solution would surface upcoming obligations by owner and severity. | Reporting & Analytics | Operational dashboards | INDUSTRY STANDARD GAP — ABSENT | … |

*(Ellipsis: remaining columns filled per rules above.)*

### Spreadsheet export

- Primary deliverable: the **markdown table** above (Excel-friendly).  
- **Additionally**, if your environment can create files: write **`Feature_Gaps_Consolidated.xlsx`** (or **`Feature_Gaps_Consolidated.csv`** if xlsx is not available) to the **designated output folder** specified by the user or your run configuration. If no folder is specified, output the table only and state that the file was not written for lack of path.

---

═══════════════════════════════════════════════════════════════  
FINAL CHECKS (self-verify before sending)  
═══════════════════════════════════════════════════════════════  

- [ ] Every row has **evidence** (KB/code path **or** named web source for industry/competitor claims).  
- [ ] **ABSENT** never contradicts iContract code/KB evidence; contradictions → **PARTIAL** + revised %.  
- [ ] **Codebase Completion %** is a **single integer** on every row — no ranges, no blanks for classified gaps.  
- [ ] Every `CROSS-PRODUCT GAP — …` names a **specific** common product (never "common products").  
- [ ] Every co-dependent tag has **Co-Dependent Product Reference** populated.  
- [ ] Every **outbound** integration gap states the **workflow break** or workaround.  
- [ ] Every industry-standard row has **Industry Benchmark** (column 7).  
- [ ] No **PRESENT** capabilities appear as gaps.  
- [ ] **Personas** only from PW1.  
- [ ] Coverage note: at least one row from each of **Track 1**, **2A common**, **2A co-dependent inbound**, **2A co-dependent outbound**, **2B** — **or** explicitly state **zero gaps** for that sub-track in the executive summary.  
- [ ] Merged rows retain **all** classifications and **all** source tracks.  
- [ ] Inbound and outbound co-dependent gaps are **never** merged together.

---

**End of prompt (v2)**

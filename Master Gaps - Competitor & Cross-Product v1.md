# Master Gaps — Competitor & Cross-Product (iContract)

**Document:** Prompt for Master GAP Sheet · **Version:** 1 · **Note:** Baseline archive; identical substance to former `iContract-Master-GAP-Sheet-Prompt.md`.

---

## iContract Master GAP Sheet — Product Capability Gap Analysis Prompt

You are a senior product strategist and technical analyst. Your task is to identify all product capability gaps for iContract through two parallel research tracks — industry standards and cross-product analysis — and then normalize both into a single Master GAP Sheet.

Read every instruction carefully before starting. Do not skip any section or step. Do not infer, assume, or fabricate capabilities. Every gap you identify must be evidenced either by what you find in the codebase/knowledgebase, what you find via web research, or what you find in the common product codebases and co-dependent product codebases. If you cannot evidence a gap, do not include it.

Web search is enabled. Use it actively throughout this prompt.

The following are indexed in this project:
- Codebase and knowledgebase for iContract
- Codebases and knowledgebases for common platform products like:
  CWF, CMD/iMaster, Flexiform, CRMS, LMT, FL, FH, TMS, zDoc/iConsole, dewdrops, Smart Admin, linked-entity, appxtend etc.
- Codebases and knowledgebases for other co-dependent consumer-facing products like:
  eProc, eInvoice, iSource, iRequest, iSupplier, iManage, iRisk, iSave, iCost etc.

All the knowledgebase for all products can be found in the folder: /Users/sumit.begwani/KB Folder/knowledge-mining-poc

═══════════════════════════════════════════════════════════════
PRE-WORK — UNDERSTAND YOUR PRODUCT BEFORE IDENTIFYING GAPS
═══════════════════════════════════════════════════════════════
Before identifying any gaps, you must thoroughly understand what the product currently does. Do this first and use it as the baseline for all gap analysis.

STEP PW1 — SUMMARIZE THE PRODUCT:
Read the codebase and knowledgebase for iContract in full.
Produce an internal structured summary (do not output this — use it internally):

  a. Product Category and Sub-category
     (e.g., Source-to-Pay > Contract Management)
  b. All Functional Areas currently present in the product
     For each functional area:
       - Name
       - Description (what it does)
       - Key sub-features and modules present (be specific — list actual capabilities, not just menu names)
       - Implementation depth: [Basic / Intermediate / Advanced]
         Basic    = foundational capability present, limited configuration
         Intermediate = core workflows complete, some edge cases missing
         Advanced = full-featured, configurable, handles complex scenarios
  c. User Personas who interact with the product and their primary workflows
  d. Integrations currently present (internal and external)
  e. Any features that appear partially implemented — present in codebase but not functionally complete end-to-end (flag these explicitly)

STEP PW2 — CLASSIFY THE PRODUCT:
Based on the above, identify:
  - The precise product category and sub-categories
  - Top direct competitors including, but not limited to: iCertis, Agiloft, Ironclad, Malbek, Docusign CLM, Sirion Labs, ContractPodAI, Coupa, Conga etc.
  - Top 3–4 industry analyst frameworks or standards applicable to this
    product category including, but not limited to: Gartner and its Magic Quadrant criteria, Forrester, IDC (International Data Corporation), Spend Matters, MGI Research, QKS Group, APQC Process, Hackett benchmarks etc).

Use this pre-work as your baseline for all gap identification below.

═══════════════════════════════════════════════════════════════
TRACK 1 — FEATURE GAPS AGAINST INDUSTRY STANDARDS
═══════════════════════════════════════════════════════════════
Identify capabilities that are considered standard or expected in mature
products in this category but are missing or underdeveloped in iContract.

STEP 1A — IDENTIFY TOP INDUSTRY CAPABILITIES (web search required):
Search the web systematically for each of the following:
  1. "[Product Category] software must-have features [current year]"
  2. "Gartner [Product Category] critical capabilities"
  3. "Forrester [Product Category] evaluation criteria"
  4. "MGI Research [Product Category] evaluation criteria"
  5. "[Competitor 1] features list" for each of your top 8 competitors
  6. "G2 [Product Category] top features" and "Capterra [Product Category]
     features comparison"
  7. "[Industry standard/framework] [Product Category] process requirements"

For each search, extract every distinct capability mentioned.
Build an internal comprehensive list of ALL industry-standard capabilities
for this product category. Do not output this list — use it internally.

IMPORTANT: Be exhaustive. Cast a wide net. It is better to identify too many
capabilities at this stage and filter in Step 1B than to miss something important.

STEP 1B — MAP EACH INDUSTRY CAPABILITY AGAINST THE PRODUCT:
For each industry-standard capability identified in Step 1A, compare it
against your pre-work product summary (Step PW1).

Classify each capability as ONE of:
  PRESENT:     The product fully supports this capability today.
               Evidence must come from the codebase or knowledgebase.
               Do not mark as Present based on assumption.
  PARTIAL:     The product has some implementation of this capability but
               it is incomplete, limited in scope, or missing key sub-features.
               Document specifically what is present and what is missing.
  ABSENT:      No evidence of this capability exists in the codebase or
               knowledgebase. The product does not support this at all today.

Only carry PARTIAL and ABSENT classifications forward as GAPs.
Silently discard PRESENT capabilities — do not list them in the output.

STEP 1C — DETAIL EACH GAP:
For each PARTIAL or ABSENT capability, document:
  - What the industry standard or competitor implementation looks like
    (specific detail — not vague descriptions)
  - What specifically is missing or incomplete in iContract
  - Which competitors have this capability and how mature their implementation is
  - Which user persona(s) are impacted and how
  - The business consequence of this gap (lost deals, customer friction,
    competitive disadvantage, compliance risk, etc.)

STEP 1D — ASSIGN CLASSIFICATION AND THEME:
For each Track 1 gap, assign:

  Theme: The high-level functional domain this gap belongs to
    (e.g., "Reporting & Analytics", "Workflow Automation", "Supplier Management")

  Sub-category: The specific capability area within the theme
    (e.g., within "Reporting & Analytics" → "Real-time Dashboards")

  Gap Classification: ONE of the following:
    INDUSTRY STANDARD GAP — ABSENT:
      Capability is fully missing. No implementation exists in codebase.
    INDUSTRY STANDARD GAP — PARTIAL:
      Capability exists but is incomplete. Document completion % as an
      absolute integer based on what is present vs. what is expected.

═══════════════════════════════════════════════════════════════
TRACK 2 — FEATURE GAPS AGAINST COMMON PRODUCTS, CO-DEPENDENT PRODUCTS & INCOMPLETE FEATURES
═══════════════════════════════════════════════════════════════
This track has three sub-tracks running in parallel:

  TRACK 2A: Cross-product adoption gaps —
    Capabilities that exist in common platform products OR co-dependent consumer-facing products but have not been adopted in iContract. This includes both:
      (a) capabilities iContract should adopt FROM other products, AND
      (b) capabilities iContract should be exposing TO co-dependent products but currently does not (outbound integration gaps)

  TRACK 2B: Incomplete feature gaps —
    Capabilities that were started in iContract but are only
    partially complete within the product itself

--- TRACK 2A: CROSS-PRODUCT AND CO-DEPENDENT PRODUCT GAPS ---

STEP 2A1 — SUMMARIZE EACH COMMON PLATFORM PRODUCT:
Read the codebase and knowledgebase for each of the following common platform products as available:
  CWF, CMD/iMaster, Flexiform, CRMS, LMT, FL, FH, zDoc/iConsole, TMS, dewdrops, Smart Admin, linked-entity, appxtend etc.

For each common platform product, build an internal structured summary:
  - Product purpose (what problem does it solve)
  - All functional areas and key capabilities present
  - Themes and sub-categories of its functionality
  - Integrations it exposes or supports

Do not output these summaries — use them internally for comparison.

STEP 2A2 — IDENTIFY RELEVANT CAPABILITIES FROM COMMON PLATFORM PRODUCTS:
For each common platform product, compare its capabilities against iContract.

A capability from a common platform product is a CROSS-PRODUCT GAP if ALL of the following are true:
  a. The capability exists and is functional in the common platform product (evidenced in its codebase or knowledgebase)
  b. The capability is RELEVANT to iContract — it would add value to the users of iContract based on their workflows and personas
  c. The capability has NOT been adopted in iContract (no evidence in its codebase or knowledgebase)
  d. The capability is not a pure infrastructure or internal technical concern — it must represent user-facing or workflow-level functionality

Do NOT flag a capability as a gap if:
  - It is already present in iContract in equivalent form
  - It is irrelevant to the product's user base or use cases
  - It is a backend technical component with no user-facing value

For each confirmed gap from common platform products, document:
  - Which common platform product has this capability
  - What the capability does (specific, not vague)
  - Why it is relevant to iContract and which personas would benefit
  - Estimated integration effort [High / Medium / Low]:
      High   = requires new architecture, significant re-engineering, or deep data model changes
      Medium = extension of existing modules, moderate API integration work
      Low    = configuration change, UI addition, or shallow integration

STEP 2A3 — SUMMARIZE EACH CO-DEPENDENT CONSUMER-FACING PRODUCT:
Read the codebase and knowledgebase for each of the following co-dependent consumer-facing products as available:
  eProc, eInvoice, iSource, iRequest, iSupplier, iManage, iRisk, iSave, iCost etc.

For each co-dependent product, build an internal structured summary:
  - Product purpose (what problem does it solve and who uses it)
  - All functional areas and key capabilities present
  - Themes and sub-categories of its functionality
  - Any existing touchpoints, data flows, or integration points it has with iContract today
  - Integrations it exposes or supports (APIs, events, shared data objects)
  - User-facing workflows and features that could logically extend or integrate with contract lifecycle use cases (e.g., requisition-to-contract, contract-to-invoice, supplier-to-contract)

Do not output these summaries — use them internally for comparison.

STEP 2A4 — IDENTIFY RELEVANT CAPABILITY GAPS FROM CO-DEPENDENT PRODUCTS:
For each co-dependent consumer-facing product, perform two parallel analyses against iContract:

**Part A — Inbound gaps (capabilities iContract should adopt FROM co-dependent products):**
For each co-dependent product, identify capabilities that iContract should adopt. Apply the same relevance filter as Step 2A2:
  a. The capability exists and is functional in the co-dependent product (evidenced in its codebase or knowledgebase)
  b. The capability is RELEVANT to iContract — it would add value to iContract's users based on their contract-related workflows and personas
  c. The capability has NOT been adopted in iContract (no evidence in its codebase or knowledgebase)
  d. The capability is user-facing or workflow-level — not a pure backend technical concern

Apply a strict relevance filter: only include capabilities where there is a direct and meaningful connection to contract management workflows. Do not include capabilities that are peripheral to iContract's core purpose.

**Part B — Outbound integration gaps (capabilities iContract should expose TO co-dependent products):**
For each co-dependent product, identify contract-related data, events, or workflow triggers that the co-dependent product clearly needs from iContract but that iContract does not currently expose. A gap here exists when:
  a. The co-dependent product has a workflow or feature that is logically dependent on contract data, contract status, or contract events
  b. iContract does not currently publish, expose, or push this data/event to the co-dependent product (no evidence of integration in either codebase or knowledgebase)
  c. The absence of this integration causes a real workflow break, manual workaround, or data inconsistency for users of the co-dependent product

For each confirmed gap from co-dependent products (both Part A and Part B), document:
  - Which co-dependent product is the source or recipient
  - Whether this is an inbound gap (iContract should adopt) or outbound gap (iContract should expose)
  - What the capability or integration does (specific, not vague)
  - Why it is relevant to iContract and/or the co-dependent product, and which personas would benefit or be impacted
  - The workflow break or manual workaround that results from this gap today (especially for outbound gaps)
  - Estimated integration effort [High / Medium / Low] using the same definition as Step 2A2

STEP 2A5 — ASSIGN CLASSIFICATION AND THEME FOR ALL TRACK 2A GAPS:
For EVERY gap identified across Steps 2A2 and 2A4 (both inbound and outbound co-dependent gaps), assign:

  Theme: The high-level functional domain this gap belongs to (use the same framework as Track 1 where possible for consistency)

  Sub-category: The specific capability area within the theme

  Gap Classification: Use SEPARATE tags to preserve the origin of each gap:
    For common platform product gaps:
      CROSS-PRODUCT GAP — [SOURCE PRODUCT NAME]
      (e.g., "CROSS-PRODUCT GAP — CMD")
    For co-dependent product gaps (inbound):
      CO-DEPENDENT GAP — [SOURCE PRODUCT NAME]
      (e.g., "CO-DEPENDENT GAP — ePROC")
    For co-dependent product gaps (outbound):
      CO-DEPENDENT INTEGRATION GAP — [TARGET PRODUCT NAME]
      (e.g., "CO-DEPENDENT INTEGRATION GAP — eINVOICE")

  A gap may carry multiple classification tags if it was identified from more than one source or applies to more than one co-dependent product.

--- TRACK 2B: INCOMPLETE FEATURE GAPS ---

STEP 2B1 — IDENTIFY INCOMPLETE FEATURES IN iContract:
Re-examine the codebase and knowledgebase of iContract specifically
looking for features that are partially implemented — where work has clearly
been started but the feature is not functionally complete end-to-end.

Evidence of an incomplete feature includes:
  - Code modules that exist but are not connected to a UI or workflow
  - Configuration options that are defined but not functional
  - Features documented in the knowledgebase as "coming soon", "beta",
    "limited", or "planned"
  - Workflows that start but have no completion path (e.g., can create
    a record but cannot approve, submit, or close it)
  - Features that work for simple scenarios but break or lack support for
    standard edge cases (e.g., single-currency support when multi-currency
    is expected)
  - API endpoints that exist in code but are not exposed or documented
  - UI components that are rendered but non-functional or hidden behind
    feature flags

For each incomplete feature identified, document:
  - What the feature was intended to do (full intended scope)
  - What is currently implemented and functional
  - What is missing or non-functional
  - Estimated completion percentage as an ABSOLUTE INTEGER
    (e.g., 40% — meaning 40% of the intended functionality is present)
    Base this on your assessment of: features present vs. features missing,
    workflows supported vs. workflows broken, and edge cases handled vs. not.
    Do not give ranges. Give one integer.
  - The user impact of the incomplete state

STEP 2B2 — ASSIGN CLASSIFICATION AND THEME FOR TRACK 2B:
For each incomplete feature gap assign:
  Theme, Sub-category
  Gap Classification: INCOMPLETE FEATURE — [FEATURE NAME]
  Completion %: [Absolute integer]

═══════════════════════════════════════════════════════════════
STEP 3 — NORMALIZE ALL GAPS INTO MASTER GAP SHEET
═══════════════════════════════════════════════════════════════
You now have four raw gap lists:
  - Track 1: Industry Standard Gaps (Absent + Partial)
  - Track 2A (common platform): Cross-Product Adoption Gaps
  - Track 2A (co-dependent): Co-Dependent Inbound Gaps and Co-Dependent Outbound Integration Gaps
  - Track 2B: Incomplete Feature Gaps

Combine all four and normalize into a single Master GAP Sheet.

NORMALIZATION RULES:

  MERGE two gaps if they describe the same underlying missing capability, even if they were identified through different tracks. For example:
    - A Track 1 gap and a Track 2A gap that both point to the same missing capability should be merged into one row.
    - When merging, retain ALL gap classifications (e.g., a merged gap can be both "INDUSTRY STANDARD GAP — ABSENT" and "CROSS-PRODUCT GAP — CMD" and "CO-DEPENDENT GAP — ePROC")

  KEEP SEPARATE if the gaps describe different capabilities, affect different personas, or merging would lose important specificity. In particular:
    - An inbound gap (iContract should adopt a capability) and an outbound gap (iContract should expose a capability) should always be kept separate, even if they relate to the same co-dependent product.

  If uncertain whether to merge, keep separate and note in "Normalization Notes" column.

═══════════════════════════════════════════════════════════════
STEP 4 — OUTPUT: MASTER GAP SHEET
═══════════════════════════════════════════════════════════════
Produce a single table with ONE ROW per normalized gap.
Columns in this exact order:

  1.  **Normalized Gap Title**
      (max 10 words — describes the missing or incomplete capability clearly)

  2.  **Description**
      (2–3 sentences — what is missing, what the product cannot do today, and what the complete capability would enable)

  3.  **Theme**
      (high-level functional domain, e.g., "Reporting & Analytics")

  4.  **Sub-category**
      (specific capability area within the theme, e.g., "Real-time Dashboards")

  5.  **Gap Classification**
      ONE or MORE of the following (comma-separated if multiple apply):
        INDUSTRY STANDARD GAP — ABSENT
        INDUSTRY STANDARD GAP — PARTIAL
        CROSS-PRODUCT GAP — [SOURCE PRODUCT NAME]
        CO-DEPENDENT GAP — [SOURCE PRODUCT NAME]
        CO-DEPENDENT INTEGRATION GAP — [TARGET PRODUCT NAME]
        INCOMPLETE FEATURE

  6.  **Source Track(s)**
      [Track 1 / Track 2A / Track 2B — comma-separated if multiple]

  7.  **Industry Benchmark**
      (Track 1 only — which competitor(s) or standard defines this as expected? Include competitor name and brief description of their implementation. Blank for Track 2A/2B-only gaps.)

  8.  **Common Product Source**
      (For CROSS-PRODUCT GAP rows only — which common platform product has this capability?
      e.g., "CMD — Supplier onboarding wizard with tier-based routing". Blank for all other gap types.)

  9.  **Co-Dependent Product Reference**
      (For CO-DEPENDENT GAP and CO-DEPENDENT INTEGRATION GAP rows only — which co-dependent product is the source or target, and what is the specific capability or integration at stake?
      e.g., "eProc — Contract-linked PO creation requires approved contract status from iContract". Blank for all other gap types.)

  10. **Gap Direction**
      (Track 2A co-dependent gaps only — one of: "Inbound" / "Outbound" / "Bidirectional". Blank for Track 1, common platform gaps, and Track 2B gaps.)

  11. **What Exists Today**
      (specific modules, functions, or partial implementations currently present in iContract. "Nothing" if fully absent.)

  12. **What Is Missing**
      (specific capabilities, workflows, or sub-features not yet built or not yet functional)

  13. **Codebase Completion %**
      (absolute integer — 0% if fully absent, 1–99% if partial, 100% would not appear here as it would be PRESENT)
      For Track 1 ABSENT gaps: 0%
      For Track 1 PARTIAL gaps: your assessed % based on Step 1B
      For Track 2B gaps: your assessed % based on Step 2B1
      For Track 2A gaps where product has zero adoption: 0%
      For Track 2A gaps where product has partial adoption: your assessed %

  14. **Personas Affected**
      (comma-separated list of personas from pre-work Step PW1 who are impacted by this gap)

  15. **Business Impact of Gap**
      (1–2 sentences — what is the consequence of this gap existing? e.g., deal loss, customer churn risk, compliance exposure, manual workaround burden, competitive disadvantage)

  16. **Integration Effort**
      (Track 2A only — [High / Medium / Low] per Step 2A2 definition. Blank for Track 1 and 2B gaps.)

  17. **Occurrence Score**
      (Leave blank — to be populated in Phase 3 when cross-referenced with customer sources)

  18. **Recency Score**
      (Leave blank — to be populated in Phase 3)

  19. **Priority Signal [High / Medium / Low]**
      Apply in order — first match wins:
      HIGH:   Gap Classification includes INDUSTRY STANDARD GAP — ABSENT
              OR gap appears in both Track 1 and Track 2A (double-confirmed)
              OR Codebase Completion % ≤ 25% for an INCOMPLETE FEATURE that is user-facing
              OR Business impact mentions deal loss, compliance, or churn
              OR Gap Classification is CO-DEPENDENT INTEGRATION GAP where the outbound absence causes a broken end-to-end workflow in a co-dependent product
      MEDIUM: Gap Classification is INDUSTRY STANDARD GAP — PARTIAL
              OR single-track Cross-Product Gap with Medium/Low effort
              OR CO-DEPENDENT GAP (inbound) with clear persona benefit and Medium/Low integration effort
              OR Incomplete Feature with Completion % between 26–74%
      LOW:    Single-track Cross-Product or Co-Dependent Gap with High integration effort
              OR Incomplete Feature with Completion % ≥ 75% (mostly done, minor work remaining)
              OR niche capability with limited persona impact

  20. **Normalization Notes**
      (only if merge was uncertain, a gap spans multiple tracks with conflicting classifications, or a gap combines inbound and outbound co-dependent signals that were kept separate; blank otherwise)

**SORTING:**
  Primary:   Priority Signal — High first, then Medium, then Low
  Secondary: Gap Classification — INDUSTRY STANDARD GAP — ABSENT first, then INDUSTRY STANDARD GAP — PARTIAL, then CROSS-PRODUCT GAP, then CO-DEPENDENT GAP, then CO-DEPENDENT INTEGRATION GAP, then INCOMPLETE FEATURE
  Tertiary:  Theme — alphabetical

═══════════════════════════════════════════════════════════════
FINAL CHECKS BEFORE OUTPUTTING
═══════════════════════════════════════════════════════════════
Before producing the final table, verify the following:

  ✓ Every gap has evidence — either from web research (Track 1) or from a common product codebase/KB (Track 2A common) or from a co-dependent product codebase/KB (Track 2A co-dependent) or from the product's own codebase/KB (Track 2B). No gaps based on assumption.

  ✓ No capability marked ABSENT has any evidence in the product codebase or knowledgebase. If evidence exists, it must be PARTIAL, not ABSENT.

  ✓ Codebase Completion % is an absolute integer for every row — not a range, not "approximately", not blank for classified gaps.

  ✓ Every CROSS-PRODUCT GAP — [SOURCE] has named a specific common platform product as the source. "Common products" is not sufficient.

  ✓ Every CO-DEPENDENT GAP or CO-DEPENDENT INTEGRATION GAP has named a specific co-dependent product and populated the "Co-Dependent Product Reference" column.

  ✓ Every CO-DEPENDENT INTEGRATION GAP (outbound) has documented the specific workflow break or manual workaround that results from the missing integration today.

  ✓ Every INDUSTRY STANDARD GAP has named at least one specific competitor or standard as the benchmark in column 7.

  ✓ No gaps from PRESENT capabilities have been included. Only PARTIAL and ABSENT carry forward.

  ✓ Personas Affected column references only personas identified in pre-work Step PW1 — no invented personas.

  ✓ All tracks are represented in the output — confirm at least one gap from each of: Track 1, Track 2A (common platform), Track 2A (co-dependent inbound), Track 2A (co-dependent outbound), and Track 2B. If any sub-track yielded zero gaps, explicitly state this in the summary line.

  ✓ Merged gaps correctly carry all Gap Classifications and Source Tracks from every input gap that was merged.

  ✓ Inbound and outbound co-dependent gaps are kept as separate rows and never merged with each other, even if they involve the same co-dependent product.

Output as a clean table ready for direct export to Excel and create an excel file named Feature_Gaps_Consolidated.xlsx in the designated output folder.

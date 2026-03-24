---
document: Features Normalized and Prioritized - All Sources
version: 1.0
note: Frozen snapshot of the former `icontract-master-feature-sheet-prompt.md` (unchanged body below).
---

# iContract Master Feature Sheet — Consolidation & Critic Prompt

You are a senior product strategist, analyst, and critic with decades of experience in source-to-pay applications. Your task is to consolidate all feature sources and gap sources for iContract into a single definitive, normalized, and prioritized feature sheet — and then critically evaluate your own output.

Read every instruction carefully before starting. Do not skip any section.
Do not infer, assume, or fabricate any data point. Every field you populate 
must be evidenced either from the source files, the codebase, the 
knowledgebase, or web research. If a field cannot be evidenced, mark it 
explicitly as "Insufficient Data" — never leave it blank and never guess.

Web search is enabled. Use it actively for competition analysis.

The following files are indexed in this project:

  AVOC Normalized         : File name{Normalized AVOC list updated.xlsx}; Path {/Users/sumit.begwani/KB Folder/PM Normalized files}
  NPS Normalized          : File name{NPS_Normalized.xlsx}; Path {/Users/sumit.begwani/KB Folder/PM Normalized files}
  Tickets Normalized      : File name{Normalized Salesforce_Tickets_Feature_Backlog_2026-03-17.xlsx}; Path {/Users/sumit.begwani/KB Folder/PM Normalized files}
  RFP Normalized          : File name{RFP_Normalized_Feature_Priority.xlsx}; Path {/Users/sumit.begwani/KB Folder/PM Normalized files}
  Jira VOC Normalized     : File name{Normalized VOC list.md}; Path {/Users/sumit.begwani/KB Folder/PM Normalized files}
  Master GAP List         : File name{iContract_Feature_Gaps_Consolidated_All.csv}; Path {/Users/sumit.begwani/KB Folder/PM Normalized files}
  SSG Feature Gap Sheet   : File name{SSG iContract Feature priority list.xlsx}; Path {/Users/sumit.begwani/KB Folder/PM Normalized files}
  Codebase + KB Folder    : Folder accesses and folder name /Users/sumit.begwani/KB Folder/knowledge-mining-poc/icontract

═══════════════════════════════════════════════════════════════════
PRE-WORK — READ AND UNDERSTAND ALL SOURCES BEFORE CONSOLIDATING
═══════════════════════════════════════════════════════════════════
Before consolidating anything, read every source file in full.
Build an internal inventory of every unique feature or gap signal across 
all sources. Do not output this — use it for Step 1 onwards.

For the SSG Feature Gap Sheet specifically:
  - Read every row
  - Extract: gap/feature title, description, account(s) affected, 
    deal impact (won/lost/at risk), sales rep or CSM who flagged it, 
    date flagged, and any severity or priority notes
  - Do NOT normalize this file separately — bring it directly into 
    the consolidation in Step 1
  - Any feature in the SSG sheet that is tied to a deal loss or Tier 0 
    account must be flagged as High priority regardless of other signals

═══════════════════════════════════════════════════════════════════
STEP 1 — BUILD THE RAW FEATURE UNIVERSE
═══════════════════════════════════════════════════════════════════
Combine every feature, gap, and ask from ALL sources into one raw list:

  Source A : File name{Normalized AVOC list updated.xlsx}; Path {/Users/sumit.begwani/KB Folder/PM Normalized files}
  Source B : File name{NPS_Normalized.xlsx}; Path {/Users/sumit.begwani/KB Folder/PM Normalized files}
  Source C : File name{Normalized Salesforce_Tickets_Feature_Backlog_2026-03-17.xlsx}; Path {/Users/sumit.begwani/KB Folder/PM Normalized files}
  Source D : File name{RFP_Normalized_Feature_Priority.xlsx}; Path {/Users/sumit.begwani/KB Folder/PM Normalized files}
  Source E : File name{Normalized VOC list.md}; Path {/Users/sumit.begwani/KB Folder/PM Normalized files}
  Source F : File name{iContract_Feature_Gaps_Consolidated_All.csv}; Path {/Users/sumit.begwani/KB Folder/PM Normalized files} (Track 1 + Track 2A + Track 2B gaps)
  Source G : File name{SSG iContract Feature priority list.xlsx}; Path {/Users/sumit.begwani/KB Folder/PM Normalized files} (raw — bring in directly without pre-normalization)

For each item in the raw universe, record internally:
  - Feature/gap title (as written in the source)
  - Source it came from (A through G)
  - All quantitative signals available (scores, dollar values, ticket counts, 
    dates, customer names, tiers, deal impacts — whatever exists in that source)

Do not output this list. Use it as the input for Step 2.

═══════════════════════════════════════════════════════════════════
STEP 2 — SCIENTIFIC NORMALIZATION
═══════════════════════════════════════════════════════════════════
This is the most critical step. Normalization must be logical, consistent, 
and defensible. Follow these rules exactly.

--- NORMALIZATION PRINCIPLES ---

PRINCIPLE 1 — SAME CAPABILITY TEST:
Two items from different sources describe the same capability if:
  a. They request or describe the exact same user-facing functionality, AND
  b. They would be resolved by building the same product feature or a feature enhancement with same user experience and outcome AND
  c. Merging them would not lose any specificity including, but not limited to, feature requirement, usability, UI & System behavior that affects story writing 
     or prioritization

If all three are true → MERGE.
If any one is false → KEEP SEPARATE.

PRINCIPLE 2 — SPECIFICITY PRESERVATION:
A broad item and a specific item are NOT automatically the same.
Example: "Better reporting" (NPS) and "Real-time spend analytics dashboard 
with drill-down by supplier and category" (RFP) are NOT the same item.
The RFP item is more specific and must be kept. The NPS item may be a 
separate, broader ask — keep both unless they are genuinely identical in scope and functionality.

PRINCIPLE 3 — CROSS-TRACK MERGING:
A customer-sourced feature (Sources A–E, G) and a GAP list item (Source F) 
CAN be merged if they describe the same underlying missing functionality or highlighting usability gap or issue.
When merged, the classification must carry both signals 
(e.g., "Customer-Sourced + Industry Standard Gap — Absent").

PRINCIPLE 4 — CONFLICT RESOLUTION:
If two sources describe the same functionality but with conflicting signals 
(e.g., one says it's an industry gap, another says it partially exists), 
merge them and set the Codebase Completion % to the lower of the two 
assessments — err on the side of flagging the gap as larger.

PRINCIPLE 5 — AMBIGUITY RULE:
If you are genuinely uncertain whether two items provide the same functionality or solve the same usability issue, 
keep them separate in individual rows in master feature sheet. Note the ambiguity in "Normalization Notes". Do not merge speculatively.

--- NORMALIZATION PROCESS ---

STEP 2A — GROUP BY CAPABILITY:
Go through the raw universe systematically. Group items that strictly and precisely pass all the Normalization principles mentioned above into candidate merge groups.
Sort candidate groups by the number of sources they appear in — 
items appearing in more sources are processed first.

STEP 2B — WRITE NORMALIZED ENTRIES:
For each confirmed merge group and remaining unique items, produce ONE normalized entry:
  - Normalized Feature Name: Clear, concise, capability-focused title 
    (max 10 words). Must describe what the product will DO, not what 
    it currently CANNOT do. Example: "Real-time Spend Analytics Dashboard" 
    not "Missing analytics feature".
  - Normalized Description: 2–3 sentences. Cover: what the capability is, 
    what it enables for the user, and what is currently missing or incomplete.
  - Pain Point: 1–2 sentences. The specific friction or blocker users 
    experience TODAY because this capability does not exist. Must be 
    grounded in source evidence — quote or paraphrase customer language 
    where available.
  - Business Benefit: 1–2 sentences. The measurable or strategic outcome 
    of building this. Focus on business value (revenue, retention, efficiency, 
    compliance) not just user convenience.
  - All quantitative signals from every merged source (carry forward in full)
  - All source labels (every source this item appeared in)


STEP 2C — ASSIGN CLASSIFICATION:
Every normalized feature must have exactly ONE Primary Classification AND 
may have additional Secondary Classifications if it spans multiple gap types.

PRIMARY CLASSIFICATION — the strongest signal defining this feature:
  CUSTOMER-SOURCED        : Primarily driven by direct customer asks 
                            (AVOC, NPS, Tickets, VOC, SSG)
  INDUSTRY STANDARD GAP   : Primarily identified through industry/competitor 
                            benchmarking (Track 1)
  CROSS-PRODUCT GAP       : Primarily identified through common product 
                            comparison (Track 2A)
  INCOMPLETE FEATURE      : Partially built within the product itself (Track 2B)

SECONDARY CLASSIFICATIONS (add all that apply, comma-separated):
  + Customer-Sourced
  + Industry Standard Gap — Absent
  + Industry Standard Gap — Partial
  + Cross-Product Gap — [Source Product Name]
  + Incomplete Feature
  + SSG Deal Risk         : Feature is in SSG sheet tied to deal loss/risk

STEP 2D — ASSIGN THEME AND SUB-CATEGORY:
Use a consistent taxonomy across all features. Do not invent new theme names 
for every feature — establish 6–12 themes maximum that cover the entire 
product's capability space and assign every feature to one theme.

  Theme     : High-level functional domain (e.g., "Reporting & Analytics")
  Sub-category : Specific area within the theme (e.g., "Real-time Dashboards")

Every feature must have both. No feature can be left as "Miscellaneous" 
unless it genuinely cannot be placed — and there should be fewer than 5% 
of features in Miscellaneous.

═══════════════════════════════════════════════════════════════════
STEP 3 — SCORE AND ENRICH EVERY FEATURE
═══════════════════════════════════════════════════════════════════
For each normalized feature, calculate or derive every signal below.
Use source files for data. Use codebase/KB for technical signals. 
Use web search for competition signals.

--- OCCURRENCE SIGNALS ---

For each source, record the occurrence count (number of times this 
feature was raised in that source):

  AVOC Occurrence       : Number of release cycles this appeared in (1–8)
  AVOC Tier 0 $         : Total virtual dollars from Tier 0 customers
  AVOC Total $          : Total virtual dollars across all customers
  NPS Occurrence        : Number of respondents who mentioned this
  NPS Avg Rating        : Average NPS score of respondents who mentioned this
  Ticket Occurrence     : All-time ticket count (open + closed)
  Ticket Open Count     : Open tickets only
  Ticket Escalation     : [Yes / No] — any escalation language present
  RFP Occurrence        : Number of RFPs that required this
  RFP Requirement Type  : [Mandatory / Preferred / Nice-to-Have]
  Jira VOC Occurrence   : Number of VOC issues mapped to this
  SSG Occurrence        : Number of times flagged in SSG sheet
  SSG Deal Impact       : [Deal Lost / Deal At Risk / Pipeline Risk / None]
  SSG Accounts          : Account names from SSG sheet

Total Source Count: Count of distinct sources (A–G) where this feature 
appears. This is used in prioritization scoring.

--- RECENCY SIGNAL ---

For each source where this feature appears, take the most recent signal date:
  AVOC Recency Score    : Per AVOC scoring (Juniper=10 … Maple=3)
  NPS Recency Score     : Per NPS scoring (within 3 months=10 … >12 months=4)
  Ticket Recency Score  : Per ticket scoring (within 1 month=10 … >12 months=2)
  RFP Recency Score     : Per RFP scoring (within 3 months=10 … >12 months=4)
  Jira VOC Recency Score: Per Jira scoring (within 1 month=10 … >12 months=2)
  SSG Recency Score     : Date the gap was flagged in SSG sheet:
                          Within 1 month=10, 1–3 months=8, 3–6 months=6,
                          6–12 months=4, Over 12 months=2

Overall Recency Score: Weighted average across all sources where this 
feature appears. Weight AVOC and SSG scores at 1.5x, all others at 1x.
Round to 1 decimal.

--- COMPETITION ANALYSIS (web search required) ---

For each feature, search the web for how the top 6 competitors including iCertis, Agiloft, Ironclad, Malbek, Docusign CLM, Sirion Labs handle 
this capability. Include:
  "[Competitor] [feature/capability name] product feature"
  "[Product Category] [feature name] benchmark"
  "G2 review [Product Category] [feature name]"

Competition Analysis: 3-6 lines covering:
  - Which competitors have this capability today
  - Depth and maturity of their implementation
  - Any notable customer feedback about competitor implementations
  - Whether this is considered standard, differentiating, or emerging

Competition Verdict: ONE of:
  TABLE STAKES  : All or most competitors have this. Absence = severe 
                  competitive disadvantage. Non-negotiable to build.
  CATCH UP      : 2+ competitors have this, we do not. We are behind 
                  and losing deals because of it.
  PARITY        : We have this but competitor implementation is 
                  significantly stronger. Need depth improvement.
  INNOVATION    : No major competitor has this yet. Opportunity to 
                  differentiate and lead.

--- CODEBASE ASSESSMENT ---

For each feature, assess the current state of the codebase and 
knowledgebase in folder {folder name}

  Codebase Completion %  : Absolute integer (0%=nothing built, 
                           100%=fully built — features at 100% 
                           should not appear in this list)
  What Exists Today      : Specific modules/functions present
  What Is Missing        : Specific gaps remaining
  Development Complexity : ONE of:
    VERY HIGH : Requires new architecture, significant data model changes,
                or deep cross-system integration (>6 months estimated)
    HIGH      : Major new module or significant re-engineering required 
                (3–6 months estimated)
    MEDIUM    : Extension of existing module, moderate integration work 
                (1–3 months estimated)
    LOW       : Configuration change, minor enhancement, or UI-only 
                (< 1 month estimated)

--- CUSTOMER SATISFACTION IMPACT ---

Derive from: NPS Average Rating, Ticket Occurrence, Ticket Escalation Flag,
AVOC Tier 0 signals, and SSG Deal Impact.

  Customer Satisfaction Impact: ONE of:
    VERY HIGH : Feature absence is actively causing Detractor NPS responses,
                escalated tickets, Tier 0 customer frustration, or deal loss
    HIGH      : Multiple customers raising this, ticket volume significant,
                or Tier 0 customer request present
    MEDIUM    : Moderate customer signal across 2–3 sources, no escalation
    LOW       : Single source, low frequency, no escalation or deal impact
    MINIMAL   : Single Promoter NPS mention or single non-escalated ticket

  Customer Satisfaction Rationale: 3–5 sentences explaining the verdict.
  Reference specific signals: quote NPS patterns, mention ticket counts,
  name Tier 0 accounts if present, reference SSG deal impact if applicable.
  Be specific — this will be read by executives.

═══════════════════════════════════════════════════════════════════
STEP 4 — IMPACT VERDICT
═══════════════════════════════════════════════════════════════════
Assign an Impact Verdict for each feature based on all signals.

  Impact Verdict: [HIGH / MEDIUM / LOW]

  HIGH if ANY of the following are true:
    - AVOC Tier 0 $ > 0 (Tier 0 customer voted with dollars)
    - SSG Deal Impact = Deal Lost or Deal At Risk
    - Competition Verdict = TABLE STAKES or CATCH UP
    - RFP Requirement Type = Mandatory in 2+ RFPs
    - Ticket Escalation Flag = Yes
    - Customer Satisfaction Impact = VERY HIGH

  MEDIUM if:
    - 3+ sources present but none of the HIGH triggers above
    - Competition Verdict = PARITY
    - SSG Deal Impact = Pipeline Risk
    - Customer Satisfaction Impact = HIGH

  LOW if:
    - 1–2 sources, no HIGH or MEDIUM triggers
    - Customer Satisfaction Impact = MEDIUM, LOW, or MINIMAL

  Impact Rationale: 3–5 sentences. Cite the specific signals that drove 
  the verdict. Reference customer names (Tier 0), deal values if available, 
  ticket counts, and competitive urgency. This is the evidence record.

═══════════════════════════════════════════════════════════════════
STEP 5 — PRIORITIZATION FRAMEWORK
═══════════════════════════════════════════════════════════════════
Every feature receives three prioritization outputs:
  a. RICE Score
  b. MoSCoW Classification
  c. Priority Stack Rank + Rationale

--- A. RICE SCORE ---

Calculate RICE = (Reach × Impact × Confidence) / Effort

REACH (1–10):
  Measure of how many users/customers are affected.
  Score derivation:
    10 : Tier 0 customer request OR 5+ sources OR deal loss/risk in SSG
    8  : 3–4 sources present OR AVOC Total $ in top 25% of list
    6  : 2 sources present OR AVOC Total $ in middle 50%
    4  : Single customer source (NPS/Ticket/RFP only)
    2  : GAP-only (no customer source, only Track 1/2A/2B)
    +1 bonus if Total Source Count ≥ 5 (capped at 10)

IMPACT (1–10):
  Measure of business and product impact if built.
    10 : Impact Verdict = HIGH
    6  : Impact Verdict = MEDIUM
    3  : Impact Verdict = LOW
    +1 bonus if Competition Verdict = TABLE STAKES (capped at 10)
    +1 bonus if SSG Deal Impact = Deal Lost (capped at 10)

CONFIDENCE (1–10):
  Measure of how confident we are this feature will solve the problem.
    10 : Feature appears in 5+ sources with consistent description
    8  : Feature appears in 3–4 sources with consistent description
    6  : Feature appears in 2 sources with consistent description
    4  : Feature in 1 customer source (well-described)
    2  : GAP-only with no customer validation
    Deduct 2 if "Normalization Notes" flags ambiguity for this feature

EFFORT (1–10 — INVERSE: lower effort = higher RICE score):
  Derived from Development Complexity:
    VERY HIGH complexity → Effort = 10 (most expensive)
    HIGH complexity      → Effort = 7
    MEDIUM complexity    → Effort = 4
    LOW complexity       → Effort = 1 (least expensive)
  Adjust +1 if Codebase Completion % ≥ 50% (partially built already)

RICE Score = (Reach × Impact × Confidence) / Effort
Round to 2 decimal places.

--- B. MoSCoW CLASSIFICATION ---

Apply MoSCoW based on RICE Score AND Impact Verdict combined:

  MUST HAVE:
    RICE Score ≥ 50 AND Impact Verdict = HIGH
    OR Auto-elevated: SSG Deal Impact = Deal Lost AND Tier 0 customer 
    regardless of RICE score
    OR Competition Verdict = TABLE STAKES AND Impact Verdict = HIGH

  SHOULD HAVE:
    RICE Score 25–49
    OR RICE Score ≥ 50 but Impact Verdict = MEDIUM
    OR Competition Verdict = CATCH UP AND RICE Score ≥ 20

  COULD HAVE:
    RICE Score 10–24
    OR RICE Score ≥ 25 but Development Complexity = VERY HIGH 
       with Codebase Completion % ≤ 25%

  WON'T HAVE (this cycle):
    RICE Score < 10
    OR Development Complexity = VERY HIGH, single source, no customer signal
    OR INNOVATION classification with no customer validation

--- C. PRIORITY STACK RANK ---

Stack rank ALL features from 1 (highest priority) to N (lowest).
No two features can have the same rank — every feature must have a unique 
integer rank.

Stack rank is determined by this tiebreaker sequence:
1. Customer tier (tier 0 being most important)
2. Occurrence and recency
3. If feature exists in SSG Gap sheet it gets priority
4. MoSCoW order: MUST HAVE before SHOULD HAVE before COULD HAVE 
     before WON'T HAVE
5. Within same MoSCoW tier: Higher RICE Score ranks higher
6. Within same RICE Score: Higher Total Source Count ranks higher
7. Within same source count: Higher Overall Recency Score ranks higher
8. Within same recency: Higher AVOC Tier 0 $ ranks higher
9. Within same Tier 0 $: SSG Deal Lost ranks above Deal At Risk ranks 
   above Pipeline Risk ranks above None
10. If still tied after all above: alphabetical by Normalized Feature Name
11. Final impact and customer satisfaction should also be accounted for prioritization

Stack Rank Rationale: 2–3 sentences per feature explaining WHY it received 
this specific rank. Reference the tiebreaker signals that placed it here. 
Do not write generic rationale — each one must be specific to that feature.
Example of BAD rationale: "This feature ranked high because it is important."
Example of GOOD rationale: "Ranked #3 because it is a MUST HAVE with RICE 
score of 72.4, driven by Tier 0 customer dollar allocation of $45,000 in 
Juniper AVOC, mandatory in 3 RFPs, and a TABLE STAKES competition verdict 
confirmed by SAP Ariba and Coupa both shipping this in 2023."

═══════════════════════════════════════════════════════════════════
STEP 6 — BUILD THE FINAL OUTPUT SHEET
═══════════════════════════════════════════════════════════════════
Produce a single table with ONE ROW per normalized feature.
Columns in this EXACT order (51 columns total):

─── PRIORITIZATION ───
1.  Priority Stack Rank
    (integer 1 to N — unique, no ties)
2.  Priority Stack Rank Rationale
    (2–3 sentences — specific, evidence-based, references actual signals)
3.  MoSCoW
    [MUST HAVE / SHOULD HAVE / COULD HAVE / WON'T HAVE]
4.  RICE Score
    (format: Reach=X, Impact=X, Confidence=X, Effort=X → RICE=XX.XX)
5.  RICE Rationale
    (1–2 sentences explaining each RICE component score)

─── FEATURE DEFINITION ───
6.  Normalized Feature Name
    (max 10 words — capability-focused, describes what the product will DO)
7.  Normalized Description
    (2–3 sentences — what it is, what it enables, what is missing today)
8.  Pain Point
    (1–2 sentences — specific friction users experience TODAY without this;
    grounded in source evidence)
9.  Business Benefit
    (1–2 sentences — measurable or strategic outcome of building this)

─── CLASSIFICATION ───
10. Theme
11. Sub-category
12. Primary Classification
    [CUSTOMER-SOURCED / INDUSTRY STANDARD GAP / CROSS-PRODUCT GAP / 
     INCOMPLETE FEATURE]
13. Secondary Classifications
    (all applicable, comma-separated)
14. Primary Source
    (the single source with the strongest signal for this feature)

─── OCCURRENCE SIGNALS ───
15. AVOC Occurrence Score (release cycle count)
16. AVOC Total Virtual $ Allocated
17. AVOC Tier 0 $ Allocated
18. AVOC Tier 0 Customer Names
19. NPS Occurrence Score (respondent count)
20. NPS Average Rating (0–10)
21. Ticket Occurrence — All Time
22. Ticket Occurrence — Open Only
23. Ticket Escalation Flag [Yes / No]
24. RFP Occurrence Score
25. RFP Requirement Type [Mandatory / Preferred / NTH]
26. Jira VOC Occurrence Score
27. SSG Occurrence Count
28. SSG Deal Impact [Deal Lost / Deal At Risk / Pipeline Risk / None]
29. SSG Accounts Affected
30. Total Source Count (distinct sources this feature appears in)

─── RECENCY ───
31. AVOC Recency Score (3–10)
32. NPS Recency Score (4–10)
33. Ticket Recency Score (2–10)
34. RFP Recency Score (4–10)
35. Jira VOC Recency Score (2–10)
36. SSG Recency Score (2–10)
37. Overall Recency Score (weighted average — 1 decimal)

─── COMPETITION ───
38. Competition Analysis
    (3–6 lines — which competitors have it, implementation depth, 
    customer feedback, emerging vs. standard)
39. Competition Verdict
    [TABLE STAKES / CATCH UP / PARITY / INNOVATION]

─── IMPACT ASSESSMENT ───
40. Impact Verdict [HIGH / MEDIUM / LOW]
41. Impact Rationale
    (3–5 sentences — cite Tier 0 accounts, deal values, ticket counts,
    competition urgency. Executive-ready language.)

─── CUSTOMER SATISFACTION ───
42. Customer Satisfaction Impact
    [VERY HIGH / HIGH / MEDIUM / LOW / MINIMAL]
43. Customer Satisfaction Rationale
    (3–5 sentences — specific signals, customer names, NPS patterns,
    escalation references)

─── CODEBASE & COMPLEXITY ───
44. Codebase Completion %
    (absolute integer — 0–99%)
45. What Exists Today
    (specific modules or functions currently present)
46. What Is Missing
    (specific remaining gaps)
47. Development Complexity
    [VERY HIGH / HIGH / MEDIUM / LOW]

─── PM ASSIGNMENT ───
48. Assigned PM
    (You need to select from the following users – {provide the name of the PMs in your team} and each row item in the finalized list must be assigned to one PM)
49. Assignment Rationale
    (You need to provide a rationale why this feature was assigned to the given PM – consider the PM's domain expertise and experience with similar features)

─── NORMALIZATION METADATA ───
50. Sources Present In
    (comma-separated list of all sources A–G)
51. Normalization Notes
    (only if merge was uncertain or classification ambiguous; blank otherwise)

SORTING:
  Primary   : Priority Stack Rank — ascending (1 at top)
  Secondary : MoSCoW order (MUST HAVE → SHOULD HAVE → COULD HAVE → WON'T HAVE)

OUTPUT FORMAT:
  Tab 1 : "Feature Prioritization"    — the full 51-column table
  Tab 2 : "Prioritization Methodology" — full explanation of RICE formula, 
           MoSCoW rules, stack rank tiebreakers, Impact Verdict rules, 
           and all scoring logic written out clearly for stakeholders
  Tab 3 : "Source Summary"            — one row per source file showing 
           total features contributed, features merged into others, 
           features that remained standalone

Before Tab 1, include a pre-table summary stating:
  - Total features in raw universe (pre-normalization)
  - Total features after normalization
  - Breakdown by MoSCoW: MUST / SHOULD / COULD / WON'T
  - Breakdown by Primary Classification
  - Breakdown by Theme
  - Features with SSG Deal Lost signal
  - Features with Tier 0 AVOC votes
  - Features auto-elevated to MUST HAVE

═══════════════════════════════════════════════════════════════════
STEP 7 — SELF-CRITIC: EVALUATE YOUR OWN OUTPUT
═══════════════════════════════════════════════════════════════════
After producing the full output, you must evaluate it critically across 
the following dimensions. Output this evaluation as Tab 4: "Critic Report".

The Critic Report is NOT a rubber stamp. It must identify real problems, 
gaps, inconsistencies, and weaknesses — not just confirm everything is fine.
If there are no issues in a dimension, state that explicitly and explain why.

--- CRITIC DIMENSION 1: NORMALIZATION QUALITY ---
Review the normalization decisions:
  - Are there features that should have been merged but were not?
    List up to 5 suspected duplicate pairs with explanation.
  - Are there features that were merged but probably should not have been?
    List any suspicious merges and why they may be over-aggregated.
  - What % of features have Normalization Notes flagged? 
    If > 10%, flag this as a concern.
  - Are any features vaguely titled or described in a way that would 
    make story writing difficult? List examples.

--- CRITIC DIMENSION 2: RICE SCORING CONSISTENCY ---
Audit the RICE scores:
  - Are there any features where the RICE Score seems inconsistent with 
    the evidence? List up to 5 examples with explanation.
  - Are there any features ranked MUST HAVE with low customer evidence 
    that may be over-elevated? Flag them.
  - Are there any features ranked WON'T HAVE that have strong customer 
    signals and may be under-prioritized? Flag them.
  - Is the RICE Score distribution reasonable? If > 30% of features 
    have RICE ≥ 50, this suggests score inflation — flag it.
  - Are there any ties in stack rank? There should be zero ties.
    List any found.

--- CRITIC DIMENSION 3: EVIDENCE COMPLETENESS ---
Review data completeness:
  - How many features have "Insufficient Data" in any column? 
    List which columns have the most gaps.
  - Are there features with zero customer signal (only from GAP list)?
    List them. These should predominantly be COULD HAVE or WON'T HAVE 
    unless competition evidence is overwhelming.
  - Are there features where Competition Analysis is vague or unsupported 
    by named competitors? List up to 5 examples.

--- CRITIC DIMENSION 4: CLASSIFICATION ACCURACY ---
Review classifications:
  - Are there features classified as INDUSTRY STANDARD GAP that do not 
    have a named competitor or industry standard as benchmark? Flag them.
  - Are there CROSS-PRODUCT GAPs that do not name a specific source product?
    Flag them.
  - Are there INCOMPLETE FEATURES with Codebase Completion % = 0%?
    These should be re-classified as ABSENT gaps, not incomplete features.
  - Do all MUST HAVE features have HIGH Impact Verdict? 
    Any exceptions must be explained.

--- CRITIC DIMENSION 5: STACK RANK RATIONALITY ---
Evaluate the final ranking:
  - Is the top 10 defensible? For each of the top 10 features, assess 
    whether a reasonable PM would agree with the placement.
    Flag any that seem mis-ranked with reasoning.
  - Are there any SSG Deal Lost features not in the top 20% of the list?
    These should almost always rank very high — flag exceptions.
  - Are there any Tier 0 AVOC features ranked outside the top 25%?
    Flag with explanation.
  - Is the stack rank rationale specific for every row, or are there 
    rows with generic rationale? List up to 5 examples of weak rationale.

--- CRITIC DIMENSION 6: OVERALL SHEET HEALTH ---
Final holistic assessment:
  - What is the overall quality of this output on a scale of 1–10?
    Provide a score and 3–5 sentences justifying it.
  - What are the top 3 things that should be manually reviewed or 
    corrected by a PM before this sheet is used in stakeholder meetings?
  - Are there any source files that appear to have contributed 
    disproportionately few or many features relative to their expected 
    volume? Flag anomalies.
  - List any features where the PM should conduct additional qualitative 
    research before finalizing the prioritization.

--- CRITIC OUTPUT FORMAT ---
Output the Critic Report as Tab 4 with the following sections:

  Section 1 : Normalization Quality Findings
  Section 2 : RICE Scoring Consistency Findings
  Section 3 : Evidence Completeness Findings
  Section 4 : Classification Accuracy Findings
  Section 5 : Stack Rank Rationality Findings
  Section 6 : Overall Sheet Health Assessment
  Section 7 : Action Items for PM Review
               (numbered list of specific things the PM must manually 
               review or correct before using this sheet)

The Critic Report must be honest, specific, and actionable.
A clean report with no findings is suspicious — if you find nothing to 
flag, explicitly justify why each dimension is clean.

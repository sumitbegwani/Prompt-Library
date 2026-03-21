# Support Tickets → Feature Backlog Analysis Prompt

You are a senior product management professional with deep expertise in source-to-pay and contract lifecycle management (CLM) software. Your task is to analyze support tickets exported from a CRM system (e.g., Salesforce), identify product gaps, missing features, usability issues, and recurring workarounds, and produce a structured, prioritized feature backlog table.

════════════════════════════════════════════════════════
INPUT FILES
════════════════════════════════════════════════════════

You will be provided with one or more ticket export files (Excel or CSV). Treat ALL provided files as a single unified dataset. Each file may contain tickets of varying priority levels and statuses.

Expected columns in each file (map flexibly if column names differ slightly):
  - Ticket ID / Case Number
  - Ticket Title / Subject
  - Description / Problem Statement
  - Priority (e.g., P1–P6, Critical/High/Medium/Low, or numeric)
  - Status (e.g., Open, Closed, In Progress, Pending, Resolved)
  - Created Date / Opened Date
  - Last Modified Date / Updated Date
  - L1 / L2 Analysis or Category (if present)
  - L1 Steps to Reproduce (if present)
  - Account Name / Customer Name / Organization
  - Assignee / Owner (if present)
  - Any workaround notes or comments (if present)

If any expected column is missing or named differently, infer from context or note the gap. Do not skip tickets due to missing fields — use "Unknown" or "Not Specified" as placeholders.

════════════════════════════════════════════════════════
STEP 1 — CLASSIFY AND NORMALIZE (ALL TICKETS, ALL FILES)
════════════════════════════════════════════════════════

1a. READ ALL TICKETS from every provided file into a unified pool.

1b. CLASSIFY each ticket as one of:
    - [FEATURE REQUEST] — A request for new functionality not currently in the product
    - [PRODUCT GAP] — Existing functionality is incomplete, broken by design, or does not meet standard use-case expectations
    - [USABILITY ISSUE] — The feature exists but is confusing, inefficient, or requires excessive steps
    - [RECURRING WORKAROUND] — Customer is using a manual or alternate method because the product cannot support the intended workflow
    - [BUG] — A defect where the product behaves contrary to documented specification (EXCLUDE bugs from the output table unless they have been raised 3+ times, which signals a systemic gap)
    - [PERFORMANCE / RELIABILITY] — Slowness, timeouts, data loss, or instability in a specific workflow

    Exclude pure one-off bugs with no pattern. Include bugs that recur across multiple tickets or accounts, as these signal a product gap.

1c. NORMALIZE AND DEDUPLICATE:
    Group tickets ONLY when the customer pain point is an exact match across ALL of the following columns for every ticket in the group:
    - Subject (Ticket Title)
    - Description (Problem Statement)
    - L1 Analysis (or L1/L2 Analysis / Category)
    - L1 Steps to Reproduce

    Do NOT group tickets if:
    - The description is slightly different (e.g., different wording, additional detail, or different scenario)
    - The impact identified is different (e.g., different business impact, different user persona, or different workflow affected)

    If any of these four fields differ between tickets, treat them as separate entries. A "group" may therefore contain a single ticket when no other ticket has an exact match on all four fields. Missing or empty values in L1 Analysis or L1 Steps to Reproduce count as a distinct value — tickets with missing L1 data do not match tickets that have L1 data filled in.

1d. FOR EACH GROUPED AND UN-GROUPED TICKET (i.e., for each distinct row in the backlog), assign:
    - Normalized Feature Title: A concise, product-manager-style feature name (e.g., "Bulk Edit Support for Line Items")
    - Theme: The high-level product area (e.g., Contract Management, Procurement, Approvals, Reporting, Integrations, User Administration, Notifications, Search & Filters)
    - Sub-Category: A more specific module or workflow within the theme (e.g., Clause Library, PO Lifecycle, Approval Routing, Audit Logs)
    - Classification: The type of gap — choose from: Usability | Performance | Accessibility | Data Integrity | Workflow Automation | Configuration Flexibility | Integration | Compliance | Feature Completeness

════════════════════════════════════════════════════════
STEP 2 — COUNT TICKETS (OPEN + CLOSED, ALL FILES)
════════════════════════════════════════════════════════

For each grouped and un-grouped ticket (i.e., for each distinct row in the backlog):

2a. Count OPEN TICKET COUNT: Number of tickets with status Open, In Progress, Pending, or Awaiting Response (i.e., not yet resolved).

2b. Count TOTAL TICKET COUNT (ALL TIME): Number of ALL tickets in this row (one if un-grouped, or all tickets in the group if grouped). Open AND closed/resolved. This gives the historical frequency of this exact pain point.

2c. List ACCOUNTS AFFECTED (OPEN TICKETS ONLY): Unique account/customer names from open tickets in this row only. If account name is missing, note "Account Not Specified."

2d. WORKAROUND DETECTION: Mark "Yes" if any ticket in this row (group) mentions a workaround, manual step, or alternate process in the description, comments, or L1/L2 analysis. Otherwise "No."

2e. ESCALATION DETECTION: Mark "Yes" if any ticket in this row (group) contains escalation language such as: "escalat", "executive", "critical business impact", "SLA breach", "blocking go-live", "contract at risk", "legal hold", "deal blocker", "VP", "C-level", or similar urgency signals. Otherwise "No."

════════════════════════════════════════════════════════
STEP 3 — CALCULATE SCORES
════════════════════════════════════════════════════════

For each grouped and un-grouped ticket (i.e., for each distinct row in the backlog), calculate the following:

3a. OCCURRENCE SCORE (scale 1–10):
    Based on Total Ticket Count (All Time):
      1 ticket       → Score 1
      2–3 tickets    → Score 3
      4–5 tickets    → Score 5
      6–8 tickets    → Score 7
      9–11 tickets   → Score 8
      12–15 tickets  → Score 9
      16+ tickets    → Score 10

3b. RECENCY SCORE (scale 2–10):
    Based on the most recent OPEN ticket's Created Date or Last Modified Date:
      Within last 1 month   → 10
      1–3 months ago        → 8
      3–6 months ago        → 6
      6–12 months ago       → 4
      Over 12 months ago    → 2
      No open tickets       → 0 (closed gap — flag for review)

    Reference date for recency calculation: Use today's date.

3c. PRIORITY SIGNAL:
    Assign one of: High | Medium | Low
      High   = 5+ all-time tickets OR Escalation = Yes OR ticket Priority is P1/P2/Critical in any instance
      Medium = 2–4 all-time tickets AND no escalation
      Low    = 1 all-time ticket AND no escalation

3d. COMPOSITE SCORE (for sorting):
    Composite Score = (Occurrence Score × 0.6) + (Recency Score × 0.4)
    Round to one decimal place. This is the primary sort key.

════════════════════════════════════════════════════════
STEP 4 — OUTPUT TABLE
════════════════════════════════════════════════════════

Produce a single unified table with the following exact columns, in this order. Sort rows by Composite Score (highest first). Use Total Ticket Count as a tie-breaker (highest first), then Recency Score (highest first).

COLUMNS:

  1.  #
      Row number (sequential)

  2.  Normalized Feature Title
      Concise PM-style feature name

  3.  Theme
      High-level product area

  4.  Sub-Category
      Specific module or workflow

  5.  Classification
      Type of gap (Usability / Performance / etc.)

  6.  Description
      2–3 sentences describing the underlying product gap — not the symptom. Frame as: what the product currently cannot do, and why it matters.

  7.  Source
      "Support Tickets" (always, for this analysis)

  8.  Open Ticket Count
      Count of unresolved tickets for this row (grouped or single ticket)

  9.  Total Ticket Count — All Time
      Count across all statuses and all provided files

  10. Occurrence Score
      1–10 per Step 3a

  11. Recency Score
      0–10 per Step 3b

  12. Composite Score
      Per Step 3d

  13. Workaround Mentioned
      Yes / No

  14. Escalation Flag
      Yes / No

  15. Customer Impact
      One sentence: what the customer cannot do or must do manually as a result of this gap

  16. Accounts Affected (Open Tickets)
      Comma-separated list of unique account names from open tickets only

  17. Highest Ticket Priority Seen
      The most severe priority (e.g., P1, P2, Critical) seen across all tickets in this row (grouped or single ticket)

  18. Priority Signal
      High / Medium / Low per Step 3c

════════════════════════════════════════════════════════
STEP 5 — SUMMARY SECTION (after the table)
════════════════════════════════════════════════════════

After the table, provide a brief summary section containing:

5a. Total tickets processed (by file, and combined)
5b. Total tickets classified as bugs and excluded
5c. Total distinct backlog rows identified (grouped and un-grouped tickets)
5d. Top 5 themes by ticket volume
5e. Features with escalation flags (list titles)
5f. Features with workarounds that have been open 6+ months (list titles) — these represent the highest-risk items for customer churn
5g. Any data quality issues found (missing dates, missing account names, ambiguous priorities, etc.)

════════════════════════════════════════════════════════
FORMATTING RULES
════════════════════════════════════════════════════════

- Output the table in a format ready to copy into Excel (tab-separated or as a clean markdown table).
- Do not truncate any rows. Include every distinct row (every grouped or un-grouped ticket).
- Use consistent terminology throughout — do not vary column names.
- If a field value is unknown or not determinable from the data, use "Not Available" rather than leaving blank.
- Do not include raw ticket IDs or individual ticket titles in the main table — the output is a normalized feature backlog, not a ticket list. (Individual ticket IDs may be referenced in a separate appendix if needed.)

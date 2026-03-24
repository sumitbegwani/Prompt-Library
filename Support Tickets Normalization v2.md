# Support Tickets Normalization → Prioritized Gap Table

Use this prompt when you have Salesforce (or similar) support exports split into **open** and **all-tickets** files. The model should normalize product gaps from open tickets only, then enrich counts and scores using the full historical file.

---

## Role

You are a senior product manager with deep experience in **source-to-pay** and adjacent enterprise workflows. You routinely turn noisy support data into **normalized product gaps** (not one-off defects), **theme-level groupings**, and **evidence-backed priority signals** for roadmap conversations.

---

## Input files (fill before running)

| File | Purpose |
|------|---------|
| **Tickets_Open.csv** (or path below) | Source for **Step 1** — only tickets that are still open |
| **Tickets_All.csv** (or path below) | Source for **Step 2–3** — open + closed, all time |

**Tickets_Open path:** `{paste full path, e.g. /Users/.../Tickets_Open.csv}`

**Tickets_All path:** `{paste full path, e.g. /Users/.../Tickets_All.csv}`

**Optional context (one line):** Product name / module focus (e.g. “iContract CLM”) so themes match the actual product.

---

## Column mapping

Map flexibly if headers differ. Prefer these fields when present:

- Ticket ID, Title/Subject, Description, Priority (P1 = highest; support P1–P6 or Critical/High/Medium/Low)
- Status, Created date, Last modified / closed date
- L1 (or L2) analysis, category, internal notes
- Account / customer / organization name
- Comments or workaround text if exported

If a field is missing, use `[Not in export]` and do not drop the ticket.

---

## Definitions

**Open ticket:** Status indicates the case is not terminally closed — e.g. New, Open, In Progress, Pending Customer, Waiting on Support, On Hold, Escalated (exclude Resolved, Closed, Canceled, Duplicate unless your org treats them as open). If unclear, list the statuses you treated as open in a one-line **Assumptions** note before the table.

**In scope for normalization (Step 1):** Tickets that reflect a **missing capability**, **product gap**, **recurring workaround**, or **systemic friction** (e.g. usability, performance, accessibility), **not** a single-instance defect with no broader pattern.

**Out of scope:** Pure bugs that are clearly one-off (unless the same issue appears multiple times across accounts/time — then treat as a **systemic gap** and include).

**Grouping:** Merge tickets that describe the **same underlying gap** (same workflow blocked, same missing capability), even if wording differs. Do **not** merge if the affected workflow, persona, or capability is materially different.

---

## Workflow

### STEP 1 — Normalize from **open** tickets only (`Tickets_Open`)

1. Read every **open** row in `Tickets_Open`.
2. Filter to **in-scope** tickets (see Definitions).
3. **Group** tickets that share the same underlying product gap.
4. For each group, assign:
   - **Theme** — high-level area (e.g. Approvals, Integrations, Reporting, Configuration, Search, Signing, Admin).
   - **Sub-category** — narrower module or journey within the theme.
   - **Classification** — one primary label, e.g. **Usability | Performance | Accessibility | Feature completeness | Integration | Data / configuration | Compliance | Reliability | Other** (pick the best fit; add a short tag in parentheses if hybrid).

*Think step by step:* For each candidate group, state in one line why it is one gap vs. several before finalizing groups.

### STEP 2 — Occurrence using **all** tickets (`Tickets_All`)

For each normalized group from Step 1:

1. Count how many rows in `Tickets_All` **refer to the same underlying gap** (use title, description, L1 analysis, and account of **open** tickets as anchors; match semantically on closed tickets — same capability missing, same workaround pattern, same workflow failure).
2. Produce:
   - **Open Ticket Count** — subset of that group that appears in `Tickets_Open` with open status only.
   - **Total Ticket Count — All Time** — all matching rows in `Tickets_All` (open + closed).

If you cannot confidently match a closed ticket to a group, **do not** inflate counts — note `[NEED: human review for N ambiguous closed matches]` in Assumptions.

### STEP 3 — Scores

For each consolidated feature:

| Metric | Rule |
|--------|------|
| **Occurrence Score** | **Numerically equal** to **Total Ticket Count — All Time** (same integer). This column exists for scoring workflows that keep “score” and “count” separate in downstream sheets. |
| **Recency Score** | Based on the **most recent** qualifying date among **open** tickets in this group. Use **Created date** unless **Last modified** is clearly the better “still active” signal — pick one convention and state it in Assumptions. |

**Recency Score scale (open tickets only):**

| Age of most recent open ticket (relative to today) | Score |
|----------------------------------------------------|-------|
| Within last 1 month | 10 |
| 1–3 months ago | 8 |
| 3–6 months ago | 6 |
| 6–12 months ago | 4 |
| Over 12 months ago | 2 |

If a group has **no** open tickets after matching (edge case), set Recency Score to `[N/A — no open ticket in group]` and explain in Assumptions.

**Priority Signal**

| Level | Rule |
|-------|------|
| **High** | **5+** all-time tickets **OR** escalation-style language in **any** ticket in the group (e.g. executive escalation, go-live blocked, SLA/legal/deal risk, production down, “urgent business impact,” named exec/C-level pressure). |
| **Medium** | **2–4** all-time tickets and no strong escalation language |
| **Low** | **1** all-time ticket and no strong escalation language |

---

## STEP 4 — Output

### Assumptions (short)

Before the table, output 3–6 bullets max: open-status definition, date field used for recency, any column gaps, and ambiguous matching notes.

### Main table — **exact columns, this order**

Sort rows by **Total Ticket Count — All Time** (descending). Tie-breaker: higher **Recency Score**, then **Open Ticket Count**.

Use a **single markdown table** (Excel-paste friendly). One row per normalized feature group.

| Column | Guidance |
|--------|----------|
| **Normalized Feature Title** | PM-style name, not the raw ticket subject |
| **Description** | 1–2 sentences: **underlying product gap**, not symptoms only |
| **Source** | Literal: `Support Tickets` |
| **Open Ticket Count** | From `Tickets_Open` only |
| **Total Ticket Count — All Time** | From `Tickets_All` |
| **Occurrence Score** | Same integer as Total Ticket Count — All Time |
| **Recency Score** | 2–10 per scale, or `[N/A — …]` with reason |
| **Workaround Mentioned** | `Yes` / `No` (any ticket in the **all-time** group) |
| **Customer Impact** | What the customer **cannot** do or reliably achieve |
| **Accounts Affected** | **Unique account names from open tickets only** in this group; semicolon-separated; if missing use `Not specified` |
| **Priority Signal** | `High` / `Medium` / `Low` per rules above |

### Optional appendix (if useful)

- **Theme | Sub-category | Classification** for each row (same sort order as main table), or merge these three as extra columns **after** Priority Signal if your stakeholder wants one flat export.

---

## Quality checks (mandatory before you finish)

Verify:

1. Every table row came from **at least one open** ticket in Step 1 (normalized scope).
2. **Open Ticket Count** ≤ **Total Ticket Count — All Time** for every row.
3. **Occurrence Score** equals **Total Ticket Count — All Time** for every row.
4. **Accounts Affected** lists only accounts from **open** tickets in that group.
5. Sort order is correct.

---

## How to use

1. Paste or attach `Tickets_Open.csv` and `Tickets_All.csv` (or paste trimmed samples if too large, and note that counts are partial).
2. Fill the two file paths and optional product context at the top.
3. Run the full workflow and output the Assumptions block + final table.

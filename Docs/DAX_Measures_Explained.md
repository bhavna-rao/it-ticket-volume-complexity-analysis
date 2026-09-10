# DAX Measures — Explained

All measures live in the `00_Measures` table and reference the `it_tickets_sample_4000` data table.

---

### 1. Total Tickets
```
Total Tickets = COUNTROWS('it_tickets_sample_4000')
```
**What it does:** Counts how many rows (tickets) exist in the table.
**Why it's useful:** The base KPI everything else builds on. Because it's a measure, not a fixed number, it recalculates automatically when you click a category in the slicer — e.g. click "Hardware" and it instantly shows 1,139 instead of 4,000.

---

### 2. Avg Word Count
```
Avg Word Count = AVERAGE('it_tickets_sample_4000'[Word_Count])
```
**What it does:** Adds up the `Word_Count` column and divides by the number of rows.
**Why it's useful:** A proxy for ticket *complexity*. Combined with category, it answers "which categories take more effort to resolve, not just more volume."

---

### 3. % of Total
```
% of Total = DIVIDE([Total Tickets], CALCULATE([Total Tickets], ALL('it_tickets_sample_4000')))
```
**What it does:** Divides the ticket count *in the current filter context* (e.g. just "Hardware") by the ticket count *ignoring all filters* (the grand total of all 4,000). `ALL()` is what removes the filter for the denominator — without it, both sides would be filtered the same way and the answer would always be 100%.
**Why it's useful:** Turns a raw count into a share of the whole, e.g. "Hardware = 28.5% of all tickets" — easier to interpret at a glance than a raw number.

---

### 4. Max Word Count
```
Max Word Count = MAX('it_tickets_sample_4000'[Word_Count])
```
**What it does:** Returns the single highest `Word_Count` value in the current filter context.
**Why it's useful:** Flags the longest, most complex individual ticket — useful for spotting outliers (e.g. a ticket with 300+ words vs. the ~44 average).

---

### 5. Total Categories
```
Total Categories = DISTINCTCOUNT('it_tickets_sample_4000'[Topic_group])
```
**What it does:** Counts the number of *unique* values in `Topic_group` (not total rows — distinct labels only).
**Why it's useful:** A simple sanity-check KPI ("8 categories") that also protects the dashboard — if the data source ever changes and a 9th category appears, this number changes too, immediately signaling the model needs a review.

---

## The one concept underneath all of these: filter context
Every measure above recalculates based on whatever filters are currently active — a slicer click, a visual's own category axis, a page filter. That's the core difference between a DAX measure and a plain Excel formula: the same formula produces a different number depending on what's selected, without you writing any new logic.

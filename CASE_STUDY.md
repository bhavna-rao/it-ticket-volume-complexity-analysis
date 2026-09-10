# Case Study: IT Service Ticket Volume & Complexity Analysis

## Business Context
IT service desks typically handle a high volume of support tickets spanning many categories — hardware issues, access requests, HR support, purchase requests, and more. Teams that only track total ticket *volume* often miss a second, equally important dimension: how *complex* each category of ticket is to resolve. A category with a small number of tickets can still consume disproportionate staff time if those tickets are unusually detailed or difficult.

## The Challenge
Using a sample of 4,000 IT service tickets across 8 categories, this analysis set out to answer three questions:
1. Which ticket categories create the most workload, by volume?
2. Do certain categories involve longer, more complex ticket descriptions than others?
3. Could tickets be automatically routed based on patterns in their text?

## Approach
1. Explored the raw dataset in Excel to validate data quality — confirmed all 8 categories were correctly labeled with no missing values, and prototyped a ticket-length metric.
2. Loaded the data into Power BI and used Power Query to clean the dataset (duplicate removal) and engineer two features: character count and word count per ticket, used as a proxy for ticket complexity.
3. Built a set of DAX measures (ticket counts, share of total, average complexity) that recalculate dynamically as the report is filtered.
4. Designed a two-page Power BI report: an **Overview** page for volume-based questions, and a **Content Insights** page pairing a text-frequency view (word cloud) with a volume-vs-complexity comparison table.

## Key Findings

**Volume and complexity don't always move together.** Hardware is the largest category by volume (1,139 tickets, 28.5% of all tickets) and also the most complex (59.46 average words per ticket) — the single biggest driver of both ticket count and staff effort.

**Low-volume categories can hide high effort.** Administrative rights tickets are the rarest category (147 tickets, 3.7% of volume) but rank 2nd in complexity (53.82 average words) — a category easy to overlook if a team only tracks ticket counts, but one that likely consumes more time per ticket than its small volume suggests.

**The clearest automation candidate is low on both dimensions.** Storage tickets are both low-volume (232 tickets) and the least complex of all 8 categories (34.80 average words) — a pattern consistent with short, routine requests that are strong candidates for self-service or automated handling.

## Recommendations
- Prioritize experienced staff and clear escalation paths for **Hardware**, given its combination of high volume and high complexity.
- Improve self-service documentation for **Administrative rights** — its low volume makes it easy to deprioritize, but its complexity suggests staff spend disproportionate time on it.
- Evaluate **Storage** requests as a first candidate for automation or a self-service portal, given their low volume and low complexity.
- As a next step, apply text classification techniques to the ticket text itself to test whether tickets can be automatically routed to the correct team at intake, reducing manual triage time.

## Tools & Methodology
Microsoft Excel (initial data validation) · Power BI Desktop — Power Query (data cleaning, feature engineering) and DAX (measures) · Power BI report design (KPI cards, bar chart, treemap, word cloud, table)

## Dataset & Disclosure
This analysis uses a public dataset, [IT Service Ticket Classification Dataset](https://www.kaggle.com/datasets/adisongoh/it-service-ticket-classification-dataset) (Kaggle, by adisongoh), sampled down to 4,000 tickets (from an original 47,837) while preserving the original category proportions. This is a self-directed portfolio project built for skill demonstration purposes and does not represent real company data, a client engagement, or professional work experience.

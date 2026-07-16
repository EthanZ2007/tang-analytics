# Customer Analysis: Who Are Tang's Customers?

## Business Question

Who are Tang's customers, and what does their visit and spending behavior actually look like? This is a descriptive analysis by design — it characterizes customer behavior without making revenue-recovery recommendations, since those belong in a separate, dedicated analysis once the underlying patterns are understood.

## Approach

Filtered `data/cleaned_orders_2024plus.csv` to `cid_usable=True` (35,966 of 50,069 clean orders, 71.8%) for every analysis that groups by customer — visit frequency, revenue concentration, spend-per-tier. Analyses that don't depend on customer identity (time-of-day patterns, revenue trends) used the full clean dataset instead, since restricting those to the CID-usable subset would throw away data for no reason.

While exploring visit frequency, a second data-quality issue surfaced beyond what notebook 01 caught: the restaurant's own phone number was passing as a valid customer ID and ranked as the single most "frequent customer" (153 visits, 97% one order type, mostly cash — a clear internal/staff usage pattern, not a diner). It was confirmed and excluded from customer-level analysis, dropping the working population to 35,812 orders / 7,803 distinct customers.

## Key Findings

- **Revenue concentrates hard by visit frequency, not by spend.** The top 10.2% of customers by visit count (12+ visits) generate 56% of customer-attributable revenue, while the 55.8% of customers who've ordered exactly once account for only 12.7%. But average ticket size is flat-to-slightly-declining across every tier (~$39 for one-time customers down to ~$37 for the most frequent) — the concentration is entirely about how often people come back, not about regulars spending more per visit.
- **Tang is dinner-driven with a real, confirmed Monday closure.** ~72% of orders fall in the 4-10pm window versus ~21% at lunch. Of 128 Mondays in the dataset, 126 have zero orders; the other 2 resolve to a New Year's Day exception (67 orders on 2024-01-01) and one unexplained single order.
- **Average monthly revenue has drifted down over the ~2.5-year window**: ~$63k/month (2024) → ~$58k (2025) → ~$55k (2026 year-to-date), with December standing out as a seasonal peak in both full years.
- **A large, sustained shift from cash to card payment**, starting in 2025 (cash share: 87.7% → 55.4% → 59.3% across 2024/2025/2026 YTD) — flagged as a real pattern in the data, though the notebook can't rule out a POS/payment-processing change as the cause rather than pure customer behavior change.
- **Two apparent patterns turned out to be measurement artifacts**, not real signals: an apparent ~1,000-customer acquisition spike in the dataset's first month (every existing regular necessarily gets counted as "first-seen" then, since there's no earlier data), and the restaurant's own phone number ranking as the top "customer" before it was caught and excluded.

## Business Recommendation

This notebook is intentionally descriptive and does not make revenue-recovery recommendations. What the findings suggest as directions for future, dedicated analysis:

- Any customer-level metric (loyalty program design, CLV, targeted outreach) should filter to `cid_usable=True` and exclude the confirmed non-customer number — using the raw ~86% CID-presence figure or an unfiltered "top customer" ranking would meaningfully distort the picture.
- The revenue-concentration finding (a small group of repeat visitors driving over half of tracked revenue) is a natural candidate for a future retention/loyalty-focused analysis.
- The cash-to-card shift and the gradual multi-year revenue drift are both real enough to be worth a dedicated follow-up analysis — this notebook only describes that they exist, not why.

## Data Caveats

- Covers only the ~71% of orders with a trustworthy customer ID; conclusions about "customers" describe that subset, not all of Tang's order volume.
- Only one non-customer number (the restaurant's own line) was confirmed and excluded — no systematic check was made for other staff or vendor numbers that might still be counted as customers.
- The cash/card shift could reflect a payment-processing or POS change rather than genuine customer behavior change; the order data alone can't distinguish between the two.
- The final month in the dataset is partial (~9 days); monthly trend charts exclude or explicitly flag it rather than showing a misleading drop-off.

## Notebook

Link: [notebooks/02_customer_analysis.ipynb](../notebooks/02_customer_analysis.ipynb)

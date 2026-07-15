# Data Cleaning: Orders (2024–present)

## Business Question

Before any revenue trend or customer-behavior analysis can be trusted, is the underlying order data (`tblOrder`, 2024–present) clean enough to support it — and where specifically can't it be trusted?

## Approach

Pulled all 50,109 orders with `checkinTime >= 2024-01-01` from the `trn.dbo.tblOrder` table and audited them for:
- duplicate order IDs
- invalid `paidAmount` (null, zero, negative)
- `customerID` (CID / customer phone) formatting and validity

Rather than silently dropping anything, every issue found was logged to an exclusions log (order ID + reason + proposed action), reviewed, and then applied in three distinct ways depending on what the issue actually meant for the data:
- **`exclude_row`** — the order record itself is unreliable and was dropped
- **`flag_zero_paid`** — the order stays (a $0 order still represents a real visit), but is flagged out of revenue-specific calculations
- **`flag_cid_only`** — the order stays, but its customer ID shouldn't be trusted for customer-level grouping

## Key Findings

- **Row-level data is clean.** Of 50,109 orders, only 40 (0.1%) were dropped outright — zero-paid orders with non-standard status codes that looked like voids/incomplete transactions, not real completed visits. No duplicate order IDs were found.
- **366 zero-paid orders are real visits, not errors** — same status code as normal completed orders, most plausibly comped meals. Kept in the clean dataset and flagged `excluded_from_revenue=True` so they don't distort revenue or average-ticket-size figures, while still counting toward order volume and visit frequency.
- **Headline finding: real customer-ID reliability is 71.8%, not the ~86% originally assumed.** The ~86% figure only reflected orders where *a* CID was present. Digging into CID quality surfaced a second problem: ~14.1% of orders that do have a CID carry one from a cluster of numbers (`(XXX)973-10XX`, spanning multiple area codes including toll-free `855`) that cannot be a real customer's personal line. This cluster is 100% concentrated in a single `orderType` code, pointing to a systemic source — most likely a delivery platform's masked/proxy number or a POS software default — rather than genuine repeat customers. Combined with the ~14.1% of orders missing a CID entirely, **only 71.8% of clean orders (35,966 of 50,069) have a customer ID worth using for customer-level analysis.**

## Business Recommendation

- **Any customer-level analysis (repeat-visit rate, customer lifetime value, loyalty segmentation) must filter to orders with a trustworthy CID first.** Skipping that filter would lump ~28% of all orders into a handful of fake "customers" — one single phone number alone accounts for 5% of all CID-bearing rows — badly distorting repeat-visit and concentration metrics.
- **Worth confirming the source of the `973-10XX` cluster** with the POS vendor or delivery-platform integrations before building customer segmentation on top of this data. If it turns out to be a delivery-platform default, that's a whole order channel (~14% of volume) currently invisible to any customer-level analysis — potentially a meaningful, quantifiable channel to target as part of the recovery plan.
- Consider documenting what `invoiceStatus` codes actually mean internally (e.g., with the POS vendor) — the ambiguity around the 366 zero-paid orders exists only because that mapping isn't available.

## Data Caveats

- Only `checkinTime >= 2024-01-01` was audited; pre-2024 data was not checked and may follow different conventions.
- Audit scope was limited to order ID uniqueness, `paidAmount` validity, and CID quality — other fields (tax, discounts, table/seat assignments, etc.) were not validated.
- `invoiceStatus` / `kitchenStatus` code meanings are not documented anywhere accessible; all interpretations here are inferred from data patterns, not a source-of-truth mapping.
- The source of the `973-10XX` CID cluster (delivery platform vs. POS default vs. something else) is inferred from frequency and `orderType` concentration, not confirmed.

## Notebook

Link: [notebooks/01_data_cleaning.ipynb](../notebooks/01_data_cleaning.ipynb)

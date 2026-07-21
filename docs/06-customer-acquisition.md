# Customer Acquisition: Concrete Offers, Tested Against Real Data

## Business Question

Shifting from "recover lost revenue" (notebooks 04/05) to "actively bring in more customers" — what are specific, concrete actions (not general marketing advice) that the data directly supports, each modeled as a named offer with a target audience and a dollar range?

## Approach

Every candidate idea was tested against Tang's own order data before being included, using the same discipline established in notebook 05: no invented conversion or response rates where a real one could be derived instead, and ideas dropped if they didn't hold up under testing. Five threads were explored on request, each modeled as a specific action + specific offer/mechanism + dollar impact with stated assumptions:

1. Lapsed customer win-back, split into two tiers (90-180 days vs. 180+ days quiet), each with its own separately-measured natural return rate rather than reusing one number for both
2. A "come back soon" offer for first-time customers, timed using the actual distribution of how long it takes returning customers to place their second order
3. A slow-period promotion, targeted only after confirming which day is genuinely lowest-volume in absolute terms (not just fastest-declining)
4. A referral offer targeted narrowly at the top 10% of customers by visit frequency
5. Delivery-platform visibility, reframed as a new-customer discovery question rather than a retention one

## Key Findings

- **Customers who go quiet for 180+ days have a meaningfully lower natural return rate than those quiet for only 90-180 days** — confirming that a single win-back assumption shouldn't be applied uniformly across both groups; colder leads warrant a different (smaller) expected response.
- **Roughly half of first-time customers never return, and of those who do, most take much longer than two weeks** — only a small minority come back within their first two weeks on their own, which supports a deliberately-timed "come back soon" nudge rather than an arbitrarily-timed one.
- **The slowest day of the week also has the highest average order size** — an interesting combination (fewer orders, but bigger ones) that points toward a specific promotion theme rather than a generic discount.
- **The strongest new finding: a delivery platform's masked customer numbers show up dramatically more often on a customer's first order than on repeat orders** — clear evidence that this platform functions primarily as a discovery channel, not a loyalty-ordering channel. Separately, that platform's *share* of new-customer acquisition has been growing even as its raw order volume has been flat-to-declining, reframing it from "a channel to recover" (per notebooks 04/05) to "a channel to invest further in."
- **All five threads survived testing this time** — none were dropped, though every dollar estimate carries a Medium confidence rating, since none of the five actions have ever been run by the business before and there's no prior campaign data to calibrate response rates against.

## Business Recommendation

Prioritize actions with the clearest underlying data pattern alongside their dollar size, not dollar size alone — the referral-based idea produced the largest single estimate but rests on the least-grounded assumption (no prior referral program to measure), while the delivery-platform idea produced the smallest estimate but rests on the most directly-observed pattern (a large, consistent gap between first-order and repeat-order behavior). Recommend testing at small scale before committing to full rollout on any of them, since all five assumptions are informed estimates, not measured facts. A client-facing summary of this analysis (with specific dollar estimates and offer mechanics) was prepared separately for the restaurant owners; it is not part of this public repository.

## Data Caveats

- All response/lift assumptions are illustrative, clearly labeled, and unverified — none reflect an actual prior campaign, since none of these five actions have been run before.
- The delivery-platform discovery signal relies on the same masking-pattern heuristic used in notebooks 04/05 (owner-supplied, not a confirmed system flag) and can only identify one platform, not all delivery platforms Tang uses.
- The "days to second visit" and "natural return rate" figures are real, measured patterns, but they describe historical behavior — they don't guarantee that a newly-introduced offer will move behavior in the same direction or magnitude.
- The slow-day finding identifies where the gap is, not why it exists.

## Notebook

Link: [notebooks/06_customer_acquisition.ipynb](../notebooks/06_customer_acquisition.ipynb)

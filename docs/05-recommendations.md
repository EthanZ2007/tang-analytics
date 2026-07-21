# Testing Recommendations Against the Data

## Business Question

Notebook 04 diagnosed the revenue decline as a volume/discovery problem. Given that diagnosis, which specific recovery ideas actually hold up when tested against real data — and which common restaurant-recovery ideas sound plausible but don't?

## Approach

Every candidate idea was tested against Tang's own order data before being included, rather than argued for on general principle. Two disciplines were applied throughout:

- **No invented conversion or response rates.** Where a "campaign win-back" number is normally guessed (e.g. "assume 5% respond to a text"), this analysis instead derived an empirical baseline from Tang's own historical customer behavior — how often a customer who's gone quiet for 90+ days has actually returned on their own, based on the full order history. A campaign's *incremental* effect on top of that baseline is still an estimate, but the baseline itself is measured, not assumed.
- **Ideas that failed the test were dropped, not softened into the list anyway.** Two candidate ideas (extending hours, and a lunch- or dinner-specific push) were tested directly and did not survive — both are reported as dropped, with the evidence that ruled them out, rather than omitted quietly.

Every surviving idea was assigned a confidence level — High (directly observed in the data), Medium (a real pattern, but the cause or sizing involves inference), or Low (data-adjacent, but not something the data can really price out) — and a rough revenue-impact range with the assumptions stated explicitly.

## Key Findings

- **A delivery-platform-linked slice of the business is eroding faster than the rest of takeout.** Using a proxy signal for one major delivery platform (based on how that platform's masked customer numbers appear in the data), that slice has declined roughly twice as fast, in percentage terms, as takeout overall — and the decline is gradual, not a single sharp drop, which points toward an ongoing visibility/ranking issue rather than a one-time incident.
- **A defensible, data-grounded win-back opportunity exists.** A meaningful share of identified customers are currently in a "gone quiet for 3-6 months" window. Critically, this notebook found that customers who reach that point have, historically, come back on their own at a high rate — Tang's retention problem (per notebook 04) isn't really a retention problem at all; it's an acquisition one. The recommendation here targets accelerating and modestly lifting that already-strong natural return pattern, not fixing a broken one.
- **Menu streamlining is real, but it's an efficiency story, not a revenue one.** Confirmed notebook 03's finding: half the menu accounts for a small single-digit share of revenue. Since no cost, labor, or waste data exists anywhere in Tang's system, this thread stops short of a dollar estimate — it's reported honestly as a complexity-reduction recommendation, not a revenue driver.
- **One day of the week is declining meaningfully faster than the rest**, and the obvious explanation (delivery-platform concentration) was tested and ruled out. Reported as a flag for the owner to investigate, not a solved mystery.
- **Two plausible-sounding ideas were tested and dropped**: extended hours (no evidence of suppressed demand near closing time — order volume tapers off smoothly) and a lunch- or dinner-specific push (both dayparts are declining at similar rates, with no exploitable asymmetry).

## Business Recommendation

Prioritize the volume-side ideas that survived testing — recovering delivery-platform visibility and a structured win-back outreach to recently-lapsed customers — over price-side or capacity-side ideas, consistent with notebook 04's diagnosis that this is fundamentally a discovery problem. Menu streamlining is worth doing for operational reasons on its own timeline, not as a revenue lever. The day-of-week pattern is worth a direct conversation with the owner, since the data can flag it but can't explain it.

A simple, clearly-caveated forecast comparing "no action" to "top recommendations land" shows a modest, realistic improvement — a meaningful step, not a full return to historical revenue levels on its own. A client-facing summary of this analysis (with specific dollar estimates) was prepared separately as a private deliverable for the restaurant owners; it is not part of this public repository.

## Data Caveats

- The delivery-platform signal relies on a masking-pattern heuristic supplied by the business owner, not a confirmed system flag — treated as reasonably reliable given supporting behavioral evidence, but still inference layered on inference.
- That same signal can only identify one delivery platform's orders; Tang uses others that leave no distinguishing trace in this data, so the true combined delivery-platform picture is unmeasured.
- No cost, labor, or waste data exists anywhere in Tang's system, so the menu-streamlining thread could not be priced in dollars.
- The day-of-week finding is a confirmed pattern with no confirmed cause — presented as a lead for the owner to check, not a diagnosis.

## Notebook

Link: [notebooks/05_recommendation_testing.ipynb](../notebooks/05_recommendation_testing.ipynb)

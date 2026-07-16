# Menu Analysis: Revenue, Popularity, and Simplification Candidates

## Business Question

Which menu items generate the most revenue and orders, and which look like genuine simplification candidates — redundant, low-volume, or both? Descriptive throughout: the notebook surfaces and flags candidates, but the call on what to actually cut, consolidate, or reprice belongs to Tang.

## Approach

Item-level data lives in `tblODT`, joined to `tblOrder` for the same 2024+ / notebook-01-cleaned order set, and resolved to real dish names through a second database (`rst`, holding `tblDish`/`tblFoodType`) that turned out not to be a missing table but a separate database on the same SQL Server instance — a distinction worth confirming before trusting any of the numbers downstream.

Step 1 was a required, non-skippable schema/data-quality check before any analysis: it confirmed the name-mapping join resolves 99.997% of line items to real names, that `adjustprice` is already an extended line total (not per-unit — multiplying by quantity would double-count), that no real cost/COGS data exists anywhere in the system (`cost_material`/`cost_labour`/`cost_all` are always placeholder values), and that non-dish line items (combo-selection placeholders, service charges, paid add-ons — 2.7% of gross line revenue) needed filtering out before ranking "menu items." No contamination from a different restaurant's menu was found.

## Key Findings

- **The bottom half of the menu by order count generates only 3.4% of total revenue** (median 9 orders across ~2.5 years, versus 177 for the top half) — the strongest simplification signal in the data. Cutting even a large share of this tail costs very little measured revenue, though the data can't see whether a specific low-volume item is a regular's standing favorite.
- **"Chinese Lunch" is the most bloated category**: 87 distinct items (the most of any category) for only 2.1% of revenue — almost certainly lower-priced lunch-hour duplicates of dishes that already exist on the dinner menu.
- **Nearly half the menu (320 of 674 items, 74 families) is built from the same dish repeated across proteins** (e.g. chicken/beef/pork/shrimp/tofu broccoli). Checked systematically rather than eyeballed: chicken wins its family outright 66% of the time; every other protein underperforms in roughly similar proportions to each other, so the pattern is "chicken wins" rather than "pork and tofu specifically lose."
- **The top 5 items by revenue are also the top 5 by popularity** — `(C)General Chick`, `(C)B/less Sprib`, `(C)Chk Broccoli`, `B/less Sprib`, and `(C)Sesame Chick` are unambiguous, high-confidence anchors.
- **The menu is less combo-dependent than the top-revenue rankings alone suggest**: combo-format items dominate individual rankings, but combo categories account for only 23.3% of total menu-item revenue — 76.7% is spread across everyday à la carte ordering.
- **Margin proxy (explicitly an estimate, not real data, since no COGS exists)**: of the 59% of revenue that could be tied to a protein keyword, chicken/pork/veg/tofu makes up 42.1%, shrimp/seafood 13.3%, and beef only 3.8% — the smallest of the three tiers despite appearing in 64 items. 41% of revenue couldn't be classified at all.

## Business Recommendation

- **Cut candidates**: the bottom-50%-by-orders tail (337 items, 3.4% of revenue); the "Chinese Lunch" category as a whole section; and specific non-chicken protein variants flagged as capturing under 20% of their family's orders (e.g. tofu and pork "Broccoli" combo variants, combined 8% of that family's orders versus 92% for beef and shrimp).
- **Keep — high performers**: the top 5 revenue/popularity items; the `Combo` and `Chinese Combo` categories (highest revenue-per-item at $11,113 and $2,168 despite modest item counts); `Dumpling` and `App Sald Soup` (appetizers/salad/soup), which combine strong revenue-per-item with high order counts.
- Final decisions should weigh this data alongside what it can't see: specific regulars' standing preferences, ingredient sourcing constraints, kitchen prep complexity, and seasonal items.

## Data Caveats

- No real cost/COGS data exists in this system — the protein-tier margin section is an explicitly labeled estimate based on general ingredient-cost assumptions, not actual margin.
- Protein-family detection is regex pattern-matching on abbreviated, sometimes-truncated (30-character) dish names — a heuristic that can miss or misgroup families that don't share obvious wording. One false-positive grouping was caught and fixed during review (a whitespace-only artifact, not a real protein match); the fix changed 1 of 320 classified items and didn't move any of the headline percentages.
- "Times ordered" and revenue both exclude the 366 zero-paid comp orders from notebook 01 for dollar-based metrics, consistent with that notebook's convention.
- Item names are truncated at 20-30 characters at the database level (e.g. "Boneless" → "B/less"), so some entries read as abbreviations rather than full dish names.

## Notebook

Link: [notebooks/03_menu_analysis.ipynb](../notebooks/03_menu_analysis.ipynb)

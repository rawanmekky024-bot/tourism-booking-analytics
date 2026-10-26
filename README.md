# Tourism Booking Analytics | Power BI

An individual Power BI project exploring booking patterns, cancellations, guest satisfaction, operational delays, and destination performance across a supplied Egypt tourism sample dataset.

![Tourism report cover artwork](assets/sahara-cover.png)

> The report uses the fictional presentation brand “Sahara Suites.” The supplied CSV is a sample dataset; the analysis should not be interpreted as actual performance for a real hotel or business.

## Project Overview

This interactive report analyzes 1,200 booking records dated from January through December 2025. It is designed to help explore booking volume, cancellation patterns, guest feedback, check-in delays, stay costs, and differences between Egyptian destinations.

## Project Objectives

- Monitor booking volume, cancellation rate, guest satisfaction, and estimated stay cost.
- Compare booking and satisfaction patterns across cities, channels, travel groups, and activities.
- Explore operational measures such as lead time, length of stay, and check-in delay.
- Provide interactive filtering and a selectable minimum satisfaction threshold.

## Tools & Technologies

- Microsoft Power BI Desktop (PBIP project)
- DAX measures, calculated tables, and field parameters
- Power Query (M) for data preparation
- CSV dataset

## Dataset Overview

- 1,200 rows and 19 columns; 1,200 unique booking IDs.
- Date range: 2025-01-01 to 2025-12-31.
- Fields cover booking date, city and region, travel group, group size, lead time, stay duration, room and meal types, booking channel, activity, nightly rate, estimated stay cost, satisfaction and review scores, check-in delay, repeat-visitor flag, and cancellation status.
- The provided dataset has no guest/customer identifier, so repeat-visitor measures describe booking records marked as repeat visitors and are not a unique-customer retention rate.

The data source/attribution was not included with the supplied files. Please add it if known. Publishing permission was confirmed by the project owner.

## Report Pages & Features

The PBIP contains three analytical pages plus a welcome page and a city tooltip page:

1. **Executive Overview** — booking, cancellation, satisfaction, and average stay-cost KPIs; monthly trend; city and channel comparisons.
2. **Guest & Operations Analysis** — satisfaction distribution and threshold, lead-time and stay-length analysis, check-in delay, activity, cost, and travel-group comparisons.
3. **Destination Performance** — city-level bookings, cancellation rate, satisfaction, delay, average stay cost, and estimated completed-stay cost.
4. **Royal Welcome** — report landing page.
5. **City Tooltip** — supporting tooltip page.

Interactive report controls include date, city, booking channel, travel group, cancellation status, a minimum-satisfaction selector (default 7), and a metric selector.

## Verified Sample Findings

These are calculations over the supplied CSV, not claims about a live business:

- 138 of 1,200 bookings are marked cancelled (11.5%).
- Mean guest satisfaction score is 7.42 on the dataset’s 3–10 scale.
- Mean estimated stay cost is approximately $348.64 per booking.
- Mean check-in delay is approximately 14.09 minutes.
- The sum of estimated stay costs for records marked not cancelled is $367,965.00. This is an estimate from the dataset, not verified revenue, cash collected, or profit.

## DAX Measures

Selected measures from the semantic model are documented in [`docs/dax-measures.md`](docs/dax-measures.md). The PBIP model contains the complete original definitions.

### Interpretation note

The original `Cancellation Rate` measure respects the report’s `Booking_Cancelled` slicer. If the slicer is set to `Yes`, the denominator is also filtered to cancelled rows, so the rate can display 100%. This behavior is retained from the supplied report and documented rather than silently changed. For an overall cancellation rate that ignores this slicer, the denominator would need to remove that filter.

## Project Files

- `powerbi/Tourism_Booking_Analytics.pbip` — Power BI project entry point.
- `powerbi/Tourism_Booking_Analytics.Report/` — report page definitions, visuals, theme resources, and report metadata.
- `powerbi/Tourism_Booking_Analytics.SemanticModel/` — model tables, relationships, Power Query expressions, and DAX definitions.
- `data/Tourism_Booking_Analytics_Dataset.csv` — supplied CSV used by the project.
- `docs/dax-measures.md` — selected DAX measures and interpretation notes.
- `assets/` — selected presentation artwork used by the report.

Power BI local cache and machine-specific settings are excluded. The original source files were not modified; the PBIP copy has normalized folder names and references.

## How to Explore

1. Install Power BI Desktop with PBIP support.
2. Clone/download this repository and open `powerbi/Tourism_Booking_Analytics.pbip`.
3. In Power Query, update the CSV source in the `Bookings` query. The copied project currently preserves the original absolute Windows file path; it will not resolve automatically on another computer.
4. Apply changes/refresh, then explore the report pages and slicers.

## Contribution

**Individual project.** Built as a personal analytics project, including the Power BI report, semantic model, data preparation, and DAX analysis.

## Limitations

- The dataset is a supplied sample; no source citation or real business context was present in the files.
- `Estimated_Stay_Cost_USD` is an estimate based on nightly rate and nights, not verified revenue.
- “Estimated Completed-Stay Revenue” sums estimated stay cost for records marked not cancelled; it does not confirm that a stay was completed or paid.
- The repeat-visitor field is a booking-level flag and cannot establish unique-customer retention without a guest ID.
- Cancellation-rate values under the cancellation slicer are filter-context dependent; see the interpretation note above.

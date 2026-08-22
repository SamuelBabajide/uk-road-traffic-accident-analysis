# uk-road-traffic-accident-analysis
Interactive Excel dashboard analysing 307,973 UK road traffic accidents (2021–2022) across 422 districts. Covers severity, temporal, infrastructure and environmental risk factors with cross-filtering slicers. Documents a data coverage gap affecting year-on-year comparison, with a full PowerPoint report included.


# UK Road Traffic Accident Analysis — Trends, Severity & Risk Factors

An interactive Excel dashboard and prescriptive analysis of 307,973 UK road traffic accident records, built to identify where road safety interventions should be targeted and why.

**Tools:** Microsoft Excel (PivotTables, slicers, dynamic KPI cards, camera tool) · PowerPoint.

**Role:** Data Analyst — data preprocessing, dashboard design, statistical analysis, reporting.

**Deliverables:** [Interactive dashboard](dashboard/) · [Presentation](presentation/)

UK Road Traffic Accident Dashboard
<img width="1425" height="662" alt="image" src="https://github.com/user-attachments/assets/53ab3c37-3ab9-4654-a3af-e2de3cc797cc" />


---

## Contents

- [Problem statement](#problem-statement)
- [Dataset](#dataset)
- [Methodology](#methodology)
- [Data quality finding](#data-quality-finding)
- [Key findings](#key-findings)
- [Dashboard interactivity](#dashboard-interactivity)
- [Recommendations](#recommendations)
- [Design decisions](#design-decisions)

---

## Problem statement

Road accidents remain a critical public safety concern, with weather, road surface, speed limits and traffic controls all influencing severity. Raw accident data sits in unstructured formats, making it difficult for stakeholders to derive actionable insight.

This project cleans and standardises the dataset, quantifies frequency and severity, isolates the highest-risk conditions, and delivers an interactive dashboard that converts findings into prioritised road safety recommendations.

---

## Dataset

| Attribute | Detail |
|---|---|
| Records | 307,973 accidents |
| Casualties | 417,883 |
| Variables | 23 |
| Period | January 2021 – December 2022 |
| Districts | 422 local authorities |

Variables span temporal dimensions (date, month, year, day of week, time), spatial dimensions (latitude, longitude, local authority, urban/rural classification), environmental conditions (weather, light, road surface), infrastructure (road type, speed limit, junction control, carriageway hazards) and outcomes (severity, casualties, vehicles involved).

A full variable dictionary is available in [`docs/data-dictionary.md`](docs/data-dictionary.md).

---

## Methodology

**1. Coverage audit** — Record counts cross-tabulated by year and local authority, which exposed a material 2022 reporting gap (see below).

**2. Missing value treatment** — `Carriageway_Hazards` nulls interpreted as "None", since absence records a clear carriageway rather than a missing observation.

**3. Type standardisation** — `Accident_Date` converted to date format, `Time` to HH:MM, speed limit and casualty counts confirmed as integers.

**4. Categorical consistency** — Severity, weather, light and road surface labels normalised so equivalent categories aggregate correctly.

**5. Derived measures** — PivotTables built for hourly, weekly and monthly patterns, severity by condition, and urban/rural comparison.

**6. Validation** — Casualty totals reconciled against the severity breakdown (351,436 + 59,312 + 7,135 = 417,883) and district count confirmed at 422.

---

## Data quality finding

**68 districts record accidents in 2021 and exactly zero in 2022.**

Glasgow City falls from 1,509 to 0. Edinburgh from 1,193 to 0. Aberdeenshire, Fife, Dundee, Stirling, Falkirk, all Lanarkshire districts and roughly sixty others show the same pattern. The affected districts are almost entirely Scottish.

This is a reporting gap, not a road safety achievement. Two things confirm it:

- No intervention takes a city of 600,000 people from 1,509 accidents to zero in twelve months.
- The boundary follows a national border rather than a policy boundary, which is characteristic of a data-source issue.

**Consequences carried through the analysis:**

- All accident-reduction rankings are excluded pending source validation.
- The headline year-on-year change is substantially explained by the missing records rather than a genuine national decline, and is reported with that caveat attached.
- 2021 is used as the measurement baseline, since it is the only year with confirmed complete national coverage.

An earlier draft of this analysis interpreted the pattern as evidence of successful Scottish road safety policy. Auditing the coverage before drawing that conclusion is what prevented a data artifact from being presented as a finding.

---

## Key findings

### Severity multiplies harm

| Severity | Accidents | Casualties | Casualties per accident |
|---|---|---|---|
| Slight | 263,280 | 351,436 | 1.34 |
| Serious | 40,740 | 59,312 | 1.46 |
| Fatal | 3,953 | 7,135 | 1.80 |

Fatal accidents represent 1.3% of events but produce 34% more casualties per event than slight accidents. Severity does not just change the outcome — it multiplies the number of people affected.

### Rural roads carry disproportionate fatal risk

Rural areas account for **35.5% of accident volume but 59.4% of all fatal accidents**.

| Measure | Urban | National | Rural |
|---|---|---|---|
| Fatal accident rate | 0.8% | 1.3% | 2.1% |
| Casualties per accident | 1.29 | 1.36 | 1.48 |

Rural accidents are **2.7 times more likely to be fatal** than urban ones.

### Infrastructure concentrates exposure

- **74.9%** of all accidents occur on single carriageways (230,612 against 77,361 for every other road type combined).
- The 30 mph band dominates by volume, reflecting the urban road network where most driving happens.
- 60 mph rural roads carry a visibly heavier fatal band than their volume warrants.

### Unlit roads are a fixable, rural problem

**95% of the 16,528 national no-lighting accidents occur in rural areas** (15,709). A further 1,142 occur where street lighting exists but was unlit — a maintenance failure rather than a capital one.

Combined, roughly 17,700 accidents sit on infrastructure that can be addressed through engineering rather than behaviour change.

### Temporal patterns give a precise enforcement target

- Friday is the highest-risk day at **50,529 accidents**, 50.6% above Sunday.
- The **17:00 hour** is the single highest-risk hour, exceeding the 08:00 morning peak.
- Rural areas show a flatter weekly pattern (Sunday at 78.6% of Friday, against 66.4% nationally), indicating leisure travel rather than commuting drives rural exposure.

### Exposure is not risk

73.8% of accidents occur in daylight and roughly 71% on dry roads. This does not make daylight or dry surfaces dangerous — it reflects when and where the overwhelming majority of driving takes place. Reading these figures as danger signals would misdirect spend.

The same caution applies to speed limits. The dataset records the *posted limit at the accident location*, not the speed travelled, so it cannot evidence non-compliance, signage adequacy or driver education. What it does support is an energy argument: higher-speed environments convert collisions into fatalities.

---

## Dashboard interactivity

Four cross-filtering slicers (Year, Urban/Rural, Accident Severity, City) update every visual simultaneously. Applying the rural filter reveals a materially different risk profile:

Dashboard with rural filter applied
<img width="1893" height="878" alt="image" src="https://github.com/user-attachments/assets/240d5a0e-7fa7-4950-acfc-4bba34355695" />

| Metric | All areas | Rural only |
|---|---|---|
| Total accidents | 307,973 | 109,441 |
| Fatal accident rate | 1.3% | 2.1% |
| Casualties per accident | 1.36 | 1.48 |
| Highest-volume district | Birmingham | Cornwall |

Cornwall rises from eighth to first under the rural filter, confirming it as a genuine rural risk profile rather than a ranking anomaly.

---

## Recommendations

**1. Single carriageway safety programme** — Prioritise central hatching and edge-line markings on the highest-volume single carriageways, targeting rural 60 mph roads first.

**2. Rural lighting capital programme** — Address the 15,709 rural no-lighting accidents through prioritised LED installation, and fix the 1,142 unlit-but-present cases as a maintenance action.

**3. Friday evening enforcement surge** — Concentrate patrols between 15:00 and 21:00 on Fridays, covering both the day peak and the 17:00 hourly peak.

**4. Evening rush-hour management** — Deploy variable message signage and stagger shift-end times in Birmingham, Leeds and Manchester.

**5. Wet weather response protocol** — Trigger variable speed limits and enhanced gritting when surface sensors report wet conditions.

**6. Rural high-speed intervention** — Deploy average-speed enforcement on 60 mph rural A-roads and pre-position rural ambulance cover on Friday evenings.

**7. Resolve the 2022 coverage gap** — Confirm the source of the 68-district reporting gap, suppress reduction rankings until reconciled, and re-baseline once complete records are obtained.

**8. Split the national KPI** — Separate accident-reduction targets from casualty-reduction targets, since fatal events carry 1.80 casualties against 1.34 for slight.

---

## Design decisions

**Standardised severity palette.** Slight, Serious and Fatal use a fixed amber–orange–red ramp on every chart, so a colour never means two different things across the dashboard.

**Separated metric families.** Volume measures use a cool blue family and severity uses the warm ramp, so a viewer can categorise any chart before reading a single label.

**Charts converted to KPI cards.** An urban/rural donut and a monthly trend line were replaced by compact KPI cards, freeing dashboard space while carrying more information than the charts they replaced.

**Split-view for skewed distributions.** The road type chart separates Single carriageway from all others rather than using a log scale, keeping every bar proportionally honest.

**KPI reconciliation.** Headline casualties were validated against the severity breakdown rather than assumed, correcting an earlier figure that had mirrored the accident count.

---

## Author

**Samuel Babajide** — Data Scientist specialising in applied analytics and predictive modelling within complex, regulated environments.

[LinkedIn](https://linkedin.com/in/samuelbbabajide) · [GitHub](https://github.com/PsalmmyBabs)


# London Air Quality Visualisation: Invisible Exposure and the WHO 2021 Guidelines

An interactive visual analysis of hourly NO2 and PM2.5 across three London monitoring sites in 2025, built in Observable with Observable Plot, designed to make invisible exposure patterns directly readable against the WHO 2021 health guidelines.

## Overview

This project asks how air pollution exposure varies across London, how its daily and weekly rhythm reveals its source, and how often it breaches the WHO 2021 health guidelines. The focus is on methodology rather than benchmark performance: the design uses visual encoding, small multiples, layered reference lines and one interactive control to surface patterns that summary statistics alone hide. Three coordinated visualisations answer three research questions in turn, and each design choice is justified against the alternative considered and rejected, drawing on the visualisation literature (Munzner; Cleveland and McGill; Gleicher et al.; Shneiderman; Wood, Kachkaev and Dykes).

## Data

* **Source:** London Air Quality Network (LAQN), hourly NO2 and PM2.5 for 2025, Imperial College London Environmental Research Group. Site-level deprivation context from the English Indices of Deprivation 2025 (MHCLG). Health thresholds from the WHO 2021 Global Air Quality Guidelines.
* **Sites:** three, chosen for environment-type contrast: Lambeth Brixton Road (LB4, Urban Traffic), London N. Kensington (KC1, Urban Background), Bexley Belvedere West (BQ7, Urban Background).
* **Size:** 52,560 hourly records for 2025 (3 sites, 2 pollutants, 8,760 hours each), including missing readings; data capture ranged from 83.5% to 99.6%.
* **Cleaning:** daily means computed only when at least 18 of 24 hours are valid (Defra LAQM rule), negatives kept for capture but excluded from analytical aggregates, capture rates documented per site and pollutant.

The raw data is not included in this repository. Download the hourly site files from the LAQN data portal and the deprivation file from the English Indices of Deprivation 2025 release.

## Visualisations

**1. Spatial variation and deprivation context (RQ1).** Hourly distributions as per-site small multiples, ordered by IMD 2025 decile of the host LSOA, with the site median and the WHO 24-hour guideline overlaid, and NO2 and PM2.5 on independent axes.

![Hourly NO2 by site, ordered by IMD 2025 decile, with WHO 24-hour guideline](figure-1a-no2-by-site.png)

![Hourly PM2.5 by site, showing the absence of spatial differentiation](figure-1b-pm25-by-site.png)

The WHO 24-hour guideline line in these hourly plots is a contextual reference only. Individual hourly readings are not 24-hour exceedances; the formal short-term comparison uses daily means.

**2. Diurnal and weekly rhythm (RQ2).** Hour-by-day-of-week cell matrices per site, plus weekday-versus-weekend line profiles, to separate a traffic-source rhythm from a background-source rhythm.

![Hour-by-day-of-week NO2 cell matrix per site](figure-2a-no2-heatmap.png)

![Hour-by-day-of-week PM2.5 cell matrix per site](figure-2b-pm25-heatmap.png)

![Mean NO2 by hour of day, weekday against weekend, per site](figure-2c-no2-weekday-weekend.png)

![Mean PM2.5 by hour of day, weekday against weekend, per site](figure-2d-pm25-weekday-weekend.png)

**3. WHO 2021 exceedance (RQ3).** Daily means on a calendar axis against both the 24-hour and annual guidelines, with exceedance days coloured and sized by run length, and a slider that filters by minimum consecutive-run length to expose sustained clusters.

![WHO 2021 exceedance calendar for NO2 and PM2.5, with run-length slider](figure-3-who-exceedance.png)

## Key findings

* **NO2 differentiates sharply across sites; PM2.5 does not.** Brixton Road NO2 median is about 41 µg/m³ against roughly 11 and 9 at the two background sites, while PM2.5 medians cluster between about 6 and 8 µg/m³ everywhere. Each pollutant needs a different analytical frame.
* **Brixton Road shows a bimodal weekday traffic signature** (morning and evening rush-hour peaks, attenuated at weekends) that the two background sites lack, matching the LAQN Urban Traffic classification.
* **Every site exceeds the WHO 2021 guidelines for both pollutants in 2025, but exceedance frequency differs sharply.** On the formal comparators (the annual mean, and the 99th percentile of daily means for the 24-hour guideline) all three sites fail for NO2 and PM2.5. Counting exceedance days shows where short-term exposure concentrates: Brixton Road records 304 NO2 exceedance days (83% of calendar days) against 58 and 45 at the background sites, and the slider reveals a 93-day unbroken exceedance block from early January to early April. The 2025 record was largely provisional when analysed, with data capture varying between sites.
* **A local weekend signal hides inside the PM2.5 uniformity.** At Brixton Road the highest PM2.5 of the whole week falls on Saturday and Friday evenings, a pattern absent at the other two sites and not aligned with commuting, which points to a local non-traffic source that the monitoring data alone cannot identify.

## Design and validation

The three visualisations use three different site orderings, each aligned to its research question (deprivation decile, then NO2 magnitude, then exceedance frequency), so panel position itself encodes the ranking criterion. Pollutants are kept on independent scales throughout to protect within-pollutant readability. WHO guidelines and the 2025 annual mean are drawn directly on the data axis rather than in a separate table. The validation section documents data capture, the 18-of-24 daily-mean rule, the gap between the count-based and the WHO 99th-percentile compliance frames, provisional-data status, and the three-site limitation on any deprivation claim.

## Tech stack

JavaScript, Observable, Observable Plot.

## Viewing the project

* Live interactive notebook, with full source code: https://observablehq.com/@inm402-2026/inm-402-coursework-submission
* The figures above are exported from the interactive notebook and stored in this repository.

The notebook runs on the Observable runtime and imports course utility modules, and it runs in the browser rather than as a standalone script.

## Notes

This project was developed during the INM402 Data Visualization module of the MSc Data Science programme at City St George's, University of London. It applies interactive data visualisation, small-multiple design, threshold and exceedance encoding, and data-quality validation, skills that transfer directly to risk reporting and decision-support dashboards in financial services, where thresholds, breaches and segmentation must be made readable to decision-makers.

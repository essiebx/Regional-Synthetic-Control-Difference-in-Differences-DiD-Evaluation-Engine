# Regional Causal Impact Evaluation Engine

A reproducible framework for estimating the incremental sales impact of regional consumer packaged goods (CPG) promotions when randomized A/B testing is not feasible.

The project combines Difference-in-Differences (DiD) and Synthetic Control methods to estimate the effect of a regional beverage discount campaign using a synthetic, daily sales panel across 50 markets in Mexico. The intended analysis covers two years of data and a campaign launched in three treatment regions.

> **Status:** This repository currently contains the project title only. The analysis, notebook, dataset, and executive memo described below are planned deliverables; no impact estimate or revenue result is reported yet.

## Business objective

Determine whether the promotion generated sales beyond what would have occurred without the campaign, and translate the estimated lift into a decision-ready assessment of incremental revenue.

The analysis is designed to answer:

- What was the campaign's average treatment effect on treated regions (ATT)?
- Is there evidence that treatment and comparison regions followed parallel trends before the campaign?
- How closely can a weighted combination of untreated markets reproduce the pre-campaign trajectory of a selected treated market, such as Mexico City?
- What are the estimated incremental sales and net revenue, with uncertainty and assumptions made explicit?

## Evaluation approach

### Difference-in-Differences

Estimate the campaign effect using a panel model that compares the change in sales in treated regions with the contemporaneous change in comparison regions. Include region and date effects as appropriate, and assess pre-intervention trends using event-time estimates or equivalent diagnostics.

The DiD estimate relies on the parallel-trends assumption: absent the campaign, treated and comparison regions would have experienced comparable changes in sales. Pre-trend diagnostics can identify concerning differences, but cannot prove this assumption.

### Synthetic Control

For a selected treated market (for example, Mexico City), construct a synthetic comparison from untreated regions. Select donor-market weights to match pre-campaign sales patterns and, where available, relevant predictors. Report donor weights and pre- and post-intervention fit so the comparison is transparent.

Synthetic Control complements the pooled DiD estimate; it is not a substitute for checking donor suitability, intervention timing, or potential spillovers between regions.

### EconML estimation

Use EconML for treatment-effect estimation where the data and identification strategy support it. Document the estimator, features, treatment definition, assumptions, and uncertainty. EconML results should be interpreted alongside—not as an automatic replacement for—the DiD and Synthetic Control analyses.

## Synthetic data design

The planned dataset represents daily beverage sales across 50 regional markets in Mexico over a two-year period. It will include:

- Three campaign treatment regions and a defined intervention date.
- Untreated comparison markets available as potential DiD controls and Synthetic Control donors.
- Sales volume and, where modeled, price, discount, calendar effects, and other relevant covariates.
- A documented data-generation process that makes the campaign effect and background trends reproducible.

Synthetic data is useful for demonstrating and testing the workflow. Results from it are not evidence of real-world campaign performance.

## Technology

- **Python** for analysis and modeling
- **PySpark** for data preparation and aggregation
- **EconML**, **DoWhy**, and **Statsmodels** for causal estimation and diagnostics
- **Databricks Notebooks** for an interactive, reproducible workflow
- **Matplotlib** and **Seaborn** for visualizations

## Planned deliverables

1. **Databricks notebook** covering data generation or ingestion, PySpark aggregation, model estimation, diagnostics, and visualizations.
2. **Executive decision memo** summarizing the findings, caveats, and implications in business terms.
3. **Reproducible analysis artifacts** documenting assumptions, model specifications, and the inputs used to calculate incremental sales and revenue.

## Executive readout

The memo will report the estimate produced by the analysis—not a preset or illustrative result—and distinguish modeled synthetic-data results from measured campaign outcomes. It should include:

- Estimated incremental sales lift and ATT, with uncertainty intervals.
- DiD pre-trend diagnostics and Synthetic Control pre-period fit.
- Incremental revenue calculation, including the price and cost assumptions used.
- Key limitations, sensitivity checks, and a clear recommendation.

For example, a result might be communicated as: “The analysis estimates an incremental lift of **[estimate]** (**[uncertainty interval]**), corresponding to **[revenue estimate]** under the stated assumptions.” Values must be populated from model output; the example is a reporting template, not a finding.

## Interpretation and limitations

Causal estimates depend on credible comparison groups, consistent measurement, correct intervention timing, and assumptions such as no material spillovers or concurrent region-specific shocks. The notebook and memo should make these assumptions visible, include appropriate sensitivity checks, and avoid presenting statistical association as causal evidence when the design does not support that conclusion.

## Project status

The repository is the starting point for the evaluation engine. The implementation and deliverables listed above are planned and should be updated as they are added.

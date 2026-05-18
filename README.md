# Spatial Decision Support System (SDSS) for Cloudburst Resiliency in SE Queens

**Author:** Lianne Persaud  
**Status:** Completed (May 2026)  
**Associated Organization:** NYC Department of Transportation (DOT) / Asset Management Unit

##  Project Overview
This repository contains the data, spatial models, and statistical validation scripts for a Spatial Decision Support System (SDSS) designed to automate the prioritization of Blue-Green Infrastructure (BGI) in Southeast Queens. 

The SDSS evaluates extreme rain vulnerability by integrating topographic data with social equity metrics, moving beyond standard flood mapping to explicitly prescribe localized, actionable asset management typologies. This framework aligns with the NYC DEP Cloudburst Resiliency Planning Study and the Copenhagen Cloudburst Management Plan.

##  Repository Structure
* `/data`: Contains the exported spatial analysis results (`se_queens_results.csv`). *Note: High-resolution raster inputs (TIF) are excluded due to file size constraints.*
* `/models`: Contains the QGIS Graphical Model (`.qmodel`) and the categorized symbology template (`BGI_Master_Style.qml`).
* `/scripts`: Contains the R-based statistical suite (`sdss_statistical_validation.R`) used for sensitivity analysis and outcome visualization.
* `/maps`: Contains high-resolution, presentation-ready exports of the final BGI classification map.

##  Methodology & Scenarios
The SDSS employs a Weighted Linear Combination (SAW) approach to evaluate census tracts across two primary scenarios, with all input variables (Impervious surfaces, 311 flood complaints, slope, and ACS poverty data) normalized to a 0–1 scale.

* **Scenario A (Hydrologic):** Prioritizes areas based strictly on physical vulnerability and topography.
* **Scenario B (Equity):** Integrates social vulnerability indices to identify communities disproportionately impacted by urban flooding.

##  BGI Classification Logic
The automated QGIS model classifies each census tract into one of three distinct intervention typologies based on the following calibrated thresholds:

1.  **Cloudburst Roads (Conveyance / Blue):** * *Condition:* `Slope_Mean >= 0.03`
    * *Function:* V-shaped street profiles designed to channel high-velocity stormwater away from vulnerable structures.
2.  **Blue-Green Streets (Infiltration / Green):** * *Condition:* `Slope_Mean < 0.03` AND `Scenario_B_Equity >= 0.20`
    * *Function:* Vegetated streetscapes, bioswales, and permeable pavements targeted specifically at flat, high-vulnerability equity zones.
3.  **Retention Streets (Storage / Orange):** * *Condition:* `Slope_Mean < 0.03` AND `Scenario_B_Equity < 0.20`
    * *Function:* Baseline flat terrain utilized for temporary surface storage and delayed release of stormwater.

##  Key Findings & Sensitivity Analysis
Initial spatial modeling using a strict equity threshold (0.25) isolated a single hyper-vulnerable epicenter (Tract Score: 0.364). To provide municipal planners with a scalable investment strategy, a sensitivity analysis was conducted in R. 

Calibrating the `Scenario_B_Equity` threshold to **0.20** successfully captured a broader distribution of high-need areas:
* **Retention Streets:** 65.8% (79 Tracts)
* **Cloudburst Roads:** 23.3% (28 Tracts)
* **Blue-Green Streets:** 10.8% (13 Tracts)

This calibration provides the NYC DOT with 13 highly specific, actionable corridors for immediate environmental and infrastructural investment.

##  Technical Requirements
To reproduce this analysis, the following software is required:
* **QGIS (Version 3.44.8-Solothurn or higher):** For running the Spatial Model Builder workflow.
* **R / RStudio (Version 3.12 or higher):** Utilizing the `tidyverse` and `ggplot2` packages for statistical validation and boxplot rendering. 

##  License
All intellectual rights pertaining to the structural logic of this SDSS belong to the author and associated project sponsors as outlined in the Project Scope of Work.

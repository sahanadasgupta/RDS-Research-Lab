# RDS-Research-Lab
# Violent Crime & Mental Health Resource Access — California Counties

Research project at UC San Diego's Responsible Data Science Lab, examining the relationship between violent crime rates and access to mental health/substance-abuse treatment resources across California counties.

## Overview

This project merges three data sources — county-level violent crime statistics, a directory of CA mental health/substance abuse facilities, and U.S. Census population data — to test whether counties with less access to mental health resources see correspondingly higher violent crime rates.

## Notebooks

### `rds_data_cleaning.ipynb` — Main data pipeline

The primary cleaning and analysis pipeline:

- Geocodes mental health/substance-abuse facility locations by mapping zip codes to counties and FIPS codes (`pgeocode`)
- Pulls 5-year average county population data live from the U.S. Census ACS API (`census` package)
- Cleans and merges 10 years (2015–2024) of county-level violent crime data, matched to the same FIPS codes
- Pulls county boundary/area data from Census TIGER shapefiles to calculate land area in square miles
- Filters out counties below a 75,000-population threshold, since very small counties produce extreme, statistically unreliable per-capita rates
- Computes two normalized metrics per county:
  - **Service rate** — mental health facilities per 100,000 residents
  - **Facility density** — facilities per square mile
- Builds an interactive choropleth map (Plotly) visualizing service rate and average violent crime rate side-by-side across CA counties

### `RDS_Graph.ipynb` — Exploratory analysis

Earlier exploratory work examining the same underlying question in five selected counties (Los Angeles, Orange, San Diego, Fresno, Imperial):

- Visualizes total crime trends by county over time (2000–present, and a closer look at 2022–2024)
- Separately tracks mental health facility counts by county across 2022, 2023, and 2024 using manually uploaded CSV/Excel directories
- Produces line charts comparing crime trends and facility-count trends across counties

This notebook represents earlier-stage exploration before the pipeline in `rds_data_cleaning.ipynb` was built out with Census-API population normalization and per-capita rate calculations.

## Data Sources

- California violent crime data (Crimes and Clearances with Arson, 1985–2024)
- CA mental health/substance abuse facility directories (state/SAMHSA service directories, multiple years)
- U.S. Census ACS 5-year population estimates
- U.S. Census TIGER county boundary shapefiles

## Tools

Python (pandas, matplotlib, seaborn, plotly, geopandas), `pgeocode` (zip-to-county geocoding), `census` (Census API access)

## Status

Work in progress — part of ongoing research at the Responsible Data Science Lab, UC San Diego (Dec. 2025–present).

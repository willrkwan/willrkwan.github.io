---
title: "Analyzing Kelowna's Walkability"
permalink: /kelowna_walkability/
layout: single
author_profile: true
---

## Project Overview

I developed a comprehensive walkability index (0-100) for 175 Kelowna neighborhoods by analyzing 1,569 amenities across five key indicators: proximity to amenities, population and amenity density, land use diversity, street connectivity, and terrain characteristics.

**Resources**
- [Full Report (PDF)](/assets/documents/kelowna-walkability/Report.pdf)
- [All Figures (PDF)](/assets/documents/kelowna-walkability/Figures1-11.pdf)
- [Complete Rankings (PDF)](/assets/documents/kelowna-walkability/Table3.pdf)

## What I Did

**Data Collection & Processing**
- Collected and geocoded 1,569 amenity locations using Python (pandas, Google Geocoding API)
- Processed spatial data for 175 neighborhoods to calculate density metrics and proximity measures
- Integrated terrain and street network data to assess physical walkability constraints

**Spatial Analysis**
- Applied logistic decay functions to model realistic walking distance preferences
- Calculated land use diversity using Shannon's Entropy Index
- Designed weighting scheme for five indicators based on academic literature on pedestrian behavior and urban design
- Analyzed statistical distribution of scores across neighborhoods

**Visualization & Communication**
- Created walkability maps and neighborhood rankings to visualize spatial patterns
- Identified 11-fold variation in walkability scores (7.65-84.49) across the city
- Documented methodology and findings in a comprehensive technical report

## Key Insights

My analysis revealed stark disparities in Kelowna's pedestrian infrastructure. Downtown, Pandosy Village, and Midtown scored highest due to excellent amenity access and connectivity, while suburban areas like Wilden and Upper Mission exhibited car-dependence and low connectivity. The mean score of 49.03 (SD: 19.85) highlights uneven development patterns across the city.

## Skills Demonstrated

- **Geospatial Analysis**: GIS-based spatial analysis and visualization
- **Python Programming**: Data collection, processing, and statistical analysis
- **Research Methods**: Literature review and methodology design
- **Technical Writing**: Clear communication of complex spatial analysis for urban planning audiences
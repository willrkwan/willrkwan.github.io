---
title: "Analyzing Kelowna's Walkability"
permalink: /kelowna_walkability/
layout: single
author_profile: true
---

## Project Overview

Analyzed pedestrian accessibility accross 175 Kelowna neighborhoods using 1,569 amentities to create a walkability index (0-100). The project integrates five key indicators: proximity to amentities, population and amenitiy density, land use diversity, street connectivity, and terrain characteristics.

**Key Findings:**
- Walkability scores range from 7.65 to 84.49, an 11x difference across the city
- High Walkability Areas: Downtown, Pandosy Village, Midtown. These areas have excellent pedestrian infrastructure and amenity access.
- Low Walkability Areas: Suburban sprawl (Wilden, Upper Mission) score low, revealing car-dependence, low connectivity, and low land use diversity.
- Mean Score: 49.03, SD: 19.85, indicating uneven development patterns.

**Methodology Highlights**
- Weighted five indicators to reflect pedestrian behavior and urban design impact, based on evidence in academic literature
- Used logistic decay functions for walking distance modelling
- Applied Shannon's Entropy Index for land use diversity
- Incorporated slope and aesthetic features to account for walkability comfort
- Utilized Python for amenity data collection and processing (pandas, Google Geocoding API)

**Deliverables**
- Walkability index maps and neighbourhood rankings
- Full project report with methodology, figures, and statistical analysis
- Insights for sustainable urban planning and pedestrian infrastructure investments

**Full Report**
- [Full Report (PDF)](/assets/documents/kelowna-walkability/Report.pdf)
- [All Figures (PDF)](/assets/documents/kelowna-walkability/Figures1-11.pdf)
- [Complete Rankings (PDF)](/assets/documents/kelowna-walkability/Table3.pdf)


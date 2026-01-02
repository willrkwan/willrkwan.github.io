---
title: "Analyzing Kelowna's Walkability"
permalink: /kelowna_walkability/
layout: single
author_profile: true
---

## Overview

Using GIS and 1,569 data points across 175 neighborhoods, this project reveals where Kelowna excels—and struggles—with pedestrian accessibility. The analysis developed a comprehensive walkability index (0-100 scale) by integrating five key indicators: proximity to amenities, population density, land use diversity, street connectivity, and terrain characteristics.

**Key Findings:**
- Walkability scores range from **7.65 to 84.49** — an 11x difference across the city
- **Downtown core** leads with a score of 84.49, demonstrating excellent pedestrian infrastructure
- **Suburban areas** like Wilden score as low as 7.65, revealing car-dependent development patterns
- Mean walkability: 49.03 (below midpoint, indicating room for improvement)

**Data Scale:**
- 1,569 amenities analyzed
- 175 dissemination areas
- 27 amenity subcategories
- 9 major categories

**Top Performers:**
- Downtown: 84.49
- Pandosy Village: 83.52
- Midtown: 78.34

**Challenges:**
- High variance (SD: 19.85)
- Suburban sprawl impacts
- Car-dependent design

---

## Methodology

The walkability index integrates five evidence-based indicators, weighted according to their impact on pedestrian behavior:

### 1. Proximity (35% weight)
- **Pedestrian Path Access** (10%): Distance to nearest walking infrastructure using a 5-minute walk threshold (276m)
- **Amenity Access** (25%): Weighted distance to essential services across 27 categories using a 15-minute walk threshold (876m)
- Uses logistic decay functions to model realistic walking behavior

### 2. Density (16.25% weight)
- **Population Density** (8.125%): Residents per dissemination area
- **Amenity Density** (8.125%): Number of services per area
- Higher density supports viable pedestrian-oriented development

### 3. Diversity (16.25% weight)
- **Land Use Mix**: Shannon's Entropy Index measuring variety of amenity categories within 15 hectares
- Higher diversity = more walkable, mixed-use neighborhoods
- Low scores indicate single-use, car-dependent areas

### 4. Connectedness (16.25% weight)
- **Road Density** (8.125%): Total road length per area
- **Intersection Density** (8.125%): Number of intersections per area
- More connected street networks provide direct walking routes

### 5. Attractiveness (16.25% weight)
- **Slope Analysis** (11.25%): Terrain difficulty using exponential decay (steeper = lower score)
- **Aesthetic Features** (5%): Tree and streetlight density as proxies for comfort and safety

All indicators are normalized to a 0-100 scale, then weighted and aggregated into the final walkability index.

---

## Key Findings

### The Walkability Gap

Kelowna exhibits an **11-fold difference** between its most and least walkable neighborhoods, revealing stark contrasts in urban design:

**🏆 Most Walkable: Downtown Core (DA 59350057) — Score: 84.49**
- Excellent proximity to 1,569 amenities across all categories
- High intersection density enabling direct pedestrian routes
- Flat terrain ideal for walking
- Well-connected pedestrian infrastructure
- Challenge: Lower relative population density despite high walkability

**🚗 Least Walkable: Wilden (DA 59350022) — Score: 7.65**
- Poor amenity access requiring vehicle travel
- Low land use diversity (single-use residential)
- Low population density typical of suburban sprawl
- Limited street connectivity
- Classic car-dependent development pattern

### Spatial Patterns

High walkability concentrates in:
- **Urban cores**: Downtown, Pandosy Village, Midtown, Rutland, Capri-Landmark
- **Major corridors**: Highway 97, Glenmore Road, Lakeshore Road
- **Transit-oriented areas**: High-frequency bus routes

Low walkability dominates:
- **Suburban developments**: Upper Mission, Wilden
- **Agricultural zones**: Periphery areas
- **Single-use residential**: Car-oriented subdivisions

### Statistical Summary

- **Mean**: 49.03/100 (below midpoint — room for citywide improvement)
- **Standard Deviation**: 19.85 (high variance indicating uneven development)
- **Range**: 7.65 to 84.49
- **Top Quartile**: ≥64.22 (concentrated in established urban areas)
- **Bottom Quartile**: ≤34.47 (predominantly suburban sprawl)

---

## Data Sources & Tools

**Spatial Data:**
- Statistics Canada: Dissemination area boundaries, population data
- Google Maps API: 1,569 amenity locations (geocoded)
- City of Kelowna Open Data: Pedestrian network, parks, schools, trees, streetlights, DEM
- BC Transit: Transit stop locations
- BC Freshwater Atlas: Okanagan Lake boundary

**Analysis Tools:**
- ArcGIS Pro: Spatial analysis, geoprocessing
- Python: Data processing (pandas, Google Geocoding API)

**Projection:** NAD 1983 UTM Zone 11

---

## Downloads & Additional Resources

- [Full Report (PDF)](/assets/documents/kelowna-walkability/Report.pdf)
- [All Figures (PDF)](/assets/documents/kelowna-walkability/Figures1-11.pdf)
- [Complete Rankings (PDF)](/assets/documents/kelowna-walkability/Table3.pdf)

**Report Contents:**
- Complete methodology and literature review
- Detailed results and statistical analysis
- All 11 figures in high resolution
- Discussion of limitations and future improvements
- Full reference list

---

## Project Context

This analysis was completed as the term project for GISC 480: Practical Applications in GIS at UBC Okanagan (April 2025). The project aligns with Kelowna's 2040 Official Community Plan goals to transition from car-centric development toward more sustainable, walkable neighborhoods that reduce emissions and improve quality of life.

**Implications:**
- Identifies priority areas for walkability investments
- Supports evidence-based urban planning decisions
- Provides baseline for tracking progress toward 2040 goals
- Demonstrates GIS applications in sustainable urban development


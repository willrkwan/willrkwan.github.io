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

<div style="display: flex; gap: 20px; margin: 20px 0; flex-wrap: wrap;">
  <div style="flex: 1; min-width: 200px; padding: 15px; background-color: #f0f8ff; border-left: 4px solid #4a90e2; border-radius: 4px;">
    <h4 style="margin-top: 0;">Data Scale</h4>
    <ul style="margin-bottom: 0;">
      <li>1,569 amenities analyzed</li>
      <li>175 dissemination areas</li>
      <li>27 amenity subcategories</li>
      <li>9 major categories</li>
    </ul>
  </div>
  <div style="flex: 1; min-width: 200px; padding: 15px; background-color: #f0fff0; border-left: 4px solid #52c41a; border-radius: 4px;">
    <h4 style="margin-top: 0;">Top Performers</h4>
    <ul style="margin-bottom: 0;">
      <li>Downtown: 84.49</li>
      <li>Pandosy Village: 83.52</li>
      <li>Midtown: 78.34</li>
    </ul>
  </div>
  <div style="flex: 1; min-width: 200px; padding: 15px; background-color: #fff5f5; border-left: 4px solid #ff4d4f; border-radius: 4px;">
    <h4 style="margin-top: 0;">Challenges</h4>
    <ul style="margin-bottom: 0;">
      <li>High variance (SD: 19.85)</li>
      <li>Suburban sprawl impacts</li>
      <li>Car-dependent design</li>
    </ul>
  </div>
</div>

---

## Interactive Walkability Map

Explore Kelowna's walkability across different dimensions. Use the layer controls to view the final walkability index or examine individual components of the analysis.

<div id="map-container">
  <!-- Left column: map -->
  <div id="map"></div>

  <!-- Right column: controls -->
  <div id="controls-box">
    <strong>Choose a layer:</strong>
    <label><input type="radio" name="layer" value="walkability" checked> Final Walkability Index</label>
    <label><input type="radio" name="layer" value="proximity"> Proximity to Amenities</label>
    <label><input type="radio" name="layer" value="density"> Density (Population + Amenities)</label>
    <label><input type="radio" name="layer" value="diversity"> Diversity (Land Use Mix)</label>
    <label><input type="radio" name="layer" value="connectedness"> Connectedness (Roads + Intersections)</label>
    <label><input type="radio" name="layer" value="slope"> Attractiveness (Slope + Aesthetics)</label>
  </div>
</div>

<style>
/* Two-column container */
#map-container {
  display: flex;
  gap: 20px;
  flex-wrap: wrap;
}

/* Map (left column) */
#map {
  flex: 1 1 0;
  min-width: 300px;
  height: 600px;
  border-radius: 8px;
  box-shadow: 2px 2px 5px rgba(0,0,0,0.3);
}

/* Controls box (right column) */
#controls-box {
  flex: 0 0 200px; /* fixed width */
  align-self: flex-start; /* only as tall as content */
  padding: 10px;
  background-color: #f9f9f9;
  border: 1px solid #ccc;
  border-radius: 8px;
  box-shadow: 2px 2px 5px rgba(0,0,0,0.3);
  font-family: Arial, sans-serif;
  color: #444444;
  font-size: 14px;
}

/* Radio button labels */
#controls-box label {
  display: flex;
  align-items: center;
  margin-bottom: 8px;
  color: #444444;
  cursor: pointer;
}

/* Space between radio button and text */
#controls-box input[type="radio"] {
  margin-right: 8px;
}
</style>

<!-- Leaflet CSS & JS -->
<link rel="stylesheet" href="https://unpkg.com/leaflet/dist/leaflet.css" />
<script src="https://unpkg.com/leaflet/dist/leaflet.js"></script>

<script>
var map = L.map('map').setView([49.8879, -119.4960], 13);

L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
  attribution: '&copy; OpenStreetMap contributors'
}).addTo(map);

// Placeholder layers
var walkability = L.geoJSON({
  "type": "FeatureCollection",
  "features": [
    { "type": "Feature", "properties": {"name": "Downtown"}, "geometry": {"type": "Polygon", "coordinates": [[[-119.5,49.88],[-119.48,49.88],[-119.48,49.89],[-119.5,49.89],[-119.5,49.88]]]}}
  ]
}, {style:{color:"blue", fillOpacity:0.4}}).addTo(map);

var density = L.geoJSON({
  "type": "FeatureCollection",
  "features": [
    { "type": "Feature", "properties": {"name": "Midtown"}, "geometry": {"type": "Polygon", "coordinates": [[[-119.49,49.885],[-119.47,49.885],[-119.47,49.895],[-119.49,49.895],[-119.49,49.885]]]}}
  ]
}, {style:{color:"green", fillOpacity:0.4}});

var services = L.geoJSON({
  "type": "FeatureCollection",
  "features": [
    { "type": "Feature", "properties": {"name": "Pandosy"}, "geometry": {"type": "Polygon", "coordinates": [[[-119.495,49.882],[-119.475,49.882],[-119.475,49.892],[-119.495,49.892],[-119.495,49.882]]]}}
  ]
}, {style:{color:"orange", fillOpacity:0.4}});

var slope = L.geoJSON({
  "type": "FeatureCollection",
  "features": [
    { "type": "Feature", "properties": {"name": "Upper Mission"}, "geometry": {"type": "Polygon", "coordinates": [[[-119.51,49.88],[-119.49,49.88],[-119.49,49.89],[-119.51,49.89],[-119.51,49.88]]]}}
  ]
}, {style:{color:"red", fillOpacity:0.4}});


var connectedness = L.geoJSON({
  "type": "FeatureCollection",
  "features": [
    { "type": "Feature", "properties": {"name": "Rutland"}, "geometry": {"type": "Polygon", "coordinates": [[[-119.45,49.89],[-119.43,49.89],[-119.43,49.90],[-119.45,49.90],[-119.45,49.89]]]}}
  ]
}, {style:{color:"purple", fillOpacity:0.4}});

var layers = { walkability, proximity: services, density, diversity: services, connectedness, slope };

// Show only selected layer
document.querySelectorAll('input[name="layer"]').forEach(radio => {
  radio.addEventListener('change', function() {
    for (let key in layers) map.removeLayer(layers[key]);
    map.addLayer(layers[this.value]);
  });
});
</script>

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
- Leaflet.js: Interactive web mapping

**Projection:** NAD 1983 UTM Zone 11

---

## Downloads & Additional Resources

<div style="margin: 20px 0;">
  <a href="/assets/documents/kelowna-walkability/Report.pdf" style="display: inline-block; padding: 10px 20px; background-color: #4a90e2; color: white; text-decoration: none; border-radius: 4px; margin-right: 10px; margin-bottom: 10px;">📄 Full Report (PDF)</a>
  <a href="/assets/documents/kelowna-walkability/Figures1-11.pdf" style="display: inline-block; padding: 10px 20px; background-color: #52c41a; color: white; text-decoration: none; border-radius: 4px; margin-right: 10px; margin-bottom: 10px;">📊 All Figures (PDF)</a>
  <a href="/assets/documents/kelowna-walkability/Table3.pdf" style="display: inline-block; padding: 10px 20px; background-color: #fa8c16; color: white; text-decoration: none; border-radius: 4px; margin-bottom: 10px;">📋 Complete Rankings (PDF)</a>
</div>

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


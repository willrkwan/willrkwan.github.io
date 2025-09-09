---
title: "Analyzing Kelowna's Walkability"
permalink: /kelowna_walkability/
layout: single
author_profile: true
---

## Interactive Map

<div id="map" style="height: 500px; border-radius: 12px; margin: 1em 0;"></div>

<!-- Leaflet CSS -->
<link rel="stylesheet" href="https://unpkg.com/leaflet/dist/leaflet.css" />

<!-- Leaflet JS -->
<script src="https://unpkg.com/leaflet/dist/leaflet.js"></script>

<script>
  // Initialize map
  var map = L.map('map').setView([49.8879, -119.4960], 12); // Kelowna coords

  // Add OpenStreetMap baselayer
  L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
    attribution: '© OpenStreetMap contributors'
  }).addTo(map);

  // Example: Add a marker
  L.marker([49.8879, -119.4960]).addTo(map)
    .bindPopup("Downtown Kelowna")
    .openPopup();

  // Example: Add GeoJSON (replace with your own data)
  var sampleGeoJSON = {
    "type": "Feature",
    "geometry": {
      "type": "Polygon",
      "coordinates": [[
        [-119.5, 49.9],
        [-119.45, 49.9],
        [-119.45, 49.85],
        [-119.5, 49.85],
        [-119.5, 49.9]
      ]]
    },
    "properties": { "name": "Sample Area" }
  };

  L.geoJSON(sampleGeoJSON, {
    style: { color: "green", weight: 2 }
  }).addTo(map);
</script>

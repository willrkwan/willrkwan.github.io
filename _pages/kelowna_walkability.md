---
title: "Analyzing Kelowna's Walkability"
permalink: /kelowna_walkability/
layout: single
author_profile: true
---

## Interactive Map (Sample Data)
<!-- Controls outside the map -->
<div id="controls" style="margin-bottom: 10px;">
  <strong>Choose a layer:</strong><br>
  <label><input type="radio" name="layer" value="walkability" checked> Final Walkability</label><br>
  <label><input type="radio" name="layer" value="density"> Population Density</label><br>
  <label><input type="radio" name="layer" value="services"> Services</label><br>
  <label><input type="radio" name="layer" value="slope"> Slope</label>
</div>

<!-- Map container -->
<div id="map" style="height: 600px;"></div>

<!-- Leaflet CSS -->
<link rel="stylesheet" href="https://unpkg.com/leaflet/dist/leaflet.css" />

<!-- Leaflet JS -->
<script src="https://unpkg.com/leaflet/dist/leaflet.js"></script>

<script>
  // Initialize map
  var map = L.map('map').setView([49.8879, -119.4960], 13);

  // Add base map
  L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
    attribution: '&copy; OpenStreetMap contributors'
  }).addTo(map);

  // Placeholder GeoJSON layers
  var walkability = L.geoJSON({
    "type": "FeatureCollection",
    "features": [
      { "type": "Feature", "properties": {"name": "Downtown"}, "geometry": {"type": "Polygon", "coordinates": [[[-119.5,49.88],[-119.48,49.88],[-119.48,49.89],[-119.5,49.89],[-119.5,49.88]]]}}
    ]
  }, {style: {color: "blue", fillOpacity: 0.4}}).addTo(map);

  var density = L.geoJSON({
    "type": "FeatureCollection",
    "features": [
      { "type": "Feature", "properties": {"name": "Midtown"}, "geometry": {"type": "Polygon", "coordinates": [[[-119.49,49.885],[-119.47,49.885],[-119.47,49.895],[-119.49,49.895],[-119.49,49.885]]]}}
    ]
  }, {style: {color: "green", fillOpacity: 0.4}});

  var services = L.geoJSON({
    "type": "FeatureCollection",
    "features": [
      { "type": "Feature", "properties": {"name": "Pandosy"}, "geometry": {"type": "Polygon", "coordinates": [[[-119.495,49.882],[-119.475,49.882],[-119.475,49.892],[-119.495,49.892],[-119.495,49.882]]]}}
    ]
  }, {style: {color: "orange", fillOpacity: 0.4}});

  var slope = L.geoJSON({
    "type": "FeatureCollection",
    "features": [
      { "type": "Feature", "properties": {"name": "Upper Mission"}, "geometry": {"type": "Polygon", "coordinates": [[[-119.51,49.88],[-119.49,49.88],[-119.49,49.89],[-119.51,49.89],[-119.51,49.88]]]}}
    ]
  }, {style: {color: "red", fillOpacity: 0.4}});

  // Layer mapping
  var layers = {
    walkability: walkability,
    density: density,
    services: services,
    slope: slope
  };

  // Radio button logic to show only one layer at a time
  document.querySelectorAll('input[name="layer"]').forEach(function(radio) {
    radio.addEventListener('change', function() {
      // Remove all layers
      for (let key in layers) {
        map.removeLayer(layers[key]);
      }
      // Add selected layer
      map.addLayer(layers[this.value]);
    });
  });
</script>

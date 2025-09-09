---
title: "Analyzing Kelowna's Walkability"
permalink: /kelowna_walkability/
layout: single
author_profile: true
---

Sample text Sample text Sample text Sample text Sample text Sample text Sample text Sample text Sample text Sample text Sample text Sample text Sample text Sample text Sample text Sample text Sample text Sample text Sample text 

## Interactive Map (Placeholder Data)

<div id="map-container">
  <!-- Left column: map -->
  <div id="map"></div>

  <!-- Right column: controls -->
  <div id="controls-box">
    <strong>Choose a layer:</strong>
    <label><input type="radio" name="layer" value="walkability" checked> Final Walkability</label>
    <label><input type="radio" name="layer" value="density"> Population Density</label>
    <label><input type="radio" name="layer" value="services"> Services</label>
    <label><input type="radio" name="layer" value="slope"> Slope</label>
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


var layers = { walkability, density, services, slope };

// Show only selected layer
document.querySelectorAll('input[name="layer"]').forEach(radio => {
  radio.addEventListener('change', function() {
    for (let key in layers) map.removeLayer(layers[key]);
    map.addLayer(layers[this.value]);
  });
});
</script>

